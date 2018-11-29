---
title: 1 度のデータベース トランザクションでメッセージを実行する (アプリ用 Common Data Service) | Microsoft Docs
description: ExecuteTransactionRequest メッセージ要求を使用して、1 度のデータベース トランザクションで組織サービスの要求を 2 つ以上実行できます。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: brandonsimons
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="execute-messages-in-a-single-database-transaction"></a>単一のデータベース トランザクションでメッセージを実行する

 ビジネス アプリケーションでは、システム内の複数のレコードの変更を調整して、すべてのデータの変更が成功したか失敗したかのいずれかになるようにすることが一般的な要件です。 データベースの用語では、どれか一つの操作が失敗したときにすべてのデータの変更をロール バックする機能を持つ単一のトランザクションで、複数の操作を実行することとして知られています。  
  
 <xref:Microsoft.Xrm.Sdk.Messages.ExecuteTransactionRequest> メッセージ要求を使用して、1 つのデータベース トランザクションで、組織のサービス要求を 2 つ以上実行できます。 このメッセージを使用するには、<xref:Microsoft.Xrm.Sdk.Messages.ExecuteTransactionRequest.Requests> コレクションに、トランザクションで実行される組織の要求を 2 つ以上設定します。 <xref:Microsoft.Xrm.Sdk.Messages.ExecuteTransactionResponse.Responses> コレクションで、実行したメッセージ要求ごとに 1 つ、応答のコレクションを戻す場合は、<xref:Microsoft.Xrm.Sdk.Messages.ExecuteTransactionRequest.ReturnResponses> を `true` に設定します。 <xref:Microsoft.Xrm.Sdk.Messages.ExecuteTransactionRequest.Requests> コレクションのメッセージ要求は、コレクションに表示されている順序で実行されます。この場合、インデックス 0 の要素が最初に実行されます。 この同じ順序は、<xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleResponse.Responses> コレクションで維持されます。  
  
 要求のいずれかが失敗し、トランザクションがロールバックされた場合、トランザクション中に完了したデータの変更は取り消されます。 また、<xref:Microsoft.Xrm.Sdk.ExecuteTransactionFault> が返されて、エラーを発生した要求メッセージの要求コレクションのインデックスを特定します。  
  
 <xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleRequest> には、1 つまたは複数の <xref:Microsoft.Xrm.Sdk.Messages.ExecuteTransactionRequest> インスタンスが格納されていることがあります。  <xref:Microsoft.Xrm.Sdk.Messages.ExecuteTransactionRequest> インスタンスに、<xref:Microsoft.Xrm.Sdk.Messages.ExecuteTransactionRequest> または <xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleRequest> を含むことはできません。 <xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleRequest> に関する詳細は [組織サービスを使用して複数の要求を実行する](execute-multiple-requests.md) を参照してください。 

## <a name="example"></a>例

このサンプルでは 1 つの Web メソッド呼び出しを使用して、コレクション内すべてのメッセージ要求を 1 度のデータベース トランザクションの一部として実行します。 実行時の動作を変更する設定も示しています。

```csharp
// Create an ExecuteTransactionRequest object.
var requestToCreateRecords = new ExecuteTransactionRequest()
{
// Create an empty organization request collection.
Requests = new OrganizationRequestCollection(),
ReturnResponses = true
};

// Create several (local, in memory) entities in a collection. 
var input = new EntityCollection()
{
EntityName = Account.EntityLogicalName,
Entities = {
            new Account { Name = "ExecuteTransaction Example Account 1" },
            new Account { Name = "ExecuteTransaction Example Account 2" },
            new Account { Name = "ExecuteTransaction Example Account 3" },
            new Account { Name = "ExecuteTransaction Example Account 4" },
            new Account { Name = "ExecuteTransaction Example Account 5" }
        }
};

// Add a CreateRequest for each entity to the request collection.
foreach (var entity in input.Entities)
{
CreateRequest createRequest = new CreateRequest { Target = entity };
requestToCreateRecords.Requests.Add(createRequest);
}

// Execute all the requests in the request collection using a single web method call.
try
{
var responseForCreateRecords =
    (ExecuteTransactionResponse)svc.Execute(requestToCreateRecords);

int i = 0;
// Display the results returned in the responses.
foreach (var responseItem in responseForCreateRecords.Responses)
{
    if (responseItem != null)
    Console.WriteLine("Created " + ((Account)requestToCreateRecords.Requests[i].Parameters["Target"]).Name
        + " with account id as " + responseItem.Results["id"].ToString());
    i++;
}
}
catch (FaultException<OrganizationServiceFault> ex)
{
Console.WriteLine("Create request failed for the account{0} and the reason being: {1}",
    ((ExecuteTransactionFault)(ex.Detail)).FaultedRequestIndex + 1, ex.Detail.Message);
throw;
}
```

### <a name="see-also"></a>関連項目

[メタデータを組織サービスと共に使用する](use-messages.md)<br />
[組織サービスを使用して複数の要求を実行する](execute-multiple-requests.md)
---
title: 組織サービスを用いた重複データの検出 (アプリ用Common Data Service) | Microsoft Docs
description: 組織サービスを使用すると、アプリ用 Common Data Service (CDS) の重複レコードを検出してデータの整合性を維持できる
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: mayadumesh
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="detect-duplicate-data-using-the-organization-service"></a>組織サービスを使用して重複データを検出する

アプリ用 Common Data Service (CDS) の組織サービスを使用すると、重複レコードを検出してデータの整合性を維持できます。 コードを使用した重複データの検出の詳細については、[コードを使用した重複データの検出](../detect-duplicate-data-with-code.md) を参照してください。 

> [!NOTE]
> 適切な重複データ検出ルールが存在することを確認します。 アプリ用 CDS には、取引先企業、取引先担当者、および潜在顧客のための既定の重複データ検出ルールが含まれますが、他のレコードの種類のための既定のルールは含まれません。 システムが他のレコードの種類の重複データを検出するようにするには、新しいルールを作成する必要があります。 <br/>- UI を使用して重複データの検出ルールを作成する方法については、[データを整理するための重複データ検出ルールの設定](/dynamics365/customer-engagement/admin/set-up-duplicate-detection-rules-keep-data-clean) を参照してください。<br/>- コードを使用して重複データ検出ルールを作成する方法の詳細については、[重複ルール エンティティ](../duplicaterule-entities.md) を参照してください。


## <a name="use-retrieveduplicatesrequest-message-to-detect-duplicates-before-you-create-or-update-record"></a>RetrieveDuplicatesRequest メッセージを使用して、レコードを作成または更新する前に重複を検知する

<xref:Microsoft.Crm.Sdk.Messages.RetrieveDuplicatesRequest> クラスを使用すると、エンティティが重複しているかどうか、または重複することになるかどうかを、エンティティを作成または更新する前にプログラム的に確認できます。

```csharp
var account = new Account();
account.Name = "Sample Account";

var request = new RetrieveDuplicatesRequest()
{
    BusinessEntity = account,
    MatchingEntityName = account.LogicalName,
    PagingInfo = new PagingInfo() { PageNumber = 1, Count = 50 }
};

var response = (RetrieveDuplicatesResponse)svc.Execute(request);

if (response.DuplicateCollection.Entities.Count >= 1)
{
    Console.WriteLine("{0} Duplicate records found.", response.DuplicateCollection.Entities.Count);
}
```

## <a name="use-suppressduplicatedetection-parameter-to-throw-errors-when-you-create-or-update-record"></a>SuppressDuplicateDetection パラメータを使用して、レコードを作成または更新するときにエラーをスローする

作成した新しいレコードが重複レコードであると判断された場合、または重複データ検出ルールが評価されるように既存のレコードを更新するときにプラットフォームがエラーをスローするようにするには、<xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> または <xref:Microsoft.Xrm.Sdk.Messages.UpdateRequest> クラスを <xref:Microsoft.Xrm.Sdk.IOrganizationService> で使用する必要があります。<xref:Microsoft.Xrm.Sdk.IOrganizationService.Execute*> メソッドと、`false` に設定されている `SuppressDuplicateDetection` パラメーターを適用します。

次のコードは、以下が true である場合に、`InvalidOperationException` の例外を `A record was not created or updated because a duplicate of the current record already exists.` メッセージと共にスローします:

- レコードを作成または更新するときは、環境の重複データ検出は有効になっています。
- 取引先企業エンティティに重複データ検出が有効になっている
- 取引先企業名の値が既存のレコードと完全に一致するかどうかを確認する重複データ検出ルールが公開されています。
- `Sample Account` という名前の既存の取引先企業がある

```csharp
var account = new Account();
account.Name = "Sample Account";

var request = new CreateRequest();
request.Target = account;
request.Parameters.Add("SuppressDuplicateDetection", false);

try
{
    svc.Execute(request);
}
catch (FaultException<OrganizationServiceFault> ex)
{
    switch (ex.Detail.ErrorCode)
    {
        case -2147220685:
            throw new InvalidOperationException(ex.Detail.Message);
        default:
            throw ex;
    }
}
```

### <a name="see-also"></a>関連項目
[Web API を使用した重複データの検出](../webapi/manage-duplicate-detection-create-update.md)


---
title: 'メッセージを非同期的に実行するために ExecuteAsync を使用します (Common Data Service)| Microsoft Docs '
description: ExecuteAsync メッセージを使用して非同期的にソリューションをインポートできます
ms.custom: ''
ms.date: 06/08/2019
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
# <a name="use-executeasync-to-execute-messages-asynchronously"></a>メッセージを非同期に実行するために ExecuteAsync を使用します

2 つを除き、SDK アセンブリ要求クラスを使用した全てのデータ操作は同期します。

ソリューションのインポートは大量のリソースを必要とする操作の 1 つです。そのため <xref:Microsoft.Xrm.Sdk.Messages.ExecuteAsyncRequest> 要求クラスを使用して、この操作を非同期的に実行するオプションが存在します。 <xref:Microsoft.Crm.Sdk.Messages.DeleteAndPromoteRequest> 要求クラスでは同様のリソース集約的な操作を実行します。

ソリューションを非同期にインポートすることで、サーバーの負荷が少なくなる時点までメッセージの実行を延期し、システムのパフォーマンスを改善します。 対話型ユーザーは、対象メッセージの実行を、続行可能になるまで待つ必要はありません。 これはソリューションのインポートを実行するのに数分以上かかる場合に特に有効です。  
  
> [!NOTE]
>  <xref:Microsoft.Crm.Sdk.Messages.ImportSolutionRequest> および <xref:Microsoft.Crm.Sdk.Messages.DeleteAndPromoteRequest>のみが、`ExecuteAsync` メッセージで使用できる要求クラスです。
  
<xref:Microsoft.Xrm.Sdk.Messages.ExecuteAsyncRequest> 要求クラスは、メッセージを非同期的に実行する場合に使用します。 要求を構成して、引数として要求インスタンスを <xref:Microsoft.Xrm.Sdk.IOrganizationService>/<xref:Microsoft.Xrm.Sdk.IOrganizationService.Execute*> へ渡します。 <xref:Microsoft.Xrm.Sdk.Messages.ExecuteAsyncResponse> は、非同期ジョブの ID を返します。 (オプション) ID を使用してジョブをクエリし、現在の状態を確認できます。  
  
非同期にインポートされるように、<xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleRequest> 要求クラスを使用して、複数のソリューションをキューできます。そのためには 1 つの `ExecuteMultiple` メッセージ要求に対し、1 つ以上の `ExecuteAsync` メッセージ要求を追加する必要があります。 システム全体のパフォーマンスを向上させる調整制限により、非同期に実行する 1 つのメッセージのみを、組織ごとに 1 度に実行できます。

`ExecuteMultiple` メッセージに関する詳細は、「[組織サービスを使用して複数の要求を実行する](execute-multiple-requests.md)」を参照してください。  

## <a name="example"></a>例

次の例では <xref:Microsoft.Crm.Sdk.Messages.ImportSolutionRequest> メッセージ要求クラスと共に、 <xref:Microsoft.Xrm.Sdk.Messages.ExecuteAsyncRequest> メッセージ要求クラスを使用する方法を示します。

```csharp
string ManagedSolutionLocation = @"C:\temp\ManagedSolutionForImportExample.zip";

byte[] fileBytes = File.ReadAllBytes(ManagedSolutionLocation);

ImportSolutionRequest impSolReq = new ImportSolutionRequest()
{
CustomizationFile = fileBytes
};

ExecuteAsyncRequest asyncReq = new ExecuteAsyncRequest()
{
Request = impSolReq
};

var asyncResp = (ExecuteAsyncResponse)svc.Execute(asyncReq);

Guid asyncOperationId = asyncResp.AsyncJobId;
```
[AsyncOperation](../reference/entities/asyncoperation.md) エンティティを [AsyncOperationId](../reference/entities/asyncoperation.md#BKMK_AsyncOperationId) と一致するシステム ジョブの `asyncOperationId` の値を用いてポーリングします。これは操作が成功 (30) 、失敗 (31) またはキャンセル (32) されたことを示す [StatusCode](../reference/entities/asyncoperation.md#BKMK_StatusCode) の値を検出するためです。

### <a name="see-also"></a>関連項目

[メタデータを組織サービスと共に使用する](use-messages.md)<br />
[ExecuteTransactionを使用する](use-executetransaction.md)<br />
[組織サービスを使用して複数の要求を実行する](execute-multiple-requests.md)


  
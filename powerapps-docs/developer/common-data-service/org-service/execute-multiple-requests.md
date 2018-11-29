---
title: 組織サービス (アプリ用 Common Data Service) を使用して複数の要求を実行する | Microsoft Docs
description: ExecuteMultipleRequest メッセージは、アプリ用 Common Data Service でより高い効率の一括メッセージ渡しシナリオをサポートします。
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
# <a name="execute-multiple-requests-using-the-organization-service"></a>組織サービスを使用して複数の要求を実行する

<!-- 

https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/org-service/use-executemultiple-improve-performance-bulk-data-load 

-->
複数の要求を実行する主な目的は、ネットワークを介して送信されるデータの総量を減らすことによって、長い待ち時間の環境でのパフォーマンスを向上させることです。

アプリ用 Common Data Service でより高いスループットの一括メッセージ渡しシナリオをサポートするために、<xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleRequest> メッセージを使用することができます。 <xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleRequest> はメッセージの <xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleRequest.Requests> 入力コレクションを受け入れ、入力コレクションに表示される受注でメッセージ要求のサンプルのそれぞれを実行し、必要に応じて、各メッセージの応答または発生したエラーを含む <xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleResponse.Responses> のコレクションを戻します。 入力コレクションの各メッセージ要求が別のデータベース トランザクションで処理されます。 <xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleRequest> は <xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Execute*>  メソッドを使用して実行されます。  
  
一般に、<xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleRequest> は、より優れたパフォーマンスの場合を除き、入力要求コレクションの各メッセージ要求を実行する場合とほぼ同じように動作します。 サービス プロキシの <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceProxy.CallerId> パラメーターの使用は受け入れられ、入力要求コレクションの各メッセージの実行に適用されます。 処理されるメッセージごとに見込まれるため、プラグインとワークフロー活動が実行されます。  
  
プラグインおよびカスタム ワークフロー活動の形式のユーザー定義コードでも <xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleRequest>を実行できます。 ただし、覚えておく必要のある数個の急所があります。 同期の登録プラグインでスローされた例外は応答コレクション アイテム <xref:Microsoft.Xrm.Sdk.ExecuteMultipleResponseItem.Fault> パラメーターで戻ります。 プラグインがデータベース トランザクション内で実行する場合、プラグインは <xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleRequest>を実行し、トランザクションのロールバックが開始され、そのロールバックには、<xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleRequest>によって実行された要求によって発生したすべてのデータ変更が含まれます。  
  
<a name="example"></a>

## <a name="example"></a>例

 次のサンプル コードは、複数の作成操作を実行する単一の <xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleRequest> を示します。 *設定*と呼ばれるランタイム実行オプションは、要求処理と返された結果をコントロールするために使用されます。 これらのランタイム オプションは、次のセクションで説明します。  
  
```csharp

// Create an ExecuteMultipleRequest object.
requestWithResults = new ExecuteMultipleRequest()
{
    // Assign settings that define execution behavior: continue on error, return responses. 
    Settings = new ExecuteMultipleSettings()
    {
        ContinueOnError = false,
        ReturnResponses = true
    },
    // Create an empty organization request collection.
    Requests = new OrganizationRequestCollection()
};

// Create several (local, in memory) entities in a collection. 
EntityCollection input = GetCollectionOfEntitiesToCreate();

// Add a CreateRequest for each entity to the request collection.
foreach (var entity in input.Entities)
{
    CreateRequest createRequest = new CreateRequest { Target = entity };
    requestWithResults.Requests.Add(createRequest);
}

// Execute all the requests in the request collection using a single web method call.
ExecuteMultipleResponse responseWithResults =
    (ExecuteMultipleResponse)service.Execute(requestWithResults);

// Display the results returned in the responses.
foreach (var responseItem in responseWithResults.Responses)
{
    // A valid response.
    if (responseItem.Response != null)
        DisplayResponse(requestWithResults.Requests[responseItem.RequestIndex], responseItem.Response);

    // An error has occurred.
    else if (responseItem.Fault != null)
        DisplayFault(requestWithResults.Requests[responseItem.RequestIndex], 
            responseItem.RequestIndex, responseItem.Fault);
}
```
  
詳細:  [サンプル: 複数の要求を実行する](samples/execute-multiple-requests.md)
  
<a name="options"></a>
 
## <a name="specify-run-time-execution-options"></a>ランタイム実行方法を指定する  

<xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleRequest> の <xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleRequest.Settings> パラメーターは、実行動作と返されたをコントロールする要求コレクションの要求のすべてに適用されます。 これらのオプションをより詳細に参照することにします。  
  
|ExecuteMultipleSettings のメンバー|説明|  
|------------------------------------|-----------------|  
|<xref:Microsoft.Xrm.Sdk.ExecuteMultipleSettings.ContinueOnError>|`true`の場合、コレクションの次の要求の処理を続けます。フォールトがコレクションの現在の要求の処理から戻されている場合でもそうです。 `false`場合、次の要求は処理し続けません。|  
|<xref:Microsoft.Xrm.Sdk.ExecuteMultipleSettings.ReturnResponses>|`true`の場合、処理された各メッセージ要求から応答を戻します。 `false`の場合、応答は返されません。<br /><br /> `true`に設定され、要求が応答を戻さない場合、そのような設計なので、その要求の <xref:Microsoft.Xrm.Sdk.ExecuteMultipleResponseItem> は `null`に設定されます。<br /><br /> しかし、エラーが返された場合、`false`、<xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleResponse.Responses> のコレクションは空ではなくなります。 エラーが返された場合、フォールトを返した処理された各要求のコレクションに1つの応答アイテムがあり、<xref:Microsoft.Xrm.Sdk.ExecuteMultipleResponseItem.Fault>は発生した実際のフォールトに設定されます。|  
  
 たとえば、6つの要求を含み、その3番目と5番目の要求がフォールトを返す要求コレクションの場合、次の表には<xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleResponse.Responses> のコレクションの内容を示します。  
  
|設定|応答コレクションの内容|  
|--------------|-----------------------------------|  
|ContinueOnError=true、ReturnResponses=true|6 種類の応答アイテム: 2 種類には1つの値に設定した <xref:Microsoft.Xrm.Sdk.ExecuteMultipleResponseItem.Fault> があります。|  
|ContinueOnError=false、ReturnResponses=true|3 種類の応答アイテム: 1 種類には1つの値に設定した <xref:Microsoft.Xrm.Sdk.ExecuteMultipleResponseItem.Fault> があります。|  
|ContinueOnError=true、ReturnResponses=false|2 種類の応答アイテム: 2 種類には1つの値に設定した <xref:Microsoft.Xrm.Sdk.ExecuteMultipleResponseItem.Fault> があります。|  
|ContinueOnError=false、ReturnResponses=false|1 種類の応答アイテム: 1 種類には1つの値に設定した <xref:Microsoft.Xrm.Sdk.ExecuteMultipleResponseItem.Fault> があります。|  
  
 応答アイテムの <xref:Microsoft.Xrm.Sdk.ExecuteMultipleResponseItem.RequestIndex> パラメーターは、応答が関連付けられている要求の、先頭がゼロで始まるシーケンス番号を示します。 前の例では、3 番目の要求には 2 の要求インデックスがあります。  
  
<a name="limitations"></a>

## <a name="run-time-limitations"></a>ランタイムの制限

以下のリストで示すように、<xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleRequest> の使用に関する、いくつかの制限があります。  
  
-   **再帰は許可されません** <xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleRequest> は <xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleRequest>を起動できません。 要求コレクションで見つかる <xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleRequest> は、その要求アイテムに関するエラーを生成します。  
  
-   **最大バッチ サイズ** 要求コレクションに追加できる要求の数には制限があります。 この制限を超えると、最初の要求が実行される前にフォールトがスローされます。 1000 の要求制限は一般的ですが、この上限はアプリ用 CDS 環境で設定できます。
  
-   **同時呼び出しの調整** アプリ用 CDS には、組織あたり 2 つの同時実行制限 <xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleRequest> があります。 この制限を超えると、最初の要求が実行される前に*サーバー ビジー* フォールトがスローされます。 

  
<a name="fault"></a>

## <a name="handle-a-batch-size-fault"></a>バッチ サイズのフォールトの処理

入力要求コレクションが最大サイズ バッチを超えた場合に何をすればよいですか。 コードでは、展開管理者ロールを持つアカウントで実行されていない限り、展開 web サービスを通して、最大サイズ バッチを直接を問い合わせることができません。  
  
幸いにも、使用できる別の方法があります。 入力 <xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleRequest.Requests> コレクションの要求の数が組織で許可されるバッチの最大サイズを超えている場合、フォールトが <xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleRequest> 呼び出しから返されます。 最大バッチ サイズがフォールトで返されます。 コードでは、その値のチェック、入力要求コレクションの指示制限内へのサイズ変更、および <xref:Microsoft.Xrm.Sdk.Messages.ExecuteMultipleRequest>の再送信ができます。 次のコード スニペットはこのロジックの一部を示します。  
  
```csharp
catch (FaultException<OrganizationServiceFault> fault)
{
    // Check if the maximum batch size has been exceeded. The maximum batch size is only included in the fault if it
    // the input request collection count exceeds the maximum batch size.
    if (fault.Detail.ErrorDetails.Contains("MaxBatchSize"))
    {
        int maxBatchSize = Convert.ToInt32(fault.Detail.ErrorDetails["MaxBatchSize"]);
        if (maxBatchSize < requestWithResults.Requests.Count)
        {
            // Here you could reduce the size of your request collection and re-submit the ExecuteMultiple request.
            // For this sample, that only issues a few requests per batch, we will just print out some info. However,
            // this code will never be executed because the default max batch size is 1000.
            Console.WriteLine("The input request collection contains %0 requests, which exceeds the maximum allowed (%1)",
                requestWithResults.Requests.Count, maxBatchSize);
        }
    }
    // Re-throw so Main() can process the fault.
    throw;
}
```

### <a name="see-also"></a>関連項目

[メッセージを組織サービスと共に使用する](use-messages.md)<br />
[ExecuteAsync を使用する](use-executeAsync.md)<br />
[ExecuteTransaction を使用する](use-executetransaction.md)<br />

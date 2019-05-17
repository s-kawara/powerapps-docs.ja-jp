---
title: データを作成するために XRM ツールを使用する (Common Data Service)| Microsoft Docs
description: Common Data Service で CrmServiceClient クラスを使用してデータを作成
ms.custom: ''
ms.date: 03/27/2019
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: f6a03552-1f07-4d4b-b7ae-fa246a0d7c29
caps.latest.revision: 14
author: MattB-msft
ms.author: nabuthuk
manager: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="use-xrm-tooling-to-create-data"></a>データを作成するために XRM ツールを使用する

<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient> クラスで新しいデータと関連付けを作成するには、7 つの方法を使用できます。 XRM ツール API を使用する作成操作には、ペイロード データが必要です。 データ ペイロードは `Dictionary<string, CrmDataTypeWrapper>` オブジェクトの形式を取ります。 <xref:Microsoft.Xrm.Tooling.Connector.CrmDataTypeWrapper> を使用して、参照するデータ ポイントに対してどのような処理を適用する必要があるか、インターフェイスに通知します。 データを作成する方法の一部がこのトピックに記載されています。  
  
## <a name="createnewrecord"></a>CreateNewRecord  

この方法は、任意のタイプのエンティティ データを Common Data Service で作成するために使用します。 これを使用するには、レコードを作成する対象エンティティのスキーマ名を知る必要があり、データ ペイロードを構築してそれに渡す必要があります。 この例では、取引先企業レコードを作成します。

```csharp
CrmServiceClient svc = new CrmServiceClient("connectionstring");  
// Verify that you are connected  
if (svc != null && svc.IsReady)  
{  
    // Create an account record  
    Dictionary<string, CrmDataTypeWrapper> inData = new Dictionary<string, CrmDataTypeWrapper>();  
    inData.Add("name", new CrmDataTypeWrapper("Sample Account Name", CrmFieldType.String));  
    inData.Add("address1_city", new CrmDataTypeWrapper("Redmond", CrmFieldType.String));  
    inData.Add("telephone1", new CrmDataTypeWrapper("555-0160", CrmFieldType.String));  
    accountId = ctrl.CrmConnectionMgr.svc.CreateNewRecord("account", inData);  
  
    // Verify if the account is created.  
    if (accountId != Guid.Empty)  
    {  
        Console.WriteLine(“Account created.”);  
    }  
}  
else  
{  
    // Display the last error.  
    Console.WriteLine("An error occurred: {0}", svc.LastCrmError);  
  
    // Display the last exception message if any.   
    Console.WriteLine(svc.LastCrmException.Message);  
    Console.WriteLine(svc.LastCrmException.Source);  
    Console.WriteLine(svc.LastCrmException.StackTrace);  
  
    return;  
}  
```
この例では、`indata` という名前のデータ ペイロード オブジェクトを作成しました。 次に、一般的な構文を使ってそれを設定します `crmFieldName , new CrmDataTypeWrapper(data,CrmFieldType)`。 `indata` オブジェクトを設定して、作成する値を取得後、`CreateNewRecord` メソッドをコールして、取引先企業およびデータ ペイロード (`indata`) のためのエンティティ論理名を提供しました。  
  
> [!NOTE]
> また、<xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> メッセージを <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient.ExecuteCrmOrganizationRequest*> メソッドと共に実行し、XRM ツールを使用してエンティティ レコードを作成できます。 詳細: [ExecuteCrmOrganizationRequest メソッドでメッセージを使用する](use-messages-executecrmorganizationrequest-method.md)  
  
## <a name="createannotation"></a>CreateAnnotation
  
このメソッドは、任意のエンティティ レコードに対してメモを作成および添付するために使用されます。 最初のパスのメモのためのすべての変数を設定できますが、情報カテゴリとメモ テキスト フィールドのみに入力する必要があります。 実際には、これは一般にエンティティに対してシステム生成のメモを添付するため、または Common Data Service に保存された添付ファイルをエンティティに添付するために使用されます。 また、自分のユーザーがメモを作成するために独自の UI を提供する場合、これが、そのメモを Common Data Service の所有者エンティティに添付する方法です。 この例では、前の例に続き、新しく作成された取引先企業に対してメモを作成します。  
  
```csharp
CrmServiceClient svc = new CrmServiceClient(connectionstring);  
  
// Verify that you are connected.  
if (svc != null && svc.IsReady)  
{  
    // Create and attach a note.  
    inData.Clear();   
    inData.Add("subject", new CrmDataTypeWrapper("This is a NOTE from the API" , CrmFieldType.String));
    inData.Add("notetext", new CrmDataTypeWrapper("This is text that will go in the body of the note" , CrmFieldType.String));  
    Guid noteID = svc.CreateAnnotation("account", accountId, inData);  
}  
else  
{  
    // Display the last error.  
    Console.WriteLine("An error occurred: {0}", svc.LastCrmError);  
  
    // Display the last exception message if any.  
    Console.WriteLine(svc.LastCrmException.Message);  
    Console.WriteLine(svc.LastCrmException.Source);  
    Console.WriteLine(svc.LastCrmException.StackTrace);  
  
    return;  
}  
```  
  
### <a name="see-also"></a>関連項目  

[サンプル: XRM ツール API のクイック スタート](sample-quick-start-xrm-tooling-api.md)<br />
[XRM ツール API を使用して Common Data Service のアクションを実行する](use-xrm-tooling-execute-actions.md)

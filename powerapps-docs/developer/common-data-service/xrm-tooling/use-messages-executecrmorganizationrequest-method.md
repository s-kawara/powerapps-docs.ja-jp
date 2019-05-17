---
title: ExecuteCrmOrganizationRequest メソッドと共にメッセージを使用する (Common Data Service) | Microsoft Docs
description: ExecuteCrmOrganizationRequest メソッドでメッセージを使用する方法について説明します。 サンプルは、CrmServiceClient.String) メソッドを使用して CreateRequest および RetrieveMultipleRequest メッセージを実行する方法について示しています。
ms.custom: ''
ms.date: 03/27/2019
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 1ba60f67-522d-4540-a6f9-0787d7074a79
caps.latest.revision: 17
author: MattB-msft
ms.author: kvivek
manager: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="use-messages-with-the-executecrmorganizationrequest-method"></a>ExecuteCrmOrganizationRequest メソッドでメッセージを使用する
  
次のコード サンプルは、<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient.ExecuteCrmOrganizationRequest*> メソッドを使用してメッセージを実行する方法を示しています。  
  
## <a name="example-1-createrequest-message"></a>例 1: CreateRequest メッセージ  

 次のコード サンプルは、<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient>.<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient.ExecuteCrmOrganizationRequest*> メソッドを使用して <xref:Microsoft.Xrm.Sdk.Messages.CreateRequest> メッセージを 実行する方法を示しています。 この例では、取引先企業を作成してから、応答オブジェクトに ID を表示します。  
  
```csharp 
CrmServiceClient svc = new CrmServiceClient(connectionstring);  
  
// Verify that you are connected.  
if (svc != null && svc.IsReady)  
{  
    var request = new CreateRequest();  
    var newAccount = new Entity("account");  
    newAccount.Attributes.Add("name", "Sample Test Account");  
    request.Target = newAccount;  
    var response = (CreateResponse)svc.ExecuteCrmOrganizationRequest(request);  
  
    // Display the ID of the newly created account record.  
    Console.WriteLine("Account record created with the following ID: {0}", response.id.ToString());  
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
  
## <a name="example-2-retrievemultiplerequest"></a>例 2: RetrieveMultipleRequest  

 次のコード サンプルは、<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient>.<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient.ExecuteCrmOrganizationRequest*> メソッドを使用して <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMultipleRequest> メッセージを 実行する方法を示しています。 この例では、複数取得の要求を実行し、システム内のすべての取引先担当者をフェッチし、それらの氏名を表示します。  
  
```csharp  
CrmServiceClient svc = new CrmServiceClient(connectionstring);  
  
// Verify that you are connected.  
if (svc != null && svc.IsReady)  
{  
  
    var userSettingsQuery = new QueryExpression("contact");  
    userSettingsQuery.ColumnSet.AllColumns = true;  
    var retrieveRequest = new RetrieveMultipleRequest()  
    {  
        Query = userSettingsQuery  
    };  
    EntityCollection EntCol = (svc.ExecuteCrmOrganizationRequest(retrieveRequest) as RetrieveMultipleResponse).EntityCollection;  
    foreach (var a in EntCol.Entities)  
    {  
        Console.WriteLine("Account name: {0} {1}", a.Attributes["firstname"], a.Attributes["lastname"]);  
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
  
### <a name="see-also"></a>関連項目  

[XRM ツールを使用して Common Data Service に接続する](use-crmserviceclient-constructors-connect.md)<br />
[XRM ツール API を使用して Common Data Service のアクションを実行する](use-xrm-tooling-execute-actions.md)

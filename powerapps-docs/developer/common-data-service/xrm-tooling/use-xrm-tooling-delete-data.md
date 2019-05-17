---
title: データを削除するために XRM ツールを使用する (Common Data Service)| Microsoft Docs
description: CrmServiceClient クラスを使用して Common Data Service からデータを削除
ms.custom: ''
ms.date: 03/20/2019
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 7e503d2c-89df-4846-8528-632b5ee12bd5
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
# <a name="use-xrm-tooling-to-delete-data"></a>XRM ツールを使用してデータを削除

Common Data Service でデータを削除するために、<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient> クラスには、<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient.DeleteEntity(System.String,System.Guid,System.Guid)> と <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient.DeleteEntityAssociation(System.String,System.Guid,System.String,System.Guid,System.String,System.Guid)> の 2 つのメソッドが用意されています。  
  
## <a name="deleteentity"></a>DeleteEntity  

`DeleteEntity` は Common Data Service から単一行のデータを削除するために使用されます。 このメソッドを使用するには、対象となるエンティティ スキーマ名と、削除する列の GUID を知る必要があります。  
  
```csharp  
CrmServiceClient svc = new CrmServiceClient(connectionstring);  
  
// Verify that you are connected  
if (svc != null && svc.IsReady)  
{  
    // Delete the entity record  
    svc.DeleteEntity("account", <accountId>);  
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
  
## <a name="deleteentityassociation"></a>DeleteEntityAssociation  

`DeleteEntityAssociation` はエンティティのレコード間で多対多の関連付けを削除します。 この例では、潜在顧客エンティティおよび取引先企業エンティティ内の関連付けを削除します。  
  
```csharp  
CrmServiceClient svc = new CrmServiceClient(connectionstring);  
  
// Verify that you are connected  
if (svc != null && svc.IsReady)  
{  
    Guid accountId = new Guid("<Account_GUID>");  
    Guid leadId = new Guid("<Lead_GUID>");  
    string accountLeadRelationshipName= "accountleads_association";   
    svc.DeleteEntityAssociation("account" , accountId, "lead" ,  leadId, accountLeadRelationshipName)  
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
[XRM ツールを使用して Common Data Service に接続する](use-crmserviceclient-constructors-connect.md)<br />
[XRM ツール API を使用して Common Data Service のアクションを実行する](use-xrm-tooling-execute-actions.md)

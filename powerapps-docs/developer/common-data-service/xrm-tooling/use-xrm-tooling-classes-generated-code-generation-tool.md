---
title: コード生成ツールを使用して生成されたクラスに XRM ツールを使用 (アプリ用 Common Data Service)| Microsoft Docs
description: CrmServiceClient クラスを使用して、コード生成ツールでエンティティ クラスとデータ コンテキスト クラスを設定できます。 サンプルでは、このクラスのインスタンスを使用してアプリ用 CDS への接続を作成し、OrganizationServiceProxy オブジェクトの値を CrmServiceClient.OrganizationServiceProxy プロパティに設定する方法を示しています。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 7c81c1e5-2229-4a15-8374-6ee9456d18a9
caps.latest.revision: 19
author: MattB-msft
ms.author: kvivek
manager: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="use-xrm-tooling-with-classes-generated-using-the-code-generation-tool"></a>コード生成ツールを使用して生成されたクラスに XRM ツールを使用

<!-- TODO:
The <xref:Microsoft.Xrm.Tooling.Connector> assembly doesn’t directly provide interfaces for the entity and data context classes generated using the code-generation tool. However, you can use the CDS for Apps connection created by the <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient> class to set up your entity and data context classes by using the code-generation tool. More information: [Create Early Bound Entity Classes with the Code Generation Tool (CrmSvcUtil.exe)](../org-service/create-early-bound-entity-classes-code-generation-tool.md) -->
  
 <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient> クラスによって作成されたアプリ用 CDS 接続を使用するには、このクラスのインスタンスを使用してアプリ用 CDS への接続を作成し、<xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceProxy> オブジェクトの値を <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient>.<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient.OrganizationServiceProxy> プロパティに設定します。 プロパティに設定します。  
  
```csharp  
CrmServiceClient crmSvc = new CrmServiceClient(new System.Net.NetworkCredential("<UserName>", "<Password>",“<Domain>”),"<Server>", "<Port>", "<OrgName>");  
  
// Verify that you are connected.  
if (crmSvc != null && crmSvc.IsReady)  
{  
    //Display the CRM version number and org name that you are connected to  
    Console.WriteLine("Connected to CRM! (Version: {0}; Org: {1}",   
    crmSvc.ConnectedOrgVersion, crmSvc.ConnectedOrgUniqueName);  
  
    Microsoft.Xrm.Sdk.Client.OrganizationServiceProxy prox = crmSvc.OrganizationServiceProxy;   
}  
else  
{  
    // Display the last error.  
    Console.WriteLine("Error occurred: {0}", crmSvc.LastCrmError);  
  
    // Display the last exception message if any.  
    Console.WriteLine(crmSvc.LastCrmException.Message);  
    Console.WriteLine(crmSvc.LastCrmException.Source);  
    Console.WriteLine(crmSvc.LastCrmException.StackTrace);  
  
    return;  
}  
  
```  
  
> [!NOTE]
>  <xref:Microsoft.Xrm.Sdk.Client.OrganizationServiceProxy> クラスは、スレッド セーフではありません。 コード生成ツールまたは LINQ を使用して生成されたエンティティおよびデータ コンテキストを使用して作業してデータを取得する際、マルチスレッド環境で実行する場合には、コード内でロック スキームの作成を検討する場合があります。  
  
### <a name="see-also"></a>関連項目  

<!-- TODO:
[Use the IOrganizationService Web Service to Read and Write Data or Metadata](../org-service/use-organization-service-read-write-data-metadata.md)<br /> -->
[XRM ツールを使用して Windows のクライアント アプリケーションを作成](build-windows-client-applications-xrm-tools.md)

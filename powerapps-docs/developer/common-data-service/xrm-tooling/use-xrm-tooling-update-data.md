---
title: データを更新するために XRM ツールを使用する (Common Data Service)| Microsoft Docs
description: Common Data Service で CrmServiceClient クラスを使用してデータを更新
ms.custom: ''
ms.date: 03/27/2019
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 8ec3d4ca-d836-4e7e-b2bf-9d9f806bd145
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
# <a name="use-xrm-tooling-to-update-data"></a>XRM ツールを使用してデータを更新

Common Data Service でデータを更新するために、<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient> クラスには、<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient.UpdateEntity(System.String,System.String,System.Guid,System.Collections.Generic.Dictionary{System.String,Microsoft.Xrm.Tooling.Connector.CrmDataTypeWrapper},System.String,System.Boolean,System.Guid)> と <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient.UpdateStateAndStatusForEntity(System.String,System.Guid,System.String,System.String,System.Guid)> の 2 つのメソッドが用意されています。  
  
XRM ツール API を使用し更新操作にはデータ ペイロードが必要です。 データ ペイロードは Dictionary\<string, CrmDataTypeWrapper> オブジェクトの形式をとります。 <xref:Microsoft.Xrm.Tooling.Connector.CrmDataTypeWrapper> を使用して、参照するデータ ポイントに対してどのような処理を適用する必要があるか、インターフェイスに通知します。  
  
## <a name="updateentity"></a>UpdateEntity  

これは、レコードのステータスや状態の設定を除いて、Common Data Service でレコードを更新するための anchor メソッドです。 これを使用するには、いくつかの情報を知る必要があります。更新対象のエンティティのスキーマ名、更新するエンティティの主キー フィールド、更新するレコードの GUID、および更新に使用するデータ ペイロードの配列がそれです。  
  
```csharp  
CrmServiceClient svc = new CrmServiceClient(connectionstring);  
  
// Verify that you are connected  
if (svc != null && svc.IsReady)  
{ 
   // Update the account record  
    Dictionary<string, CrmDataTypeWrapper> updateData = new Dictionary<string, CrmDataTypeWrapper>();  
    updateData.Add("name", new CrmDataTypeWrapper("Updated Sample Account Name", CrmFieldType.String));  
    updateData.Add("address1_city", new CrmDataTypeWrapper("Boston", CrmFieldType.String));  
    updateData.Add("telephone1", new CrmDataTypeWrapper("555-0161", CrmFieldType.String));   
    bool updateAccountStatus = svc.UpdateEntity("account","accountid",_accountId,updateData);  
  
    // Validate if the account record was updated successfully, and then display the updated information  
    if (updateAccountStatus == true)  
    {  
        Console.WriteLine("Updated the account details as follows:");  
        Dictionary<string, object> data = svc.GetEntityDataById("account", accountId, null);  
        foreach (var pair in data)  
        {  
            if ((pair.Key == "name") || (pair.Key == "address1_city") || (pair.Key == "telephone1"))  
            {  
                Console.WriteLine(pair.Key.ToUpper() + ": " + pair.Value);  
            }  
        }  
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
  
## <a name="updatestateandstatusforentity"></a>UpdateStateAndStatusForEntity
 
このメソッドは、Common Data Service でレコードの状態を設定するために使用します。 たとえば、通常、すべてのレコードは "オープン" 状態で起動されます。 状態の名前は、レコードの種類に基づいて、もしくは開発者の選択によって変更されます。 たとえば、見積もりは、**下書き**、**アクティブ**、**クローズ**、**失注**、**受注**という複数の状態とステータスをとります。  
  
エンティティの状態を更新するには、対象の状態とステータスを名前または ID のいずれかで認識することが必要です。 ID と名前のどちらも、エンティティのメタデータをクエリし、ステータス フィールドと状態フィールドを調べることによって確認することができます。 この例では、取引先企業レコードのステータスを**非アクティブ**に設定する方法を示します。  
  
```csharp  
CrmServiceClient svc = new CrmServiceClient(connectionstring);  
  
// Verify that you are connected  
if (svc != null && svc.IsReady)  
{   
    // Here are the state and status code values  
    // statecode = 1 ( Inactive )   
    // statuscode = 2 ( Inactive )   
  
    svc.UpdateStateAndStatusForEntity("account" , accountId , 1 , 2 );  
  
    // the same command using the second form of the method  
    svc.UpdateStateAndStatusForEntity("account" , accountId , "Inactive" , "Inactive");  
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
[XRM ツール API を使用して Common Data Service のアクションを実行する](use-xrm-tooling-execute-actions.md)<br />


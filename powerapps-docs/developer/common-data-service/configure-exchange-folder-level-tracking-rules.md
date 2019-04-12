---
title: Exchange フォルダー レベルの追跡ルールの構成 (Common Data Service) | Microsoft Docs
description: Exchange フォルダー レベルの追跡のルールの構成について説明します。
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
# <a name="configure-exchange-folder-level-tracking-rules"></a>Exchange フォルダー レベルの追跡ルールの構成

Microsoft Exchange の受信トレイ フォルダーを Common Data Service レコードにマップできるようにするフォルダー レベルの追跡ルールを構成します。これにより、Microsoft Exchange フォルダー内のすべての電子メールが Common Data Service のマップされたレコードに対して自動的に追跡されます。 電子メールのフォルダー レベルの追跡は、以下の場合にのみ使用できます。  

- フォルダー レベルの追跡機能が Common Data Service インスタンスに対して有効化されている。 Web クライアントや Dynamics 365 for Outlook を使用して、フォルダー レベルの追跡を有効にできます。 詳細: [フォルダー レベルの追跡](/dynamics365/customer-engagement/admin/configure-outlook-exchange-folder-level-tracking)  

- 追跡の対象のフォルダーが、Microsoft Exchange の**受信トレイ**の下にあります。 **受信トレイ**の下にないフォルダーの電子メールは追跡されません。  

<a name="Create"></a>   

## <a name="create-and-manage-folder-level-tracking-rules"></a>フォルダー レベルの追跡のルールの作成と管理 
 
 フォルダー レベルの追跡のルールをプログラムで構成および管理するには、 [MailboxTrackingFolder エンティティ](/reference/entities/mailboxtrackingfolder.md)を使用します。 追跡ルールを設定するには、以下の属性を使用します。  


|                                   属性                                   |                                                                                                                                                                                                                説明                                                                                                                                                                                                                 |
|-------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|  [ExchangeFolderId](/reference/entities/mailboxtrackingfolder.md#BKMK_ExchangeFolderId)  | マッピングする Microsoft Exchange フォルダー ID を指定します。 Exchange Web サービス (EWS) を使用して、受信トレイの下にあるフォルダーの ID を取得できます。 詳細については、「[MSDN: Exchange で EWS を使用してフォルダーを操作する方法について](https://msdn.microsoft.com/library/office/dn535504.aspx)」を参照してください。 これは必須の属性です。 |
|         [MailboxId](/reference/entities/mailboxtrackingfolder.md#BKMK_MailboxId)         |                                                                                                                                         Common Data Service でルールを作成する対象のメールボックス ID を指定します。 これは必須の属性です。                                                                                                                                          |
| [RegardingObjectId](/reference/entities/mailboxtrackingfolder.md#BKMK_RegardingObjectId) |                                                                                                       指定した Microsoft Exchange フォルダーのマップ先となる Common Data Service の関連オブジェクトを設定します。 これは任意の属性です。                                                                                                       |

 次のサンプル コードは、フォルダー レベルの追跡のルールの作成方法を示しています。  

```csharp  
// Create a folder-level tracking rule  
MailboxTrackingFolder newTrackingFolder = new MailboxTrackingFolder();  

// Set the required attributes  
newTrackingFolder.ExchangeFolderId = "123456"; // Sample value. Retrieve this value using Exchange Web Services (EWS)  
newTrackingFolder.MailboxId = new EntityReference(Mailbox.EntityLogicalName, _mailboxId);  

// Set the optional attributes  
newTrackingFolder.RegardingObjectId = new EntityReference(Account.EntityLogicalName, _accountId);  
newTrackingFolder.RegardingObjectId.Name = _accountName;  
newTrackingFolder.ExchangeFolderName = "Sample Exchange Folder";  

// Execute the request to create the rule   
_folderTrackingId = _serviceProxy.Create(newTrackingFolder);  
Console.WriteLine("Created folder-level tracking rule for '{0}'.\n", _mailboxName);  
```  

 メールボックスごとに、フォルダー レベルの追跡のルールを最大 25 まで作成できます。 Microsoft Exchange フォルダーのフォルダー ID は、SDK を使用してマッピングの作成時点では検証できません。 ただし、マッピング ルールを作成した時点でそのフォルダー ID が無効な場合、マッピングが無効であることを示すために Common Data Service の UI に表示されます。  

 フォルダー レベルの追跡のルールの結果、Common Data Service に作成された追跡対象の活動レコードに含まれる関連オブジェクトに手動で変更を加えた場合、その変更は次のサーバー側同期が行われたときに上書きされます。 たとえば `Adventure Works` フォルダーと `Adventure Works` 取引先企業との間にマッピングを設定した場合、`Adventure Works` Microsoft Exchange フォルダーにあるすべての電子メールは、`Adventure Works` 取引先企業レコードとの関連を保った状態で Common Data Service の活動として追跡されます。 他のレコードとのいくつかの活動の関連を変更した場合は、次にサーバー側同期が動作したときにその変更は自動的に上書きされます。  

<a name="Retrieve"></a>   

## <a name="retrieve-folder-level-tracking-rules-for-a-mailbox"></a>メールボックスのフォルダー レベルの追跡のルールの取得  

 <xref:Microsoft.Crm.Sdk.Messages.RetrieveMailboxTrackingFoldersRequest> メッセージを使用して、メールボックスのすべてのフォルダー レベルの追跡のルールを取得できます。 <xref:Microsoft.Crm.Sdk.Messages.RetrieveMailboxTrackingFoldersRequest>.<xref:Microsoft.Crm.Sdk.Messages.RetrieveMailboxTrackingFoldersRequest.MailboxId> プロパティでルールを取得するメールボックス ID を渡し、メッセージを実行します。  

 次のサンプル コードは、メールボックスのフォルダー レベルの追跡のルールの取得方法を示しています。  

```csharp  
// Retrieve the folder mapping rules for a mailbox  
RetrieveMailboxTrackingFoldersRequest req = new RetrieveMailboxTrackingFoldersRequest  
{  
    MailboxId = _mailboxId.ToString()  
};  

RetrieveMailboxTrackingFoldersResponse resp = (RetrieveMailboxTrackingFoldersResponse_serviceProxy.Execute(req);  
Console.WriteLine("Retrieved folder-level tracking rules for {0}:", _mailboxName);  
int n = 1;  
foreach (var folderMapping in resp.MailboxTrackingFolderMappings)  
{  
    Console.WriteLine("\tRule {0}: '{1}' is mapped to '{2}'.",   
        n, folderMapping.ExchangeFolderName, folderMapping.RegardingObjectName);  
    n++;  
}  
```  

### <a name="see-also"></a>関連項目  
 <xref href="Microsoft.Dynamics.CRM.RetrieveMailboxTrackingFolders?text=RetrieveMailboxTrackingFolders Function" /><br />
 [MailboxTrackingFolder エンティティ](/reference/entities/mailboxtrackingfolder.md)<br />
 [Mailbox エンティティ](/reference/entities/mailbox.md)<br />
 [フォルダー レベルの追跡の構成](/dynamics365/customer-engagement/admin/configure-outlook-exchange-folder-level-tracking)<br />
 [サーバー側の同期エンティティ](server-side-synchronization-entities.md)<br />

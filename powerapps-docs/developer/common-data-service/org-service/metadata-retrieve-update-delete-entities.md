---
title: <Topic Title> (アプリ用 Common Data Service) | Microsoft Docs
description: <Description>
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
# <a name="retrieve-update-and-delete-entities"></a>エンティティの取得、更新、および削除

このトピックでは、「[ユーザー定義エンティティの作成](create-custom-entity.md)」で作成したユーザー定義 `Bank Account` (銀行口座) エンティティを使用してエンティティを取得、更新、削除する方法を説明します。  
  
<a name="BKMK_RetrieveAndUpdateEntity"></a>  
 
## <a name="retrieve-and-update-an-entity"></a>エンティティの取得と更新  

 次のサンプルでは、<xref:Microsoft.Xrm.Sdk.Messages.RetrieveEntityRequest> メッセージでエンティティを取得します。 次に、そのエンティティを更新し、<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.IsMailMergeEnabled> プロパティを `false` に設定して差し込み印刷を無効にします。また、<xref:Microsoft.Xrm.Sdk.Messages.UpdateEntityRequest> の <xref:Microsoft.Xrm.Sdk.Messages.UpdateEntityRequest.HasNotes> を `true` に設定することで、このエンティティに `Annotation` エンティティへの関連付けを含められるようにして、このエンティティでメモを表示できるようにします。  
  
```csharp

RetrieveEntityRequest retrieveBankAccountEntityRequest = new RetrieveEntityRequest
{
 EntityFilters = EntityFilters.Entity,
 LogicalName = _customEntityName
};
RetrieveEntityResponse retrieveBankAccountEntityResponse = (RetrieveEntityResponse)_serviceProxy.Execute(retrieveBankAccountEntityRequest);
EntityMetadata BankAccountEntity = retrieveBankAccountEntityResponse.EntityMetadata;

// Disable Mail merge
BankAccountEntity.IsMailMergeEnabled = new BooleanManagedProperty(false);
// Enable Notes
UpdateEntityRequest updateBankAccountRequest = new UpdateEntityRequest
{
 Entity = BankAccountEntity,
 HasNotes = true
};



_serviceProxy.Execute(updateBankAccountRequest);
```
  
<a name="BKMK_DeleteCustomEntity"></a>   

## <a name="delete-a-custom-entity"></a>ユーザー定義エンティティの削除  

次のサンプルでは、<xref:Microsoft.Xrm.Sdk.Messages.DeleteEntityRequest> を使用し、`_customEntityName` 変数で指定した論理名を持つエンティティを削除します。  
  
```csharp

DeleteEntityRequest request = new DeleteEntityRequest()
{
 LogicalName = _customEntityName,
};
_serviceProxy.Execute(request);
```
  
### <a name="see-also"></a>関連項目  
 [IOrganizationService サンプルとヘルパー コードの使用](/dynamics365/customer-engagement/developer/use-sample-helper-code)   
 [エンティティ メタデータのカスタマイズ](../customize-entity-metadata.md)   
 [電子メール活動を送信するエンティティの作成および更新](/dynamics365/customer-engagement/developer/create-update-entity-emailed)   
 [ユーザー定義エンティティを作成する](create-custom-entity.md)
---
title: ユーザー定義エンティティの作成 (Common Data Service) | Microsoft Docs
description: Common Data Service でユーザー定義エンティティをプログラムで作成する方法を示します。
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
# <a name="create-custom-entity"></a>ユーザー定義エンティティの作成

このトピックでは、ユーザーが所有する **Bank Account** (銀行口座) という名前のユーザー定義エンティティをプログラムで作成し、そのエンティティに対して 4 種類の属性を追加する方法について説明します。  
  
組織所有のカスタム エンティティも作成できます。 詳細情報: [エンティティの所有権](/dynamics365/customer-engagement/developer/introduction-entities#entity-ownership)  
  
> [!NOTE]
>  このエンティティは、エンティティのプロパティを編集して**このエンティティが表示される領域**を設定しない限り、アプリケーション ナビゲーションには表示されません。  
  
<a name="BKMK_CreateCustomEntity"></a>   

## <a name="create-a-custom-entity"></a>ユーザー定義エンティティの作成  

 以下のサンプルは、<xref:Microsoft.Xrm.Sdk.Messages.CreateEntityRequest> を使用してエンティティおよび <xref:Microsoft.Xrm.Sdk.Metadata.StringAttributeMetadata><xref:Microsoft.Xrm.Sdk.Messages.CreateEntityRequest.PrimaryAttribute>を作成します。  
  
 `_customEntityName` 値は "new_bankaccount" です。  
  
```csharp
CreateEntityRequest createrequest = new CreateEntityRequest
{

 //Define the entity
 Entity = new EntityMetadata
 {
  SchemaName = _customEntityName,
  DisplayName = new Label("Bank Account", 1033),
  DisplayCollectionName = new Label("Bank Accounts", 1033),
  Description = new Label("An entity to store information about customer bank accounts", 1033),
  OwnershipType = OwnershipTypes.UserOwned,
  IsActivity = false,

 },

 // Define the primary attribute for the entity
 PrimaryAttribute = new StringAttributeMetadata
 {
  SchemaName = "new_accountname",
  RequiredLevel = new AttributeRequiredLevelManagedProperty(AttributeRequiredLevel.None),
  MaxLength = 100,
  FormatName = StringFormatName.Text,
  DisplayName = new Label("Account Name", 1033),
  Description = new Label("The primary attribute for the Bank Account entity.", 1033)
 }

};
_serviceProxy.Execute(createrequest);
Console.WriteLine("The bank account entity has been created.");
```  
  
<a name="BKMK_AddStringAttribute"></a>   

## <a name="add-a-string-attribute-to-the-custom-entity"></a>文字列属性をユーザー定義エンティティに追加する  

以下のサンプルは、<xref:Microsoft.Xrm.Sdk.Metadata.StringAttributeMetadata> 属性を `Bank Account` エンティティに追加します。  
  
```csharp
CreateAttributeRequest createBankNameAttributeRequest = new CreateAttributeRequest
{
 EntityName = _customEntityName,
 Attribute = new StringAttributeMetadata
 {
  SchemaName = "new_bankname",
  RequiredLevel = new AttributeRequiredLevelManagedProperty(AttributeRequiredLevel.None),
  MaxLength = 100,
  FormatName = StringFormatName.Text,
  DisplayName = new Label("Bank Name", 1033),
  Description = new Label("The name of the bank.", 1033)
 }
};

_serviceProxy.Execute(createBankNameAttributeRequest);
```
  
<a name="BKMK_AddMoneyAttribute"></a>   

## <a name="add-a-money-attribute-to-the-custom-entity"></a>通貨属性をユーザー定義エンティティに追加する  

 以下のサンプルは、<xref:Microsoft.Xrm.Sdk.Metadata.MoneyAttributeMetadata> 属性を `Bank Account` エンティティに追加します。  
  
```csharp
CreateAttributeRequest createBalanceAttributeRequest = new CreateAttributeRequest
{
 EntityName = _customEntityName,
 Attribute = new MoneyAttributeMetadata
 {
  SchemaName = "new_balance",
  RequiredLevel = new AttributeRequiredLevelManagedProperty(AttributeRequiredLevel.None),
  PrecisionSource = 2,
  DisplayName = new Label("Balance", 1033),
  Description = new Label("Account Balance at the last known date", 1033),

 }
};

_serviceProxy.Execute(createBalanceAttributeRequest);

```  
  
<a name="BKMK_AddDateTimeAttribute"></a>   

## <a name="add-a-datetime-attribute-to-the-custom-entity"></a>datetime 属性をユーザー定義エンティティに追加する  

以下のサンプルは、<xref:Microsoft.Xrm.Sdk.Metadata.DateTimeAttributeMetadata> 属性を `Bank Account` エンティティに追加します。  
  
```csharp
CreateAttributeRequest createCheckedDateRequest = new CreateAttributeRequest
{
 EntityName = _customEntityName,
 Attribute = new DateTimeAttributeMetadata
 {
  SchemaName = "new_checkeddate",
  RequiredLevel = new AttributeRequiredLevelManagedProperty(AttributeRequiredLevel.None),
  Format = DateTimeFormat.DateOnly,
  DisplayName = new Label("Date", 1033),
  Description = new Label("The date the account balance was last confirmed", 1033)

 }
};

_serviceProxy.Execute(createCheckedDateRequest);
Console.WriteLine("An date attribute has been added to the bank account entity.");
```
  
<a name="BKMK_AddLookupAttribute"></a>
   
## <a name="add-a-lookup-attribute-to-the-custom-entity"></a>検索属性をユーザー定義エンティティに追加する 
 
 以下のサンプルは、<xref:Microsoft.Xrm.Sdk.Messages.CreateOneToManyRequest> を使用して `Contact` エンティティとの 1 対多の関連付けを作成し、<xref:Microsoft.Xrm.Sdk.Metadata.LookupAttributeMetadata> 属性が `Bank Account` エンティティに追加されるようにします。  
  
```csharp
CreateOneToManyRequest req = new CreateOneToManyRequest()
{
    Lookup = new LookupAttributeMetadata()
    {
        Description = new Label("The referral (lead) from the bank account owner", 1033),
        DisplayName = new Label("Referral", 1033),
        LogicalName = "new_parent_leadid",
        SchemaName = "New_Parent_leadId",
        RequiredLevel = new AttributeRequiredLevelManagedProperty(AttributeRequiredLevel.Recommended)
    },
    OneToManyRelationship = new OneToManyRelationshipMetadata()
    {
        AssociatedMenuConfiguration = new AssociatedMenuConfiguration()
        {
            Behavior = AssociatedMenuBehavior.UseCollectionName,
            Group = AssociatedMenuGroup.Details,
            Label = new Label("Bank Accounts", 1033),
            Order = 10000
        },
        CascadeConfiguration = new CascadeConfiguration()
        {
            Assign = CascadeType.Cascade,
            Delete = CascadeType.Cascade,
            Merge = CascadeType.Cascade,
            Reparent = CascadeType.Cascade,
            Share = CascadeType.Cascade,
            Unshare = CascadeType.Cascade
        },
        ReferencedEntity = "lead",
        ReferencedAttribute = "leadid",
        ReferencingEntity = _customEntityName,
        SchemaName = "new_lead_new_bankaccount"
    }
};
_serviceProxy.Execute(req);
```
  
### <a name="see-also"></a>関連項目  
 [IOrganizationService サンプルとヘルパー コードの使用](/dynamics365/customer-engagement/developer/use-sample-helper-code)   
 <xref:Microsoft.Xrm.Sdk.Messages.CreateEntityRequest>   
 [エンティティ メタデータのカスタマイズ](../customize-entity-metadata.md)   
 [カスタマイズ可能なエンティティ](/dynamics365/customer-engagement/developer/which-entities-are-customizable)   
 [エンティティの取得、更新、および削除](/dynamics365/customer-engagement/developer/retrieve-update-delete-entities)   
 [電子メール活動を送信するエンティティの作成および更新](/dynamics365/customer-engagement/developer/create-update-entity-emailed)   
 [カスタム活動エンティティの作成](/dynamics365/customer-engagement/developer/create-custom-activity-entity)   
 [エンティティ アイコンの変更](/dynamics365/customer-engagement/developer/modify-icons-entity)   
 [エンティティ メッセージの変更](/dynamics365/customer-engagement/developer/modify-messages-entity)

---
title: 電子メール アクティビティをレコードに送信するエンティティを作成および更新する (Common Data Service) | Microsoft Docs
description: エンティティのレコードに電子メール活動を送信するために使用可能な、電子メール アドレスを含むエンティティの作成について学習します。
ms.custom: ''
ms.date: 04/05/2019
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
# <a name="create-and-update-an-entity-to-send-email-activities-to-records"></a>電子メール アクティビティをレコードに送信するエンティティを作成および更新する

電子メール アドレスを含むエンティティを作成できます。このアドレスは、エンティティのレコードに電子メール活動を送信するために使用できます。  
  
 次のサンプル コードでは、カスタム エンティティを作成し、その <xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.IsActivityParty> プロパティを `true` に設定します。 また、attribute using <xref:Microsoft.Xrm.Sdk.Metadata.StringFormatName> を使用して <xref:Microsoft.Xrm.Sdk.Metadata.StringAttributeMetadata> 属性を作成します。`Email` は使用する電子メール アドレスを指定します。  
  
 他の <xref:Microsoft.Xrm.Sdk.Metadata.StringAttributeMetadata> 属性を電子メール アドレスとして追加する場合でも、使用されるのは最初に指定した属性のみです。  

```csharp
// Create the custom entity.
CreateEntityRequest createrequest = new CreateEntityRequest
{
    // Define an entity to enable for emailing. In order to do so,
    // IsActivityParty must be set.
    Entity = new EntityMetadata
    {
        SchemaName = _customEntityName,
        DisplayName = new Label("Agent", 1033),
        DisplayCollectionName = new Label("Agents", 1033),
        Description = new Label("Insurance Agents", 1033),
        OwnershipType = OwnershipTypes.UserOwned,
        IsActivity = false,

        // Unless this flag is set, this entity cannot be party to an
        // activity.
        IsActivityParty = true
    },

    // As with built-in emailable entities, the Primary Attribute will
    // be used in the activity party screens. Be sure to choose descriptive
    // attributes.
    PrimaryAttribute = new StringAttributeMetadata
    {
        SchemaName = "new_fullname",
        RequiredLevel = new AttributeRequiredLevelManagedProperty(AttributeRequiredLevel.None),
        MaxLength = 100,
        FormatName = StringFormatName.Text,
        DisplayName = new Label("Agent Name", 1033),
        Description = new Label("Agent Name", 1033)
    }
};

_serviceProxy.Execute(createrequest);
Console.WriteLine("The emailable entity has been created.");

// The entity will not be selectable as an activity party until its customizations
// have been published. Otherwise, the e-mail activity dialog cannot find
// a correct default view.
PublishAllXmlRequest publishRequest = new PublishAllXmlRequest();
_serviceProxy.Execute(publishRequest);

// Before any emails can be created for this entity, an Email attribute
// must be defined.
CreateAttributeRequest createFirstEmailAttributeRequest = new CreateAttributeRequest
{
    EntityName = _customEntityName,
    Attribute = new StringAttributeMetadata
    {
        SchemaName = "new_emailaddress",
        RequiredLevel = new AttributeRequiredLevelManagedProperty(AttributeRequiredLevel.None),
        MaxLength = 100,
        FormatName = StringFormatName.Email,
        DisplayName = new Label("Email Address", 1033),
        Description = new Label("Email Address", 1033)
    }
};

_serviceProxy.Execute(createFirstEmailAttributeRequest);
Console.WriteLine("An email attribute has been added to the emailable entity.");

// Create a second, alternate email address. Since there is already one 
// email attribute on the entity, this will never be used for emailing
// even if the first one is not populated.
CreateAttributeRequest createSecondEmailAttributeRequest = new CreateAttributeRequest
{
    EntityName = _customEntityName,
    Attribute = new StringAttributeMetadata
    {
        SchemaName = "new_secondaryaddress",
        RequiredLevel = new AttributeRequiredLevelManagedProperty(AttributeRequiredLevel.None),
        MaxLength = 100,
        FormatName = StringFormatName.Email,
        DisplayName = new Label("Secondary Email Address", 1033),
        Description = new Label("Secondary Email Address", 1033)
    }
};

_serviceProxy.Execute(createSecondEmailAttributeRequest);

Console.WriteLine("A second email attribute has been added to the emailable entity.");
```

### <a name="see-also"></a>関連項目

[組織サービスを使用したエンティティの作成](entity-operations-create.md)  
[組織サービスを使用したエンティティの更新と削除](entity-operations-update-delete.md)

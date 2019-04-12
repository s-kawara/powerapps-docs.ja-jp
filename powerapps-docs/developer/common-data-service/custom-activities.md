---
title: ユーザー定義の活動 (Common Data Service) | Microsoft Docs
description: ユーザー定義の活動は、Dynamics 365 のインスタント メッセージング (IM) やショート メッセージ サービス (SMS) などの業務上の通信ニーズをサポートします。
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
# <a name="custom-activities"></a>ユーザー定義の活動

Common Data Service でカスタム活動を作成し、インスタント メッセージング (IM) やショート メッセージ サービス (SMS) などの業務上の通信ニーズをサポートできます。 Common Data Service でユーザー定義の活動を作成するには、ユーザー定義エンティティを作成し、<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.IsActivity> を使用してこのエンティティを活動エンティティとして指定します。 にバインドされます。  
  
 ただし、他のユーザー定義エンティティと異なり、ユーザー定義活動には主属性を指定できません。これは、ユーザー定義活動の主属性は既定で "Subject" という名前にする必要があるためです。  
  
 カスタム活動エンティティを作成すると、`activitypointer` エンティティのすべてのプロパティと特権がカスタム活動に継承されます。 また、すべての活動関係者の種類をカスタム活動に使用できるようになり、その結果として対応するプロパティも継承されます。  
  
 他の活動と同じように、カスタム活動にも 1 対多 (1:N) の関連付けを作成できます。また、既存の関連付けを更新できます。  
  
## <a name="privileges-and-access-rights"></a>特権およびアクセス権 
 
 ユーザー定義の活動を操作するには、ユーザー定義エンティティを操作する場合と同等の Common Data Service の特権およびアクセス権セットが必要です。 ユーザー定義エンティティの詳細については、[エンティティ メタデータのカスタマイズ](customize-entity-metadata.md) を参照してください。  
  
## <a name="creating-a-custom-activity"></a>ユーザー定義の活動の作成  
 カスタム活動エンティティを作成するには、以下の表に示すプロパティの値を設定します。  
  
|プロパティ名|値|注意|  
|-------------------|-----------|-----------|  
|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.IsActivity>|`true`|ユーザー定義エンティティをカスタム活動として指定します。|  
|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.IsAvailableOffline>|`true`|カスタム活動エンティティをオフラインで使用できるようにする必要があります。|  
|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.IsMailMergeEnabled>|`false`|カスタム活動エンティティの差し込み印刷を有効にすることはできません。|  
|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.OwnershipType>|<xref:Microsoft.Xrm.Sdk.Metadata.OwnershipTypes>. TeamOwned<br />または<br /><xref:Microsoft.Xrm.Sdk.Metadata.OwnershipTypes>. ユーザーによる所有|カスタム活動エンティティはチーム所有またはユーザー所有にすることができます。|  
|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.ActivityTypeMask>|0 - なし<br />または<br />1 – 通信活動|(任意) カスタム活動を Web アプリケーションの活動メニューに表示するかどうかを指定します。<br /><br /> -   活動メニューに表示しない場合は **0 (なし)** を指定します。 カスタム活動は関連する (関連付けがある) エンティティのみの関連グリッドに表示されます。<br />-   活動メニューに表示する場合は **1 (通信活動)** を指定します。<br /><br /> このプロパティを指定しない場合、カスタム活動は既定のプロパティ値 (1) で作成されます。 つまり、カスタム活動は活動メニューに表示されます。 また、`ActivityTypeMask` は活動の作成時にのみ設定できます。一度設定したら、変更はできません。|  
|<xref:Microsoft.Xrm.Sdk.Messages.CreateEntityRequest>.<xref:Microsoft.Xrm.Sdk.Messages.CreateEntityRequest.HasActivities>|`false`|カスタム活動エンティティには活動との関連付けを設定できません。|  
|<xref:Microsoft.Xrm.Sdk.Messages.CreateEntityRequest>.<xref:Microsoft.Xrm.Sdk.Messages.CreateEntityRequest.HasNotes>|`true`|カスタム活動エンティティにはメモへの関連付けを設定する必要があります。|  
|<xref:Microsoft.Xrm.Sdk.Messages.CreateEntityRequest>. <xref:Microsoft.Xrm.Sdk.Messages.CreateEntityRequest.PrimaryAttribute>|<xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata.SchemaName> は "Subject" です。|すべての活動の `PrimaryAttribute` のスキーマ名を "Subject" にする必要があります。|  
  
## <a name="example"></a>例  
 次のサンプルはユーザー定義の活動を作成する方法を示します。  
  
```csharp
String prefix = "new_";

String customEntityName = prefix + "instantmessage";

// Create the custom activity entity.
CreateEntityRequest request = new CreateEntityRequest
{
    HasNotes = true,
    HasActivities = false,
    PrimaryAttribute = new StringAttributeMetadata
    {
        SchemaName = "Subject",
        RequiredLevel = new AttributeRequiredLevelManagedProperty(AttributeRequiredLevel.None),
        MaxLength = 100,
        DisplayName = new Label("Subject", 1033)
    },
    Entity = new EntityMetadata
    {
        IsActivity = true,
        SchemaName = customEntityName,
        DisplayName = new Label("Instant Message", 1033),
        DisplayCollectionName = new Label("Instant Messages", 1033),
        OwnershipType = OwnershipTypes.UserOwned,
        IsAvailableOffline = true,

    }
};

_serviceProxy.Execute(request);

//Entity must be published
``` 

### <a name="see-also"></a>関連項目  
 [活動エンティティ](activity-entities.md)   
 [ActivityPointer (活動) エンティティ](activitypointer-activity-entity.md)   
 [サンプル: カスタム活動の作成](/dynamics365/customer-engagement/developer/sample-create-custom-activity)   
 [サンプル: エンティティ メタデータの作成と更新](/dynamics365/customer-engagement/developer/org-service/sample-create-update-entity-metadata)
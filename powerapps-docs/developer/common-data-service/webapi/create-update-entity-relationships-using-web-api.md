---
title: Web API を使用したエンティティ関係の作成および更新 (Common Data Service) | Microsoft Docs
description: メタデータ駆動のアーキテクチャを使用してユーザー定義エンティティや追加のシステム エンティティ属性を柔軟に作成するのに役立つ Common Data Service エンティティの作成および更新について説明します。
ms.custom: ''
ms.date: 10/31/2018
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 923538e2-15fe-4718-8eae-d939c5d200cd
caps.latest.revision: 15
author: brandonsimons
ms.author: jdaly
ms.reviewer: susikka
manager: annbe
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="create-and-update-entity-relationships-using-the-web-api"></a>Web API を使用してエンティティ関係を作成および更新する


Web API は、リレーションシップ メタデータでの作業をサポートします。 [エンティティ関係メタデータ](../entity-relationship-metadata.md)で説明されている概念は、Web API にも適用されます。  

<a name="bkmk_RelationshipEligibility"></a>

## <a name="eligibility-for-relationships"></a>関連付けの有効性


エンティティ関係を作成する前に、それらのエンティティがその関連付けにふさわしいかどうかを確認してください。 次の表に表示されているアクションを使用して有効性を確認できます。 これらのアクションは、[エンティティの関連付けの有効性](../entity-relationship-eligibility.md) で説明されている組織サービス メッセージに対応します。  


  
|操作|内容|  
|------------|-----------------|  
|<xref href="Microsoft.Dynamics.CRM.CanBeReferenced?text=CanBeReferenced Action" />|指定されたエンティティが一対多の関連付けの主エンティティ (一) になるかどうかをチェックします。|  
|<xref href="Microsoft.Dynamics.CRM.CanBeReferencing?text=CanBeReferencing Action" />|指定されたエンティティが一対多の関連付けの参照エンティティ (多) になるかどうかをチェックします。|  
|<xref href="Microsoft.Dynamics.CRM.CanManyToMany?text=CanManyToMany Action" />|エンティティが多対多の関連付けに参加できるかどうかをチェックします。|  
|<xref href="Microsoft.Dynamics.CRM.GetValidManyToMany?text=GetValidManyToMany Function" />|多対多の関連付けに参加できる一連のエンティティを返します。|  
|<xref href="Microsoft.Dynamics.CRM.GetValidReferencedEntities?text=GetValidReferencedEntities Function" />|指定されたエンティティから、1 対多の関連付けの主エンティティ (1 の側) として有効な一連のエンティティを返します。|  
|<xref href="Microsoft.Dynamics.CRM.GetValidReferencingEntities?text=GetValidReferencingEntities Function" />|指定されたエンティティに、1 対多の関連付けの関連エンティティ (多の側) として有効な一連のエンティティを返します。|  
  
<a name="bkmk_createOnetoMany"></a>

## <a name="create-a-one-to-many-relationship"></a>一対多の関連付けを作成する

一対多の関連付けを作成する場合は、<xref href="Microsoft.Dynamics.CRM.OneToManyRelationshipMetadata?text=OneToManyRelationshipMetadata EntityType" /> を使用して定義します。 この定義には、<xref href="Microsoft.Dynamics.CRM.LookupAttributeMetadata?text=LookupAttributeMetadata EntityType" /> を使用して定義される検索属性が含まれ、<xref href="Microsoft.Dynamics.CRM.AssociatedMenuConfiguration?text=AssociatedMenuConfiguration ComplexType" /><xref href="Microsoft.Dynamics.CRM.CascadeConfiguration?text=CascadeConfiguration ComplexType" /><xref href="Microsoft.Dynamics.CRM.Label?text=Label ComplexType" /> および <xref href="Microsoft.Dynamics.CRM.LocalizedLabel?text=LocalizedLabel ComplexType" /> を使用した複雑なプロパティも必要です。 検索属性は `OneToManyRelationshipMetadata` オブジェクトの検索の単一値のナビゲーション プロパティに設定され、*ディープ挿入* を使用して同時に作成されます。 詳細: [1 回の操作で関連するエンティティを作成する](create-entity-web-api.md#bkmk_CreateRelated)および[エンティティの関連付けのメタデータ メッセージ](../entity-relationship-metadata.md)
  
一対多の関連付けにカスタム ナビゲーション プロパティ名を使用する場合は、 `ReferencingEntityNavigationPropertyName` および `ReferencedEntityNavigationPropertyName` プロパティの値を設定きます。  
  
関連付けと検索属性の定義に必要な JSON を生成したら、JSON を RelationshipDefinitions エンティティ セットに `POST` します。 作成する関連付けの種類を明確にするために Microsoft.Dynamics.CRM.OneToManyRelationshipMetadata の `@odata.type` プロパティ値を含める必要がありますが、これはこの同じエンティティ セットが多対多の関連付けの作成に使用されるためです。 作成された関連付けの URI が応答で返されます。  
  
 **要求**  
```http 
POST [Organization URI]/api/data/v9.0/RelationshipDefinitions HTTP/1.1  
Accept: application/json  
Content-Type: application/json; charset=utf-8  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
  
{  
 "SchemaName": "new_contact_new_bankaccount",  
 "@odata.type": "Microsoft.Dynamics.CRM.OneToManyRelationshipMetadata",  
 "AssociatedMenuConfiguration": {  
  "Behavior": "UseCollectionName",  
  "Group": "Details",  
  "Label": {  
   "@odata.type": "Microsoft.Dynamics.CRM.Label",  
   "LocalizedLabels": [  
    {  
     "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
     "Label": "Bank Accounts",  
     "LanguageCode": 1033  
    }  
   ],  
   "UserLocalizedLabel": {  
    "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
    "Label": "Bank Accounts",  
    "LanguageCode": 1033  
   }  
  },  
  "Order": 10000  
 },  
 "CascadeConfiguration": {  
  "Assign": "Cascade",  
  "Delete": "Cascade",  
  "Merge": "Cascade",  
  "Reparent": "Cascade",  
  "Share": "Cascade",  
  "Unshare": "Cascade"  
 },  
 "ReferencedAttribute": "contactid",  
 "ReferencedEntity": "contact",  
 "ReferencingEntity": "new_bankaccount",  
 "Lookup": {  
  "AttributeType": "Lookup",  
  "AttributeTypeName": {  
   "Value": "LookupType"  
  },  
  "Description": {  
   "@odata.type": "Microsoft.Dynamics.CRM.Label",  
   "LocalizedLabels": [  
    {  
     "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
     "Label": "The owner of the account",  
     "LanguageCode": 1033  
    }  
   ],  
   "UserLocalizedLabel": {  
    "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
    "Label": "The owner of the account",  
    "LanguageCode": 1033  
   }  
  },  
  "DisplayName": {  
   "@odata.type": "Microsoft.Dynamics.CRM.Label",  
   "LocalizedLabels": [  
    {  
     "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
     "Label": "Account Owner",  
     "LanguageCode": 1033  
    }  
   ],  
   "UserLocalizedLabel": {  
    "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
    "Label": "Account Owner",  
    "LanguageCode": 1033  
   }  
  },  
  "RequiredLevel": {  
   "Value": "ApplicationRequired",  
   "CanBeChanged": true,  
   "ManagedPropertyLogicalName": "canmodifyrequirementlevelsettings"  
  },  
  "SchemaName": "new_AccountOwner",  
  "@odata.type": "Microsoft.Dynamics.CRM.LookupAttributeMetadata"  
 }  
}  
```  
  
 **応答**  
```http 
HTTP/1.1 204 No Content  
OData-Version: 4.0  
OData-EntityId: [Organization URI]/api/data/v9.0/RelationshipDefinitions(d475020f-5d7c-e511-80d2-00155d2a68d2)  
```  
  
<a name="bkmk_CreateManyToMany"></a>
  
## <a name="create-a-many-to-many-relationship"></a>多対多の関連付けを作成する

<!-- TODO:
When you create a many-to-many relationship, you must the relationship by using the <xref href="Microsoft.Dynamics.CRM.ManyToManyRelationshipMetadata?text=ManyToManyRelationshipMetadata EntityType" />. This definition includes the name of the intersect entity to be created as well as how the relationship should be displayed in the application by using <xref href="Microsoft.Dynamics.CRM.AssociatedMenuConfiguration?text=AssociatedMenuConfiguration ComplexType" />, <xref href="Microsoft.Dynamics.CRM.Label?text=Label ComplexType" /> and <xref href="Microsoft.Dynamics.CRM.LocalizedLabel?text=LocalizedLabel ComplexType" />. More information:[Many-to-many relationships](../customize-entity-relationship-metadata.md#BKMK_ManyToManyRelationships)   -->
  
 多対多の関連付けにカスタム ナビゲーション プロパティ名を使用する場合は、 `Entity1NavigationPropertyName` および `Entity2NavigationPropertyName` プロパティの値を設定きます。  
  
 関連付けの定義に必要な JSON を生成したら、JSON を RelationshipDefinitions エンティティ セットに `POST` します。 作成する関連付けの種類を明確にするために Microsoft.Dynamics.CRM.ManyToManyRelationshipMetadata の `@odata.type` プロパティ値を含める必要がありますが、これはこの同じエンティティ セットが一対多の関連付けの作成に使用されるためです。 作成された関連付けの URI が応答で返されます。  
  
 **要求**
  
```http 
POST [Organization URI]/api/data/v9.0/RelationshipDefinitions HTTP/1.1  
Accept: application/json  
Content-Type: application/json; charset=utf-8  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
  
{  
 "SchemaName": "new_accounts_campaigns",  
 "@odata.type": "Microsoft.Dynamics.CRM.ManyToManyRelationshipMetadata",  
 "Entity1AssociatedMenuConfiguration": {  
  "Behavior": "UseLabel",  
  "Group": "Details",  
  "Label": {  
   "@odata.type": "Microsoft.Dynamics.CRM.Label",  
   "LocalizedLabels": [  
    {  
     "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
     "Label": "Account",  
     "LanguageCode": 1033  
    }  
   ],  
   "UserLocalizedLabel": {  
    "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
    "Label": "Account",  
    "LanguageCode": 1033  
   }  
  },  
  "Order": 10000  
 },  
 "Entity1LogicalName": "account",  
 "Entity2AssociatedMenuConfiguration": {  
  "Behavior": "UseLabel",  
  "Group": "Details",  
  "Label": {  
   "@odata.type": "Microsoft.Dynamics.CRM.Label",  
   "LocalizedLabels": [  
    {  
     "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
     "Label": "Campaign",  
     "LanguageCode": 1033  
    }  
   ],  
   "UserLocalizedLabel": {  
    "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
    "Label": "Campaign",  
    "LanguageCode": 1033  
   }  
  },  
  "Order": 10000  
 },  
 "Entity2LogicalName": "campaign",  
 "IntersectEntityName": "new_accounts_campaigns"  
}  
```  
  
 **応答**  
```http 
HTTP/1.1 204 No Content  
OData-Version: 4.0  
OData-EntityId: [Organization URI]/api/data/v9.0/RelationshipDefinitions(420245fa-c77c-e511-80d2-00155d2a68d2)    
```  
  
<a name="bkmk_updateRelationships"></a>

## <a name="update-relationships"></a>関連付けの更新

[エンティティの更新](create-update-entity-definitions-using-web-api.md#bkmk_updateEntities) で説明されているように、HTTP PUT メソッドを使用して関連付けを更新して、既存の定義を適用する変更と置き換えます。 ビジネス データ エンティティと同じように HTTP PATCH メソッドを使用して個々のプロパティを編集することはできません。 エンティティや属性の場合と同じように、 `true` に設定された値の `MSCRM.MergeLabels` 見出しを使用して、更新に含まれていないローカライズ済みのラベルの上書きを防止し、システムでアクティブ化される前にカスタマイズを公開する必要があります。  
  
<a name="bkmk_deleteRelationship"></a>
 
## <a name="delete-relationships"></a>関連付けの削除

Web API を使用して関連付けを削除するには、HTTP DELETE メソッドを関連付けの URI で使用します。  
  
### <a name="see-also"></a>関連項目

<!-- TODO:
[Customize entity relationship metadata](../customize-entity-relationship-metadata.md)<br /> -->
[Web API を Common Data Service メタデータで使用する](use-web-api-metadata.md)<br />
[Web API を使用したクエリ メタデータ](query-metadata-web-api.md)<br />
[名前または MetadataId でのメタデータの取得](retrieve-metadata-name-metadataid.md)<br />
[Web API を使用してエンティティおよび属性をモデリング](create-update-entity-definitions-using-web-api.md)

---
title: Web API を使用したクエリ メタデータ (アプリ用 Common Data Service) | Microsoft Docs
description: システム メタデータのクエリ機能は、 RetrieveMetadataChangesRequest を使用することによって、組織サービスだけでなく Web API を使用しても利用できます。
ms.custom: ''
ms.date: 11/04/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 3ad4a332-a304-421f-a9fa-82ea3e0503fe
caps.latest.revision: 18
author: brandonsimons
ms.author: jdaly
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="query-metadata-using-the-web-api"></a>Web API を使用したクエリ メタデータ

アプリ用 Common Data Service はメタデータ駆動型アプリケーションであるため、開発者は実行時にシステム メタデータをクエリして、組織が構成されている方法に適合させる必要があります。 この機能は RESTful クエリ スタイルを使用します。

> [!NOTE]
> また、<xref href="Microsoft.Dynamics.CRM.EntityQueryExpression?text=EntityQueryExpression ComplexType" /> と <xref href="Microsoft.Dynamics.CRM.RetrieveMetadataChanges?text=RetrieveMetadataChanges Function" />.を使用するオブジェクト ベース スタイルを使用してクエリを作成できます。 この関数によって、2 つの時間期間の間にメタデータへの変更を取得するほか、ユーザーが指定するクエリによって定義される限られたメタデータのセットを返せるようになります。

<a name="bkmk_QueryingEntityMetadata"></a>

## <a name="querying-the-entitymetadata-entity-type"></a>EntityMetadata エンティティ型をクエリ

EntityMetadata をクエリするとき、「[Web API を使用したクエリ データ](query-data-web-api.md)」に記載されているのと同じ方法を使用します。この方法にはいくつかのバリエーションがあります。 `EntityDefinitions` エンティティ セット パスを使用して、<xref href="Microsoft.Dynamics.CRM.EntityMetadata?text=EntityMetadata EntityType" /> に関する情報を取得します。 EntityMetadata エンティティには多数のデータが含まれているので、必要なデータのみを慎重に取得する必要があります。 次の例は、 `Account` エンティティのメタデータの DisplayName、IsKnowledgeManagementEnabled、および EntitySetName プロパティだけに対して返されるデータを示しています。 `MetadataId` プロパティ値は常に返されます。  
  
 **要求**

```http
GET [Organization URI]/api/data/v9.0/EntityDefinitions(LogicalName='account')?$select=DisplayName,IsKnowledgeManagementEnabled,EntitySetName HTTP/1.1  
Accept: application/json  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
```

 **応答**
```http
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  

{  
 "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#EntityDefinitions(DisplayName,IsKnowledgeManagementEnabled,EntitySetName)",  
 "value": [  
  {  
   "DisplayName": {  
    "LocalizedLabels": [  
     {  
      "Label": "Account",  
      "LanguageCode": 1033,  
      "IsManaged": true,  
      "MetadataId": "2a4901bf-2241-db11-898a-0007e9e17ebd",  
      "HasChanged": null  
     }  
    ],  
    "UserLocalizedLabel": {  
     "Label": "Account",  
     "LanguageCode": 1033,  
     "IsManaged": true,  
     "MetadataId": "2a4901bf-2241-db11-898a-0007e9e17ebd",  
     "HasChanged": null  
    }  
   },  
   "IsKnowledgeManagementEnabled": false,  
   "EntitySetName": "accounts",  
   "MetadataId": "70816501-edb9-4740-a16c-6a5efbc05d84"  
  }  
 ]  
}  
  
```

`$select` システム クエリ オプションが付いた `EntityMetadata` プロパティのいずれかを使用することが可能であり、またプリミティブ値や列挙値を使用するプロパティに対して `$filter` を使用することができます。  

クエリで返されるエンティティ メタデータの数に制限はありません。 ページングはありません。 すべての一致するリソースが最初の応答で返されます。  

<a name="bkmk_filterEnumTypes"></a>

## <a name="use-enum-types-in-filter-operations"></a>$filter 操作で enum 型の使用

列挙を使用するプロパティの値に基づいてエンティティ メタデータをフィルター処理する必要がある場合は、その文字列値の前に、その列挙の名前空間を含める必要があります。 Enum 型は、エンティティ メタデータおよび複合型のみのプロパティ値として使用されます。 たとえば、<xref href="Microsoft.Dynamics.CRM.OwnershipTypes?text=OwnershipTypes EnumType" /> を使用する `OwnershipType` プロパティに基づいてエンティティをフィルター処理する必要がある場合、次の `$filter` を使用して UserOwned であるエンティティのみを返すことができます。

```http
GET [Organization URI]/api/data/v9.0/EntityDefinitions?$select=LogicalName&$filter=OwnershipType eq Microsoft.Dynamics.CRM.OwnershipTypes'UserOwned'  
```

<a name="bkmk_complexTypesAsFilters"></a>

## <a name="use-complex-types-in-filter-operations"></a>$filter 操作で複合型の使用

複合型を使用するプロパティの値に基づいてエンティティ メタデータをフィルター処理する必要がある場合は、その文字列値の前に、基になるプリミティブ型へのパスを含める必要があります。 複合型は、エンティティ メタデータのみのプロパティ値として使用されます。 たとえば、<xref href="Microsoft.Dynamics.CRM.BooleanManagedProperty?text=BooleanManagedProperty ComplexType" /> を使用する CanCreateAttributes プロパティに基づいてエンティティをフィルター処理する必要がある場合、次の `$filter` を使用して `true` の `Value` を持つエンティティのみを返すことができます。

```http
GET [Organization URI]/api/data/v9.0/EntityDefinitions?$select=LogicalName&$filter=CanCreateAttributes/Value eq true  
```

このパターンは、チェックの対象のプリミティブ値は 1 レベル深いので、<xref href="Microsoft.Dynamics.CRM.BooleanManagedProperty?text=BooleanManagedProperty ComplexType" /> に対して機能します。 ただし、これは、<xref href="Microsoft.Dynamics.CRM.Label?text=Label ComplexType" /> のプロパティに対しては機能しません。  

<a name="bkmk_queryAttributes"></a>

## <a name="querying-entitymetadata-attributes"></a>EntityMetadata 属性をクエリ

`Attributes` コレクション値ナビゲーション プロパティを拡張することによってエンティティのコンテキストでエンティティ属性をクエリできますが、これには、すべての属性が共有する <xref href="Microsoft.Dynamics.CRM.AttributeMetadata?text=AttributeMetadata EntityType" /> で使用できる一般的なプロパティのみが含まれます。 たとえば、次のクエリは、そのエンティティの `LogicalName` と、`AttributeType` 値が `Picklist` の <xref href="Microsoft.Dynamics.CRM.AttributeTypeCode?text=AttributeTypeCode EnumType" /> 値と等しい、すべての展開された属性を返します。

<a name="bkmk_queryAttributesexample"></a>

```http
GET [Organization URI]/api/data/v9.0/EntityDefinitions(LogicalName='account')?$select=LogicalName&$expand=Attributes($select=LogicalName;$filter=AttributeType eq Microsoft.Dynamics.CRM.AttributeTypeCode'Picklist')  
```

<xref href="Microsoft.Dynamics.CRM.PicklistAttributeMetadata?text=PicklistAttributeMetadata EntityType" /> 属性のこのクエリの `$select` フィルターの範囲内にある、`OptionSet` または `GlobalOptionSet` コレクション値ナビゲーション プロパティを含めることはできません。  

特定の種類の属性のプロパティを取得するには、`Attributes` コレクション値ナビゲーション プロパティを必要な型にキャストする必要があります。 次のクエリは <xref href="Microsoft.Dynamics.CRM.PicklistAttributeMetadata?text=PicklistAttributeMetadata EntityType" /> 属性のみを返し、このクエリには `LogicalName` だけでなく、`OptionSet` および `GlobalOptionSet` コレクション値ナビゲーション プロパティの展開も含まれます  

```http
GET [Organization URI]/api/data/v9.0/EntityDefinitions(LogicalName='account')/Attributes/Microsoft.Dynamics.CRM.PicklistAttributeMetadata?$select=LogicalName&$expand=OptionSet,GlobalOptionSet  
```

> [!NOTE]
> `OptionSet` および `GlobalOptionSet` コレクション値ナビゲーション プロパティが <xref href="Microsoft.Dynamics.CRM.EnumAttributeMetadata?text=EnumAttributeMetadata EntityType" /> 内で定義されているにもかかわらず、これらの属性をこの型にキャストすることはできません。 すなわち、これらのプロパティも継承する他の種類に対してフィルター処理が必要な場合 (「[EnumAttributeMetadata から継承するエンティティの種類](/dynamics365/customer-engagement/web-api/enumattributemetadata?view=dynamics-ce-odata-9#Derived_Types)」を参照)、種類ごとにフィルター処理するためにクエリを別々に実行する必要があります。

このもう 1 つの例は、<xref href="Microsoft.Dynamics.CRM.MoneyAttributeMetadata?text=MoneyAttributeMetadata EntityType" /> および <xref href="Microsoft.Dynamics.CRM.DecimalAttributeMetadata?text=DecimalAttributeMetadata EntityType" /> 属性で使用できる `Precision` プロパティへのアクセスです。 このプロパティにアクセスするには、これらの属性のコレクションを <xref href="Microsoft.Dynamics.CRM.MoneyAttributeMetadata?text=MoneyAttributeMetadata EntityType" /> または <xref href="Microsoft.Dynamics.CRM.DecimalAttributeMetadata?text=DecimalAttributeMetadata EntityType" /> としてキャストする必要があります。 `MoneyAttributeMetadata` へのキャストを示す例を以下に示します。

```http
GET [Organization URI]/api/data/v9.0/EntityDefinitions(LogicalName='account')/Attributes/Microsoft.Dynamics.CRM.MoneyAttributeMetadata?$select=LogicalName,Precision
```

### <a name="filtering-by-required-level"></a>必要なレベル別のフィルター処理

<xref href="Microsoft.Dynamics.CRM.AttributeMetadata?text=AttributeMetadata EntityType" /> `RequiredLevel` プロパティは、`Value` プロパティが <xref href="Microsoft.Dynamics.CRM.AttributeRequiredLevel?text=AttributeRequiredLevel EnumType" /> である特殊な <xref href="Microsoft.Dynamics.CRM.AttributeRequiredLevelManagedProperty?text=AttributeRequiredLevelManagedProperty ComplexType" /> を使用します。 この場合には、「[$filter 操作で複合型の使用](query-metadata-web-api.md#bkmk_complexTypesAsFilters)」と「[$filter 操作で enum 型の使用](query-metadata-web-api.md#bkmk_filterEnumTypes)」にあるパターンを結合して、この固有のプロパティでフィルター処理する必要があります。 次のクエリでは、ApplicationRequired である取引先企業エンティティの属性をフィルター処理します。

```http
GET [Organization URI]/api/data/v9.0/EntityDefinitions(LogicalName='account')/Attributes?$select=SchemaName&$filter=RequiredLevel/Value eq Microsoft.Dynamics.CRM.AttributeRequiredLevel'ApplicationRequired'  
```

<a name="bkmk_retrieveAttributes"></a>

## <a name="retrieving-attributes"></a>属性の取得

EntityMetadata と AttributeMetadata の両方の MetadataId が分かっている場合、次のようにクエリを使用して、個々の属性を取得して、プロパティにアクセスできます。 このクエリは、OptionSet コレクション値ナビゲーション プロパティの展開だけでなく、この属性の LogicalName プロパティを取得します。 OptionSet コレクション値ナビゲーション プロパティにアクセスするには、この属性を Microsoft.Dynamics.CRM.PicklistAttributeMetadata としてキャストする必要があります。  

 **要求**
 ```http
GET [Organization URI]/api/data/v9.0/EntityDefinitions(LogicalName='account')/Attributes(5967e7cc-afbb-4c10-bf7e-e7ef430c52be)/Microsoft.Dynamics.CRM.PicklistAttributeMetadata?$select=LogicalName&$expand=OptionSet HTTP/1.1  
Accept: application/json  
Content-Type: application/json; charset=utf-8  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
```

 **応答**
 ```http
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0

{
 "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#EntityDefinitions(70816501-edb9-4740-a16c-6a5efbc05d84)/Attributes/Microsoft.Dynamics.CRM.PicklistAttributeMetadata(LogicalName,OptionSet)/$entity",  
 "LogicalName": "preferredappointmentdaycode",  
 "MetadataId": "5967e7cc-afbb-4c10-bf7e-e7ef430c52be",  
 "OptionSet@odata.context": "[Organization URI]/api/data/v9.0/$metadata#EntityDefinitions(70816501-edb9-4740-a16c-6a5efbc05d84)/Attributes(5967e7cc-afbb-4c10-bf7e-e7ef430c52be)/Microsoft.Dynamics.CRM.PicklistAttributeMetadata/OptionSet/$entity",  
 "OptionSet": {  
  "Options": [  
   {  
    "Value": 0,  
    "Label": {  
     "LocalizedLabels": [  
      {  
       "Label": "Sunday",  
       "LanguageCode": 1033,  
       "IsManaged": true,  
       "MetadataId": "21d6a218-2341-db11-898a-0007e9e17ebd",  
       "HasChanged": null  
      }  
     ],  
     "UserLocalizedLabel": {  
      "Label": "Sunday",  
      "LanguageCode": 1033,  
      "IsManaged": true,  
      "MetadataId": "21d6a218-2341-db11-898a-0007e9e17ebd",  
      "HasChanged": null  
     }  
    },  
    "Description": {  
     "LocalizedLabels": [],  
     "UserLocalizedLabel": null  
    },  
    "Color": null,  
    "IsManaged": true,  
    "MetadataId": null,  
    "HasChanged": null  
   }  
Additional options removed for brevity  
  ],  
  "Description": {  
   "LocalizedLabels": [  
    {  
     "Label": "Day of the week that the account prefers for scheduling service activities.",  
     "LanguageCode": 1033,  
     "IsManaged": true,  
     "MetadataId": "1b67144d-ece0-4e83-a38b-b4d48e3f35d5",  
     "HasChanged": null  
    }  
   ],  
   "UserLocalizedLabel": {  
    "Label": "Day of the week that the account prefers for scheduling service activities.",  
    "LanguageCode": 1033,  
    "IsManaged": true,  
    "MetadataId": "1b67144d-ece0-4e83-a38b-b4d48e3f35d5",  
    "HasChanged": null  
   }  
  },  
  "DisplayName": {  
   "LocalizedLabels": [  
    {  
     "Label": "Preferred Day",  
     "LanguageCode": 1033,  
     "IsManaged": true,  
     "MetadataId": "ebb7e979-f9e3-40cd-a86d-50b479b1c5a4",  
     "HasChanged": null  
    }  
   ],  
   "UserLocalizedLabel": {  
    "Label": "Preferred Day",  
    "LanguageCode": 1033,  
    "IsManaged": true,  
    "MetadataId": "ebb7e979-f9e3-40cd-a86d-50b479b1c5a4",  
    "HasChanged": null  
   }  
  },  
  "IsCustomOptionSet": false,  
  "IsGlobal": false,  
  "IsManaged": true,  
  "IsCustomizable": {  
   "Value": true,  
   "CanBeChanged": false,  
   "ManagedPropertyLogicalName": "iscustomizable"  
  },  
  "Name": "account_preferredappointmentdaycode",  
  "OptionSetType": "Picklist",  
  "IntroducedVersion": null,  
  "MetadataId": "53f9933c-18a0-40a6-b4a5-b9610a101735",  
  "HasChanged": null  
 }  
}  
```

この属性のどのプロパティも必要とせず、OptionsSet などのコレクション値ナビゲーション プロパティの値のみが必要な場合は、それを URL に含めて、多少クエリの効率を上げるために、`$select` システム クエリ オプションでプロパティを制限できます。 次の例では、OptionSet の Options プロパティのみが含まれます。  

 **要求**
 ```http
GET [Organization URI]/api/data/v9.0/EntityDefinitions(LogicalName='account')/Attributes(5967e7cc-afbb-4c10-bf7e-e7ef430c52be)/Microsoft.Dynamics.CRM.PicklistAttributeMetadata/OptionSet?$select=Options HTTP/1.1  
Accept: application/json  
Content-Type: application/json; charset=utf-8  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
```

 **応答**
 ```http
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  

{  
 "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#EntityDefinitions('account')/Attributes(5967e7cc-afbb-4c10-bf7e-e7ef430c52be)/Microsoft.Dynamics.CRM.PicklistAttributeMetadata/OptionSet(Options)/$entity",  
 "Options": [{  
   "Value": 0,  
   "Label": {  
    "LocalizedLabels": [{  
     "Label": "Sunday",  
     "LanguageCode": 1033,  
     "IsManaged": true,  
     "MetadataId": "21d6a218-2341-db11-898a-0007e9e17ebd",  
     "HasChanged": null  
    }],  
    "UserLocalizedLabel": {  
     "Label": "Sunday",  
     "LanguageCode": 1033,  
     "IsManaged": true,  
     "MetadataId": "21d6a218-2341-db11-898a-0007e9e17ebd",  
     "HasChanged": null  
    }  
   },  
   "Description": {  
    "LocalizedLabels": [],  
    "UserLocalizedLabel": null  
   },  
   "Color": null,  
   "IsManaged": true,  
   "MetadataId": null,  
   "HasChanged": null  
  }  
Additional options removed for brevity  
 ],  
 "MetadataId": "53f9933c-18a0-40a6-b4a5-b9610a101735"  
}  
```

<a name="bkmk_queryRelationshipMetadata"></a>

## <a name="querying-relationship-metadata"></a>関連付けのメタデータのクエリ

属性のクエリとほぼ同じ方法で、特定のエンティティのコンテキストで、関連付けメタデータを取得することができます。 `ManyToManyRelationships`、`ManyToOneRelationships`、および `OneToManyRelationships` コレクション値ナビゲーション プロパティは、`Attributes` コレクション値ナビゲーション プロパティと同様にクエリすることができます。 詳細: [EntityMetadata 属性をクエリ](query-metadata-web-api.md#bkmk_queryAttributes)  

ただし、エンティティ関連付けも、`RelationshipDefinitions` エンティティ セットを使用してクエリすることができます。 次のようなクエリを使用して、すべての関連付けの `SchemaName` プロパティを取得できます。

```http
GET [Organization URI]/api/data/v9.0/RelationshipDefinitions?$select=SchemaName  
```

このプロパティはこのエンティティ セットをクエリしたときに使用可能になり、その使用は <xref href="Microsoft.Dynamics.CRM.RelationshipMetadataBase?text=RelationshipMetadataBase EntityType" /> のプロパティに限定されます。 `RelationshipMetadataBase` から継承するエンティティの種類からプロパティにするには、次のようなクエリに含めて、<xref href="Microsoft.Dynamics.CRM.OneToManyRelationshipMetadata?text=OneToManyRelationshipMetadata EntityType" /> のみを返す必要があります。  

```http
GET [Organization URI]/api/data/v9.0/RelationshipDefinitions/Microsoft.Dynamics.CRM.OneToManyRelationshipMetadata?$select=SchemaName  
```

返されるエンティティは `OneToManyRelationshipMetadata` として型指定されるので、`ReferencedEntity` などのプロパティに対してフィルター処理を行って、次のクエリに示されるように、取引先企業エンティティなどの特定のエンティティの一対多のエンティティ関連付けのみを返すクエリを作成することができます。  

```http
GET [Organization URI]/api/data/v9.0/RelationshipDefinitions/Microsoft.Dynamics.CRM.OneToManyRelationshipMetadata?$select=SchemaName&$filter=ReferencedEntity eq 'account' 
```

このクエリは、取引先企業エンティティの `EntityMetadataOneToManyRelationships` コレクション値ナビゲーション プロパティに含まれているので、基本的には、フィルター処理される次のクエリと同じ結果を返します。 その違いは、前のクエリの場合は、取引先企業エンティティの `MetadataId` を知る必要がないということです。  

```http
GET [Organization URI]/api/data/v9.0/EntityDefinitions(LogicalName='account')/OneToManyRelationships?$select=SchemaName  
```

<a name="bkmk_GlobalOptionSets"></a>

## <a name="querying-global-optionsets"></a>グローバル オプション セットのクエリ

`GlobalOptionSetDefinitions` エンティティ セット パスを使用してグローバル オプション セットに関する情報を取得できますが、このパスは、`$filter` システム クエリ オプションの使用をサポートしていません。 したがって、特定のグローバル オプション セットの `MetadataId` が分かっていなければ、それらのすべてを取得することになります。 グローバル オプション セットを使用する属性の `GlobalOptionSet` の単一値のナビゲーション プロパティ内から、グローバル オプション セットの定義にアクセスすることもできます。 これはすべての [EnumAttributeMetadata EntityType 派生型](/dynamics365/customer-engagement/web-api/enumattributemetadata?view=dynamics-ce-odata-9#Derived_Types)に使用できます。 詳細: [属性の取得](query-metadata-web-api.md#bkmk_retrieveAttributes)  

### <a name="see-also"></a>関連項目

[Web API をアプリ用 Common Data Service メタデータで使用](use-web-api-metadata.md)<br />
[名前または MetadataId でのメタデータの取得](retrieve-metadata-name-metadataid.md)<br />
[Web API を使用したメタデータのエンティティおよび属性](create-update-entity-definitions-using-web-api.md)<br />
[Web API を使用したエンティティ関係のモデリング](create-update-entity-relationships-using-web-api.md)

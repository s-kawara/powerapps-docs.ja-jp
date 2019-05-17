---
title: Web API を使用したエンティティ定義の作成および更新 (Common Data Service) | Microsoft Docs
description: Web API を使用したエンティティ定義の作成と更新について説明します。
ms.custom: ''
ms.date: 10/31/2018
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 1f430d2d-e829-4ffa-922e-dfcfb7c9e86e
caps.latest.revision: 24
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
# <a name="create-and-update-entity-definitions-using-the-web-api"></a>Web API を使用してエンティティ定義を作成および更新



組織サービスで実行できるモデル エンティティに対する同じすべての操作を実行できます。 このトピックでは、Web サービス API を使用したメタデータ エンティティに対する操作に重点を置いています。 エンティティのメタデータ プロパティの詳細については、[エンティティ メタデータのカスタマイズ](../customize-entity-metadata.md)および<xref href="Microsoft.Dynamics.CRM.EntityMetadata?text=EntityMetadata EntityType" />を参照してください。  

<a name="bkmk_createEntities"></a>

## <a name="create-entities"></a>エンティティの作成

エンティティを作成するには、エンティティ データの JSON 表現を `EntityDefinitions` エンティティ セット パスに投稿します。 このエンティティには、エンティティのプライマリ名属性に関する定義を含める必要があります。 すべてのプロパティの値を設定する必要はありません。 説明の設定は推奨されるベスト プラクティスですが、このリストの説明以外のアイテムは必須です。 指定しないプロパティ値は既定値に設定されます。 規定値について理解するには、[エンティティの更新](create-update-entity-definitions-using-web-api.md#bkmk_updateEntities) セクションの例を参照してください。 このトピックの例では、以下のエンティティ プロパティを使用します。  
  
|エンティティ プロパティ|Value|  
|---------------------|-----------|  
|SchemaName|new_BankAccount **注:** ソリューション発行者に一致するカスタマイズの接頭辞を含める必要があります。 ここでは既定値 "new_" を使用しますが、自分のソリューションに合った接頭辞を選択する必要があります。|  
|DisplayName|銀行口座|  
|DisplayCollectionName|銀行口座|  
|内容|顧客の銀行口座に関する情報を格納するエンティティ。|  
|OwnershipType|UserOwned **注:** ここで設定することができる値については、<xref href="Microsoft.Dynamics.CRM.OwnershipTypes?text=OwnershipTypes EnumType" /> を参照してください。|  
|IsActivity|false|  
|HasActivities|false|  
|HasNotes|false|  
  
 前の一覧に示したプロパティのほかに、`EntityMetadataAttributes` プロパティに、エンティティのプライマリ名属性を表す <xref href="Microsoft.Dynamics.CRM.StringAttributeMetadata?text=StringAttributeMetadata EntityType" /> を 1 つ含む配列を含める必要があります。 IsPrimaryName プロパティは true である必要があります。 次の表では、例で設定するプロパティについて説明します。  
  
|主属性プロパティ|Value|  
|--------------------------------|-----------|  
|SchemaName|new_AccountName|  
|RequiredLevel|なし <br />**注意:**  ここに設定できる値については、<xref href="Microsoft.Dynamics.CRM.AttributeRequiredLevelManagedProperty?text=AttributeRequiredLevelManagedProperty ComplexType" />および<xref href="Microsoft.Dynamics.CRM.AttributeRequiredLevel?text=AttributeRequiredLevel EnumType" />を参照してください。|  
|MaxLength|100|  
|FormatName|Text <br />**注意:**  プライマリ名属性はテキスト形式を使用する必要があります。 他の文字列属性で使用できる書式オプションについては、[文字列書式](../entity-attribute-metadata.md#string-formats)を参照してください。|  
|DisplayName|取引先企業名|  
|説明|銀行口座の名前を入力します。|  
|IsPrimaryName|True|  
  
> [!NOTE]
>  <xref href="Microsoft.Dynamics.CRM.Label?text=Label ComplexType" /> を使用してラベルを作成または更新するとき、`LocalizedLabels` プロパティのみを設定する必要があります。 返される `UserLocalizedLabel` 値は、ユーザーの言語設定に基づき、かつ読み取り専用です。  
  
次の例では、プロパティを設定して、ユーザー定義エンティティの作成を示します。 言語は、ロケール ID (LCID) が 1033 である英語です。 [!INCLUDE [lcid](../../../includes/lcid.md)]  
  
 **要求**  
```http 
POST [Organization URI]/api/data/v9.0/EntityDefinitions HTTP/1.1  
Accept: application/json  
Content-Type: application/json; charset=utf-8  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
  
{  
  "@odata.type": "Microsoft.Dynamics.CRM.EntityMetadata",  
 "Attributes": [  
  {  
   "AttributeType": "String",  
   "AttributeTypeName": {  
    "Value": "StringType"  
   },  
   "Description": {  
     "@odata.type": "Microsoft.Dynamics.CRM.Label",  
    "LocalizedLabels": [  
     {  
       "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
      "Label": "Type the name of the bank account",  
      "LanguageCode": 1033  
     }  
    ]  
   },  
   "DisplayName": {  
     "@odata.type": "Microsoft.Dynamics.CRM.Label",  
    "LocalizedLabels": [  
     {  
       "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
      "Label": "Account Name",  
      "LanguageCode": 1033  
     }  
    ]  
   },  
   "IsPrimaryName": true,  
   "RequiredLevel": {  
    "Value": "None",  
    "CanBeChanged": true,  
    "ManagedPropertyLogicalName": "canmodifyrequirementlevelsettings"  
   },  
   "SchemaName": "new_AccountName",  
    "@odata.type": "Microsoft.Dynamics.CRM.StringAttributeMetadata",  
   "FormatName": {  
    "Value": "Text"  
   },  
   "MaxLength": 100  
  }  
 ],  
 "Description": {  
   "@odata.type": "Microsoft.Dynamics.CRM.Label",  
  "LocalizedLabels": [  
   {  
     "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
    "Label": "An entity to store information about customer bank accounts",  
    "LanguageCode": 1033  
   }  
  ]  
 },  
 "DisplayCollectionName": {  
   "@odata.type": "Microsoft.Dynamics.CRM.Label",  
  "LocalizedLabels": [  
   {  
     "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
    "Label": "Bank Accounts",  
    "LanguageCode": 1033  
   }  
  ]  
 },  
 "DisplayName": {  
   "@odata.type": "Microsoft.Dynamics.CRM.Label",  
  "LocalizedLabels": [  
   {  
     "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
    "Label": "Bank Account",  
    "LanguageCode": 1033  
   }  
  ]  
 },  
 "HasActivities": false,  
 "HasNotes": false,  
 "IsActivity": false,  
 "OwnershipType": "UserOwned",  
 "SchemaName": "new_BankAccount"  
}  
```  
  
 **応答**  
```http 
HTTP/1.1 204 No Content  
OData-Version: 4.0  
OData-EntityId: [Organization URI]/api/data/v9.0/EntityDefinitions(417129e1-207c-e511-80d2-00155d2a68d2)  
```  
  
<a name="bkmk_updateEntities"></a>
 
## <a name="update-entities"></a>エンティティの更新
  
> [!IMPORTANT]
>  モデル エンティティの更新には、HTTP PATCH メソッドを使用することはできません。 メタデータ エンティティは、エンティティ定義を組み込みのエンティティ定義に置き換える組織サービス <xref:Microsoft.Xrm.Sdk.Messages.UpdateEntityRequest> と同じです。 これにより、モデル エンティティを更新するときは、HTTP PUT メソッドを使用して、変更する予定のない既存のすべてのプロパティを含めるように注意する必要があります。 個々のプロパティを更新することはできません。  
  
 ラベルを持つメタデータ エンティティを更新するときは、更新プログラムに含まれるラベルの処理方法を制御するために、ユーザー定義の `MSCRM.MergeLabels` ヘッダーを組み込む必要があります。 任意のアイテムのラベルにほかの言語のラベルが含まれていて、そのラベルを特定の言語のラベルのみを含むラベルに更新する場合、`MSCRM.MergeLabels` ヘッダーは、既存のラベルを上書きするか、または既存の言語のラベルに新しいラベルを統合するかを制御します。 `MSCRM.MergeLabels` を `true` に設定した場合、言語コードが一致するときだけ、定義した新しいラベルが既存のラベルに上書きされます。 組み込んだラベルのみが組み込まれるように既存のラベルを上書きする場合は、`MSCRM.MergeLabels` を `false` に設定します。  
  
> [!IMPORTANT]
>  `MSCRM.MergeLabels` ヘッダーを組み込まない場合、既定では、この値が `false` であるものとして動作し、更新プログラムに含まれていないローカライズされたラベルは失われます。  
  
 エンティティや属性を更新するときは、加える変更をアプリケーションに適用する前に、<xref href="Microsoft.Dynamics.CRM.PublishXml?text=PublishXml Action" />または<xref href="Microsoft.Dynamics.CRM.PublishAllXml?text=PublishAllXml Action" />を使用する必要があります。 詳細: [カスタマイズの公開](../../model-driven-apps/publish-customizations.md)  
  
 通常、その属性の JSON 定義を取得し、それを戻す前にそのプロパティを変更します。 次の例では、[エンティティの作成](create-update-entity-definitions-using-web-api.md#bkmk_createEntities) の例で作成されたエンティティのすべてのメタデータ プロパティが含まれますが、DisplayName は「銀行事業名」に変更されます。 ここでは、[エンティティの作成](create-update-entity-definitions-using-web-api.md#bkmk_createEntities) の例で設定されていないプロパティの既定値が JSON によって指定されることに留意すると役に立つことがあります。  
  
 **要求**  
```http 
PUT [Organization URI]/api/data/v9.0/EntityDefinitions(417129e1-207c-e511-80d2-00155d2a68d2) HTTP/1.1  
Accept: application/json  
Content-Type: application/json; charset=utf-8  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
MSCRM.MergeLabels: true  
  
{  
 "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#EntityDefinitions/$entity",  
 "ActivityTypeMask": 0,  
 "AutoRouteToOwnerQueue": false,  
 "CanTriggerWorkflow": true,  
 "Description": {  
  "LocalizedLabels": [  
   {  
    "Label": "An entity to store information about customer bank accounts",  
    "LanguageCode": 1033,  
    "IsManaged": false,  
    "MetadataId": "edc3abd7-c5ae-4822-a3ed-51734fdd0469",  
    "HasChanged": null  
   }  
  ]  
 },  
 "DisplayCollectionName": {  
  "LocalizedLabels": [  
   {  
    "Label": "Bank Accounts",  
    "LanguageCode": 1033,  
    "IsManaged": false,  
    "MetadataId": "7c758e0c-e9cf-4947-93b0-50ec30b20f60",  
    "HasChanged": null  
   }  
  ]  
 },  
 "DisplayName": {  
  "@odata.type": "Microsoft.Dynamics.CRM.Label",  
  "LocalizedLabels": [  
   {  
    "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
    "Label": "Bank Business Name",  
    "LanguageCode": 1033  
   }  
  ]  
 },  
 "EntityHelpUrlEnabled": false,  
 "EntityHelpUrl": null,  
 "IsDocumentManagementEnabled": false,  
 "IsOneNoteIntegrationEnabled": false,  
 "IsInteractionCentricEnabled": false,  
 "IsKnowledgeManagementEnabled": false,  
 "AutoCreateAccessTeams": false,  
 "IsActivity": false,  
 "IsActivityParty": false,  
 "IsAuditEnabled": {  
  "Value": false,  
  "CanBeChanged": true,  
  "ManagedPropertyLogicalName": "canmodifyauditsettings"  
 },  
 "IsAvailableOffline": false,  
 "IsChildEntity": false,  
 "IsAIRUpdated": false,  
 "IsValidForQueue": {  
  "Value": false,  
  "CanBeChanged": true,  
  "ManagedPropertyLogicalName": "canmodifyqueuesettings"  
 },  
 "IsConnectionsEnabled": {  
  "Value": false,  
  "CanBeChanged": true,  
  "ManagedPropertyLogicalName": "canmodifyconnectionsettings"  
 },  
 "IconLargeName": null,  
 "IconMediumName": null,  
 "IconSmallName": null,  
 "IsCustomEntity": true,  
 "IsBusinessProcessEnabled": false,  
 "IsCustomizable": {  
  "Value": true,  
  "CanBeChanged": true,  
  "ManagedPropertyLogicalName": "iscustomizable"  
 },  
 "IsRenameable": {  
  "Value": true,  
  "CanBeChanged": true,  
  "ManagedPropertyLogicalName": "isrenameable"  
 },  
 "IsMappable": {  
  "Value": true,  
  "CanBeChanged": false,  
  "ManagedPropertyLogicalName": "ismappable"  
 },  
 "IsDuplicateDetectionEnabled": {  
  "Value": false,  
  "CanBeChanged": true,  
  "ManagedPropertyLogicalName": "canmodifyduplicatedetectionsettings"  
 },  
 "CanCreateAttributes": {  
  "Value": true,  
  "CanBeChanged": false,  
  "ManagedPropertyLogicalName": "cancreateattributes"  
 },  
 "CanCreateForms": {  
  "Value": true,  
  "CanBeChanged": true,  
  "ManagedPropertyLogicalName": "cancreateforms"  
 },  
 "CanCreateViews": {  
  "Value": true,  
  "CanBeChanged": true,  
  "ManagedPropertyLogicalName": "cancreateviews"  
 },  
 "CanCreateCharts": {  
  "Value": true,  
  "CanBeChanged": true,  
  "ManagedPropertyLogicalName": "cancreatecharts"  
 },  
 "CanBeRelatedEntityInRelationship": {  
  "Value": true,  
  "CanBeChanged": true,  
  "ManagedPropertyLogicalName": "canberelatedentityinrelationship"  
 },  
 "CanBePrimaryEntityInRelationship": {  
  "Value": true,  
  "CanBeChanged": true,  
  "ManagedPropertyLogicalName": "canbeprimaryentityinrelationship"  
 },  
 "CanBeInManyToMany": {  
  "Value": true,  
  "CanBeChanged": true,  
  "ManagedPropertyLogicalName": "canbeinmanytomany"  
 },  
 "CanEnableSyncToExternalSearchIndex": {  
  "Value": true,  
  "CanBeChanged": true,  
  "ManagedPropertyLogicalName": "canenablesynctoexternalsearchindex"  
 },  
 "SyncToExternalSearchIndex": false,  
 "CanModifyAdditionalSettings": {  
  "Value": true,  
  "CanBeChanged": true,  
  "ManagedPropertyLogicalName": "canmodifyadditionalsettings"  
 },  
 "CanChangeHierarchicalRelationship": {  
  "Value": true,  
  "CanBeChanged": true,  
  "ManagedPropertyLogicalName": "canchangehierarchicalrelationship"  
 },  
 "IsOptimisticConcurrencyEnabled": true,  
 "ChangeTrackingEnabled": false,  
 "IsImportable": true,  
 "IsIntersect": false,  
 "IsMailMergeEnabled": {  
  "Value": true,  
  "CanBeChanged": true,  
  "ManagedPropertyLogicalName": "canmodifymailmergesettings"  
 },  
 "IsManaged": false,  
 "IsEnabledForCharts": true,  
 "IsEnabledForTrace": false,  
 "IsValidForAdvancedFind": true,  
 "IsVisibleInMobile": {  
  "Value": false,  
  "CanBeChanged": true,  
  "ManagedPropertyLogicalName": "canmodifymobilevisibility"  
 },  
 "IsVisibleInMobileClient": {  
  "Value": false,  
  "CanBeChanged": true,  
  "ManagedPropertyLogicalName": "canmodifymobileclientvisibility"  
 },  
 "IsReadOnlyInMobileClient": {  
  "Value": false,  
  "CanBeChanged": true,  
  "ManagedPropertyLogicalName": "canmodifymobileclientreadonly"  
 },  
 "IsOfflineInMobileClient": {  
  "Value": false,  
  "CanBeChanged": true,  
  "ManagedPropertyLogicalName": "canmodifymobileclientoffline"  
 },  
 "DaysSinceRecordLastModified": 0,  
 "IsReadingPaneEnabled": true,  
 "IsQuickCreateEnabled": false,  
 "LogicalName": "new_bankaccount",  
 "ObjectTypeCode": 10009,  
 "OwnershipType": "UserOwned",  
 "PrimaryNameAttribute": "new_accountname",  
 "PrimaryImageAttribute": null,  
 "PrimaryIdAttribute": "new_bankaccountid",  
 "Privileges": [  
  {  
   "CanBeBasic": true,  
   "CanBeDeep": true,  
   "CanBeGlobal": true,  
   "CanBeLocal": true,  
   "CanBeEntityReference": false,  
   "CanBeParentEntityReference": false,  
   "Name": "prvCreatenew_BankAccount",  
   "PrivilegeId": "d1a8de4b-27df-42e1-bc5c-b863e002b37f",  
   "PrivilegeType": "Create"  
  },  
  {  
   "CanBeBasic": true,  
   "CanBeDeep": true,  
   "CanBeGlobal": true,  
   "CanBeLocal": true,  
   "CanBeEntityReference": false,  
   "CanBeParentEntityReference": false,  
   "Name": "prvReadnew_BankAccount",  
   "PrivilegeId": "726043b1-de2c-487e-9d6d-5629fca2bf22",  
   "PrivilegeType": "Read"  
  },  
  {  
   "CanBeBasic": true,  
   "CanBeDeep": true,  
   "CanBeGlobal": true,  
   "CanBeLocal": true,  
   "CanBeEntityReference": false,  
   "CanBeParentEntityReference": false,  
   "Name": "prvWritenew_BankAccount",  
   "PrivilegeId": "fa50c539-b6c7-4eaf-bd49-fd8224bc51b6",  
   "PrivilegeType": "Write"  
  },  
  {  
   "CanBeBasic": true,  
   "CanBeDeep": true,  
   "CanBeGlobal": true,  
   "CanBeLocal": true,  
   "CanBeEntityReference": false,  
   "CanBeParentEntityReference": false,  
   "Name": "prvDeletenew_BankAccount",  
   "PrivilegeId": "17c1fd6e-f856-45e7-b563-796f53108b85",  
   "PrivilegeType": "Delete"  
  },  
  {  
   "CanBeBasic": true,  
   "CanBeDeep": true,  
   "CanBeGlobal": true,  
   "CanBeLocal": true,  
   "CanBeEntityReference": false,  
   "CanBeParentEntityReference": false,  
   "Name": "prvAssignnew_BankAccount",  
   "PrivilegeId": "133ca81d-668e-4c19-a71e-10c6dfe099cd",  
   "PrivilegeType": "Assign"  
  },  
  {  
   "CanBeBasic": true,  
   "CanBeDeep": true,  
   "CanBeGlobal": true,  
   "CanBeLocal": true,  
   "CanBeEntityReference": false,  
   "CanBeParentEntityReference": false,  
   "Name": "prvSharenew_BankAccount",  
   "PrivilegeId": "15f27df4-9c67-47c9-b1f1-274e1c44f24a",  
   "PrivilegeType": "Share"  
  },  
  {  
   "CanBeBasic": true,  
   "CanBeDeep": true,  
   "CanBeGlobal": true,  
   "CanBeLocal": true,  
   "CanBeEntityReference": false,  
   "CanBeParentEntityReference": false,  
   "Name": "prvAppendnew_BankAccount",  
   "PrivilegeId": "ac8b1920-8f93-4e9d-94e3-c680e2a2f228",  
   "PrivilegeType": "Append"  
  },  
  {  
   "CanBeBasic": true,  
   "CanBeDeep": true,  
   "CanBeGlobal": true,  
   "CanBeLocal": true,  
   "CanBeEntityReference": false,  
   "CanBeParentEntityReference": false,  
   "Name": "prvAppendTonew_BankAccount",  
   "PrivilegeId": "f63a5f46-3bc7-4eac-81d0-7f77f566ef46",  
   "PrivilegeType": "AppendTo"  
  }  
 ],  
 "RecurrenceBaseEntityLogicalName": null,  
 "ReportViewName": "Filterednew_BankAccount",  
 "SchemaName": "new_BankAccount",  
 "IntroducedVersion": "1.0",  
 "IsStateModelAware": true,  
 "EnforceStateTransitions": false,  
 "EntityColor": null,  
 "LogicalCollectionName": "new_bankaccounts",  
 "CollectionSchemaName": "new_BankAccounts",  
 "EntitySetName": "new_bankaccounts",  
 "IsEnabledForExternalChannels": false,  
 "IsPrivate": false,  
 "MetadataId": "417129e1-207c-e511-80d2-00155d2a68d2",  
 "HasChanged": null  
}  
```  
  
 **応答**  
```http 
HTTP/1.1 204 No Content  
OData-Version: 4.0  
```  
  
<a name="bkmk_CreateAttributes"></a>

## <a name="create-attributes"></a>属性の作成

プライマリ名属性として機能する文字列属性に加えて投稿するエンティティの `Attributes` 配列に属性の JSON 定義を組み込むことによって、エンティティの作成と同時に属性を作成することができます。 既に作成されているエンティティに属性を追加する場合、その属性の JSON 定義を含む POST 要求をエンティティ `Attributes` のコレクション値ナビゲーション プロパティに送信することができます。  
  
<a name="bkmk_CreateString"></a>

### <a name="create-a-string-attribute"></a>文字列属性の作成

次の例では、文字列属性の作成に次のプロパティを使用します。  
  
|文字列属性のプロパティ|値|  
|---------------------------------|------------|  
|SchemaName|new_BankName|  
|DisplayName|銀行名|  
|内容|銀行の名前を入力します。|  
|RequiredLevel|なし|  
|MaxLength|100|  
|FormatName|テキスト|  
  
次の例では、これらのプロパティを使用して文字列属性を作成し、その日時属性を MetadataId の値が 402fa40f-287c-e511-80d2-00155d2a68d2 のエンティティに追加します。

この属性の URI が応答で返されます。  
  
 **要求**

```http 
POST [Organization URI]/api/data/v9.0/EntityDefinitions(402fa40f-287c-e511-80d2-00155d2a68d2)/Attributes HTTP/1.1  
Accept: application/json  
Content-Type: application/json; charset=utf-8  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
  
{  
 "AttributeType": "String",  
 "AttributeTypeName": {  
  "Value": "StringType"  
 },  
 "Description": {  
  "@odata.type": "Microsoft.Dynamics.CRM.Label",  
  "LocalizedLabels": [  
   {  
    "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
    "Label": "Type the name of the bank",  
    "LanguageCode": 1033  
   }  
  ]  
 },  
 "DisplayName": {  
  "@odata.type": "Microsoft.Dynamics.CRM.Label",  
  "LocalizedLabels": [  
   {  
    "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
    "Label": "Bank Name",  
    "LanguageCode": 1033  
   }  
  ]  
 },  
 "RequiredLevel": {  
  "Value": "None",  
  "CanBeChanged": true,  
  "ManagedPropertyLogicalName": "canmodifyrequirementlevelsettings"  
 },  
 "SchemaName": "new_BankName",  
 "@odata.type": "Microsoft.Dynamics.CRM.StringAttributeMetadata",  
 "FormatName": {  
  "Value": "Text"  
 },  
 "MaxLength": 100  
}  
  
```  
  
 **応答**  
```http 
HTTP/1.1 204 No Content  
OData-Version: 4.0  
OData-EntityId: [Organization URI]/api/data/v9.0/EntityDefinitions(402fa40f-287c-e511-80d2-00155d2a68d2)/Attributes(f01bef16-287c-e511-80d2-00155d2a68d2)  
```  
  
<a name="bkmk_createMoney"></a>

### <a name="create-a-money-attribute"></a>通貨属性の作成

次の例では、通貨属性の作成に次のプロパティを使用します。  
  
|通貨属性のプロパティ|値|  
|--------------------------------|------------|  
|SchemaName|new_Balance|  
|DisplayName|残高|  
|内容|残高金額を入力します。|  
|RequiredLevel|なし|  
|PrecisionSource|2 <br />**注意:**  PrecisionSource の有効な値については、[MoneyType](../entity-attribute-metadata.md#money_type)を参照してください。 値 2 は、小数点以下の精度のレベルが、現在のレコードに関連付けられている TransactionCurrency.CurrencyPrecision に一致することを意味します。|  


  
次の例では、これらのプロパティを使用して通貨属性を作成し、その日時属性を MetadataId の値が 402fa40f-287c-e511-80d2-00155d2a68d2 のエンティティに追加します。 この属性の URI が応答で返されます。  
  
 **要求**  
```http   
POST [Organization URI]/api/data/v9.0/EntityDefinitions(402fa40f-287c-e511-80d2-00155d2a68d2)/Attributes HTTP/1.1  
Accept: application/json  
Content-Type: application/json; charset=utf-8  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
  
{  
 "AttributeType": "Money",  
 "AttributeTypeName": {  
  "Value": "MoneyType"  
 },  
 "Description": {  
  "@odata.type": "Microsoft.Dynamics.CRM.Label",  
  "LocalizedLabels": [  
   {  
    "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
    "Label": "Enter the balance amount",  
    "LanguageCode": 1033  
   }  
  ]  
 },  
 "DisplayName": {  
  "@odata.type": "Microsoft.Dynamics.CRM.Label",  
  "LocalizedLabels": [  
   {  
    "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
    "Label": "Balance",  
    "LanguageCode": 1033  
   }  
  ]  
 },  
 "RequiredLevel": {  
  "Value": "None",  
  "CanBeChanged": true,  
  "ManagedPropertyLogicalName": "canmodifyrequirementlevelsettings"  
 },  
 "SchemaName": "new_Balance",  
 "@odata.type": "Microsoft.Dynamics.CRM.MoneyAttributeMetadata",  
 "PrecisionSource": 2  
}  
```  
  
 **応答**  
```http 
HTTP/1.1 204 No Content  
OData-Version: 4.0  
OData-EntityId: [Organization URI]/api/data/v9.0/EntityDefinitions(402fa40f-287c-e511-80d2-00155d2a68d2)/Attributes(f11bef16-287c-e511-80d2-00155d2a68d2)  
```  
  
<a name="bkmk_createDateTime"></a>

### <a name="create-a-datetime-attribute"></a>日時属性の作成

次の例では、日時属性の作成に次のプロパティを使用します。  
  
|日時属性のプロパティ|値|  
|-----------------------------------|------------|  
|SchemaName|new_Checkeddate|  
|DisplayName|日付|  
|内容|勘定残高が最後に確認された日付。|  
|RequiredLevel|なし|  
|書式|DateOnly **注:** このプロパティの有効なオプションについては、<xref href="Microsoft.Dynamics.CRM.DateTimeFormat?text=DateTimeFormat EnumType" /> を参照してください。|  
  
次の例では、これらのプロパティを使用して日付属性を作成し、その日時属性を MetadataId の値が 402fa40f-287c-e511-80d2-00155d2a68d2 のエンティティに追加します。 この属性の URI が応答で返されます。  
  
 **要求**

```http 
POST [Organization URI]/api/data/v9.0/EntityDefinitions(402fa40f-287c-e511-80d2-00155d2a68d2)/Attributes HTTP/1.1  
Accept: application/json  
Content-Type: application/json; charset=utf-8  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
  
{  
 "AttributeType": "DateTime",  
 "AttributeTypeName": {  
  "Value": "DateTimeType"  
 },  
 "Description": {  
  "@odata.type": "Microsoft.Dynamics.CRM.Label",  
  "LocalizedLabels": [  
   {  
    "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
    "Label": "The date the account balance was last confirmed",  
    "LanguageCode": 1033  
   }  
  ]  
 },  
 "DisplayName": {  
  "@odata.type": "Microsoft.Dynamics.CRM.Label",  
  "LocalizedLabels": [  
   {  
    "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
    "Label": "Date",  
    "LanguageCode": 1033  
   }  
  ]  
 },  
 "RequiredLevel": {  
  "Value": "None",  
  "CanBeChanged": true,  
  "ManagedPropertyLogicalName": "canmodifyrequirementlevelsettings"  
 },  
 "SchemaName": "new_Checkeddate",  
 "@odata.type": "Microsoft.Dynamics.CRM.DateTimeAttributeMetadata",  
 "Format": "DateOnly"  
}  
```  
  
 **応答**  
```http 
HTTP/1.1 204 No Content  
OData-Version: 4.0  
OData-EntityId: [Organization URI]/api/data/v9.0/EntityDefinitions(402fa40f-287c-e511-80d2-00155d2a68d2)/Attributes(fe1bef16-287c-e511-80d2-00155d2a68d2)  
```  
  
<a name="bkmk_CreateCustomerLookup"></a>

### <a name="create-a-customer-lookup-attribute"></a>顧客検索属性の作成

他の属性とは異なり、顧客検索属性は <xref href="Microsoft.Dynamics.CRM.CreateCustomerRelationships?text=CreateCustomerRelationships Action" /> を使用して作成されます。 

このアクションのパラメーターは、参照属性の種類の定義と 1 組の一対多関連付けを必要とします。 顧客検索属性には複数の一対多関連付けがあります: 1 つは取引先企業エンティティに対して、他方は取引先担当者エンティティに対してです。  
  
 次の例では、顧客検索属性の作成に次のプロパティを使用します。  
  
|顧客検索属性のプロパティ|値|  
|------------------------------------------|------------|  
|SchemaName|new_CustomerId|  
|DisplayName|Customer|  
|内容|サンプルの顧客検索属性|  
  
例では、顧客検索属性、`new_CustomerId` を作成し、それはユーザー定義エンティティ、`new_bankaccount` に追加されます。 応答は <xref href="Microsoft.Dynamics.CRM.CreateCustomerRelationshipsResponse?text=CreateCustomerRelationshipsResponse ComplexType" /> です。  
  
 **要求**

```http 
POST [Organization URI]/api/data/v9.0/CreateCustomerRelationships HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Accept: application/json  
Content-Type: application/json; charset=utf-8  
  
{  
    "OneToManyRelationships": [{  
        "SchemaName": "new_bankaccount_customer_account",  
        "ReferencedEntity": "account",  
        "ReferencingEntity": "new_bankaccount"  
    }, {  
        "SchemaName": "new_bankaccount_customer_contact",  
        "ReferencedEntity": "contact",  
        "ReferencingEntity": "new_bankaccount"  
    }],  
    "Lookup": {  
        "AttributeType": "Lookup",  
        "AttributeTypeName": {  
            "Value": "LookupType"  
        },  
        "Description": {  
            "@odata.type": "Microsoft.Dynamics.CRM.Label",  
            "LocalizedLabels": [{  
                "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
                "Label": "Sample Customer Lookup Attribute",  
                "LanguageCode": 1033  
            }],  
            "UserLocalizedLabel": {  
                "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
                "Label": "Sample Customer Lookup Attribute",  
                "LanguageCode": 1033  
            }  
        },  
        "DisplayName": {  
            "@odata.type": "Microsoft.Dynamics.CRM.Label",  
            "LocalizedLabels": [{  
                "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
                "Label": "Customer",  
                "LanguageCode": 1033  
            }],  
            "UserLocalizedLabel": {  
                "@odata.type": "Microsoft.Dynamics.CRM.LocalizedLabel",  
                "Label": "Customer",  
                "LanguageCode": 1033  
            }  
        },  
        "SchemaName": "new_CustomerId",  
        "@odata.type": "Microsoft.Dynamics.CRM.ComplexLookupAttributeMetadata"  
    }  
}  
```  
  
 **応答**  
```http 
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
  
{  
    "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#Microsoft.Dynamics.CRM.CreateCustomerRelationshipsResponse",  
    "RelationshipIds": [  
        "a7d261bc-3580-e611-80d7-00155d2a68de", "aed261bc-3580-e611-80d7-00155d2a68de"  
    ],  
    "AttributeId": "39a5d94c-e8a2-4a41-acc0-8487242d455e"  
}  
  
```  
  
<a name="bkmk_updateAttribute"></a>
 
## <a name="update-an-attribute"></a>属性の更新

[エンティティの更新](create-update-entity-definitions-using-web-api.md#bkmk_updateEntities) で述べたように、モデル エンティティは HTTP PUT メソッドを現在のアイテムの JSON 定義全体を使用して更新されます。 これは、エンティティだけでなく属性にも適用されます。 エンティティの場合とまったく同様に、値が `false` に設定された `MSCRM.MergeLabels` ヘッダーを使用してラベルを上書きすることが可能であり、カスタマイズがシステムでアクティブになる前にそのカスタマイズを公開する必要があります。  
  
### <a name="see-also"></a>関連項目

[Web API を Common Data Service メタデータで使用する](use-web-api-metadata.md)<br />
[Web API を使用したクエリ メタデータ](query-metadata-web-api.md)<br />
[名前または MetadataId でのメタデータの取得](retrieve-metadata-name-metadataid.md)<br />
[Web API を使用したエンティティ関係のモデリング](create-update-entity-relationships-using-web-api.md)<br />

[組織サービスを使用したメタデータに関する作業](../org-service/work-with-metadata.md)<br />
[属性メタデータ](../entity-attribute-metadata.md)

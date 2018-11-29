---
title: メタデータへの変更を取得および検出する (アプリ用 Common Data Service) | Microsoft Docs
description: Query 名前空間のクラスと RetrieveMetadataChangesRequest および RetrieveMetadataChangesResponse クラスで、有効なメタデータ クエリの構築と時間経過に伴って発生するメタデータへの変更の取得が可能です。
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
# <a name="retrieve-and-detect-changes-to-metadata"></a>メタデータへの変更の取得および検出

<xref:Microsoft.Xrm.Sdk.Metadata.Query> 名前空間のクラスと <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesRequest> および <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesResponse> クラスで、有効なメタデータ クエリの構築と時間経過に伴って発生するメタデータへの変更の取得が可能です。  
  
 このドキュメントで参照されるすべてのコード例は、「[サンプル: メタデータのクエリと変更の検出](/dynamics365/customer-engagement/developer/org-service/sample-query-metadata-detect-changes)」にあります。  
  
 技術記事「[JavaScript を使用したメタデータのクエリ](https://msdn.microsoft.com/library/jj919080.aspx)」に、クライアント側コードでオブジェクトとメッセージを使用するための JavaScript ライブラリがあります。  
  
<a name="BKMK_MetadataStrategies"></a> 
  
## <a name="strategies-for-using-metadata"></a>メタデータの使用方法  

 メタデータでアプリ用 Common Data Service のデータ モデリングの変更に合わせたアプリケーションを作成することができます。 メタデータは次の種類のアプリケーションで重要です。  
  
-   クライアント アプリケーションの UI  
  
-   外部システムに Dynamics 365 データをマップする統合ツール  
  
-   開発ツール  
  
 <xref:Microsoft.Xrm.Sdk.Metadata.Query> 名前空間のクラスを使用して軽量のクエリと永続メタデータ キャッシュ間に存在する設計を実行できます。  
  
### <a name="lightweight-query"></a>軽量のクエリ
  
 軽量クエリの例には、Dynamics 365 オプション セット (候補リスト) 属性で、現在のオプションを表示するための選択コントロールを設定するユーザー定義 Web リソース UI がある場合が含まれます。 使用可能なオプションが変更されると、コードを更新する必要があるため、これらのオプションはハード コードにするのは好ましくありません。 その代わり、メタデータから、オプション値とラベルを取得するクエリを作成できます。  
  
 Dynamics 365 アプリケーション キャッシュからこのデータを直接取得する場合に <xref:Microsoft.Xrm.Sdk.Metadata.Query> クラスを使用できるため、このデータをキャッシュする必要はありません。  
  
### <a name="persistent-metadata-cache"></a>永続メタデータ キャッシュ
  
 Dynamics 365 Server から切断しているときに動作可能でなければならないアプリケーションがある場合や、モバイル アプリケーションなどのクライアントとサーバー間のネットワーク帯域幅の制限に影響を受けやすいアプリケーションがある場合、永続メタデータ キャッシュを実装することができます。  
  
 永続メタデータ キャッシュを使用すると、アプリケーションで最初の接続時に、必要なすべてのメタデータをクエリする必要があります。 次にそのアプリケーションにそのデータを保存します。 次にアプリケーションが接続する時には、最後のクエリからの差異のみを取得できます。これにより、送信する必要があるデータが少なくなり、アプリケーションを読み込んでいる間に、変更をメタデータ キャッシュに統合します。  
  
 メタデータの変更へのポーリング頻度は、アプリケーションのメタデータの変化予測と、アプリケーションの実行時間に基づいて決めます。 メタデータの変更がいつ発生するかの検出に使用できるイベントはありません。 検出されたメタデータの変更が保存される日数には制限があります。また、素の制限を超えて発生する変更要求があった場合、メタデータ キャッシュの完全再初期化が必要です。 詳細については、「[削除されたメタデータの有効期限](/dynamics365/customer-engagement/developer/retrieve-detect-changes-metadata#BKMK_DeletedMetadataExpiration)」を参照してください。  
  
 変更がない場合は、クエリはすぐに応答し、送信されるデータはありません。 ただし、特にキャッシュから削除される予定の削除済みメタデータ アイテムがある場合、その要求が終了するまでさらに時間がかかることが予想されます。 詳細については、「[削除されたメタデータを取得するときのパフォーマンス](/dynamics365/customer-engagement/developer/retrieve-detect-changes-metadata#BKMK_PerformanceRetrievingDeletedMetadata)」を参照してください。  
  
<a name="BKMK_RetrieveJusttheMetadataYouNeed"></a>
   
## <a name="retrieve-only-the-metadata-you-need"></a>必要なメタデータのみの取得  

 メタデータは、アプリケーションを起動した時に頻繁に取得または同期されるため、アプリケーションの読み込み時間に影響を与えます。 これは、メタデータを取得するのが初めてのモバイル アプリケーションで特に当てはまります。 必要なメタデータのみを取得することは、アプリケーションのパフォーマンスを向上させるために非常に重要です。  
  
 <xref:Microsoft.Xrm.Sdk.Metadata.Query.EntityQueryExpression> クラスは、エンティティ データを取得する複雑なクエリを作成するときに使用する <xref:Microsoft.Xrm.Sdk.Query.QueryExpression> クラスと構造的に一貫しています。 <xref:Microsoft.Xrm.Sdk.Messages.RetrieveAllEntitiesRequest>、<xref:Microsoft.Xrm.Sdk.Messages.RetrieveEntityRequest>、<xref:Microsoft.Xrm.Sdk.Messages.RetrieveAttributeRequest>、または <xref:Microsoft.Xrm.Sdk.Messages.RetrieveRelationshipRequest> クラスとは異なり、<xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesRequest> には必要なプロパティに加えて返されるデータの特定の条件を指定するときに使用できる <xref:Microsoft.Xrm.Sdk.Metadata.Query.EntityQueryExpression> インスタンスを受け入れる `Query` パラメーターが含まれます。 <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesRequest> を使用して、<xref:Microsoft.Xrm.Sdk.Messages.RetrieveAllEntitiesRequest> を使用して取得したメタデータのフル セットまたは特定の属性のラベルだけを返すことができます。  
  
### <a name="specify-your-filter-criteria"></a>フィルターの条件の指定  

 <xref:Microsoft.Xrm.Sdk.Metadata.Query.EntityQueryExpression>.<xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataQueryExpression.Criteria> プロパティは、値に基づいてエンティティのプロパティをフィルター処理するための要件を定義できる <xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataConditionExpression> オブジェクトのコレクションを含む <xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataFilterExpression> を受け取ります。 これらの要件では、以下の演算子で使用できる <xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataConditionOperator> を使用します。  
  
-   <xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataConditionOperator>.Equals  
  
-   <xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataConditionOperator>.NotEquals  
  
-   <xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataConditionOperator>.In  
  
-   <xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataConditionOperator>.NotIn  
  
-   <xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataConditionOperator>.GreaterThan  
  
-   <xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataConditionOperator>.LessThan  
  
 <xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataFilterExpression> には、条件の評価時に `And` または `Or` ロジックを適用するかどうかを表す <xref:Microsoft.Xrm.Sdk.Query.LogicalOperator> も含まれます。  
  
 一部のプロパティをフィルターの条件として使用できます。 シンプルなデータ型、列挙体、<xref:Microsoft.Xrm.Sdk.BooleanManagedProperty> または <xref:Microsoft.Xrm.Sdk.Metadata.AttributeRequiredLevelManagedProperty> 型を表すプロパティのみを <xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataFilterExpression> で使用できます。 <xref:Microsoft.Xrm.Sdk.BooleanManagedProperty> または <xref:Microsoft.Xrm.Sdk.Metadata.AttributeRequiredLevelManagedProperty> を指定すると、`Value` プロパティだけが評価されます。  
  
 次の表は、<xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataFilterExpression> で使用できない <xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata> プロパティを示します。  
  
|||||  
|-|-|-|-|  
|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.Attributes>|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.Description>|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.DisplayCollectionName>|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.DisplayName>|  
|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.ManyToManyRelationships>|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.ManyToOneRelationships>|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.OneToManyRelationships>|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.Privileges>|  
  
 次の例は、除外するエンティティの一覧に含まれない、交差するエンティティではないユーザー所有のエンティティのセットを返す <xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataFilterExpression> を示します。  
  
 ```csharp
   // An array SchemaName values for non-intersect, user-owned entities that should not be returned.
     String[] excludedEntities = {
"WorkflowLog",
"Template",
"CustomerOpportunityRole",
"Import",
"UserQueryVisualization",
"UserEntityInstanceData",
"ImportLog",
"RecurrenceRule",
"QuoteClose",
"UserForm",
"SharePointDocumentLocation",
"Queue",
"DuplicateRule",
"OpportunityClose",
"Workflow",
"RecurringAppointmentMaster",
"CustomerRelationship",
"Annotation",
"SharePointSite",
"ImportData",
"ImportFile",
"OrderClose",
"Contract",
"BulkOperation",
"CampaignResponse",
"Connection",
"Report",
"CampaignActivity",
"UserEntityUISettings",
"IncidentResolution",
"GoalRollupQuery",
"MailMergeTemplate",
"Campaign",
"PostFollow",
"ImportMap",
"Goal",
"AsyncOperation",
"ProcessSession",
"UserQuery",
"ActivityPointer",
"List",
"ServiceAppointment"};

     //A filter expression to limit entities returned to non-intersect, user-owned entities not found in the list of excluded entities.
     MetadataFilterExpression EntityFilter = new MetadataFilterExpression(LogicalOperator.And);
     EntityFilter.Conditions.Add(new MetadataConditionExpression("IsIntersect", MetadataConditionOperator.Equals, false));
     EntityFilter.Conditions.Add(new MetadataConditionExpression("OwnershipType", MetadataConditionOperator.Equals, OwnershipTypes.UserOwned));
     EntityFilter.Conditions.Add(new MetadataConditionExpression("SchemaName", MetadataConditionOperator.NotIn, excludedEntities));
     MetadataConditionExpression isVisibileInMobileTrue = new MetadataConditionExpression("IsVisibleInMobile", MetadataConditionOperator.Equals, true);
     EntityFilter.Conditions.Add(isVisibileInMobileTrue);
```
  
### <a name="specify-the-properties-you-want"></a>必要なプロパティの指定
  
 <xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataQueryExpression.Properties> プロパティは <xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataPropertiesExpression> を受け取ります。 すべてのプロパティを返す場合は <xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataPropertiesExpression>.<xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataPropertiesExpression.AllProperties> を `true` に設定することができます。または文字列のコレクションを <xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataPropertiesExpression>.<xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataPropertiesExpression.PropertyNames> に提供して 状態をどのプロパティに含めるかを定義することができます。  
  
 返される、厳密に型指定されたオブジェクトには、すべてのプロパティが含まれますが、要求したオブジェクトのみにデータがあります。 他のプロパティはすべて null ですが、いくつかの例外があります。メタデータの各アイテムはいずれも、そのアイテムの値が存在する場合は  <xref:Microsoft.Xrm.Sdk.Metadata.MetadataBase.MetadataId>、`LogicalName` および <xref:Microsoft.Xrm.Sdk.Metadata.MetadataBase.HasChanged> の値が含まれます。 要求した <xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataQueryExpression.Properties> 内に指定する必要はありません。  
  
 マネージド コードを使用せず、XMLHttpRequest から返される `responseXML` を実際に分析する場合、各プロパティの要素が取得されますが、要求したものだけにデータが含まれます。 次の XML は `IsVisibleInMobile` が要求した唯一のプロパティの場合に返される、取引先担当者エンティティ メタデータを示します。  
  
```xml  
<a:EntityMetadata>  
 <c:MetadataId>608861bc-50a4-4c5f-a02c-21fe1943e2cf</c:MetadataId>  
 <c:HasChanged i:nil="true"/>  
 <c:ActivityTypeMask i:nil="true"/>  
 <c:Attributes i:nil="true"/>  
 <c:AutoRouteToOwnerQueue i:nil="true"/>  
 <c:CanBeInManyToMany i:nil="true"/>  
 <c:CanBePrimaryEntityInRelationship i:nil="true"/>  
 <c:CanBeRelatedEntityInRelationship i:nil="true"/>  
 <c:CanCreateAttributes i:nil="true"/>  
 <c:CanCreateCharts i:nil="true"/>  
 <c:CanCreateForms i:nil="true"/>  
 <c:CanCreateViews i:nil="true"/>  
 <c:CanModifyAdditionalSettings i:nil="true"/>  
 <c:CanTriggerWorkflow i:nil="true"/>  
 <c:Description i:nil="true"/>  
 <c:DisplayCollectionName i:nil="true"/>  
 <c:DisplayName i:nil="true"/>  
 <c:IconLargeName i:nil="true"/>  
 <c:IconMediumName i:nil="true"/>  
 <c:IconSmallName i:nil="true"/>  
 <c:IsActivity i:nil="true"/>  
 <c:IsActivityParty i:nil="true"/>  
 <c:IsAuditEnabled i:nil="true"/>  
 <c:IsAvailableOffline i:nil="true"/>  
 <c:IsChildEntity i:nil="true"/>  
 <c:IsConnectionsEnabled i:nil="true"/>  
 <c:IsCustomEntity i:nil="true"/>  
 <c:IsCustomizable i:nil="true"/>  
 <c:IsDocumentManagementEnabled i:nil="true"/>  
 <c:IsDuplicateDetectionEnabled i:nil="true"/>  
 <c:IsEnabledForCharts i:nil="true"/>  
 <c:IsImportable i:nil="true"/>  
 <c:IsIntersect i:nil="true"/>  
 <c:IsMailMergeEnabled i:nil="true"/>  
 <c:IsManaged i:nil="true"/>  
 <c:IsMappable i:nil="true"/>  
 <c:IsReadingPaneEnabled i:nil="true"/>  
 <c:IsRenameable i:nil="true"/>  
 <c:IsValidForAdvancedFind i:nil="true"/>  
 <c:IsValidForQueue i:nil="true"/>  
 <c:IsVisibleInMobile>  
  <a:CanBeChanged>false</a:CanBeChanged>  
  <a:ManagedPropertyLogicalName>canmodifymobilevisibility</a:ManagedPropertyLogicalName>  
  <a:Value>false</a:Value>  
 </c:IsVisibleInMobile>  
 <c:LogicalName>contact</c:LogicalName>  
 <c:ManyToManyRelationships i:nil="true"/>  
 <c:ManyToOneRelationships i:nil="true"/>  
 <c:ObjectTypeCode i:nil="true"/>  
 <c:OneToManyRelationships i:nil="true"/>  
 <c:OwnershipType i:nil="true"/>  
 <c:PrimaryIdAttribute i:nil="true"/>  
 <c:PrimaryNameAttribute i:nil="true"/>  
 <c:Privileges i:nil="true"/>  
 <c:RecurrenceBaseEntityLogicalName i:nil="true"/>  
 <c:ReportViewName i:nil="true"/>  
 <c:SchemaName i:nil="true"/>  
</a:EntityMetadata>  
  
```  
  
 将来のリリースでは、要求していないプロパティの値に null 要素を返さないようにすることでさらなる効率性が達成される可能性もあります。 この XML を解析するためのコードを作成する場合、同じクエリで返される XML を次の XML のみに削除することができることが想定されます。  
  
```xml  
<a:EntityMetadata>  
 <c:MetadataId>608861bc-50a4-4c5f-a02c-21fe1943e2cf</c:MetadataId>  
 <c:IsVisibleInMobile>  
  <a:CanBeChanged>false</a:CanBeChanged>  
  <a:ManagedPropertyLogicalName>canmodifymobilevisibility</a:ManagedPropertyLogicalName>  
  <a:Value>false</a:Value>  
 </c:IsVisibleInMobile>  
 <c:LogicalName>contact</c:LogicalName>  
</a:EntityMetadata>  
```  
  
 メタデータは階層構造で <xref:Microsoft.Xrm.Sdk.Messages.RetrieveAllEntitiesRequest> を使用したときと同じように返されます。 特定の属性または関係にアクセスするには、その一部となるエンティティを返すクエリを作成する必要があります。 特定の属性についてのデータを取得する場合、<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.Attributes> プロパティを <xref:Microsoft.Xrm.Sdk.Metadata.Query.EntityQueryExpression>.<xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataQueryExpression.Properties> に含める必要があります。 返されるエンティティ関係で、<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata> プロパティの <xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.ManyToManyRelationships>、<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.ManyToOneRelationships>、または <xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.OneToManyRelationships> の 1 つまたは複数が含まれている必要があります。  
  
 次の例は、要求したエンティティの `Attributes` プロパティを返します。  
  
```csharp
//A properties expression to limit the properties to be included with entities
MetadataPropertiesExpression EntityProperties = new MetadataPropertiesExpression()
{
 AllProperties = false
};
EntityProperties.PropertyNames.AddRange(new string[] { "Attributes" });
```

### <a name="retrieve-attribute-metadata"></a>属性メタデータの取得 
 
 <xref:Microsoft.Xrm.Sdk.Metadata.Query.EntityQueryExpression>.<xref:Microsoft.Xrm.Sdk.Metadata.Query.EntityQueryExpression.AttributeQuery> プロパティは、<xref:Microsoft.Xrm.Sdk.Metadata.Query.EntityQueryExpression><xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataQueryExpression.Criteria> および <xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataQueryExpression.Properties> に一致するエンティティに対して返される属性の <xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataQueryExpression.Criteria> および <xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataQueryExpression.Properties> を定義する、<xref:Microsoft.Xrm.Sdk.Metadata.Query.AttributeQueryExpression> を受入れます。  
  
 次の表は、<xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataFilterExpression> で使用できない <xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata> プロパティを示します。  
  
|||  
|-|-|  
|<xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata.Description>|<xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata.DisplayName>|  
|<xref:Microsoft.Xrm.Sdk.Metadata.EnumAttributeMetadata.OptionSet>|<xref:Microsoft.Xrm.Sdk.Metadata.LookupAttributeMetadata.Targets>|  
  
 次の例は、返される属性を `OptionSet` がある属性のみに制限し、これらの属性に対し <xref:Microsoft.Xrm.Sdk.Metadata.EnumAttributeMetadata.OptionSet> および <xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata.AttributeType> プロパティのみを返します。  
  
```csharp
//A condition expresson to return optionset attributes
MetadataConditionExpression[] optionsetAttributeTypes = new MetadataConditionExpression[] { 
new MetadataConditionExpression("AttributeType", MetadataConditionOperator.Equals, AttributeTypeCode.Picklist),
new MetadataConditionExpression("AttributeType", MetadataConditionOperator.Equals, AttributeTypeCode.State),
new MetadataConditionExpression("AttributeType", MetadataConditionOperator.Equals, AttributeTypeCode.Status),
new MetadataConditionExpression("AttributeType", MetadataConditionOperator.Equals, AttributeTypeCode.Boolean)
};

//A filter expression to apply the optionsetAttributeTypes condition expression
MetadataFilterExpression AttributeFilter = new MetadataFilterExpression(LogicalOperator.Or);
AttributeFilter.Conditions.AddRange(optionsetAttributeTypes);

//A Properties expression to limit the properties to be included with attributes
MetadataPropertiesExpression AttributeProperties = new MetadataPropertiesExpression() { AllProperties = false };
AttributeProperties.PropertyNames.Add("OptionSet");
AttributeProperties.PropertyNames.Add("AttributeType");
```
  
### <a name="retrieve-relationship-metadata"></a>関連付けのメタデータの取得
  
 <xref:Microsoft.Xrm.Sdk.Metadata.Query.EntityQueryExpression>.<xref:Microsoft.Xrm.Sdk.Metadata.Query.EntityQueryExpression.RelationshipQuery> プロパティは、<xref:Microsoft.Xrm.Sdk.Metadata.Query.EntityQueryExpression><xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataQueryExpression.Criteria> および <xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataQueryExpression.Properties> と一致するエンティティに必要なエンティティの関連付け <xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataQueryExpression.Criteria> および <xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataQueryExpression.Properties> を指定する <xref:Microsoft.Xrm.Sdk.Metadata.Query.RelationshipQueryExpression> を受入れます。  
  
 ManyToMany 関連付けまたは OneToMany 関連付けを返すかどうかを指定するには、条件で <xref:Microsoft.Xrm.Sdk.Metadata.RelationshipMetadataBase.RelationshipType> プロパティを使用します。  
  
 次の表は、MetadataFilterExpression で使用できない関連付けメタデータ プロパティを示します。  
  
||  
|-|  
|<xref:Microsoft.Xrm.Sdk.Metadata.OneToManyRelationshipMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.OneToManyRelationshipMetadata.AssociatedMenuConfiguration>|  
|<xref:Microsoft.Xrm.Sdk.Metadata.OneToManyRelationshipMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.OneToManyRelationshipMetadata.CascadeConfiguration>|  
|<xref:Microsoft.Xrm.Sdk.Metadata.ManyToManyRelationshipMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.ManyToManyRelationshipMetadata.Entity1AssociatedMenuConfiguration>|  
|<xref:Microsoft.Xrm.Sdk.Metadata.ManyToManyRelationshipMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.ManyToManyRelationshipMetadata.Entity2AssociatedMenuConfiguration>|  
  
### <a name="retrieve-labels"></a>ラベルの取得
  
 最後に、<xref:Microsoft.Xrm.Sdk.Metadata.Query.EntityQueryExpression>.<xref:Microsoft.Xrm.Sdk.Metadata.Query.EntityQueryExpression.LabelQuery> プロパティは、1 つまたは複数の整数 `LCID` 値を指定してどのローカライズされたラベルを返すかを決定できる <xref:Microsoft.Xrm.Sdk.Metadata.Query.LabelQueryExpression> を受け取ります。 有効なロケール ID 値は、[ロケール ID (LCID) の一覧](http://go.microsoft.com/fwlink/?LinkId=122128)のページで確認できます。 組織で複数の言語パックがインストールされている場合は、<xref:Microsoft.Xrm.Sdk.Metadata.Query.EntityQueryExpression.LabelQuery> を指定しないとすべての言語が返されます。  
  
 次の例では、ユーザーが使用する言語を表すラベルのみに制限する  <xref:Microsoft.Xrm.Sdk.Metadata.Query.LabelQueryExpression> の定義を示します。  
  
```csharp

private Guid _userId;
private int _languageCode;
```

```csharp

_userId = ((WhoAmIResponse)_service.Execute(new WhoAmIRequest())).UserId;
_languageCode = RetrieveUserUILanguageCode(_userId);
```

```csharp

protected int RetrieveUserUILanguageCode(Guid userId)
{
 QueryExpression userSettingsQuery = new QueryExpression("usersettings");
 userSettingsQuery.ColumnSet.AddColumns("uilanguageid", "systemuserid");
 userSettingsQuery.Criteria.AddCondition("systemuserid", ConditionOperator.Equal, userId);
 EntityCollection userSettings = _service.RetrieveMultiple(userSettingsQuery);
 if (userSettings.Entities.Count > 0)
 {
  return (int)userSettings.Entities[0]["uilanguageid"];
 }
 return 0;
}
```

```csharp

//A label query expression to limit the labels returned to only those for the user's preferred language
LabelQueryExpression labelQuery = new LabelQueryExpression();
labelQuery.FilterLanguages.Add(_languageCode);
```
  
<a name="BKMK_RetrievingNeworChangedMetadata"></a> 
  
## <a name="retrieve-new-or-changed-metadata"></a>新規または変更済みのメタデータの取得

 <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesResponse> クラスは要求したデータが含まれている厳密に型指定された <xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadataCollection> を返します。 <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesResponse> クラスは、以降の要求で<xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesRequest>.<xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesRequest.ClientVersionStamp> に渡すことができる <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesResponse.ServerVersionStamp>  値も含まれています。 値が <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesRequest.ClientVersionStamp> プロパティに含まれているとき、<xref:Microsoft.Xrm.Sdk.Metadata.Query.EntityQueryExpression> に一致し、`ClientVersionStamp` が取得された以降に変更されたデータだけが返されます。 これの唯一の例外は、<xref:Microsoft.Xrm.Sdk.Metadata.Query.EntityQueryExpression>.<xref:Microsoft.Xrm.Sdk.Metadata.Query.MetadataQueryExpression.Properties> が <xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.Privileges> を含む場合です。 特権は <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesRequest.ClientVersionStamp> に関係なく、常に返されます。 こうすると、アプリケーションで最後にメタデータをクエリした後で関連する重要な変更が発生したかどうかを確認できます。 次に、新しいまたは変更されたメタデータを、アプリケーションで不要なメタデータのダウンロードに伴うパフォーマンスの問題が発生するのを防げるよう、永続メタデータ キャッシュに統合できます。  
  
 <xref:Microsoft.Xrm.Sdk.Metadata.MetadataBase.HasChanged> プロパティでは、変更されたメタデータ アイテムの子要素を検出できる方法を提供します。 すべてのメタデータが、メタデータ アイテムの一部として返されるので、<xref:Microsoft.Xrm.Sdk.Metadata.OptionMetadata> のラベルを変更した場合、含まれる <xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata>、<xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata>、<xref:Microsoft.Xrm.Sdk.Metadata.OptionSetMetadata> のプロパティが返されます。 ただし、<xref:Microsoft.Xrm.Sdk.Metadata.MetadataBase.HasChanged> プロパティがこれらのメタデータ アイテムを含む場合は false を返します。 <xref:Microsoft.Xrm.Sdk.Metadata.OptionMetadata>.<xref:Microsoft.Xrm.Sdk.Metadata.MetadataBase.HasChanged> プロパティのみが true になります。  
  
 次の例は <xref:Microsoft.Xrm.Sdk.Metadata.Query.EntityQueryExpression> を定義し、null に設定されている <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesRequest.ClientVersionStamp> の要求を実行することにより、最初の要求を作成しています。  
  
```csharp
//An entity query expression to combine the filter expressions and property expressions for the query.
EntityQueryExpression entityQueryExpression = new EntityQueryExpression()
{

 Criteria = EntityFilter,
 Properties = EntityProperties,
 AttributeQuery = new AttributeQueryExpression()
 {
  Criteria = AttributeFilter,
  Properties = AttributeProperties
 },
 LabelQuery = labelQuery

};

//Retrieve the metadata for the query without a ClientVersionStamp
RetrieveMetadataChangesResponse initialRequest = getMetadataChanges(entityQueryExpression, null, DeletedMetadataFilters.OptionSet);

```

```csharp
protected RetrieveMetadataChangesResponse getMetadataChanges(
 EntityQueryExpression entityQueryExpression,
 String clientVersionStamp,
 DeletedMetadataFilters deletedMetadataFilter)
{
 RetrieveMetadataChangesRequest retrieveMetadataChangesRequest = new RetrieveMetadataChangesRequest()
 {
  Query = entityQueryExpression,
  ClientVersionStamp = clientVersionStamp,
  DeletedMetadataFilters = deletedMetadataFilter
 };

 return (RetrieveMetadataChangesResponse)_service.Execute(retrieveMetadataChangesRequest);

}
```

<a name="BKMK_RetrieveInformationaboutDeletedMetadata"></a>
   
## <a name="retrieve-information-about-deleted-metadata"></a>削除されたメタデータに関する情報の取得  

 <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesResponse>.<xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesResponse.DeletedMetadata> プロパティは <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesRequest.ClientVersionStamp> および <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesRequest.DeletedMetadataFilters> プロパティが <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesRequest> に設定されている場合に <xref:Microsoft.Xrm.Sdk.Metadata.Query.DeletedMetadataCollection> を返します。 <xref:Microsoft.Xrm.Sdk.Metadata.Query.DeletedMetadataCollection> には、時間制限内で削除された <xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata>、<xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata> または <xref:Microsoft.Xrm.Sdk.Metadata.RelationshipMetadataBase> オブジェクトの <xref:Microsoft.Xrm.Sdk.Metadata.MetadataBase.MetadataId> の値を含みます。 詳細については、「[削除されたメタデータの有効期限](/dynamics365/customer-engagement/developer/retrieve-detect-changes-metadata#BKMK_DeletedMetadataExpiration)」を参照してください。  
  
 <xref:Microsoft.Xrm.Sdk.Metadata.Query.DeletedMetadataFilters> 列挙を <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesRequest>.<xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesRequest.DeletedMetadataFilters> とともに使用して、関心のあるメタデータの種類のみに情報を限定します。 <xref:Microsoft.Xrm.Sdk.Metadata.Query.DeletedMetadataFilters> 列挙体には次のオプションが用意されています。  
  
-   <xref:Microsoft.Xrm.Sdk.Metadata.Query.DeletedMetadataFilters>.Entity (既定)  
  
-   <xref:Microsoft.Xrm.Sdk.Metadata.Query.DeletedMetadataFilters>.Attribute  
  
-   <xref:Microsoft.Xrm.Sdk.Metadata.Query.DeletedMetadataFilters>.Relationship  
  
-   <xref:Microsoft.Xrm.Sdk.Metadata.Query.DeletedMetadataFilters>.Label  
  
-   <xref:Microsoft.Xrm.Sdk.Metadata.Query.DeletedMetadataFilters>.OptionSet  
  
 また、<xref:Microsoft.Xrm.Sdk.Metadata.Query.DeletedMetadataFilters> 列挙を <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesResponse>.<xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesResponse.DeletedMetadata> へのキーとして使用し、<xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesResponse>.<xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesResponse.DeletedMetadata> で見つかった `GUID` の値をフィルター処理します。 プロパティ。  
  
 メタデータ キャッシュの設計を行う場合、削除されたメタデータ アイテムを識別して削除できるよう、アイテムごとに <xref:Microsoft.Xrm.Sdk.Metadata.MetadataBase.MetadataId> を使用することができます。  
  
<a name="BKMK_DeletedMetadataExpiration"></a>
   
### <a name="deleted-metadata-expiration"></a>削除されたメタデータの有効期限  

 削除されたメタデータ アイテムは、`Organization.ExpireSubscriptionsInDays` の値により指定されている制限期間中、追跡されます。 既定では、値は 90 日に設定されています。 <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesRequest>.<xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesRequest.ClientVersionStamp> 値が、最後のメタデータ クエリが有効期限の前のものであることを示している場合、サービスは `ExpiredVersionStamp` エラー (0x80044352) を表示します。データを取得して更新中に、既存のメタデータ キャッシュを取得しようとするたびにこのエラーが表示され、<xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesRequest.ClientVersionStamp> を使用せずに渡された 2 番目の要求から結果を取得したメタデータ キャッシュの再初期化の準備が行われます。 `ExpiredVersionStamp` エラーは、`ExpireSubscriptionsInDays` 値の変更などのサーバー上での変更が、削除データの正確な追跡に影響する場合にもスローされます。  
  
 次の例は <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesRequest.ClientVersionStamp> を渡し、`ExpiredVersionStamp` を取得しています。 エラーが示された場合、キャッシュは `null` に設定された <xref:Microsoft.Xrm.Sdk.Messages.RetrieveMetadataChangesRequest.ClientVersionStamp> を使用した新しい要求を渡すことによって再初期化されます。  
  
```csharp

protected String updateOptionLabelList(EntityQueryExpression entityQueryExpression, String clientVersionStamp)
{
 //Retrieve metadata changes and add them to the cache
 RetrieveMetadataChangesResponse updateResponse;
 try
 {
  updateResponse = getMetadataChanges(entityQueryExpression, clientVersionStamp, DeletedMetadataFilters.OptionSet);
  addOptionLabelsToCache(updateResponse.EntityMetadata, true);
  removeOptionLabelsFromCache(updateResponse.DeletedMetadata, true);

 }
 catch (FaultException<Microsoft.Xrm.Sdk.OrganizationServiceFault> ex)
 {
  // Check for ErrorCodes.ExpiredVersionStamp (0x80044352)
  // Will occur when the timestamp exceeds the Organization.ExpireSubscriptionsInDays value, which is 90 by default.
  if (ex.Detail.ErrorCode == unchecked((int)0x80044352))
  {
   //reinitialize cache
   _optionLabelList.Clear();

   updateResponse = getMetadataChanges(entityQueryExpression, null, DeletedMetadataFilters.OptionSet);
   //Add them to the cache and display the changes
   addOptionLabelsToCache(updateResponse.EntityMetadata, true);

  }
  else
  {
   throw ex;
  }

 }
 return updateResponse.ServerVersionStamp;
}
```

  
<a name="BKMK_PerformanceRetrievingDeletedMetadata"></a>
   
### <a name="performance-when-retrieving-deleted-metadata"></a>削除されたメタデータを取得するときのパフォーマンス 
 
 メタデータ アイテムを削除すると、Dynamics 365 メタデータ キャッシュではなくデータベースに保存されます。 削除されたメタデータが <xref:Microsoft.Xrm.Sdk.Metadata.MetadataBase.MetadataId> とメタデータ アイテムの種類のみに制限されていても、データベースへのアクセスは変更をクエリするだけの場合よりもより多くのサーバー リソースが必要な操作です。  
  
### <a name="see-also"></a>関連項目  
 [アプリケーションとサーバー拡張機能の作成](/dynamics365/customer-engagement/developer/extend-dynamics-365-server)   
 [Dynamics 365 サービスをオフラインで使用する](/dynamics365/customer-engagement/developer/org-service/offline-use-services)   
 [サンプル: メタデータのクエリと変更の検出](/dynamics365/customer-engagement/developer/org-service/sample-query-metadata-detect-changes)   
 [Dynamics 365 のメタデータ モデルの拡張](/dynamics365/customer-engagement/developer/org-service/use-organization-service-metadata)   
 [エンティティ メタデータのカスタマイズ](/dynamics365/customer-engagement/developer/customize-entity-metadata)   
 [エンティティ属性メタデータのカスタマイズ](/dynamics365/customer-engagement/developer/customize-entity-attribute-metadata)   
 [エンティティ関係メタデータをカスタマイズする](/dynamics365/customer-engagement/developer/customize-entity-relationship-metadata)   
 [JavaScript を使用したメタデータのクエリ](https://msdn.microsoft.com/library/jj919080.aspx)
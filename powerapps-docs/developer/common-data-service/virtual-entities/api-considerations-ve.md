---
title: 仮想エンティティの API に関する考慮事項 (アプリ用 Common Data Service) | Microsoft Docs
description: 仮想エンティティの API について説明する
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: d329dade-16c5-46e9-8dec-4b8efb996dea
author: mayadumesh
ms.author: jdaly
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="api-considerations-of-virtual-entities"></a>仮想エンティティの API に関する考慮事項

アプリ用 Common Data Service の仮想エンティティの導入に関連付けられるメタデータ システムに対する変更には 2 つの大きなカテゴリがあります。

- 新しいアセンブリ、名前空間、クラス、およびユーザー定義の仮想エンティティ データ プロバイダーの開発をサポートするその他の種類の追加
- 外部データ ソース マッピングをサポートするためのいくつかの追加のプロパティや、この機能の初期実装の制限を反映する既存のエンティティおよび属性プロパティーの動作の変更を含む、コア プラットフォームの変更

## <a name="dynamics-365-data-sdk-assembly"></a>Dynamics 365 Data SDK アセンブリ

Dynamics 365 Data SDK アセンブリ、`Microsoft.Xrm.Sdk.Data.dll` には、ユーザー定義の仮想エンティティ データ プロバイダーの作成を支援するための種類が含まれています。 次の名前空間で構成されます:

|名前空間|説明|
|---------|---------|
|<xref:Microsoft.Xrm.Sdk.Data>|**AllowedQueryOptions** 列挙などのいくつかの一般的な種類を含むベースの名前空間|
|<xref:Microsoft.Xrm.Sdk.Data.CodeGen>|動的リフレクション、種類の一致、およびコードの生成をサポートするクラスとインターフェイスが含まれます。  主に内部プロバイダー エンジンによって使用されます。|
|<xref:Microsoft.Xrm.Sdk.Data.Converters>|標準 XRM タイプを対応する .NET 基本タイプに変換する一連のクラス|
|<xref:Microsoft.Xrm.Sdk.Data.Exceptions>|ランタイム値の解決時に発生する可能性のあるエラーを表す例外クラスのセット。  すべては Microsoft.Xrm.Sdk.SdkExceptionBase から派生しています。|
|<xref:Microsoft.Xrm.Sdk.Data.Expressions>|FILTER、JOIN、および ORDER などのサポートされているクエリ変換の実装を支援するクラス。|
|<xref:Microsoft.Xrm.Sdk.Data.Infra>|中央クエリ処理をサポートするその他のクラス。|
|<xref:Microsoft.Xrm.Sdk.Data.Mappings>|仮想エンティティ メタデータ タイプから外部タイプへのマッピングを構築するクラスとインターフェイス。|
|Microsoft.Xrm.Sdk.Data.Visitors|**RetrieveMultiple** 中に [ビジター パターン](https://en.wikipedia.org/wiki/Visitor_pattern) を実装して、データ プロバイダーに渡される **QueryExpression** パラメーター上で特定の操作を実行するクラス。 一般的なクエリと LINQ ベースの処理の両方に特定のサポートを提供します。 これらのクラスは Microsoft.Xrm.Sdk.Query.QueryExpressionVisitorBase から派生しています。|

このアセンブリは NuGet パッケージとして配布されます: [Microsoft.CrmSdk.Data](https://www.nuget.org/packages/Microsoft.CrmSdk.Data/)

## <a name="changes-to-the-core-platform"></a>コア プラットフォームへの変更

標準のアプリ用 CDS 参照種類への次の変更が、仮想エンティティをサポートするために導入されました。

### <a name="new-entities"></a>新しいエンティティ

アプリ用 Web CDS は、仮想エンティティ データ プロバイダーとソースを次の新しいエンティティとして公開します: [EntityDataProvider](../reference/entities/entitydataprovider.md) と [EntityDataSource](../reference/entities/entitydatasource.md)。 

### <a name="new-metadata-properties"></a>新しい metadata.properties.key

4 つの新しいプロパティが <xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata> クラスに追加されました。

|プロパティ|説明|
|--|--|
|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.DataProviderId>|関連する仮想エンティティ データ プロバイダーを識別する GUID|
|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.DataSourceId>|関連する仮想エンティティ データ ソースを識別する GUID|
|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.ExternalName>|外部データ ソースのこの種類の名前|
|<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.ExternalCollectionName>|UI で使用され、OData アクセスをサポートする、この種類の複数名|

2 つの新しいプロパティが <xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata> クラスに追加されました。

|プロパティ|説明|
|--|--|
|<xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata.ExternalName>|外部データ ソースの種類の名前|
|<xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata.IsDataSourceSecret>|このフィールドに機密情報を含んでいるかどうかを示します|

`ExternalName` プロパティも、<xref:Microsoft.Xrm.Sdk.Metadata.OptionMetadata> および <xref:Microsoft.Xrm.Sdk.Metadata.OptionSetMetadata> クラスに追加されました。 これらの外部の名前は、外部データソース内の関連する種類の名前を指定することによって、外部データソースのマッピングを支援します。 これらのプロパティは仮想エンティティでのみ使用されます。組み込みまたは標準のユーザー定義にエンティティの種類の場合、これらの外部名は `null` でなければなりません。


### <a name="virtual-entity-creation"></a>仮想エンティティの作成

仮想エンティティの種類をプログラムで作成するアプローチは、標準のユーザー定義のエンティティの種類の作成とは少し異なります:

- 関連付けられたデータ プロバイダー (およびオプションのデータ ソース) が作成時にわかっている場合は、これらが指定されます。
- この種類のデータ プロバイダーがわからない場合は、最低でも、<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.DataProviderId> は `7015A531-CC0D-4537-B5F2-C882A1EB65AD` に設定し、<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.DataSourceId> は `null` に設定します。 実行時にこの種類のインスタンスを使用する前に、これらのプロパティに適切な値を割り当てる必要があります。

2 つの新しいエンティティ、[EntityDataProvider](../reference/entities/entitydataprovider.md) およびオプションの [EntityDataSource](../reference/entities/entitydatasource.md) は、プラグイン、およびそれぞれの ID、`entitydataproviderid` および `entitydatasourceid` を登録する際に作成され、これらの必要な GUID を表します。 (それ以外の場合は、開発者はこれらのユーザー定義の種類に直接アクセスすることはめったにありません。) DataSourceには、対応する DataProvider の種類と一致する必要があるプロパティ `entitydataproviderid` が含まれているか、実行時例外がスローされることに注意してください。

> [!WARNING]
> 標準 (非仮想) エンティティは関連する `DataProviderId` と `DataSourceId` の値がデフォルト値 (`null`) に設定されていることが必要で、それ以外の場合は実行時例外がスローされます。  作成される、非仮想の種類を仮想の種類に変換したり、またはその逆を行うことはできません。 

### <a name="entity-metadata-property-behavior-changes"></a>エンティティ メタデータ プロパティ動作の変更

次の表は、標準の [EntityMetadata properties](/dotnet/api/microsoft.xrm.sdk.metadata.entitymetadata?view=dynamics-general-ce-9#properties) の動作が仮想エンティティに適用されたときにどのように変更されるかについて説明しています。 一部のプロパティは仮想エンティティには有効ではありませんが、その他のプロパティは範囲や値に制限があります。

|**メタデータ プロパティ**|**適用?**|**メモ**|
|---------------------|------------|---------|
|ActivityTypeMask|_無効_|常時 0|
|属性|有効||
|AutoCreateAccessTeams|_無効_|常時 false|
|AutoRouteToOwnerQueue|_無効_|常時 false、キューはサポートされていません。|
|CanBeInManyToMany|有効||
|CanBePrimaryEntityInRelationship|有効||
|CanBeRelatedEntityInRelationship|有効||
|CanChangeHierarchicalRelationship|_無効_|常時 false、階層型の関連付けはサポートされていません。|
|CanChangeTrackingBeEnabled|_無効_|常時 false、変更の追跡および値の監査はサポートされていません。|
|CanCreateAttributes|有効||
|CanCreateCharts|_無効_|常時 false|
|CanCreateForms|有効||
|CanCreateViews|有効||
|CanEnableSyncToExternalSearchIndex|_無効_|常時 false|
|CanModifyAdditionalSettings|有効||
|CanTriggerWorkflow|_無効_|常時 false、ワークフローはトリガーできません。
|ChangeTrackingEnabled|_無効_|常時 false|
|CollectionSchemaName|有効||
|DaysSinceRecordLastModified|_無効_|常時 null または 0|
|内容|有効||
|DisplayCollectionName|有効||
|DisplayName|有効||
|EnforceStateTransitions|_無効_|StateCode とステータスはサポートされていません。|
|EntityColor|有効||
|EntityHelpUrl|有効||
|EntityHelpUrlEnabled|有効||
|EntitySetName|有効||
|ExtensionData|_無効_|廃止されたプロパティ|
|HasChanged|有効||
|IconLargeName|有効||
|IconMediumName|有効||
|IconSmallName|有効||
|IntroducedVersion|有効||
|IsActivity|_無効_|常時 false、アクティビティはサポートされていません。|
|IsActivityParty|_無効_|常時 false|
|IsAIRUpdated|_無効_|廃止|
|IsAuditEnabled|_無効_|常時 false、監査はサポートされていません。|
|IsAvailableOffline|_無効_|常時 false、オフラインでの使用はサポートされていません。|
|IsBusinessProcessEnabled|_無効_|常時 false、ビジネスプロセスはサポートされていません。|
|IsChildEntity|_無効_|常時 false、すべての仮想エンティティは組織的に所有されます。|
|IsConnectionsEnabled|有効|<!-- TODO: Connection support is still TBD for Potassium -->|
|IsCustomEntity|有効||
|IsCustomizable|有効||
|IsDocumentManagementEnabled|有効||
|IsDocumentRecommendationsEnabled|_無効_|常時false、この新しい機能はサポートされていません。|
|IsDuplicateDetectionEnabled|_無効_|常時 false、しかし重複データ検出はソース データで実行できます。|
|IsEnabledForCharts|_制限あり_|サポートされた Fetch 句のみ。|
|IsEnabledForTrace|有効||
|IsImportable|有効|<!--TODO: May have limitations. -->|
|IsInteractionCentricEnabled|有効||
|IsIntersect|有効||
|IsKnowledgeManagementEnabled|_無効_|常時 false、ナレッジ マネージメントの統合はサポートされていません。|
|IsMailMergeEnabled|有効||
|IsManaged|有効||
|IsMappable|有効||
|IsOfflineInMobileClient|_無効_|常時 false、仮想エンティティ値はオフラインでの使用にはキャッシュされません。|
|IsOneNoteIntegrationEnabled|有効||
|IsOptimisticConcurrencyEnabled|_無効_|常時 false、同時実行をデータ ソースで実行する必要があります。|
|IsPrivate|有効||
|IsQuickCreateEnabled|有効||
|IsReadOnlyInMobileClient|有効||
|IsRenameable|有効||
|IsSLAEnabled|_無効_|常時 false|
|IsStateModelAware|_無効_|<!-- TODO: TBD? -->|
|IsValidForAdvancedFind|有効||
|IsValidForQueue|有効||
|IsVisibleInMobile|有効||
|IsVisibleInMobileClient|有効||
|キー|_無効_|代替キーはサポートされていません。|
|LogicalCollectionName|有効||
|LogicalName|有効||
|ManyToManyRelationships|有効||
|ManyToOneRelationships|有効| 2 つの仮想エンティティ間ではサポートされていません。 |
|MetadataId|有効||
|MobileOfflineFilters|_無効_|常時 false、オフラインでの使用はサポートされていません。|
|ObjectTypeCode|有効||
|OneToManyRelationships|有効||
|OwnershipType|_無効_|常時 **OrganizationOwned**|
|PrimaryIdAttribute|有効||
|PrimaryImageAttribute|有効||
|PrimaryNameAttribute|有効||
|特権|_無効_|<!-- TODO: TBD? -->|
|RecurrenceBaseEntityLogicalName|_無効_||
|ReportViewName|_無効_||
|SchemaName|有効||
|SyncToExternalSearchIndex|_無効_||

<!-- TODO: Add links to reference properties in first column. -->


### <a name="attribute-metadata-property-behavior-changes"></a>属性メタデータ プロパティ動作の変更

次の表は、標準の [AttributeMetadata のプロパティ](/dotnet/api/microsoft.xrm.sdk.metadata.attributemetadata?view=dynamics-general-ce-9#properties) の動作が仮想エンティティに適用されたときにどのように変更されるかについて説明しています。 一部のプロパティは仮想エンティティには有効ではありませんが、その他のプロパティは範囲や値に制限があります。

|**メタデータ プロパティ**|**適用?**|**メモ**|
|---------------------|------------|---------|
|ColumnNumber|_無効_||
|DeprecatedVersion|有効||
|内容|有効||
|DisplayName|有効||
|EntityLogicalName|有効||
|ExtensionData|_無効_|<!-- TODO: TBD? -->|
|HasChanged|有効||
|InheritsFrom|有効||
|IntroducedVersion|有効||
|IsAuditEnabled|_無効_|常時 false、監査はサポートされていません。|
|IsCustomAttribute|有効||
|IsCustomizable|有効||
|IsFilterable|有効||
|IsGlobalFilterEnabled|有効||
|IsLogical|有効||
|IsManaged|有効||
|IsPrimaryId|有効||
|IsPrimaryName|有効||
|IsRenameable|有効||
|IsSearchable|有効||
|IsSecured|_無効_|常時 false、フィールドレベルのセキュリティはサポートされていません。|
|IsSortableEnabled|有効||
|IsValidForAdvancedFind|有効||
|IsValidForCreate|有効||
|IsValidForRead|有効||
|IsValidForUpdate|有効||
|LinkedAttributeId|有効||
|LogicalName|有効||
|MetadataId|有効||
|RequiredLevel|有効||
|SchemaName|有効||
|SourceType|_無効_|常時 0、計算されたまたはロールアップ値はサポートされていません。|

### <a name="see-also"></a>関連項目

[仮想エンティティに関する入門情報](get-started-ve.md)<br />
[カスタム仮想エンティティ データ プロバイダー](custom-ve-data-providers.md)<br />
[サンプル: 汎用仮想エンティティ データ プロバイダー プラグイン](sample-generic-ve-plugin.md)


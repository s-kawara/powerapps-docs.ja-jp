---
title: エンティティの参照について (Common Data Service)| Microsoft Docs
description: このリファレンスを使用して、特定のエンティティに対して実行可能な操作、各エンティティのデフォルトの属性、エンティティ間の関連付けについて説明します。
author: JimDaly
manager: kvivek
ms.service: powerapps
ms.devlang: na
ms.topic: reference
ms.date: 03/31/2019
ms.author: jdaly
ms.reviewer: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="about-the-entity-reference"></a>エンティティの参照について

このリファレンスを使用して、特定のエンティティに対して実行可能な操作、各エンティティのデフォルトの属性、エンティティ間の関連付けについて説明します。

> [!NOTE]
> この参照には以下の場合のエンティティのみが含まれています:
>
> -  **IsPrivate** が `false` と等しい
>    - 外部のユースケースが存在しないエンティティは除外されます。
> - **IsIntersect** が `false` と等しい
>    - これは、多対多の関連付けを定義するために使用されるエンティティを除外します。
> - エンティティは特定の種類の直接データ変更操作をサポートします。
>    - これは直接作業できないエンティティを除外します。 
>
> ご使用の環境のすべてのエンティティ メタデータ情報については、[Common Data Service 開発者ガイド: 組織のメタデータの参照](/dynamics365/customer-engagement/developer/browse-your-metadata) を参照してください。


## <a name="entity-properties"></a>エンティティ プロパティ

このセクションには、すべてではなく選択されたエンティティ プロパティが含まれています。 開発者にとって最も役に立つと予想されるプロパティのみが含まれます。 一部のエンティティ プロパティ値の場合、これを変更できます。

## <a name="attributes"></a>属性
属性は次の 2 つのセクションに分かれています: **書き込み可能な属性**および**読み取り専用属性**。 この分離の目的は、エンティティ インスタンスを作成または更新するときに開発者が設定できる属性に重点を置くことです。 これらの属性を理解することは、単に値を取得するだけでなく、エンティティでできることを理解するのに役立ちます。 

**書き込み可能な属性**セクションの属性は、**IsValidForCreate** または **IsValidForUpdate** プロパティの *いずれか* に対して true を返します (通常は両方)。 これらのプロパティのいずれかが false を返す場合、これが示されます。

**読み取り専用属性**は **IsValidForCreate** *および* **IsValidForUpdate** プロパティに常に false を返します。

## <a name="relationships"></a>関係

[EntityMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.entitymetadata) クラスには、関連付けを表す 3 つのプロパティが含まれます。

|プロパティ| 型  |説明  |
|---------|---------|---------|
|[OneToManyRelationships](/dotnet/api/microsoft.xrm.sdk.metadata.entitymetadata.onetomanyrelationships#Microsoft_Xrm_Sdk_Metadata_EntityMetadata_OneToManyRelationships)|[OneToManyRelationshipMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.onetomanyrelationshipmetadata)[]|エンティティの 1 対多リレーションシップの配列を取得します。|
|[EntityMetadata.ManyToOneRelationships](/dotnet/api/microsoft.xrm.sdk.metadata.entitymetadata.manytoonerelationships#Microsoft_Xrm_Sdk_Metadata_EntityMetadata_ManyToOneRelationships)|[OneToManyRelationshipMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.onetomanyrelationshipmetadata)[]|エンティティの多対 1 リレーションシップの配列を取得します。|
|[EntityMetadata.ManyToManyRelationships](/dotnet/api/microsoft.xrm.sdk.metadata.entitymetadata.manytomanyrelationships#Microsoft_Xrm_Sdk_Metadata_EntityMetadata_ManyToManyRelationships)|[ManyToManyRelationshipMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.manytomanyrelationshipmetadata)[]|エンティティの多対多リレーションシップの配列を取得します。|

> [!NOTE]
> 各エンティティがそれに適用されるそれらの関連付けをリストする一方、各関連付けは両方のエンティティによって共有されることに留意することが重要です。 この関連付けはエンティティ*間*に存在します。 1 対多の関連付けが存在する一方で、*多対 1* 関連付けは、単に参照元エンティティからの 1 対多の関連付けのビューです。

### <a name="one-to-many-relationships"></a>一対多関連付け
混乱を最小限に抑えて実際の *多対 1* 関連付けが存在しないことを表すために、各関連付けの詳細は一度しか記録されません。 各 1 対多の関連付けは、参照されたエンティティとともにリストされ、選択された関連付けの詳細と、対応する *[多対 1]* の関連付けへのリンクを含みます。 リストされた *[多対 1]* の関連付けには、対応する 1 対多の関連付けへのリンクのみが含まれます。

各一対多関連付けには次のプロパティが含まれます。

|プロパティ|説明|
|---------|---------|
|`ReferencingEntity`|関連するエンティティの論理名です。|
|`ReferencingAttribute`|関連するエンティティでの属性の論理名には、主エンティティの主キーへの参照が含まれます。|
|`IsHierarchical`|関連付けが自己参照の階層的な関連付けを表すかどうか|
|`IsCustomizable`|関連付けの管理プロパティが変更できるかどうか。|
|`ReferencedEntityNavigationPropertyName`|この関連付けの Web API コレクション値を持つナビゲーション プロパティの名前。<br />詳細: [Common Data Service の開発者ガイド ナビゲーション プロパティ](/dynamics365/customer-engagement/developer/webapi/web-api-types-operations#navigation-properties)|
|`AssociatedMenuConfiguration`|モデル駆動型アプリで使用されるデータで、関連するエンティティ データが主エンティティから UI 内でアクセスできるかどうか、およびそのエンティティ データにアクセスする方法をコントロールします。|
|`CascadeConfiguration`|親エンティティで実行されたどの操作が、関連するエンティティに伝播するかを説明するデータ。<br />詳細: [伝播構成](../entity-relationship-metadata.md#cascade-configuration)|


### <a name="many-to-many-relationships"></a>多対多関連付け
各多対多関連付けには [Entity1LogicalName](/dotnet/api/microsoft.xrm.sdk.metadata.manytomanyrelationshipmetadata.entity1logicalname) および [Entity2LogicalName](/dotnet/api/microsoft.xrm.sdk.metadata.manytomanyrelationshipmetadata.entity2logicalname) が含まれます。 このドキュメントでは、関連付けの詳細は、*[エンティティ 1]* のトピックにのみ含まれています。 エンティティが *エンティティ 2* のそれぞれの多対多の関連付けには、*エンティティ 2* のトピックの詳細へのリンクのみが含まれています。

各多対多関連付けには次のプロパティが含まれます。

|プロパティ|説明|
|---------|---------|
|`IntersectEntityName`|多対多関連付けをサポートしている、交差するエンティティの論理名|
|`Entity1LogicalName`|関連付けの最初のエンティティに対する論理名。|
|`Entity1IntersectAttribute`|交差するエンティティ属性の論理名には、最初のエンティティの主キーへの参照が含まれます。|
|`Entity1NavigationPropertyName`|この関連付けの Web API コレクション値を持つナビゲーション プロパティの名前。<br />詳細: [Common Data Service の開発者ガイド ナビゲーション プロパティ](/dynamics365/customer-engagement/developer/webapi/web-api-types-operations#navigation-properties)|
|`Entity1AssociatedMenuConfiguration`|モデル駆動型アプリで使用されるデータで、最初のエンティティ データが 2 番目のエンティティから UI 内でアクセスできるかどうか、およびそのエンティティ データにアクセスする方法をコントロールします。|
|`Entity2LogicalName`|関連付けの 2 番目のエンティティに対する論理名。|
|`Entity2IntersectAttribute`|交差するエンティティ属性の論理名には、2 番目のエンティティの主キーへの参照が含まれます。|
|`Entity2NavigationPropertyName`|通常、これは `Entity1NavigationPropertyName` と同じです|
|`Entity2AssociatedMenuConfiguration`|モデル駆動型アプリで使用されるデータで、2 番目のエンティティ データが最初のエンティティから UI 内でアクセスできるかどうか、およびそのエンティティ データにアクセスする方法をコントロールします。|
|`IsCustomizable`|関連付けの管理プロパティが変更できるかどうか。|


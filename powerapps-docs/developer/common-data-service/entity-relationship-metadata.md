---
title: エンティティの関連付けのメタデータ | Microsoft Docs
description: アプリ用 Common Data Service で使用するエンティティ関係メタデータについて。
services: ''
suite: powerapps
documentationcenter: na
author: mayadumesh
manager: kvivek
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/31/2018
ms.author: jdaly
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="entity-relationship-metadata"></a>エンティティの関連付けのメタデータ

ソリューション エクスプローラーまたは `EntityMetadata` の 3 つの関係コレクションを表示すると、3 種類のエンティティ関係があると思われる場合があります。 次の表に示したとおり、実際は 2 つだけです。

|関係内容|説明|
|--|--|
|一対多<br />[OneToManyRelationshipMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.onetomanyrelationshipmetadata)|関連エンティティの検索フィールドを使用して、**主エンティティ**の 1 つのエンティティ レコードが他の複数の**関連エンティティ**レコードに関連付けられるエンティティ関係。<br />主エンティティ レコードを表示する際に、それに関連付けられた関連エンティティ レコードの一覧を表示できます。|
|多対多<br />[ManyToManyRelationshipMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.manytomanyrelationshipmetadata)|特殊な*関係エンティティ*に基づくエンティティ関係は、*交差する*エンティティと呼ばれることもあり、1 つのエンティティの複数のレコードが別のエンティティの複数のレコードに関連付けられます。<br />多対多の関連付けのいずれかのエンティティのレコードを表示すると、それと関連する他のエンティティのレコードのリストを表示できます。|

`EntityMetadata``ManyToOneRelationships` コレクションには、[OneToManyRelationshipMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.onetomanyrelationshipmetadata) タイプが含まれています。 一対多の関連付けは、エンティティ間にあり、*主エンティティ*または*関連エンティティ*のいずれかとして各エンティティを参照します。 *子エンティティ*とも呼ばれる関連エンティティには、主エンティティ (*親エンティティ*とも呼ばれる) からのレコードへの参照を格納できる検索属性もあります。 多対一の関係は、関連エンティティから見た単なる一対多の関係です。

> [!NOTE]
> 関連エンティティは*子エンティティ*と呼ばれることもありますが、これらをセキュリティが関連するエンティティに適用されるのを示す [子エンティティ](entity-metadata.md#child-entities) と混同しないでください。

詳細情報: [エンティティ間の関連付けの作成](../../maker/common-data-service/data-platform-entity-lookup.md)

## <a name="cascade-configuration"></a>伝播構成

一対多のエンティティ関係が存在するときは、データの整合性を維持し、ビジネス プロセスを自動化するように構成できるカスケード動作があります。 詳細情報: [エンティティ関係のカスケード動作の構成](configure-entity-relationship-cascading-behavior.md)

## <a name="create-a-hierarchy-of-entities"></a>エンティティ階層の作成

自己参照の一対多の関連付けでは、`IsHierarchical` プロパティを `true` に設定することによって階層を設定できます。

モデル駆動型アプリでは、これにより階層を表示および操作できるようになります。 

開発者にとっては、`Under` および `Not Under` 演算子を使用して階層に基づいた新しいタイプのクエリが可能になります。

詳細: [アプリ用 Common Data Service 開発者向けガイド : 階層的に関連するデータのクエリと視覚化](/dynamics365/customer-engagement/customize/query-visualize-hierarchical-data)。

### <a name="see-also"></a>関連項目

[アプリ用 Common Data Service のエンティティ](entities.md)

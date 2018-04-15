---
title: エンティティ関係メタデータ | Microsoft Docs
description: Common Data Service for Apps で使用されるエンティティ関係メタデータについて説明します。
services: ''
suite: powerapps
documentationcenter: na
author: JimDaly
manager: faisalmo
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/12/2018
ms.author: jdaly
ms.openlocfilehash: da8899151fdb40713d19ca1cb82444a486526549
ms.sourcegitcommit: 59785e9e82da8f5bd459dcb5da3d5c18064b0899
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2018
---
# <a name="entity-relationship-metadata"></a>エンティティ関係メタデータ

ソリューション エクスプローラーまたは `EntityMetadata` の 3 つの関係コレクションを見ると、エンティティ関係の種類は 3 つのようですが、 実際には次の表に示すように 2 種類しかありません。

|関係の種類|説明|
|--|--|
|一対多<br />[OneToManyRelationshipMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.onetomanyrelationshipmetadata)|関連するエンティティの参照フィールドがあるので、**プライマリ エンティティ**の 1 つのエンティティ レコードを、他の多くの**関連エンティティ** レコードに関連付けることができるエンティティ関係。<br />プライマリ エンティティ レコードを表示すると、関連付けられている関連エンティティ レコードの一覧が表示されます。|
|多対多<br />[ManyToManyRelationshipMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.manytomanyrelationshipmetadata)|1 つのエンティティの多くのレコードを別のエンティティの多くのレコードに関連付けることができるように、特殊な*関係エンティティ* (*インターセクト* エンティティとも呼ばれます) に依存しているエンティティ関係。<br />多対多の関係のいずれかのエンティティのレコードを表示すると、それに関連するもう一方のエンティティのすべてのレコードの一覧が表示されます。|

`EntityMetadata` `ManyToOneRelationships` コレクションには、[OneToManyRelationshipMetadata](/dotnet/api/microsoft.xrm.sdk.metadata.onetomanyrelationshipmetadata) 型が含まれています。 エンティティ間に一対多の関係が存在し、各エンティティを*プライマリ エンティティ*または*関連エンティティ*として参照します。 関連エンティティ (*子エンティティ*とも呼ばれます) には、プライマリ エンティティ (*親エンティティ*とも呼ばれます) のレコードへの参照を格納できる参照属性があります。 多対一の関係は、単に関連エンティティから見た一対多の関係です。

> [!NOTE]
> 関連エンティティは*子エンティティ*とも呼ばれますが、[Child エンティティ](entity-metadata.md#child-entities)と混同しないでください。Child エンティティは、関連エンティティにセキュリティを適用する方法を示します。

詳細情報:
- [Dynamics 365 Customer Engagement カスタマイズ ガイド: エンティティ間の関連付けの作成および編集](/dynamics365/customer-engagement/customize/create-edit-entity-relationships)
- [Dynamics 365 Customer Engagement 開発者ガイド: エンティティ関係メタデータをカスタマイズする](/dynamics365/customer-engagement/developer/customize-entity-relationship-metadata)

## <a name="cascade-configuration"></a>カスケード構成

一対多のエンティティ関係が存在する場合、データの整合性を維持し、ビジネス プロセスが自動化されるように構成できるカスケード動作があります。

詳細情報:

- [Dynamics 365 Customer Engagement カスタマイズ ガイド: 1:N (一対多) または N:1 (多対一) の関連付けを作成する > 関連付け動作](/dynamics365/customer-engagement/customize/create-and-edit-1n-relationships#relationship-behavior)
- [Dynamics 365 Customer Engagement 開発者ガイド: エンティティ関係の動作](/dynamics365/customer-engagement/developer/entity-relationship-behavior)


## <a name="create-a-hierarchy-of-entities"></a>エンティティの階層を作成する

自己参照の一対多関係内では、`IsHierarchical` プロパティを `true` に設定して階層を設定できます。

モデル駆動型アプリでは、階層を表示して操作するエクスペリエンスを実現できます。 

開発者の場合、`Under` および `Not Under` 演算子を使用して、階層に基づいた新しい種類のクエリを使用できます。

詳細情報: [Dynamics 365 Customer Engagement カスタマイズ ガイド: 階層関連データのクエリおよび視覚化](/dynamics365/customer-engagement/customize/query-visualize-hierarchical-data)

### <a name="see-also"></a>関連項目

[Common Data Service for Apps のエンティティ](entities.md)
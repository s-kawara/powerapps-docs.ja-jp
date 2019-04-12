---
title: Common Data Service エンティティ | Microsoft Docs
description: Common Data Service で利用可能なエンティティについて学びます。
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
<!-- 
Was Mike Carter
This topic was not migrated it was written for PowerApps 

Overlap with content in https://docs.microsoft.com/dynamics365/customer-engagement/developer/introduction-entities

-->

# <a name="common-data-service-entities"></a>Common Data Service エンティティ

データのストレージを提供することは Common Data Service で最も重要な機能です。 Common Data Service は、ビジネス アプリケーションで使用されるデータの構造体を提供する基本的な一連のエンティティを含みます。 

[Common Data Service エンティティの参照](reference/about-entity-reference.md) で基本的な一連のエンティティを確認できます。

## <a name="modify-entities"></a>エンティティの修正

異なる方法を使い、エンティティのメタデータを修正できます。

### <a name="use-designers"></a>デザイナーを使用

デザイナーを使用してエンティティのメタデータを編集する方法がいくつかあります。


|デザイナー  |説明  |
|---------|---------|
|powerapps.com|スキーマを修正する最も簡単で一般的なアプローチは、[powerapps.com](https://web.powerapps.com/) サイトを使用して、環境に関連した Common Data Service を編集することです。 ここで申請された変更は、管理されていない Common Data Service における既定のソリューションのコンテキストで実行されます。 <!-- TODO: Add link to topic that describes this -->|
|Common Data Service の既定のソリューション エクスプローラー|Common Data Service の編集時に、[powerapps.com](https://web.powerapps.com/) サイトから利用可能な別のデザイナーがいます。 左下にある**詳細設定**ボタンで、ソリューション エクスプローラーを Common Data Service の既定のソリューションに開きます。 |
|独自のソリューション エクスプローラー |管理されていないソリューションのコンテキストで新しいエンティティ、属性または関連付けを作成すべきソリューションを配布する場合は、独自のソリューションを開発するために使用します。 <br /> 詳細: [ソリューション発行者およびソリューションを作成](introduction-solutions.md#create-a-solution-publisher-and-solution)|
|フォーム エディターから|エンティティのモデル駆動型アプリ フォームを編集する場合、**フィールド エクスプローラー**で**新しいフィールド**ボタンをクリックします。 ルックアップ フィールドを作成する場合、新しいエンティティの関連付けを作成してサポートします。|

### <a name="import-a-solution"></a>ソリューションのインポート

ソリューションには、エンティティ メタデータおよびその他のカスタマイズ コンポーネントが含まれます。 マネージドまたはアンマネージド ソリューションを Common Data Service テナントにインポートすると、これらのエンティティを含んだり、既存のエンティティを含まれる新しいエンティティ メタデータで拡張します。

### <a name="from-a-data-source-using-power-query"></a>データ ソースから Power Query を使用

Power Query を使用して、新しいエンティティを作成しデータを入力できます。 詳細: [Power Query を使用して Common Data Service のエンティティにデータを追加](../../maker/common-data-service/data-platform-cds-newentity-pq.md)

### <a name="use-metadata-services"></a>メタデータ サービスを使用

Common Data Service で公開されている Web サービスには、エンティティ メタデータを作成、読み取り、書き込みおよび削除する機能が含まれています。 データは環境がどのようにカスタマイズされているかについて実行時にコードを通知することが可能なので、これらのサービスがメタデータの読み取り用に最も頻繁に使われます。 詳細: [メタデータ サービス](metadata-services.md)

## <a name="entity-metadata"></a>エンティティ メタデータ

データ モデルは、Common Data Service 内に格納されたメタデータとして定義されます。 スキーマについてのデータは、*エンティティ メタデータ*として知られています。 

- [EntityMetadata クラス](/dotnet/api/microsoft.xrm.sdk.metadata.entitymetadata) は、組織サービスを定義します。 
- [EntityMetadata EntityType](/dynamics365/customer-engagement/web-api/entitymetadata) は、Web API 用に定義します。 

エンティティ メタデータについて、次の情報を確認してください:


|データ  |説明  |
|---------|---------|
|エンティティ プロパティ|各エンティティには、どのように識別され、何ができるかを表示した 100 近くのプロパティがあります。  詳細: [エンティティ メタデータ](entity-metadata.md)|
|属性|エンティティ `Attributes` プロパティは、属性のコレクションです。 各属性には、どのように識別されたか、データの種類、どのように書式設定されたか、および何ができるかを表示した 50 近くのプロパティがあります。 詳細: [属性メタデータ](entity-attribute-metadata.md)|
|関係|3 つのエンティティ プロパティは、エンティティ間の関係付けコレクションです。 異なるタイプの関連付けをもつコレクション: 多対多、多対一、および一対多があります。 詳細: [エンティティの関連付けメタデータ](entity-relationship-metadata.md)|
|特権|エンティティ プロパティの 1 つに 0 と 8 の特権間のコレクションがあります。これらの特権は、それぞれに関連付けされた一意の識別子を使い、エンティティを実行できるデータ オペレーションの種類を識別します。 オペレーションには、*追加*、*AppendTo*、*割り当て*、*作成*、*削除*、*読み取り*、*共有*、および*書き込み*があります。|
|キー|既定では各エンティティは単一の GUID (globally unique identifier) 属性を所有し、`Keys` プロパティは空のコレクションです。 エンティティに代替キーを追加できます。 詳細: [エンティティ キー](entity-metadata.md#entity-keys)|

> [!TIP]
> システム内のエンティティ メタデータを理解することで、Common Data Service の動作を理解できます。 多くのプロパティはまた、モデル駆動型アプリのエンティティが出来ることコントロールします。 メタデータを編集できるデザイナーは、メタデータにあるすべての詳細を表示できません。 システムにあるメタデータ プロパティとすべての非表示エンティティを表示できるように、Metadata Browser というモデル駆動型のアプリをインストールできます。 詳細: [組織のメタデータをブラウザ](/dynamics365/customer-engagement/developer/browse-your-metadata)

### <a name="see-also"></a>関連項目

[Common Data Service 開発者向けの概要](overview.md)



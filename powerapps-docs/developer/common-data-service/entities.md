---
title: Common Data Service for Apps のエンティティ | Microsoft Docs
description: Common Data Service for Apps で使用できるエンティティについて説明します。
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
ms.date: 03/19/2018
ms.author: jdaly
ms.openlocfilehash: 98f2360e29af7cb0bdf5caf041dfa13b933e6323
ms.sourcegitcommit: 59785e9e82da8f5bd459dcb5da3d5c18064b0899
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2018
---
# <a name="common-data-service-for-apps-entities"></a>Common Data Service for Apps のエンティティ

データのストレージの提供は、Common Data Service for Apps の最も重要な機能です。 Common Data Service には、ビジネス アプリケーションで使用されるデータの構造を提供するエンティティの基本セットが含まれます。 

エンティティの基本セットについては、[Common Data Service for Apps のエンティティ リファレンス](reference/about-entity-reference.md)に関するページを参照してください。

## <a name="modify-entities"></a>エンティティを変更する

エンティティ メタデータを変更するには、複数の方法があります。

### <a name="use-designers"></a>デザイナーを使用する

デザイナーを使用してエンティティ メタデータを編集する方法はいくつかあります。


|デザイナー  |説明  |
|---------|---------|
|powerapps.com|スキーマを変更する最も簡単で最も一般的な方法は、[powerapps.com](https://web.powerapps.com/) サイトを使用して、環境に関連付けられた Common Data Service を編集することです。 この方法で適用される変更は、アンマネージド Common Data Service Default ソリューションのコンテキストで実行されます。 <!-- TODO: Add link to topic that describes this -->|
|Common Data Service Default ソリューション エクスプローラー|Common Data Service を編集する場合、[powerapps.com](https://web.powerapps.com/) サイトから別のデザイナーを使用できます。 左下にある **[詳細]** ボタンを選択すると、ソリューション エクスプローラーに Common Data Service Default ソリューションが表示されます。 |
|ソリューションのソリューション エクスプローラー |ソリューションを配布する場合は、アンマネージド ソリューションのコンテキストで、ソリューションの開発に使用する新しいエンティティ、属性、または関係を作成する必要があります。 <br /> 詳細情報: [ソリューション発行元とソリューションを作成する](introduction-solutions.md#create-a-solution-publisher-and-solution)|
|フォーム エディターから|エンティティのモデル駆動アプリ フォームを編集する場合は、**フィールド エクスプローラー**で **[新しいフィールド]** ボタンをクリックします。 参照フィールドを作成する場合は、それをサポートする新しいエンティティ関係を作成します。|

### <a name="import-a-solution"></a>ソリューションをインポートする

ソリューションには、エンティティ メタデータとその他のカスタマイズされたコンポーネントを含めることができます。 マネージドまたはアンマネージド ソリューションを Common Data Service テナントにインポートすると、それらのエンティティが含まれるか、既存のエンティティが拡張され、新しいエンティティ メタデータが含まれます。

### <a name="from-a-data-source-using-power-query"></a>Power Query を使用するデータ ソースから

Power Query を使用して、新しいエンティティを作成し、エンティティにデータを入力することができます。 詳細情報: [Power Query を使用して Common Data Service のエンティティにデータを追加する](../../maker/common-data-service/data-platform-cds-newentity-pq.md)

### <a name="use-metadata-services"></a>メタデータ サービスを使用する

Common Data Service で公開されている Web サービスには、エンティティ メタデータの作成、読み取り、書き込み、および削除の機能が含まれています。 これらのサービスが最もよく使用されるのは、メタデータの読み取りです。これは、実行時に環境のカスタマイズ方法をメタデータでコードに通知できるためです。

詳細情報: [メタデータ サービス](use-web-services.md#metadata-services)

## <a name="entity-metadata"></a>エンティティ メタデータ

このデータ モデルは、Common Data Service 内に格納されるメタデータと定義されています。 このスキーマに関するデータは、*エンティティ メタデータ*と呼ばれます。 

- [EntityMetadata クラス](/dotnet/api/microsoft.xrm.sdk.metadata.entitymetadata)では、Organization サービスを使用してこれを定義します。 
- [EntityMetadata EntityType](/dynamics365/customer-engagement/web-api/entitymetadata) では、Web API 用にこれを定義します。 

エンティティ メタデータには、次の情報が含まれています。


|データ  |説明  |
|---------|---------|
|エンティティ プロパティ|各エンティティには、識別方法と実行できる処理を記述する約 100 個のプロパティがあります。  詳細情報: [エンティティ メタデータ](entity-metadata.md)|
|属性|エンティティ `Attributes` プロパティは複数の属性のコレクションです。 各属性には、識別方法、含まれるデータの種類、書式設定方法、および実行できる処理を記述する約 50 個のプロパティがあります。 詳細情報: [属性メタデータ](entity-attribute-metadata.md)|
|関係|3 つのエンティティ プロパティは、エンティティ間の関係のコレクションです。 これらのコレクションには、多対多、多対一、および一対多という異なる種類の関係が含まれています。 詳細情報: [エンティティ関係メタデータ](entity-relationship-metadata.md)|
|特権|1 つのエンティティ プロパティは、0 個から 8 個の特権のコレクションです。この特権で、一意の識別子が関連付けられたエンティティに対して実行できるデータ操作の種類を指定します。 たとえば、*Append*、*AppendTo*、*Assign*、*Create*、*Delete*、*Read*、*Share*、*Write* の操作があります。|
|キー|既定で、各エンティティには 1 つの GUID (グローバルに一意の識別子) 属性があり、`Keys` プロパティは空のコレクションです。 エンティティには代替キーを追加できます。 詳細情報: [エンティティ キー](entity-metadata.md#entity-keys)|

> [!TIP]
> システム内のエンティティ メタデータについて理解を深めると、Common Data Service の仕組みを理解するために役立ちます。 プロパティの多くは、モデル駆動型アプリで実行できるエンティティも制御します。 メタデータを編集できるデザイナーでは、メタデータ内のすべての詳細情報を表示することはできません。 メタデータ ブラウザーと呼ばれるモデル駆動型アプリをインストールすると、システム内にあるすべての非表示エンティティとメタデータ プロパティを表示できます。 詳細情報: [Dynamics 365 Customer Engagement 開発者ドキュメント: 組織のメタデータの参照](/dynamics365/customer-engagement/developer/browse-your-metadata)

### <a name="see-also"></a>関連項目

[Common Data Service for Apps Developer の概要](overview.md)



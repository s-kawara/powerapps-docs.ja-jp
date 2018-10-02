---
title: 'PowerApps の概要で 1:N (1 対多) または N:1 (多対 1) のエンティティの関連付けを作成する | MicrosoftDocs'
description: 1 対多または多対 1 のエンティティの関連付けを作成する方法を学習する
ms.custom: ''
ms.date: 05/27/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - powerapps
author: Mattp123
ms.assetid: 52c00707-b2bc-4950-abec-89baefd94f6e
caps.latest.revision: 33
ms.author: matp
manager: kvivek
tags: null
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="create-one-to-many-or-many-to-one-entity-relationships-overview"></a>1 対多または多対 1 のエンティティの関連付けの概要を作成する

アプリ用 Common Data Service において、1:N (1 対多) または N:1 (多対 1) の関連付けは、2 種類のエンティティがどのように関連しているかを定義します。 
  
ユーザー定義エンティティの関連付けを作成する場合は、その前に、既存のエンティティの関連付けの使用が要件を満たしているかどうかを確認します。 <br />詳細: [新しいメタデータを作成するか既存のメタデータを使用するか](create-edit-metadata.md#create-new-metadata-or-use-existing-metadata)

1: N (1 対多) または N: 1 (多対 1) の関連付けを作成し編集するために使用できる 2 つのデザイナーがあります。

|デザイナー| 説明|
|--|--|
|[PowerApps ポータル](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)|簡単な優れたエクスペリエンスを提供しますが、一部の特殊な設定は使用できません。<br />詳細: [PowerApps ポータルで 1:N (1 対多) または N:1 (多対 1) のエンティティ関連付けを作成および編集する](create-edit-1n-relationships-portal.md)|
|ソリューション エクスプローラー|簡単ではありませんが、一般的な要件が少ない割に柔軟性が高くなっています。 <br />詳細: [ソリューション エクスプローラーを使用して 1:N (1 対多) または N:1 (多対 1) のエンティティ関連付けを作成および編集する](create-edit-1n-relationships-solution-explorer.md) |

> [!NOTE]
> また、以下を使用して、環境内に新しいエンティティの関連付けを作成することもできます:
> - モデル駆動型アプリでは、フォーム エディターから**新しいフィールド**を選択し、 *検索*フィールドを作成します。 <br />詳細: [フォームにフィールドを追加する](../model-driven-apps/add-field-form.md)
> - 関連エンティティの新しい検索フィールドを作成します。 <br />詳細: [フィールドの作成と編集](create-edit-fields.md)
> - エンティティ関連付けの定義を含むソリューションをインポートします。 <br />詳細: [ソリューションのインポート、更新およびエクスポート](import-update-export-solutions.md)
> - Power Query を使用して、新しいエンティティを作成しデータを入力します。 <br />詳細: [Power Query を使用してアプリ用 Common Data Service のエンティティにデータを追加する](data-platform-cds-newentity-pq.md).
> - 開発者は [Web サービス](../../developer/common-data-service/use-web-services.md#metadata-services)を使用して、エンティティの関連付けの作成および更新のためのプログラムを作成することができます。 <br />詳細: [エンティティ関係メタデータをカスタマイズする](https://docs.microsoft.com/dynamics365/customer-engagement/developer/customize-entity-relationship-metadata)

このトピックの情報は、使用できるデザイナーの選択に役立ちます。 

次のいずれかの要件に対処する必要がない限り、1:N (1 対多) または N:1 (多対 1) のエンティティの関連付けの作成および編集に PowerApps ポータルを使用する必要があります:

- フィールド マッピングを構成する
- モデル駆動型アプリのナビゲーション ウィンドウのオプションを構成する
- 関連付けの動作を構成する
- 関連付けが高度な検索で非表示になるかを定義します。
- 階層的な関連付けを作成する


## <a name="community-tools"></a>コミュニティ ツール

**[エンティティの関連付けの図の作成者](https://www.xrmtoolbox.com/plugins/JourneyIntoCRM.XrmToolbox.ERDPlugin/)** は、XrmToolbox コミュニティがアプリケーションの CDS 用に開発したツールです。 コミュニティが開発したツールについては、[アプリ用 Common Data Service の開発者ツール](https://docs.microsoft.com/dynamics365/customer-engagement/developer/developer-tools)を参照してください。

> [!NOTE]
> コミュニティ ツールは Microsoft の製品ではなく、コミュニティ ツールに対するサポートは提供されません。 このツールに関するご質問は、その発行元にお問い合わせください。 詳細: [XrmToolBox](https://www.xrmtoolbox.com)。

### <a name="see-also"></a>関連項目

[エンティティ間の関連付けの作成および編集](create-edit-entity-relationships.md)<br />
[PowerApps ポータルを使用して 1:N (1 対多) または N:1 (多対 1) のエンティティ関連付けを作成および編集する](create-edit-1n-relationships-portal.md)<br />
[ソリューション エクスプローラーを使用して 1:N (1 対多) または N:1 (多対 1) のエンティティ関連付けを作成および編集する](create-edit-1n-relationships-solution-explorer.md)<br />
[開発者ドキュメント: エンティティの関連付けメタデータをカスタマイズする](/dynamics365/customer-engagement/developer/customize-entity-relationship-metadata)<br />
[開発者ドキュメント: エンティティの関連付けの有効性](/dynamics365/customer-engagement/developer/entity-relationship-eligibility)



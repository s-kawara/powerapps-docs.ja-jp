---
title: アプリ用 Common Data Service の概要で多対多のエンティティの関連付けを作成する | MicrosoftDocs
description: 多対多のエンティティの関連付けを作成する方法に関する説明
ms.custom: ''
ms.date: 05/29/2018
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
ms.assetid: 248cecfd-c9e8-430b-b4b0-860669866084
caps.latest.revision: 33
ms.author: matp
manager: kvivek
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="create-many-to-many-entity-relationships-overview"></a>多対多のエンティティの関連付けの作成の概要

一対多 (1:N) のエンティティの関連付けはレコード間の階層を確立します。 多対多 (N:N) の関連付けでは、明示的階層がありません。 構成する検索フィールドまたは動作はありません。 多対多の関連付けを使用して作成されたレコードは同等であると考えられ、この関係は相互的なものです。  
  
多対多の関係では、関係 (または交差する) エンティティは、エンティティを関連付けるデータを格納します。 このエンティティには、関連エンティティの両方で一対多のエンティティの関連付けがあり、関連付けの定義に必要となる値のみを格納します。 関連付けのエンティティにユーザー定義フィールドを追加することはできず、ユーザー インターフェイスにも表示されません。 
  
多対多の関連付けを作成するには、関連付けに参加する 2 種類のエンティティを選択する必要があります。 モデル駆動型アプリでは、各エンティティのナビゲーション内で対応するリストを使用する方法を決めることができます。 これらは、1:N の関連付けの主エンティティで使用されるのと同じオプションです。 詳細: [主エンティティのナビゲーション ウィンドウ項目](create-edit-1n-relationships-solution-explorer.md#navigation-pane-item-for-primary-entity)
  
すべてのエンティティが、多対多の関連付けで使用できるわけではありません。 エンティティをデザイナーで選択できない場合、このエンティティで新しい多対多の関連付けを作成することはできません。 詳細: [開発者ドキュメント: エンティティの関連付けの有効性](https://docs.microsoft.com/dynamics365/customer-engagement/developer/entity-relationship-eligibility)

1: N (1 対多) または N: 1 (多対 1) の関連付けを作成し編集するために使用できる 2 つのデザイナーがあります。

|デザイナー| 説明|
|--|--|
|[PowerApps ポータル](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)|簡単な優れたエクスペリエンスを提供しますが、一部の特殊な設定は使用できません。<br />詳細: [PowerApps ポータルを使用してアプリ用 Common Data Service で多対多のエンティティの関連付けを作成する](create-edit-nn-relationships-portal.md)|
|ソリューション エクスプローラー|簡単ではありませんが、一般的な要件が少ない割に柔軟性が高くなっています。<br />詳細: [ソリューション エクスプローラーを使用してアプリ用 Common Data Service で N:N (多対多) のエンティティの関連付けを作成する](create-edit-nn-relationships-solution-explorer.md) |

> [!NOTE]
> また、以下を使用して、環境内に新しい多対多 (N：N) のエンティティの関連付けを作成することもできます:
> - 関連付けの定義を含むソリューションをインポートします。 詳細: [ソリューションのインポート、更新およびエクスポート](import-update-export-solutions.md)
> - 開発者は[メタデータ サービス](../../developer/common-data-service/use-web-services.md#metadata-services)を使用して、エンティティの関連付けの作成および更新のためのプログラムを作成することができます。 詳細: [開発者ドキュメント: エンティティの関連付けメタデータをカスタマイズする](https://docs.microsoft.com/dynamics365/customer-engagement/developer/customize-entity-relationship-metadata)

このトピックの情報は、使用できるデザイナーの選択に役立ちます。 

次のいずれかの要件に対処する必要がない限り、多対多 (N:N) のエンティティの関連付けの作成および編集に PowerApps ポータルを使用する必要があります:

- モデル駆動型アプリのナビゲーション ウィンドウのオプションを構成します。
- モデル駆動型アプリの高度な検索から関連付けを非表示にします。

## <a name="see-also"></a>関連項目

[エンティティ間の関連付けの作成および編集](create-edit-entity-relationships.md)<br />
[PowerApps ポータルを使用してアプリ用 Common Data Service で多対多のエンティティの関連付けを作成する](create-edit-nn-relationships-portal.md)<br />
[ソリューション エクスプローラーを使用してアプリ用 Common Data Service で N:N (多対多) のエンティティの関連付けを作成する](create-edit-nn-relationships-solution-explorer.md)<br />
[開発者ドキュメント: エンティティの関連付けメタデータをカスタマイズする](https://docs.microsoft.com/dynamics365/customer-engagement/developer/customize-entity-relationship-metadata)<br />
[開発者ドキュメント: エンティティの関連付けの有効性](https://docs.microsoft.com/dynamics365/customer-engagement/developer/entity-relationship-eligibility)

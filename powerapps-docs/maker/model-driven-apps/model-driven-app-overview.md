---
title: PowerApps でのモデル駆動型アプリの構築の概要 | Microsoft Docs
description: PowerApps アプリで使うエンティティを作成して構成する手順について説明します。
services: ''
suite: powerapps
documentationcenter: na
author: Mattp123
manager: bycho
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2018
ms.author: matp
ms.openlocfilehash: 872e06e3d260480f09f66c52b592540bae44bdda
ms.sourcegitcommit: d7ed5144f96d1ecc17084c30ed0e2ba3c6b03c26
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/19/2018
---
# <a name="overview-of-building-a-model-driven-app"></a>モデル駆動型アプリの構築の概要

モデル駆動型アプリの設計は、コンポーネントに焦点を当てたアプリ開発の手法です。 モデル駆動型アプリの設計ではコードを必要とせず、作成したアプリを単純にも、非常に複雑にもできます。  設計者がアプリのレイアウトを完全に制御するキャンバス アプリの開発とは異なり、モデル駆動型アプリでは、レイアウトの多くは、設計者がアプリに追加するコンポーネントによって自動的に決定され、大部分が指定されます。 

![モデル駆動型アプリのサンプル](media/model-driven-app-overview/model-app-sample.png)

> [!IMPORTANT]
> [!INCLUDE [cc-preview-features-definition](../../includes/cc-preview-features-definition.md)]

モデル駆動型アプリの設計には、次のような利点があります。
- コンポーネントに焦点が当てられた、コードを使わない、充実した設計環境 
- デスクトップからモバイルまでのさまざまなデバイスで同じ UI を使う複雑で応答性の高いアプリの作成
- Dynamics 365 顧客エンゲージメント プラットフォームで使用可能なものと似た機能の設計 
- ソリューションとして配布できるアプリ
 
## <a name="the-approach-to-model-driven-app-making"></a>モデル駆動型アプリの作成方法
基本的なレベルでは、モデル駆動型アプリの作成は 3 つの主要な重点領域で構成されます。

- ビジネス データのモデル化 
- ビジネス プロセスの定義 
- アプリの作成

### <a name="modeling-business-data"></a>ビジネス データのモデル化
ビジネス データをモデル化するには、アプリに必要なデータ、およびそのデータと他のデータの関連性を決定します。 モデル駆動型設計では、設計者がコードを記述しなくてもアプリケーションをカスタマイズできるように、メタデータ駆動型のアーキテクチャが使われます。 メタデータとは "データに関するデータ" のことであり、システムに格納されるデータの構造を定義しています。 [チュートリアル: PowerApps でコンポーネントがあるカスタム エンティティを作成する](../common-data-service/create-custom-entity.md)

### <a name="defining-business-processes"></a>ビジネス プロセスの定義
一貫性のあるビジネス プロセスを定義して適用することは、モデル駆動型アプリの設計の重要な側面です。 プロセスに一貫性があれば、アプリのユーザーは、一連の手動手順を忘れずに実行することではなく、自分の仕事に集中できます。 プロセスは単純なことも複雑なこともあり、多くの場合は時間の経過と共に変化します。 プロセスを作成するには、**[詳細]** を選んで[ソリューション エクスプローラー](#advanced-model-driven-app-making)を開きます。 次に、ソリューション エクスプローラーの左側のナビゲーション ウィンドウで **[プロセス]** を選んでから、**[新規]** を選びます。 詳しくは、「[ビジネス ロジックの使用](#working-with-business-logic)」をご覧ください。  

### <a name="composing-the-model-driven-app"></a>モデル駆動型アプリの作成
データをモデル化してプロセスを定義した後は、アプリ デザイナーを使って、必要なコンポーネントを選んで構成することによりアプリを構築します。

![アプリ デザイナー](media/model-driven-app-overview/app-designer.png)

## <a name="model-driven-app-components-and-designers"></a>モデル駆動型アプリのコンポーネントとデザイナー
適切に設計されたモデル駆動型アプリは、最終的なアプリの外観と機能を構築するためにデザイナーが選ぶ複数のコンポーネントで構成されます。 アプリを構成するためにデザイナーが使うコンポーネントとコンポーネントのプロパティが、メタデータになります。 これらの各コンポーネントとアプリの設計の関係を理解するため、ここではコンポーネントを "*データ*"、"*UI*"、"*ロジック*"、"*視覚化*" の各カテゴリに分けてあります。 

### <a name="data"></a>データ
これらのコンポーネントは、アプリの基になるデータを決定します。


|コンポーネント  |説明  |デザイナー  |
|---------|---------|---------|
|組織     |追跡するプロパティを持つ項目。連絡先、アカウントなど。 多くの標準エンティティを利用できます。 非システム標準エンティティ (運用エンティティ) をカスタマイズしたり、一からカスタム エンティティを作成したりできます。     | [!INCLUDE [powerapps](../../includes/powerapps.md)] エンティティ デザイナー        |
|フィールド     | エンティティに関連付けられているプロパティ。 フィールドはデータ型によって定義され、それにより入力または選択できるデータの種類が決まります。 例としては、テキスト、数値、日付と時刻、通貨、検索 (他のエンティティとのリレーションシップを作成します) などがあります。 通常、フィールドはフォーム、ビュー、検索で使われます。        | [!INCLUDE [powerapps](../../includes/powerapps.md)] エンティティ デザイナー   |
|リレーションシップ     | エンティティのリレーションシップは、エンティティが相互に関係できる方法を定義します。 リレーションシップの種類には、1:N (一対多)、N:1 (多対一)、N:N (多対多) があります。 たとえば、エンティティにルックアップ フィールドを追加すると、2 つのエンティティの間に新しい 1:N リレーションシップが作成され、そのルックアップ フィールドをフォームに配置できます。   | [!INCLUDE [powerapps](../../includes/powerapps.md)] エンティティ デザイナー        |
|オプション セット フィールド     | これは特別な種類のフィールドであり、事前に決定されているオプションのセットをユーザーに提供します。 各オプションには、番号の値とラベルがあります。 このフィールドをフォームに追加すると、ユーザー オプションを選択するためのコントロールが表示されます。  オプション セットには 2 つの種類があります。オプション セットでは、ユーザーが選択できるオプションは 1 つだけです。複数選択オプション セットでは、ユーザーは複数のオプションを選択できます。  | [!INCLUDE [powerapps](../../includes/powerapps.md)] オプション セット デザイナー     |

### <a name="ui"></a>UI
これらのコンポーネントは、ユーザーがアプリと対話する方法を決定します。 

|コンポーネント  |説明  |デザイナー  |
|---------|---------|---------|
|アプリ     | アプリのコンポーネント、プロパティ、クライアントの種類、URL など、アプリケーションの基礎を決定します。      | アプリ デザイナー   |
|サイト マップ     | アプリのナビゲーションを指定します。        | サイト マップ デザイナー        |
|フォーム     | エンティティについて組織が追跡する項目に一致する、特定のエンティティのデータ入力フィールドのセットです。 たとえば、顧客の以前の注文および要求された特定の再注文日を追跡するためのユーザーの入力関連情報が含まれるデータ入力フィールドのセットなどです。        | フォーム デザイナー        |
|表示     | ビューは、特定のエンティティのレコードの一覧がアプリケーションに表示される方法を定義します。 ビューでは、表示する列、各列の幅、並べ替えの動作、既定のフィルターが定義されています。   |  ビュー デザイナー       |

![アプリ デザイナーとフォーム デザイナー](media/model-driven-app-overview/app-and-form-designers.png)

### <a name="logic"></a>ロジック
アプリが備えるビジネス プロセス、ルール、およびオートメーションを決定します。 [!INCLUDE [powerapps](../../includes/powerapps.md)] メーカーは、プロセスまたはルールの種類に固有のデザイナーを使います。 


|ロジックの種類  |説明  |デザイナー  |
|---------|---------|---------|
|ビジネス プロセス フロー     | 標準的なビジネス プロセスに沿ってユーザーを誘導するオンライン プロセスです。 たとえば、すべてのユーザーにカスタマー サービス要求を同じように処理させたい場合や、スタッフが注文を送信する前に請求書の承認を得なければならない場合などは、ビジネス プロセス フローを使います。        | ビジネス プロセス フロー デザイナー        |
|ワークフロー     |  ユーザー インターフェイスなしでビジネス プロセスを自動化するワークフローです。 デザイナーは、ユーザーの介入を必要としないオートメーションを開始するためにワークフローを使います。       | ワークフロー デザイナー        |
|アクション    |  アクションは、カスタム動作などの操作をワークフローから直接手動で呼び出すことができるプロセスの種類です。       |  プロセス デザイナー       |
|ビジネス ルール     | フィールドの要件の設定、フィールドの非表示、データの検証など、ルールや推奨ロジックをフォームに適用するために使われます。 アプリ デザイナーは、シンプルなインターフェイスを使って、頻繁に変更され、よく使用されるルールを実装および維持します。         |  ビジネス ルール デザイナー       |
|フロー     | フローはクラウド ベースのサービスであり、アプリとサービスの間に、通知の取得、ファイルの同期、データの収集などを自動化するワークフローを作成できます。        | Microsoft Flow        |

![ワークフロー デザイナー、アクション デザイナー、ビジネス プロセス フロー デザイナー](media/model-driven-app-overview/designer-mash.png)

### <a name="visualizations"></a>視覚化
アプリが使用できるデータの視覚化とレポートの種類を決定します。


|コンポーネント  |説明  |デザイナー  |
|---------|---------|---------|
|グラフ     | ビュー内やフォーム上に表示したりダッシュボードに追加したりできる単一のグラフィックな視覚エフェクトです。        | グラフ デザイナー        |
|ダッシュボード     | アクションにつながるビジネス データの概要を提供する 1 つ以上のグラフィックな視覚化のためのプレートとして機能します。        | ダッシュボード デザイナー        |
|埋め込み Power BI     | 埋め込み Power BI タイルとダッシュボードをアプリに追加します。 Power BI はクラウド ベースのサービスであり、ビジネス インテリジェンスの分析情報を提供します。        |  グラフ デザイナー、ダッシュボード デザイナー、Power BI の組み合わせ       |

![ダッシュボードのサンプル](media/model-driven-app-overview/dashboard-designer.png)

### <a name="advanced-model-driven-app-making"></a>高度なモデル駆動型アプリの作成
ソリューション エクスプローラーは、高度なモデル駆動型アプリの構築に使われる包括的なツールです。 ソリューション エクスプローラー内では、ツールの左側にあるナビゲーション ウィンドウを使って、アプリのすべてのコンポーネントで構成される階層内を移動できます。

![ソリューション エクスプローラー](media/model-driven-app-overview/solutionexplorer-entitiescollapsed.png)

ソリューション エクスプローラーを開くには、[!INCLUDE [powerapps](../../includes/powerapps.md)] の左側のウィンドウで **[モデル駆動]** を選びます。

  ![[モデル駆動] を選ぶ](media/model-driven-app-overview/app-type-picker-mod.png)

次に、**[詳細]** タブを選びます。 

## <a name="model-driven-app-development-resources"></a>モデル駆動型アプリ開発のリソース
モデル駆動型アプリの開発について詳しくは、以下のトピックをご覧ください。
### <a name="modeling-your-data"></a>データのモデリング
- [アプリ デザイナーを使用して、カスタム ビジネス アプリを設計](https://docs.microsoft.com/dynamics365/customer-engagement/customize/design-custom-business-apps-using-app-designer)
- [フォームの作成および設計](https://docs.microsoft.com/dynamics365/customer-engagement/customize/create-design-forms)
- [ビューの作成または編集](https://docs.microsoft.com/dynamics365/customer-engagement/customize/create-edit-views)  

### <a name="modeling-and-composing-your-app"></a>アプリのモデル化と作成
- [エンティティの作成または編集](https://docs.microsoft.com/dynamics365/customer-engagement/customize/create-edit-entities)
- [リレーションシップの作成と編集](https://docs.microsoft.com/dynamics365/customer-engagement/customize/create-edit-entity-relationships) 
- [フィールドの作成と編集](https://docs.microsoft.com/dynamics365/customer-engagement/customize/create-edit-fields)
- [グローバル オプション セットの作成および編集](https://docs.microsoft.com/dynamics365/customer-engagement/customize/create-edit-global-option-sets)

### <a name="working-with-business-logic"></a>ビジネス ロジックの使用
- [ビジネス プロセス フローの概要](https://docs.microsoft.com/dynamics365/customer-engagement/customize/business-process-flows-overview)
- [ワークフロー プロセスを使用してプロセスを自動化する](https://docs.microsoft.com/dynamics365/customer-engagement/customize/workflow-processes)
- [操作の概要](https://docs.microsoft.com/dynamics365/customer-engagement/customize/actions)
- [ロジックを適用するための業務ルールおよびレコメンデーションを作成する](https://docs.microsoft.com/dynamics365/customer-engagement/customize/create-business-rules-recommendations-apply-logic-form)

### <a name="using-visualizations-in-your-app"></a>アプリでの視覚化の使用
- [システム グラフの作成または編集](https://docs.microsoft.com/dynamics365/customer-engagement/customize/create-edit-system-chart)
- [ダッシュボードの表示または編集](https://docs.microsoft.com/dynamics365/customer-engagement/customize/create-edit-dashboards)


### <a name="distributing-your-app"></a>アプリの配布。
[ソリューションを作成する](https://docs.microsoft.com/dynamics365/customer-engagement/customize/create-solution)

## <a name="next-steps"></a>次の手順
[クイック スタート: カスタム エンティティを作成する](../common-data-service/data-platform-create-entity.md)

[チュートリアル: PowerApps でコンポーネントがあるカスタム エンティティを作成する](../common-data-service/create-custom-entity.md)


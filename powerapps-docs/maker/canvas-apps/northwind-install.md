---
title: Northwind Traders データベースとアプリのインストール |Microsoft Docs
description: リレーショナルの概念を検証するための環境には、Northwind データベースとアプリをインストールします。
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 06/06/2019
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 351f9fd4fe369b3073a9edfb0158883140f50693
ms.sourcegitcommit: e85072f7a80da308c4caabe20adbf2509588ca57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66761030"
---
# <a name="install-northwind-traders-database-and-apps"></a>Northwind Traders データベースとアプリをインストールします。

次の手順に従って、[この一連のトピック](northwind-orders-canvas-part1.md)、Common Data Service のサンプル データベースに実装されているリレーショナル データに関する概念を見つけることができます。 サンプルのビジネス アプリを検索することも、キャンバスの両方と、そのデータを管理するためのモデル駆動し、このようなアプリを作成して実際の経験を獲得できます。 この最初のトピックでは、独自の環境で、Northwind Traders データベースをインストールしてビルドされた方法を表示する編集用に開くことができるサンプル アプリにアクセスする方法について説明します。

Northwind Traders は、注文、製品、顧客、サプライヤー、およびその他の多数の小規模ビジネスを管理する架空の組織です。 このサンプルでは、最初のバージョンの Microsoft Access で登場しは Access のテンプレートとして使用できます。

## <a name="prerequisites"></a>前提条件

- PowerApps のライセンスで、Common Data Service をサポートしています。 できます[無料試用版ライセンスを使用して、](../signup-for-powerapps.md) 30 日間です。
- Common Data Service データベースがある環境。 できます[このような環境を作成](https://docs.microsoft.com/power-platform/admin/create-environment)適切なアクセス許可がある場合。

## <a name="download-the-solution"></a>ソリューションをダウンロードします。

> [!div class="nextstepaction"]
> [Northwind Traders のソリューション ファイルをダウンロードします。](https://pwrappssamples.blob.core.windows.net/samples/NorthwindTraders_1_0_0_6.zip)

これは、[ソリューション](../../developer/common-data-service/introduction-solutions.md)ファイル (.zip) には、エンティティ、オプションのセット、およびビジネス プロセスの定義はキャンバスとモデル駆動型アプリと同時に使用されるその他の任意の部分が含まれています。

## <a name="install-the-solution"></a>ソリューションをインストールします。

1. サインインする[PowerApps](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)、Common Data Service データベースを含む環境で作業することを確認します。

1. 左側のナビゲーション ウィンドウで選択**ソリューション**、し、**インポート**画面の上部にあるツールバーで。

    > [!div class="mx-imgBorder"]
    > ![ソリューションのビューとインポート ソリューションのエントリ ポイント](media/northwind-install/solution-import.png)

1. **ソリューション パッケージの選択**] ページで [**参照**します。

    > [!div class="mx-imgBorder"]
    > ![パッケージを選択する前にソリューション パッケージ ページの選択](media/northwind-install/select-solution2.png)

1. ファイルをダウンロードし、**オープン**します。

    別の場所を選択していない限り、ファイルがダウンロード フォルダーになります。

1. (バージョン番号が異なる場合があります)、適切なファイルがある場合は、選択**次**:

    > [!div class="mx-imgBorder"]
    > ![パッケージを選択した後、ソリューション パッケージ ページを選択します](media/northwind-install/confirm-solution2.png)

1. **ソリューション情報**] ページで、[**次**ソリューションとパブリッシャーの名前が正しい場合。

    > [!div class="mx-imgBorder"]
    > ![ソリューションの情報 ページ](media/northwind-install/confirm-publisher.png)

1. **インポート オプション**] ページで、[**インポート**サンプルが必要です。 SDK メッセージの処理を確認します。

    > [!div class="mx-imgBorder"]
    > ![インポート オプション ページ](media/northwind-install/confirm-sdk.png)

    別のページが表示され、数分以内に、ソリューションがインストールされている進行状況を表示します。

    > [!div class="mx-imgBorder"]
    > ![進行状況バー](media/northwind-install/solution-progress.png)

    インストールが完了したら、元のページには、結果が表示されます。

    > [!div class="mx-imgBorder"]
    > ![ソリューションのインポート ページ](media/northwind-install/solution-success.png)

1. **[閉じる]** を選びます。

## <a name="load-the-sample-data"></a>サンプル データを読み込む

1. 選択**アプリ**、し、 **Northwind サンプル データ**します。

    Northwind アプリは、ソリューションをインストールした直後後に表示されない場合は、数分間待ってください。

    > [!div class="mx-imgBorder"]
    > ![アプリの一覧で Northwind データベース](media/northwind-install/sample-data-app.png)

1. アプリが Common Data Service と対話するためのアクセス許可を求めるときに選択**許可**:

    > [!div class="mx-imgBorder"]
    > ![Common Data Service の同意 ダイアログ ボックス](media/northwind-install/sample-data-permission.png)

1. アプリが読み込まれ、sample エンティティにレコードが含まれていないことを表示、選択**データの読み込み**エンティティを設定します。

    > [!div class="mx-imgBorder"]
    > ![ボタン サンプル データ マネージャーでのデータを読み込む](media/northwind-install/sample-data-load.png)

    アプリにデータが読み込まれると、アプリの上端とレコードの数の間でドット年 3 月です。

    レコード間の関係を確立できるように、エンティティが特定の順序で読み込まれます。 たとえば、 **Order Details**エンティティと多対一リレーションシップを持つ、**注文**と**製品を注文**エンティティは、最初に読み込まれます。

    プロセスを選択して、いつでもキャンセルできます**キャンセル**を選択して、いつでもデータを削除することができますと**データ削除**:

    > [!div class="mx-imgBorder"]
    > ![データが読み込まれると、データ マネージャーをサンプルします。](media/northwind-install/sample-data-progress.png)

    データの読み込み中に、最後の行が終了したとき (**多対多リレーションシップ**) を示しています**完了**、および**データの読み込み**と**データ削除**ボタンをもう一度有効にします。

    > [!div class="mx-imgBorder"]
    > ![データが読み込まれた後に、サンプル データ マネージャー](media/northwind-install/sample-data-complete.png)

## <a name="sample-apps"></a>サンプル アプリ

Northwind のソリューションには、このデータを操作するため、これらのアプリが含まれています。

- Northwind の Orders (キャンバス)
- Northwind の Orders (モデル駆動型)

前の手順でアプリを開いていることと同じ方法で、これらのアプリを開きます。

### <a name="canvas"></a>キャンバス

この 1 画面アプリの単純なマスター/詳細ビューを提供する、**注文**エンティティを表示および注文と注文の各行アイテムの概要を編集できます。 左端近くにある、注文の一覧が表示され、概要とその注文の詳細を表示するには、そのリストに矢印を選択することができます。 詳細情報:[Northwind traders 社のキャンバス アプリの概要](northwind-orders-canvas-overview.md)します。

> [!div class="mx-imgBorder"]
> ![キャンバス アプリの注文と Northwind の詳細情報の一覧](media/northwind-install/orders-canvas.png)

### <a name="model-driven"></a>モデル駆動

このアプリは、同じデータに対して動作 (で、**注文**エンティティ)、キャンバス アプリとします。 注文の一覧でその番号を選択して注文の詳細について示してください。

> [!div class="mx-imgBorder"]
> ![Northwind モデル駆動型アプリでの注文の一覧](media/northwind-install/orders-model.png)

別のフォームに注文の概要が表示されます。

> [!div class="mx-imgBorder"]
> ![モデル駆動型アプリでの注文の詳細](media/northwind-install/orders-model-2.png)

フォームをスクロールする場合は、キャンバス アプリは、同じ品目を示します。

> [!div class="mx-imgBorder"]
> ![モデル駆動型アプリで複数の注文の詳細](media/northwind-install/orders-model-3.png)

## <a name="do-it-yourself"></a>自分で行う

このトピックで前述したキャンバス アプリを作成する手順を行うことができます。  手順については、3 つの部分に分かれます。

1. [ギャラリーを作成する順序](northwind-orders-canvas-part1.md)します。
1. [概要フォームを作成する](northwind-orders-canvas-part2.md)します。
1. [ギャラリーを作成する詳細](northwind-orders-canvas-part3.md)します。

前方にスキップする場合は、ソリューションには、各部分の開始点のアプリが含まれています。  アプリの一覧で探します**Northwind の Orders (キャンバス) - パート 1 の開始**という具合です。

これは、[アプリの概要](northwind-orders-canvas-overview.md)ユーザーについて説明しますインターフェイス、データ ソース、およびリレーションシップを使用する方法。

> [!div class="nextstepaction"]
> [まず、概要](northwind-orders-canvas-overview.md)

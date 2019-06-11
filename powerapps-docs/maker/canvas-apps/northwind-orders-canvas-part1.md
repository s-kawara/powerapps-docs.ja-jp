---
title: キャンバス アプリで順序ギャラリーを作成する |Microsoft Docs
description: Northwind traders 社のデータを管理するキャンバス アプリで順序ギャラリーを作成します。
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 04/25/2019
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 94d6c104cb888bb13f3724231d7891d622f5377b
ms.sourcegitcommit: e85072f7a80da308c4caabe20adbf2509588ca57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66761007"
---
# <a name="create-an-order-gallery-in-a-canvas-app"></a>キャンバス アプリで順序ギャラリーを作成します。

Northwind Traders データベース内の架空のデータを管理するためのキャンバス アプリで、注文のギャラリーを作成する手順に従います。 このトピックでは、Common Data Service 内のリレーショナル データにビジネス アプリを構築する方法を説明するシリーズの一部です。 最良の結果をこの順序でこれらのトピックを詳細します。

1. ギャラリーを作成する順序 (**このトピックの「** ).
1. [概要フォームを作成する](northwind-orders-canvas-part2.md)します。
1. [ギャラリーを作成する詳細](northwind-orders-canvas-part3.md)します。

> [!div class="mx-imgBorder"]
> ![画面領域の定義](media/northwind-orders-canvas-part1/orders-parts.png)

## <a name="prerequisites"></a>前提条件

- [Northwind Traders データベースとアプリ インストール](northwind-install.md)します。
- 目を通してください、[キャンバス アプリの概要](northwind-orders-canvas-overview.md)Northwind traders 社にします。

## <a name="create-a-blank-app"></a>空のアプリを作成する

1. [PowerApps にサインイン](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)、し、空白のタブレット アプリを作成します。

    > [!div class="mx-imgBorder"]
    > ![空のタイルからキャンバス アプリ](media/northwind-orders-canvas-part1/start-01.png)

1. どのようなアプリの名前をクリックして、**作成**です。

    > [!div class="mx-imgBorder"]
    > ![空白のダイアログ ボックスからキャンバス アプリ](media/northwind-orders-canvas-part1/start-02.png)

    データ ソースやコントロールをアプリに追加できるように、PowerApps Studio が開きます。

    > [!div class="mx-imgBorder"]
    > ![PowerApps Studio](media/northwind-orders-canvas-part1/start-03.png)

1. 有効にする、[実験的な機能](working-with-experimental.md)数式バーから直接数式の結果を表示するためです。

    1. **ファイル**メニューの **アプリ設定**、し、**詳細設定**します。
    1. 機能の一覧の一番下までスクロールして有効に**数式バー結果ビューを有効にする**:

        > [!div class="mx-imgBorder"]
        > ![試験的な機能の一覧](media/northwind-orders-canvas-part1/start-04.png)

1. 左上隅にある、空白のキャンバスに戻るに戻る矢印を選択します。

## <a name="add-the-data"></a>データを追加します。

1. **ビュー**  タブで **データ ソース**、し、**データ ソースの追加**で、**データ**ウィンドウ。

    > [!div class="mx-imgBorder"]
    > ![データ ソース、データ ソースの追加のビューを選択します。](media/northwind-orders-canvas-part1/datasource-01.png)

1. 選択**Common Data Service**します。

    場合**Common Data Service**選択、接続の一覧に表示されない**新しい接続**、しを追加します。

    > [!div class="mx-imgBorder"]
    > ![接続の一覧](media/northwind-orders-canvas-part1/datasource-02.png)

1. **エンティティを選択する**、型**注文**を選択、**注文**チェック ボックスをオンし、 **Connect**:

    > [!div class="mx-imgBorder"]
    > ![エンティティの一覧](media/northwind-orders-canvas-part1/datasource-03.png)

    追加した、**注文**アプリへのデータ ソース。

    > [!div class="mx-imgBorder"]
    > ![データ ペイン](media/northwind-orders-canvas-part1/datasource-04.png)

    **注文**エンティティには、さまざまな種類の多くのフィールドが含まれています。

    > [!div class="mx-imgBorder"]
    > ![Orders エンティティのフィールドの一覧](media/northwind-orders-canvas-part1/datasource-05.png)

    各フィールドには、**表示名**と**名前**、論理名と呼ばれることがあります。 両方の名前は同じものを参照してください。 、アプリを構築する、いくつかのケースが不可解な必要があるとき、表示名を使用します一般に、**名前**プロシージャで説明したように、します。

1. PowerApps Studio を閉じる、**データ**ウィンドウの右上隅にある閉じるアイコン (x) を選択しています。

## <a name="create-the-order-gallery"></a>注文のギャラリーを作成します。

1. **挿入**] タブで [**ギャラリー** > **空白垂直**を追加する、 [**ギャラリー** ](controls/control-gallery.md)コントロールで、注文が表示されます。

    > [!div class="mx-imgBorder"]
    > ![Insert、ギャラリー、空の垂直方向](media/northwind-orders-canvas-part1/orders-01.png)

1. 数式バーで設定ギャラリーの**項目**に次の式のプロパティ。

    ```powerapps-dot
    Sort( Orders, 'Order Number', Descending )
    ```

    [**並べ替え**](functions/function-sort.md)関数は、最初に表示されます (これは、最高の注文番号がある) 最新の順序になるようにリストを並べ替えます。

    > [!div class="mx-imgBorder"]
    > ![ギャラリーの Items プロパティを設定します。](media/northwind-orders-canvas-part1/orders-02.png)

1. **プロパティ**右端近くにある、開いているタブ、**レイアウト**一覧。

    > [!div class="mx-imgBorder"]
    > ![レイアウト オプションの一覧](media/northwind-orders-canvas-part1/orders-03.png)

1. オプションの一覧で選択**タイトルとサブタイトル**:

    > [!div class="mx-imgBorder"]
    > ![レイアウトを選択します](media/northwind-orders-canvas-part1/orders-04.png)

    2 つ[**ラベル**](controls/control-text-box.md)ギャラリーのテンプレートにコントロールを追加します。 既定では、これらのコントロールが 2 つの列を表示、**注文**エンティティで、次に変更します。 ギャラリーのテンプレートは、エンティティ内の各レコードの垂直方向にレプリケートされます。

1. 閉じている場合、**データ**ペインで、**編集**(横に**フィールド**) で、**プロパティ**右端近くにあるタブ。

1. **データ**ペインで、 **Title1** (またはギャラリーのテンプレートで上のラベルを選択します)。

1. 数式バーで、設定、ラベルの**テキスト**に次の式のプロパティ。

    ```powerapps-dot
    "Order " & ThisItem.'Order Number'
    ```

    > [!div class="mx-imgBorder"]
    > ![タイトルのラベルの Text プロパティを設定します。](media/northwind-orders-canvas-part1/orders-06.png)

    ギャラリーの各項目の上部にある注文番号が表示されます。 ギャラリー テンプレートで**ThisItem**のすべてのフィールドへのアクセス許可、**順序**エンティティ。

1. **データ**ペインで、 **Subtitle1** (またはギャラリーのテンプレートの下のラベルを選択します)。

    > [!div class="mx-imgBorder"]
    > ![サブタイトルのラベルを選択します。](media/northwind-orders-canvas-part1/orders-07.png)

1. 数式バーで、設定、ラベルの**テキスト**に次の式のプロパティ。

    ```powerapps-dot
    ThisItem.Customer.Company
    ```

    > [!div class="mx-imgBorder"]
    > ![サブタイトルのラベルのテキストのプロパティを設定します。](media/northwind-orders-canvas-part1/orders-08.png)

    次の数式を入力すると後、は、少し赤の波線エラーを表示、可能性があります。 数式バーの外側にあるものを選択して数式バーにカーソルを返す場合、エラーがオフにします。 エラーが解決しない場合や、値が表示されない、選択、**ビュー** ] タブで [**データ ソース**、し、更新、**注文**エンティティ、省略記号 (...) を選択して、データ ソースの名前。

    指定すると**ThisItem.Customer**、多対一の関係を利用して、**注文**と**顧客**エンティティと顧客レコードを取得します。各注文に関連付けられているがします。 顧客のレコードからのデータを抽出している、**会社**表示用の列。

    すべてのリレーションシップを表示することができます、**注文**など、他のエンティティにエンティティ、**顧客**エンティティ。

    > [!div class="mx-imgBorder"]
    > ![リレーションシップの一覧](media/northwind-orders-canvas-part1/orders-09.png)

1. 閉じる、**データ**ウィンドウの右上隅にある閉じるアイコン (x) を選択します。

## <a name="show-each-orders-status"></a>各注文の状態を表示します。

この手順ではラベルのギャラリーにスペースを追加し、データに基づく別の色で各注文の状態を表示するように構成します。

1. ギャラリーのテンプレートの最初のラベルの幅を縮小**Title1**:

    > [!div class="mx-imgBorder"]
    > ![ギャラリーのテンプレートで Title1](media/northwind-orders-canvas-part1/status-01.png)

1. 2 番目のラベルで、前の手順を繰り返して**Subtitle1**:

    > [!div class="mx-imgBorder"]
    > ![ギャラリーのテンプレートで Subtitle1](media/northwind-orders-canvas-part1/status-02.png)

1. ギャラリーを選択すると、テンプレート (または、テンプレート内のコントロール) を選択**ラベル**上、**挿入** タブ。

    > [!div class="mx-imgBorder"]
    > ![ラベルを追加します。](media/northwind-orders-canvas-part1/status-03.png)

1. 新しいラベルの右側に移動、 **Title1**ラベル。

    > [!div class="mx-imgBorder"]
    > ![移動し、ラベルのサイズ変更](media/northwind-orders-canvas-part1/status-04.png)

1. 設定、**テキスト**この式に新しいラベルのプロパティ。

    ```powerapps-dot
    ThisItem.'Order Status'
    ```

    > [!div class="mx-imgBorder"]
    > ![Text プロパティを設定します。](media/northwind-orders-canvas-part1/status-05.png)

    **注文**、エンティティ、**注文ステータス**フィールドから値を保持する、**注文ステータス**オプションを設定します。 オプション セットは、他のプログラミング ツール内の列挙型に似ています。 各オプションのセットは、ためユーザーは、セット内にあるオプションのみを指定できるように、データベースで定義されます。 **注文ステータス**オプション セットもグローバル、ローカルではありません、他のエンティティで使用できるようにします。

    > [!div class="mx-imgBorder"]
    > ![状態のオプション セットを並べ替えます](media/northwind-orders-canvas-part1/status-06.png)

    セット内の各オプションは、ラベルに表示する場合に表示される名前を持ちます。 これらの名前をローカライズすることができます、および英語版のユーザーが選択したかどうか、アプリは、同じオプションを認識**Apple**、フランス語のユーザーが選択した**Pomme**、スペイン語のユーザーが選択または**Manzana**. このため、このトピックでは後で示すように、オプションについては、ハード コーディングされた文字列に依存している数式を作成することはできません。

    囲む必要があります、数式に**注文ステータス**での単一引用符、スペースが含まれています。 ただし、その名前などの関数と同じ PowerApps では、他の方法名**顧客**または**会社**は。

1. **ホーム** タブで、20 のポイントに状態のラベルのフォント サイズを大きくし、テキストを右揃えにします。

    > [!div class="mx-imgBorder"]
    > ![フォント サイズの変更と配置](media/northwind-orders-canvas-part1/status-07.png)

1. 数式バーで、設定、**色**次の数式に状態のラベルのプロパティ。

    ```powerapps-dot
    Switch( ThisItem.'Order Status',
        'Orders Status'.Closed, Green,
        'Orders Status'.New, Black,
        'Orders Status'.Invoiced, Blue,
        'Orders Status'.Shipped, Purple
    )
    ```

    > [!div class="mx-imgBorder"]
    > ![状態ラベルの色をプロパティします。](media/northwind-orders-canvas-part1/status-08.png)

    PowerApps には、このような数式は、オプション名はローカライズされる場合に、不適切な結果になる可能性がありますので、セット内の各オプションのハード コーディングされた文字列に依存する数式を作成できないようにします。 代わりに、**スイッチ**関数は、ユーザーの設定に基づいて、ラベルが表示されます任意の文字列に基づいて色を決定します。

    配置でこの数式でさまざまな状態の値として表示されます、別の色で前の図は。

## <a name="display-each-orders-total"></a>各注文の合計を表示します。

1. ギャラリーのテンプレートは、ギャラリー内の最初の項目を選択します。

    > [!div class="mx-imgBorder"]
    > ![ギャラリー テンプレートを選択します。](media/northwind-orders-canvas-part1/aggregate-01.png)

1. **挿入**] タブで [**ラベル**別のラベルを追加します。

    > [!div class="mx-imgBorder"]
    > ![ラベルを追加します。](media/northwind-orders-canvas-part1/aggregate-02.png)

1. 状態ラベルの下に表示されるように、新しいラベルを移動します。

    > [!div class="mx-imgBorder"]
    > ![サイズを変更し、新しいラベルを移動](media/northwind-orders-canvas-part1/aggregate-03.png)

1. 数式バーで、新しいラベルを設定**テキスト**に次の式のプロパティ。

    ```powerapps-dot
    Text( Sum( ThisItem.'Order Details', Quantity * 'Unit Price' ), "[$-en-US]$ #,###.00" )
    ```

    > [!div class="mx-imgBorder"]
    > ![注文の合計コストを計算する式](media/northwind-orders-canvas-part1/aggregate-04.png)

    この数式で、 [**合計**](functions/function-aggregates.md)関数を内のレコードを追加、 **Order Details**エンティティ内の各レコードに関連付けられている、**順序**一対多のリレーションシップを介してエンティティ。 これらの行アイテムが、各注文を構成して、同じ一対多リレーションシップを表示して、画面の右下の領域に行アイテムの編集に使用します。

    この数式は青の下線を表示し、[委任の警告](delegation-overview.md)Common Data Service は、複雑な集計関数 (たとえば、乗算の合計) の委任をサポートしないためです。 この例では order には 500 個を超える品目がないため、この情報は無視できます。 かどうかは別のアプリの必要に応じて、制限を増やすことで**アプリ設定**します。

    [**テキスト**](functions/function-text.md)この数式で関数が通貨記号を追加し、何千も桁区切り記号と結果を書式設定します。 米国の言語タグが、数式に含まれている書き込まれると、英語 ( **[$-EN-US]** ) とドル記号 ( **$** )。 言語タグを削除する場合は、言語設定に基づくいずれかの置き換えし、ラベルはそのタグの適切な形式で表示されます。 ドル記号をままにした場合、ラベルには、ユーザーの設定に基づいて、適切な通貨記号が表示されます。 ただし、ドル記号を使用するものに置き換えることにより表示される別の記号を強制できます。

1. **ホーム** タブで、20 のポイントを最新のラベルのフォント サイズを変更し、そのテキストを右揃えにします。

    > [!div class="mx-imgBorder"]
    > ![フォント サイズを変更して、ラベルの配置](media/northwind-orders-canvas-part1/aggregate-05.png)

1. 画面の左端にギャラリーを移動し、領域を増やしてを閉じるのギャラリーの幅を狭きます。

1. ギャラリーの高さを増やす 画面で、ほとんどの高さが、次のトピックの先頭に追加するタイトル バーの上部にある少し余裕を確保します。

    > [!div class="mx-imgBorder"]
    > ![移動して、ギャラリーのサイズを変更します。](media/northwind-orders-canvas-part1/aggregate-06.png)

## <a name="summary"></a>まとめ

要約すると、これらの要素を含む注文ギャラリーを追加することで 1 つの画面のキャンバス アプリのビルドが開始。

- 注文番号を表示する式。 `"Orders " & ThisItem.OrderNumber`
- 多対一リレーションシップでフィールド: `ThisItem.Customer.Company`
- 一連のオプションの名前を示すラベル: `ThisItem.'Order Status'`
- どちらのオプション セットのラベルに表示されますに基づいて書式設定を変更するラベル。 `Switch( ThisItem.'Order Status', 'Orders Status'.Closed, Green, ...`
- 一対多リレーションシップの上の複雑な集計関数: `Sum( ThisItem.'Order Details', Quantity * 'Unit Price' )`

## <a name="next-topic"></a>次のトピック

次のトピックでは追加します、 [**編集フォーム**](controls/control-form-detail.md)コントロールを表示し、編集、ユーザーが注文内容の概要を作成したギャラリーを選択します。

> [!div class="nextstepaction"]
> [概要フォームを作成します。](northwind-orders-canvas-part2.md)
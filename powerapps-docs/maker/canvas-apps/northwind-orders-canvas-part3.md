---
title: キャンバス アプリで詳細ギャラリーの作成 |Microsoft Docs
description: Northwind traders 社のデータを管理するキャンバス アプリの詳細のギャラリーを作成します。
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
ms.openlocfilehash: 9549b8f389cf696cf3fc8e4659da6b418383ac6e
ms.sourcegitcommit: e85072f7a80da308c4caabe20adbf2509588ca57
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66760961"
---
# <a name="create-a-detail-gallery-in-a-canvas-app"></a>キャンバス アプリの詳細のギャラリーを作成します。

Northwind Traders データベース内の架空のデータを管理するためのキャンバス アプリの詳細のギャラリーを作成する手順に従います。 このトピックでは、Common Data Service 内のリレーショナル データにビジネス アプリを構築する方法を説明するシリーズの一部です。 最良の結果をこの順序でこれらのトピックを詳細します。

1. [ギャラリーを作成する順序](northwind-orders-canvas-part1.md)します。
1. [概要フォームを作成する](northwind-orders-canvas-part2.md)します。
1. 詳細のギャラリーの作成 (**このトピックの「** ).

> [!div class="mx-imgBorder"]
> ![画面領域の定義](media/northwind-orders-canvas-part1/orders-parts.png)

## <a name="prerequisites"></a>前提条件

このトピックを開始する前に、このトピックで前述したように、データベースをインストールする必要があります。 必要がありますし、順序ギャラリーおよび概要フォームを作成するか開きます、 **Northwind の Orders (キャンバス) - パート 3 の開始**アプリで、そのギャラリーとそのフォームが既に存在します。

## <a name="create-another-title-bar"></a>別のタイトル バーを作成します。

1. 画面の上部にある選択、 [**ラベル**](controls/control-text-box.md)をタイトル バーとして機能するコントロールは、Ctrl + C キーを押して、コピーし、: ctrl キーを押して貼り付けます

    > [!div class="mx-imgBorder"]
    > ![コピーして貼り付けるタイトル バー](media/northwind-orders-canvas-part3/details-01.png)

1. サイズを変更し、集計フォームのすぐ下に表示されるように、コピーを移動します。

1. 次の方法のいずれかで、コピーからテキストを削除します。

    - テキストを選択しをダブルクリックし、Delete キーを押します。
    - ラベルの設定**テキスト**プロパティを空の文字列 ( **""** )。

    > [!div class="mx-imgBorder"]
    > ![タイトル バーのコピーからテキストを削除します。](media/northwind-orders-canvas-part3/details-02.png)

## <a name="add-a-gallery"></a>ギャラリーを追加する

1. 挿入、 [**ギャラリー** ](controls/control-gallery.md)コントロールを**空白垂直**レイアウト。

    > [!div class="mx-imgBorder"]
    > ![空の垂直ギャラリーを追加します。](media/northwind-orders-canvas-part3/details-03.png)

    左上隅で、注文の詳細が表示されます、新しいギャラリーが表示されます。

    > [!div class="mx-imgBorder"]
    > ![注文明細のギャラリーの既定の場所](media/northwind-orders-canvas-part3/details-04.png)

1. 閉じる、**データ**ウィンドウで、サイズ変更して新しいタイトル バーの下の右下隅に移動詳細ギャラリー。

    > [!div class="mx-imgBorder"]
    > ![注文明細のギャラリーの最終的な場所](media/northwind-orders-canvas-part3/details-05.png)

1. 設定、**項目**詳細ギャラリーに次の式のプロパティ。

    ```powerapps-dot
    Gallery1.Selected.'Order Details'
    ```

    > [!div class="mx-imgBorder"]
    > ![詳細のギャラリーの Items プロパティを設定します。](media/northwind-orders-canvas-part3/details-06.png)

    エラーが表示された場合の確認順序ギャラリーの名前は**Gallery1** (で、**ツリー ビュー**左端近くにあるウィンドウ)。 そのギャラリーでは、別の名前には場合、変更**Gallery1**します。

    2 つのギャラリーをリンクしただけです。 その選択内容が内のレコードを識別するユーザーは、注文のギャラリーで注文を選択するときに、**注文**エンティティ。 かどうかの順序に 1 つまたは複数の行が含まれている項目をレコード、**注文**エンティティ内の 1 つまたは複数のレコードにリンクされて、 **Order details**エンティティ、およびそれらのレコードからのデータの詳細ギャラリーに表示されます。 この動作の間に作成されたの一対多リレーションシップを反映して、**注文**と**Order Details**エンティティ。 指定した式は、ドット表記を使用してそのリレーションシップを「説明」。

    > [!div class="mx-imgBorder"]
    > ![Orders エンティティと Order Details エンティティの間の一対多のリレーションシップ](media/northwind-orders-canvas-part3/schema-orders-rel.png)

## <a name="show-product-names"></a>製品名を表示します。

1. 詳細ギャラリーで **[挿入] タブから項目を追加**ギャラリー テンプレートを選択します。

    > [!div class="mx-imgBorder"]
    > ![詳細のギャラリーのテンプレートを選択します。](media/northwind-orders-canvas-part3/details-07.png)

    ギャラリー自体ではなくギャラリー テンプレートを選択したことを確認します。 境界ボックスは若干、ギャラリーの境界内にあると、ギャラリーの高さよりも短い可能性があります。 このテンプレートにコントロールを挿入するには、ギャラリーの項目ごとに繰り返されます。

1. **挿入** タブで、詳細ギャラリーにラベルを挿入します。

    ギャラリー内で、ラベルが表示されます。いない場合、もう一度お試しがラベルを挿入する前に、ギャラリーのテンプレートを選択してください。

    > [!div class="mx-imgBorder"]
    > ![詳細のギャラリーにラベルを追加します。](media/northwind-orders-canvas-part3/details-08.png)

1. 新しいラベルの設定**テキスト**に次の式のプロパティ。

    ```powerapps-dot
    ThisItem.Product.'Product Name'
    ```

    テキストが表示されない場合は、矢印を選択**順序 0901**順序ギャラリーの下部付近でします。

1. 完全なテキストが表示されるように、ラベルのサイズを変更します。

    > [!div class="mx-imgBorder"]
    > ![注文の詳細で製品名を表示します。](media/northwind-orders-canvas-part3/details-09.png)

    この式でのレコードからについて説明します、 **Order Details**エンティティ。 レコードが保持されている**ThisItem**に、**製品を注文**多対一のリレーションシップを介してエンティティ。

    > [!div class="mx-imgBorder"]
    > ![Order Details エンティティと注文製品エンティティ間の多対一のリレーションシップ](media/northwind-orders-canvas-part3/schema-orderdetails-rel.png)

    **製品名**フィールド (およびその他のフィールドを使用しようとしています) が抽出されます。

    > [!div class="mx-imgBorder"]
    > ![製品の注文エンティティのフィールド](media/northwind-orders-canvas-part3/schema-products-fields.png)

## <a name="show-product-images"></a>製品の画像を表示します。

1. **挿入** タブで、挿入、 [**イメージ**](controls/control-image.md)詳細ギャラリー コントロール。

    > [!div class="mx-imgBorder"]
    > ![イメージ コントロールを挿入します。](media/northwind-orders-canvas-part3/details-10.png)

1. サイズを変更し、画像と並行するラベルを移動します。

    > [!TIP]
    > サイズと、コントロールの位置を細かく制御する、サイズを変更するか、Alt キーを押さずに移動してサイズを変更したり、Alt キーを押しながら、コントロールに移動し、続行します。

    > [!div class="mx-imgBorder"]
    > ![イメージ コントロールを移動します。](media/northwind-orders-canvas-part3/details-11.png)

1. イメージの設定**イメージ**に次の式のプロパティ。

    ```powerapps-dot
    ThisItem.Product.Picture
    ```

    詳細と抽出がこれに関連付けられている製品を式で参照でもう一度、注文、**画像**を表示するフィールド。

    > [!div class="mx-imgBorder"]
    > ![製品の画像を表示します。](media/northwind-orders-canvas-part3/details-12.png)

1. そのため、複数の 1 つのギャラリーのテンプレートの高さを縮小**Order Detail**一度にレコードが表示されます。

    > [!div class="mx-imgBorder"]
    > ![ギャラリーのテンプレートを短縮します。](media/northwind-orders-canvas-part3/details-13.png)

## <a name="show-product-quantity-and-cost"></a>製品の数量とコストを表示します。

1. **挿入**タブ、詳細ギャラリー、別のラベルを挿入、サイズ変更および製品情報の右側に新しいラベルを移動します。

1. 新しいラベルの設定**テキスト**に次の式のプロパティ。

    ```powerapps-dot
    ThisItem.Quantity
    ```

    この数式はから直接情報を取得、 **Order Details**エンティティ (リレーションシップが必要です)。

    > [!div class="mx-imgBorder"]
    > ![製品の数量を表示します。](media/northwind-orders-canvas-part3/details-13b.png) 

1. **ホーム** タブで、このコントロールの配置を変更する**右**:

    > [!div class="mx-imgBorder"]
    > ![配置を変更します。](media/northwind-orders-canvas-part3/details-14.png)

1. **挿入**タブ、詳細ギャラリー、別のラベルを挿入、サイズ変更および数量のラベルの右側にラベルを移動します。

1. 新しいラベルの設定**テキスト**に次の式のプロパティ。

    ```powerapps-dot
    Text( ThisItem.'Unit Price', "[$-en-US]$ #,###.00" )
    ```

    言語タグが含まれていない場合 ( **[$-EN-US]** )、言語や地域に基づいて追加されます。 別の言語タグを使用する場合は、削除たい、 **$** 終わり角かっこの直後後 ( **]** )、し、その位置に通貨記号を追加します。

    > [!div class="mx-imgBorder"]
    > ![単価を表示します。](media/northwind-orders-canvas-part3/details-15.png)

1. **ホーム** タブで、このコントロールの配置を変更する**右**:

    > [!div class="mx-imgBorder"]
    > ![配置を変更します。](media/northwind-orders-canvas-part3/details-16.png)

1. **挿入**タブ、詳細ギャラリー、別のラベル コントロールに挿入、サイズ変更および単価の右側に新しいラベルを移動します。

1. 新しいラベルの設定**テキスト**に次の式のプロパティ。

    ```powerapps-dot
    Text( ThisItem.Quantity * ThisItem.'Unit Price', "[$-en-US]$ #,###.00" )
    ```

    ここでも、言語タグが含まれていない場合 ( **[$-EN-US]** )、言語や地域に基づいて追加されます。 タグが異なる場合は、代わりに、独自の通貨記号を使用してたい、 **$** 終わり角かっこの直後後 ( **]** )。

    > [!div class="mx-imgBorder"]
    > ![価格を表示します。](media/northwind-orders-canvas-part3/details-17.png)

1. **ホーム** タブで、このコントロールの配置を変更する**右**:

    > [!div class="mx-imgBorder"]
    > ![配置を変更します。](media/northwind-orders-canvas-part3/details-18.png)

    ここでは、詳細ギャラリーにコントロールを追加が終了しました。

1. **ツリー ビュー**ペインで、 **Screen1**詳細ギャラリーが選択されていないことを確認します。

## <a name="add-text-to-the-new-title-bar"></a>新しいタイトル バーにテキストを追加します。

1. **挿入** タブで、画面に別のラベルを挿入します。

    > [!div class="mx-imgBorder"]
    > ![ラベルを挿入します。](media/northwind-orders-canvas-part3/details-19.png)

1. サイズを変更し、2 つ目のタイトル バーで、製品の画像の上に新しいラベルを移動し、テキストの色を白に変更、**ホーム**タブ。

1. ラベルのテキストをダブルクリックし、入力**製品**:

    > [!div class="mx-imgBorder"]
    > ![ラベルのテキストを製品に変更します。](media/northwind-orders-canvas-part3/details-20.png)

1. コピーし製品のラベルを貼り付けるのサイズを変更し、コピー、quantity 列の上を移動します。

1. 新しいラベルのテキストをダブルクリックし、入力**数量**:

    > [!div class="mx-imgBorder"]
    > ![ラベルのテキストの数量を変更します。](media/northwind-orders-canvas-part3/details-21.png)

1. コピーし数量のラベルを貼り付けるのサイズを変更し、unit price 列の上に移動します。

1. 新しいラベルのテキストをダブルクリックし、入力**Unit Price**:

    > [!div class="mx-imgBorder"]
    > ![ラベルのテキスト単位の価格を変更します。](media/northwind-orders-canvas-part3/details-22.png)

1. コピーし単位価格のラベルを貼り付けるとサイズを変更し、拡張 price 列の上のコピーを移動します。

1. 新しいラベルのテキストをダブルクリックし、入力**拡張**:

    > [!div class="mx-imgBorder"]
    > ![拡張のラベルのテキストを変更します。](media/northwind-orders-canvas-part3/details-23.png)

## <a name="display-order-totals"></a>注文の合計を表示します。

1. 画面の下部にある注文の合計を確保するために詳細ギャラリーの高さを減らします。

    > [!div class="mx-imgBorder"]
    > ![注文明細のギャラリーを短縮します。](media/northwind-orders-canvas-part3/sum-01.png)

1. コピーし、画面の中央のタイトル バーに貼り付けるし、そのコピーを画面の下部に移動します。

    > [!div class="mx-imgBorder"]
    > ![タイトル バーをコピーし、コピー、下端に移動](media/northwind-orders-canvas-part3/sum-02.png)

1. コピーし、中間のタイトル バーから製品のラベルを貼り付け、そのコピーの左側に、下部にあるタイトル バーに移動、**数量**列。

1. 新しいラベルのテキストをダブルクリックし、このテキストを入力します。<br>**注文の合計:**

    > [!div class="mx-imgBorder"]
    > ![注文の合計のラベルを追加します。](media/northwind-orders-canvas-part3/sum-03.png)

1. コピーし、注文合計ラベルを貼り付けますのサイズを変更し、注文合計ラベルの右側に移動します。

1. 新しいラベルの設定**テキスト**に次の式のプロパティ。

    ```powerapps-dot
    Sum( Gallery1.Selected.'Order Details', Quantity )
    ```

    次の数式に委任の警告が表示されますが、1 つの注文には 500 個を超える製品がないため、無視することができます。

1. **ホーム**に新しいラベルのテキストの配置の設定 タブで、**右**:

    > [!div class="mx-imgBorder"]
    > ![配置を変更します。](media/northwind-orders-canvas-part3/sum-04.png)

1. コピー、このラベル コントロールを貼り付けるとサイズを変更および移動でコピー、**拡張**列。

1. コピーの設定**テキスト**に次の式のプロパティ。

    ```powerapps-dot
    Text( Sum( Gallery1.Selected.'Order Details', Quantity * 'Unit Price' ), "[$-en-US]$ #,###.00" )
    ```

    次の数式に委任の警告が表示されますが、1 つの注文には 500 個を超える製品がないため、無視することができます。

    > [!div class="mx-imgBorder"]
    > ![注文の合計コストを表示します。](media/northwind-orders-canvas-part3/sum-05.png)

## <a name="add-space-for-new-details"></a>詳細については新しい領域を追加します。

任意のギャラリーでデータを表示することができますが、更新するか、レコードを追加することはできません。 詳細ギャラリーの下には、ユーザーが内のレコードを構成できる領域を追加します、 **Order Details**エンティティとその注文にレコードを挿入します。

1. そのギャラリーの下の単一項目の編集領域を確保するために十分な詳細ギャラリーの高さを削減します。

    この領域では、ユーザーは、注文の詳細を追加できるようにコントロールを追加します。

    > [!div class="mx-imgBorder"]
    > ![詳細のギャラリーを短縮します。](media/northwind-orders-canvas-part3/add-details-01.png)

1. **挿入**タブ、ラベルはのサイズを変更および詳細ギャラリーの下に移動します。

    > [!div class="mx-imgBorder"]
    > ![ラベルを挿入します。](media/northwind-orders-canvas-part3/add-details-02.png)

1. 新しいラベルのテキストをダブルクリックし、Delete キーを押します。

1. **ホーム**新しいラベルの設定 タブで、**入力**する色**LightBlue**:

    > [!div class="mx-imgBorder"]
    > ![ラベルの塗りつぶしを薄い青に変更します。](media/northwind-orders-canvas-part3/add-details-03.png)

## <a name="add-the-order-details-data-source"></a>Order Details のデータ ソースを追加します。

1. **ビュー**  タブで **データ ソース**、し、**データ ソースの追加**で、**データ**ウィンドウ。

    > [!div class="mx-imgBorder"]
    > ![データ ソースを追加します。](media/northwind-orders-canvas-part3/add-details-04.png)

1. 選択**Common Data Service**:

    > [!div class="mx-imgBorder"]
    > ![Common Data Service を選択します。](media/northwind-orders-canvas-part3/add-details-05.png)

1. 上部にある、**データ** ウィンドウで「**順序**検索ボックスで選択、 **Order Details**チェック ボックス オンにし、選択**Connect**で、ウィンドウの下部にある:

    > [!div class="mx-imgBorder"]
    > ![注文の詳細のエンティティを指定します。](media/northwind-orders-canvas-part3/add-details-06.png)

    アプリに別のデータ ソースを追加しただけです。

    > [!div class="mx-imgBorder"]
    > ![データ ソースの一覧](media/northwind-orders-canvas-part3/add-details-07.png)

    アプリは、一対多リレーションシップで見ることも、アプリできませんまだ変更を書き戻すため、このデータ ソースを追加する必要があります。 アプリでは、関連エンティティを直接変更を加える必要があります。

1. 閉じる、**データ**ウィンドウ。

## <a name="select-a-product"></a>製品を選択します。

1. **挿入**] タブで [**コントロール** > **コンボ ボックス**:

    > [!div class="mx-imgBorder"]
    > ![コンボ ボックスを挿入します。](media/northwind-orders-canvas-part3/add-details-08.png)

    [**コンボ ボックス**](controls/control-combo-box.md)左上隅にコントロールが表示されます。

1. コンボ ボックスの設定**項目**に次の式のプロパティ。

    ```powerapps-dot
    Choices( 'Order Details'.Product )
    ```

    > [!div class="mx-imgBorder"]
    > ![コンボ ボックスの項目のプロパティを設定します。](media/northwind-orders-canvas-part3/add-details-09.png)

    [**選択肢**](functions/function-choices.md)関数のすべての可能な値のテーブルを返します、**製品**フィールドに、 **Order Details**エンティティ。 このフィールドは、多対一リレーションシップ内の参照があるため**選択肢**内のすべてのレコードを返します、**製品を注文**エンティティ。

    > [!NOTE]
    > 使用することも**選択肢**にすべてのオプションのテーブルを返すオプションのセットをします。 手順は、この方法について触れていませんでしたが、既に表示されているコンボ ボックスを追加したときに使用した**注文ステータス**概要フォーム。

1. **データ**ウィンドウで、開く、**プライマリ テキスト**、一覧表示し、 **nwind_productname**。 

1. 開く、 **SearchField** 、一覧表示し、 **nwind_productname**します。

    論理名を指定するため、**データ**ウィンドウはこのケース内の表示名をまだサポートしていません。

    > [!div class="mx-imgBorder"]
    > ![コンボ ボックスの主要なテキストを設定します。](media/northwind-orders-canvas-part3/add-details-10.png)

1. 閉じる、**データ**ウィンドウ。

1. **プロパティ**右端近くにあるタブをスクロール ダウンし、オフにする**複数選択を許可する**、いることを確認し、**許可検索**がオンします。

    > [!div class="mx-imgBorder"]
    > ![複数選択を無効にして、検索を有効にします。](media/northwind-orders-canvas-part3/add-details-12.png)

1. サイズを変更し、コンボ ボックスを明るい青色の領域で、詳細ギャラリーで製品名 列のすぐ下に移動します。

    > [!div class="mx-imgBorder"]
    > ![コンボ ボックスを移動します。](media/northwind-orders-canvas-part3/add-details-13.png)

    このコンボ ボックスで、ユーザーが内のレコードを指定、**製品**のエンティティ、 **Order Details**アプリを作成するレコード。

1. Alt キーを押したまま、コンボ ボックスの下矢印を選択します。

    > [!TIP]
    > Alt キーを押しながらは、プレビュー モードを開くことがなく PowerApps Studio でのコントロールと対話できます。

1. 表示される製品の一覧で、製品を選択します。

    > [!div class="mx-imgBorder"]
    > ![コンボ ボックスで、製品を選択します。](media/northwind-orders-canvas-part3/add-details-14.png)

## <a name="add-a-product-image"></a>製品イメージを追加します。

1. **挿入**] タブで [**メディア** > **イメージ**:

    > [!div class="mx-imgBorder"]
    > ![イメージ コントロールを挿入します。](media/northwind-orders-canvas-part3/add-details-15.png)

    [**イメージ**](controls/control-image.md)左上隅にコントロールが表示されます。

    > [!div class="mx-imgBorder"]
    > ![イメージ コントロールの既定の場所](media/northwind-orders-canvas-part3/add-details-16.png)

1. サイズを変更し、イメージを明るい青色の領域およびコンボ ボックスの横にあるその他の製品の画像の下に移動します。

1. 設定、**イメージ**するイメージのプロパティ。

    ```powerapps-dot
    ComboBox1.Selected.Picture
    ```

    > [!div class="mx-imgBorder"]
    > ![イメージのイメージ プロパティを設定します。](media/northwind-orders-canvas-part3/add-details-17.png)

    概要の形式で従業員の画像を表示するために使用すると同じテクニックを使用しています。 **選択**コンボ ボックスのプロパティは、任意の製品を含む、ユーザーが選択の全体のレコードを返します、**画像**フィールド。

## <a name="add-a-quantity-box"></a>数量ボックスを追加します。

1. **挿入**] タブで [**テキスト** > **テキスト入力**:

    > [!div class="mx-imgBorder"]
    > ![テキスト入力ボックスを追加します。](media/northwind-orders-canvas-part3/add-details-18.png)

    [**テキスト入力**](controls/control-text-input.md)左上隅にコントロールが表示されます。

    > [!div class="mx-imgBorder"]
    > ![テキスト入力ボックスの既定の場所](media/northwind-orders-canvas-part3/add-details-19.png)

1. サイズを変更し、詳細ギャラリーにある quantity 列の下で、コンボ ボックスの右側にテキスト入力ボックスに移動します。

    > [!div class="mx-imgBorder"]
    > ![サイズを変更し、テキスト入力ボックスの移動](media/northwind-orders-canvas-part3/add-details-20.png)

    ユーザーを指定するこのテキスト入力ボックスを使用して、**数量**のフィールド、 **Order Details**レコード。

1. 設定、**既定**プロパティには、このコントロールの **""** :

    > [!div class="mx-imgBorder"]
    > ![設定、* * 既定 * *、テキスト入力ボックスのプロパティ](media/northwind-orders-canvas-part3/add-details-21.png)

1. **ホーム** タブで、このコントロールのテキストの配置設定**右**:

    > [!div class="mx-imgBorder"]
    > ![配置を変更します。](media/northwind-orders-canvas-part3/add-details-22.png)

## <a name="show-the-unit-and-extended-prices"></a>単位と拡張の価格を表示します。

1. **挿入** タブで、挿入、**ラベル**コントロール。

    画面の左上隅で、ラベルが表示されます。

    > [!div class="mx-imgBorder"]
    > ![ラベルを挿入します。](media/northwind-orders-canvas-part3/add-details-23.png)

1. サイズを変更して、ラベル、テキスト入力コントロールの右側に移動およびラベルの設定**テキスト**に次の式のプロパティ。

    ```powerapps-dot
    Text( ComboBox1.Selected.'List Price', "[$-en-US]$ #,###.00" )
    ```

    > [!div class="mx-imgBorder"]
    > ![ラベルの Text プロパティを設定します。](media/northwind-orders-canvas-part3/add-details-24.png)

    このコントロールに表示されます、**定価**から、**製品を注文**エンティティ。 この値が決定されます、 **Unit Price**フィールドに、 **Order Details**レコード。

    > [!NOTE]
    > このシナリオでは、値が読み取り専用が変更をアプリのユーザーの他のシナリオを呼び出すことができます。 その場合を使用して、**テキスト入力**制御、および設定の**既定**プロパティを**表示価格**。

1. **ホーム** タブで、表示価格のラベルのテキストの配置設定**右**:

    > [!div class="mx-imgBorder"]
    > ![配置を変更します。](media/northwind-orders-canvas-part3/add-details-25.png)

1. コピーし、表示価格ラベルを貼り付けますとサイズを変更し、コピー、表示価格のラベルの右側に移動します。

1. 新しいラベルの設定**テキスト**に次の式のプロパティ。

    ```powerapps-dot
    Text( Value(TextInput1.Text) * ComboBox1.Selected.'List Price', "[$-en-US]$ #,###.00" )
    ```

    > [!div class="mx-imgBorder"]
    > ![新しいラベルの Text プロパティを設定します。](media/northwind-orders-canvas-part3/add-details-27.png)

    このコントロールには、アプリのユーザーが指定されている数量とアプリのユーザーが選択されている製品の表示価格に基づいて価格が表示されます。 純粋なアプリのユーザーの情報になります。

1. 数量のテキスト入力コントロールをダブルクリックし、数値を入力します。

    **拡張**新しい値を表示する価格のラベルが再計算されます。

    > [!div class="mx-imgBorder"]
    > ![数量を指定し、拡張の価格を表示します。](media/northwind-orders-canvas-part3/add-details-28.png)

## <a name="add-an-add-icon"></a>追加アイコンを追加します。

1. **挿入**] タブで [**アイコン** > **追加**:

    > [!div class="mx-imgBorder"]
    > ![追加アイコンを挿入します。](media/northwind-orders-canvas-part3/add-details-29.png)

    画面の左上隅にアイコンが表示されます。

    > [!div class="mx-imgBorder"]
    > ![追加アイコンの既定の場所](media/northwind-orders-canvas-part3/add-details-30.png)

1. サイズを変更し、このアイコンを薄い青 領域の右端に移動し、アイコンを設定**OnSelect**に次の式のプロパティ。

    ```powerapps-dot
    Patch( 'Order Details',
        Defaults('Order Details'),
        {
            Order: Gallery1.Selected,
            Product: ComboBox1.Selected,
            Quantity: Value(TextInput1.Text),
            'Unit Price': ComboBox1.Selected.'List Price'
        }
    );
    Refresh( Orders );
    Reset( ComboBox1 );
    Reset( TextInput1 )
    ```

    > [!div class="mx-imgBorder"]
    > ![アイコンの OnSelect プロパティを設定します。](media/northwind-orders-canvas-part3/add-details-31.png)

    一般に、 [**パッチ**](functions/function-patch.md)この数式では、特定の引数が関数になります正確な変更を特定し、関数を更新し、レコードを作成します。

    - 最初の引数は、データ ソースを指定します (この場合、 **Order Details**エンティティ)、関数が更新またはレコードを作成します。
    - 2 番目の引数を指定、関数がの既定値を持つレコードを作成できる、 **Order Details**エンティティそれ以外の場合、3 番目の引数で指定されていない場合。
    - 3 番目の引数は、新しいレコードの 4 つの列がユーザーからの値を含めることを指定します。

      - **順序**順序ギャラリーで、ユーザーが選択されている注文の数が格納されます。
      - **製品**コンボ ボックスで選択したユーザーが表示される製品の製品の名前が格納されます。
      - **数量**列は、テキスト入力ボックスで、ユーザーが指定されている値が格納されます。
      - **Unit Price**列は、ユーザーがこの注文詳細の選択した製品の定価が格納されます。

    > [!NOTE]
    > 任意の列からデータを使用する数式を作成できます (で、**製品を注文**エンティティ) 製品を示すコンボ ボックスでどのような製品のアプリのユーザーを選択します。 ユーザーが内のレコードを選択すると、**製品を注文**エンティティだけでなく、製品の名前は、そのコンボ ボックス内で表示、ラベルの製品の単価も表示されます。 キャンバス アプリの各参照値は、主キーだけでなく、レコード全体を参照します。

    **更新**関数により、**注文**エンティティに追加したレコードの反映、 **Order Details**エンティティ。 **リセット**関数は、ユーザーが同じ注文のもう 1 つの注文の詳細をより簡単に作成するために、製品、数量、および単位価格データをクリアします。

1. F5 キーを押すし、選択、**追加**アイコン。

    順序には、指定した情報が反映されます。

    > [!div class="mx-imgBorder"]
    > ![注文の詳細を追加するアニメーション](media/northwind-orders-canvas-part3/add-details.gif)

1. (省略可能)別のアイテムを注文に追加します。

1. プレビュー モードを終了するには Esc キーを押します。

## <a name="remove-an-order-detail"></a>注文の詳細を削除します。

1. 画面の中央では、詳細ギャラリーのテンプレートを選択します。

    > [!div class="mx-imgBorder"]
    > ![ギャラリー テンプレートを選択します。](media/northwind-orders-canvas-part3/remove-details-01.png)

1. **挿入**] タブで [**アイコン** > **ごみ箱**:

    > [!div class="mx-imgBorder"]
    > ![ごみ箱アイコンを挿入します。](media/northwind-orders-canvas-part3/remove-details-02.png)

    ギャラリーのテンプレートの左上隅にあるごみ箱のアイコンが表示されます。

    > [!div class="mx-imgBorder"]
    > ![アイコンの既定の場所](media/northwind-orders-canvas-part3/remove-details-03.png)

1. サイズを変更して詳細ギャラリーのテンプレートの右側にあるにごみ箱アイコンを移動し、アイコンの設定**OnSelect**に次の式のプロパティ。

    ```powerapps-dot
    Remove( 'Order Details', ThisItem ); Refresh( Orders )
    ```

    > [!div class="mx-imgBorder"]
    > ![アイコンの OnSelect プロパティを設定します。](media/northwind-orders-canvas-part3/remove-details-04.png)

    この執筆時点で、リレーションシップから直接レコードを削除することはできませんので、 [**削除**](functions/function-remove-removeif.md)関数は、関連エンティティから直接レコードを削除します。 **ThisItem**ごみ箱のアイコンが表示される詳細ギャラリーで同じレコードからを削除するレコードを指定します。

    操作が、キャッシュされたデータを使用する、もう一度、**更新**関数は、通知、**注文**そのアプリは変更がその関連エンティティのいずれかのエンティティ。

1. プレビュー モードを開き、それぞれの横にあるごみ箱アイコンを選択します。 f5 キーを押して**Order Details** 、注文から削除するレコード。

1. Try を追加して、注文からさまざまな注文の詳細を削除する:

    > [!div class="mx-imgBorder"]
    > ![アニメーションを追加して、注文の詳細を削除します。](media/northwind-orders-canvas-part3/remove-details.gif)

## <a name="in-conclusion"></a>まとめ

要約すると、注文の詳細とコントロールの追加と、アプリでの注文の詳細の削除を表示するもう 1 つのギャラリーを追加します。 これらの要素を使用しました。

- 一対多のリレーションシップを介して注文ギャラリーへのリンクされた 2 番目のギャラリー コントロール。**Gallery2.Items** = `Gallery1.Selected.'Order Details'`
- 多対一のリレーションシップ、 **Order Details**エンティティを**製品を注文**エンティティ:`ThisItem.Product.'Product Name'`と `ThisItem.Product.Picture`
- **選択肢**製品の一覧を取得します。 `Choices( 'Order Details'.Product' )`
- **選択**関連するレコードを完全な多対一としてコンボ ボックスのプロパティ:`ComboBox1.Selected.Picture`と `ComboBox1.Selected.'List Price'`
- **パッチ**関数を作成する、 **Order Details**レコード。 `Patch( 'Order Details', Defaults( 'Order Details' ), ... )`
- **削除**を削除する関数、 **Order Details**レコード。 `Remove( 'Order Details', ThisItem )`

この一連のトピックが Common Data Service のリレーションシップを使用しての簡単なチュートリアルをされているし、説明を目的としてオプションでキャンバス アプリで設定。 運用環境にすべてのアプリをリリースする前に、フィールドの検証、エラー処理、およびその他の多くの要因を検討してください。

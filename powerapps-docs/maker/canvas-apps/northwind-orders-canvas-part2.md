---
title: キャンバス アプリで概要フォームを作成 |Microsoft Docs
description: Northwind traders 社のデータを管理するキャンバス アプリの概要フォームを作成します。
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
ms.openlocfilehash: 5c40cb030241d142a2ee2a68d32f7fb839a350ff
ms.sourcegitcommit: 55bc11ac6a964f22301c9fdadb06ee34e1399f83
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66805920"
---
# <a name="create-a-summary-form-in-a-canvas-app"></a>キャンバス アプリで概要フォームを作成します。

Northwind Traders データベース内の架空のデータを管理するためのキャンバス アプリで概要フォームを作成するための手順に従います。 このトピックでは、Common Data Service 内のリレーショナル データにビジネス アプリを構築する方法を説明するシリーズの一部です。 最良の結果をこの順序でこれらのトピックを詳細します。

1. [ギャラリーを作成する順序](northwind-orders-canvas-part1.md)します。
2. 概要フォームを作成する (**このトピックの「** ).
3. [ギャラリーを作成する詳細](northwind-orders-canvas-part3.md)します。

> [!div class="mx-imgBorder"]
> ![画面領域の定義](media/northwind-orders-canvas-part1/orders-parts.png)

## <a name="prerequisites"></a>前提条件

1. [Northwind Traders データベースとアプリ インストール](northwind-install.md)します。
1. レビュー、[キャンバス アプリの概要](northwind-orders-canvas-overview.md)Northwind traders 社にします。
1. [注文のギャラリーを作成](northwind-orders-canvas-part1.md)自分自身、またはオープン、 **Northwind の Orders (キャンバス) - パート 2 の開始**アプリで、既にそのギャラリーが含まれています。

## <a name="add-a-title-bar"></a>タイトル バーを追加する

アプリの上部にタイトル バーには、このトピックの最後で、動作設定ボタンを保持するを作成します。

1. **ツリー ビュー**ペインで、 **Screen1**順序ギャラリーにコントロールを誤って追加しないことを確認します。

    > [!div class="mx-imgBorder"]
    > ![ツリー ビュー ウィンドウで、Screen1 を選択します。](media/northwind-orders-canvas-part2/titlebar-01.png)

1. **挿入**] タブで [**ラベル**を挿入する、 [**ラベル**](controls/control-text-box.md)コントロール。

    > [!div class="mx-imgBorder"]
    > ![ラベルを挿入します。](media/northwind-orders-canvas-part2/titlebar-02.png)

    新しいラベルは、ギャラリーの上部に 1 回のみ表示されます。 ギャラリーの項目ごとに表示される場合、ラベルの最初のインスタンスを削除ことを確認して、画面 (ように、前の手順について説明します) が選択されて、ラベルをもう一度挿入します。

1. 移動し、新しい画面の上部にまたがるラベルのサイズを変更します。

    > [!div class="mx-imgBorder"]
    > ![移動して、ラベルのサイズを変更します。](media/northwind-orders-canvas-part2/titlebar-03.png)

1. ラベルのテキストをダブルクリックし、入力**Northwind Orders**します。

    代わりに、変更、**テキスト**同じ結果を実現するために、数式バーでのプロパティ。

    > [!div class="mx-imgBorder"]
    > ![タイトル バーにテキストを変更します。](media/northwind-orders-canvas-part2/titlebar-04.png)

1. **ホーム** タブで、ラベルの書式を設定します。
    - 24 ポイントのフォント サイズを増やします。
    - テキストを太字にします。
    - テキストを白にします。
    - 中央揃えで表示します。
    - バック グラウンドに濃い青色の塗りつぶしを追加します。

    > [!div class="mx-imgBorder"]
    > ![[ホーム] タブで書式設定オプション](media/northwind-orders-canvas-part2/titlebar-05.png)

## <a name="add-an-edit-form-control"></a>編集フォーム コントロールを追加します。

このセクションでは、ユーザーがギャラリーで選択した任意の順序の概要を表示するコントロールを追加します。

1. **挿入** タブで、挿入、 [**編集フォーム**](controls/control-form-detail.md)コントロール。

    > [!div class="mx-imgBorder"]
    > ![編集フォーム コントロールを追加します。](media/northwind-orders-canvas-part2/form-01.png)

    既定では、フォームに表示される左上隅にある、他のコントロールがしづらくなるを検索します。

    > [!div class="mx-imgBorder"]
    > ![既定の場所でコントロールをフォームを編集します。](media/northwind-orders-canvas-part2/form-02.png)

1. 移動し、タイトル バーの下の画面の右上隅をカバーするフォームのサイズを変更します。

    > [!div class="mx-imgBorder"]
    > ![移動および編集フォーム コントロールをサイズ変更](media/northwind-orders-canvas-part2/form-03.png)

1. 数式バーで設定、 **DataSource**この値をフォームのプロパティ。

    ```powerapps-dot
    Orders
    ```

    > [!div class="mx-imgBorder"]
    > ![編集フォーム コントロールの DataSource プロパティを設定します。](media/northwind-orders-canvas-part2/form-04.png)

    同じプロパティを設定することができます、**プロパティ**アプローチ不要なフィールドをフォームに追加することが、右端で、タブします。 数式バーを使用する場合、フォームは空のままです。

## <a name="add-and-arrange-fields"></a>追加して、フィールドの配置

1. **プロパティ**右端近くにある、タブ**フィールドを編集**を開く、**フィールド**ウィンドウ。

    > [!div class="mx-imgBorder"]
    > ![[フィールド] ウィンドウを開く](media/northwind-orders-canvas-part2/form-05.png)

1. **フィールド**ペインで、**フィールドの追加**のチェック ボックスをクリックして、**顧客**と**従業員**フィールド。

    > [!div class="mx-imgBorder"]
    > ![編集フォーム コントロールに顧客および従業員のフィールドを追加します。](media/northwind-orders-canvas-part2/form-06.png)

1. これらのフィールドが表示し、チェック ボックスをオンにされるまでスクロールします。

    - **備考**
    - **Order Date**
    - **注文番号**
    - **注文の状態**
    - **有料の日付**

    > [!div class="mx-imgBorder"]
    > ![編集フォーム コントロールに 5 つのフィールドを追加します。](media/northwind-orders-canvas-part2/form-07.png)

1. 下部にある、**フィールド**ペインで、**追加**を閉じて、**フィールド**ウィンドウ。

    フォームは、7 つのフィールドを示しています。

    > [!div class="mx-imgBorder"]
    > ![編集フォーム コントロールには、7 つのフィールドが表示されます。](media/northwind-orders-canvas-part2/form-08.png)

    > [!NOTE]
    > 任意のフィールドには、赤いエラー アイコンが表示される場合はデータは、ソースから取得されたときに問題が発生した可能性があります。 エラーを解決するには、データを更新します。
    >
    > 1. **[ビュー]** タブで **[データソース]** を選択します。
    > 1. **データ**ペインで、**データソース**します。
    > 1. 横に**注文**、省略記号 (...) を選択して、選択**更新**を閉じて、**データ**ウィンドウ。
    >
    > 確認して、顧客または従業員名コンボ ボックスでは、エラーが引き続き表示される場合、**プライマリ テキスト**と**SearchField**の各ボックスを選択し、開く、**データ**ウィンドウです。 [Customer] ボックスの両方のフィールドを設定する必要があります**nwind_company**します。 [従業員] ボックスの両方のフィールドを設定する必要があります**nwind_lastname**します。

1. 選択されているフォームで、フォーム内の列数 3 からに変更で 12、**プロパティ**右端近くにあるタブ。

    この手順では、フィールドを配置すると、柔軟性が追加されます。

    > [!div class="mx-imgBorder"]
    > ![編集フォーム コントロール内の列の数を変更し、](media/northwind-orders-canvas-part2/form-08b.png)

    多くの UI の設計は、1、2、3、4、6、および 12 コントロールの行に対応することに均等にできるため、12 列のレイアウトに依存します。 このトピックでは、1、2、または 4 つのコントロールを含む行を作成します。

1. 移動し、各行が指定した順序でこれらのデータ カードが含まれるように、他のコントロールと同様のハンドルをドラッグして、フィールドのサイズを変更します。

    - 最初の行。**Order Number**、 **Order Status**、 **Order Date**、および**支払日**
    - 2 番目の行。**顧客**と**従業員**
    - 3 番目の行。**備考**

    > [!NOTE]
    > 拡大変換を簡単に見つけることがあります、**ノート**、**顧客**、および**従業員**データ カードに配置する前にします。

    > [!div class="mx-imgBorder"]
    > ![移動して、フィールドのサイズ変更](media/northwind-orders-canvas-part2/form-rearrange.gif)

    フォームのフィールドを配置する方法の詳細については:[キャンバス アプリのデータ フォームのレイアウトについて](working-with-form-layout.md)します。

## <a name="hide-time-controls"></a>時間コントロールを非表示にします。

この例では、ユーザーの注意をそらす可能性そのレベルの粒度のため、日付フィールドの時間部分を必要はありません。 それらを削除すると場合、日付の値を更新またはデータ カード内の別のコントロールの位置を決定するには、そのコントロールに依存する数式で問題が発生する可能性があります。 代わりに、時間コントロールを非表示を設定します、 **Visible**プロパティ。

1. **ツリー ビュー**ペインで、 **Order Date**データ カード。

    カードは別の名前を必要がありますが、含まれている**Order Date**します。

1. Shift キーを押したまま、hour、minute、および区切り記号のコロンのコントロールを選択、 **Order Date**データ カード。

    > [!div class="mx-imgBorder"]
    > ![Order Date カードで時間コントロールを選択します。](media/northwind-orders-canvas-part2/form-09.png)

1. コントロールの設定**Visible**プロパティを**false**します。

    選択したコントロールすべてフォームから非表示になります。

    > [!div class="mx-imgBorder"]
    > ![Visible プロパティを false に設定します。](media/northwind-orders-canvas-part2/form-10.png)

1. サイズ変更、 [**日付選択カレンダー** ](controls/control-date-picker.md)完全な日付を表示するコントロール。

    > [!div class="mx-imgBorder"]
    > ![日付の選択コントロールのサイズを変更します。](media/northwind-orders-canvas-part2/form-11.png)

    次の最後のいくつかの手順を繰り返しますが、**有料日付**フィールド。

1. **ツリー ビュー**ウィンドウで、時間でコントロールを選択、**有料日付**データ カード。

    > [!div class="mx-imgBorder"]
    > ![有料の日付のカードで時のコントロールを選択します。](media/northwind-orders-canvas-part2/form-12.png)

1. 選択したコントロールの設定**Visible**プロパティを**false**:

    > [!div class="mx-imgBorder"]
    > ![Visible プロパティを false に設定します。](media/northwind-orders-canvas-part2/form-13.png)

1. 日付の選択のサイズを変更、**支払日**カード。

    > [!div class="mx-imgBorder"]
    > ![日付の選択コントロールのサイズを変更します。](media/northwind-orders-canvas-part2/form-14.png)

## <a name="connect-the-order-gallery"></a>注文のギャラリーを接続します。

1. **ツリー ビュー**ウィンドウで、注文ギャラリーの名前をより簡単に検索するためのフォームを折りたたむし、次に、必要に応じて、名前を変更する**Gallery1**します。

1. 設定の概要、フォームの**項目**に次の式のプロパティ。

    ```powerapps-dot
    Gallery1.Selected
    ```

    > [!div class="mx-imgBorder"]
    > ![フォームの Item プロパティを設定します。](media/northwind-orders-canvas-part2/form-15.png)

    フォームは、一覧内のアプリのユーザーの選択順序の概要を示しています。

    > [!div class="mx-imgBorder"]
    > ![フォームにその概要を表示する一覧で、注文を選択します](media/northwind-orders-canvas-part2/form-select.gif)

## <a name="replace-a-data-card"></a>データ カードを置換します。

**注文番号**Common Data Service のレコードを作成するときに自動的に割り当てます識別子です。 このフィールドには、 [**テキスト入力**](controls/control-text-input.md)既定では、コントロールが、ユーザーは、このフィールドを編集できないように、ラベルで置換します。

1. フォームを選択して、**フィールドを編集**で、**プロパティ**右端で、タブを選び、 **Order number**フィールド。

    > [!div class="mx-imgBorder"]
    > ![順序番号フィールドを選択します。](media/northwind-orders-canvas-part2/alt-01.png)

1. 開く、**コントロール型**一覧。

    > [!div class="mx-imgBorder"]
    > ![開く、* * * * 型リスト コントロール](media/northwind-orders-canvas-part2/alt-02.png)

1. 選択、**テキスト表示**データ カード。

    > [!div class="mx-imgBorder"]
    > ![選択、* * * * テキスト データ カードの表示](media/northwind-orders-canvas-part2/alt-02b.png)

1. 閉じる、**フィールド**ウィンドウ。

    ユーザーは、順序番号を変更不要になったことができます。

    > [!div class="mx-imgBorder"]
    > ![順序番号は読み取り専用](media/northwind-orders-canvas-part2/alt-03.png)

1. **ホーム** タブで、フィールドが見つけやすくなるように、注文番号のフォント サイズを 20 のポイントに変更します。

    > [!div class="mx-imgBorder"]
    > ![注文番号のフォント サイズを変更します。](media/northwind-orders-canvas-part2/alt-04.png)

## <a name="use-a-many-to-one-relationship"></a>多対一のリレーションシップを使用してください。

**注文**エンティティと多対一リレーションシップを持つ、**従業員**エンティティ: 各従業員が多数の注文を作成できますが、各注文は、1 つだけの従業員に割り当てることができます。 ユーザーが内の従業員を選択すると、 [**コンボ ボックス**](controls/control-combo-box.md)コントロール、その **選択**プロパティからの従業員のレコード全体を提供する、**従業員**エンティティ。 その結果、構成することができます、 [**イメージ**](controls/control-image.md)コンボ ボックスで、ユーザーの任意の従業員の画像を表示するコントロールを選択します。

1. 選択、**従業員**データ カード。

    > [!div class="mx-imgBorder"]
    > ![従業員データのカードを選択します。](media/northwind-orders-canvas-part2/employee-01.png)

1. **詳細**右端近くにあるタブで、以前に読み取り専用であった数式を編集できるようにデータ カードのロックを解除します。

    > [!div class="mx-imgBorder"]
    > ![従業員データのカードのロックを解除します。](media/northwind-orders-canvas-part2/employee-02.png)

1. データ カードでは、社員の写真を確保するために、コンボ ボックスの幅を削減します。

    > [!div class="mx-imgBorder"]
    > ![コンボ ボックス コントロールをサイズ変更します。](media/northwind-orders-canvas-part2/employee-03b.png)

1. **挿入**] タブで [**メディア** > **イメージ**:

    > [!div class="mx-imgBorder"]
    > ![イメージを挿入します。](media/northwind-orders-canvas-part2/employee-04.png)

    イメージは、それに合わせて拡張できるデータ カードに表示されます。

    > [!div class="mx-imgBorder"]
    > ![イメージ コントロールで従業員データのカード](media/northwind-orders-canvas-part2/employee-05.png)

1. イメージのサイズし、コンボ ボックスの右側に移動します。

    > [!div class="mx-imgBorder"]
    > ![移動し、イメージ コントロールをサイズ変更](media/northwind-orders-canvas-part2/employee-06.png)

1. 設定、**イメージ**DataCardValue の末尾に数値を置き換えるために必要な場合、次の数式にイメージのプロパティ。

    ```powerapps-dot
    DataCardValue7.Selected.Picture
    ```

    > [!div class="mx-imgBorder"]
    > ![イメージのイメージ プロパティを設定します。](media/northwind-orders-canvas-part2/employee-07.png)

    選択した従業員の画像が表示されます。

1. 確認するコンボ ボックスで、さまざまな従業員、Alt キーを押しながらも、画像を変更します。

    > [!div class="mx-imgBorder"]
    > ![その従業員の画像を表示する従業員を選択します。](media/northwind-orders-canvas-part2/employee-select.gif)

## <a name="add-a-save-icon"></a>追加の保存 アイコン

1. **ツリー ビュー**ペインで、 **Screen1**、し、**挿入** > **アイコン** >  **確認**:

    > [!div class="mx-imgBorder"]
    > ![チェック マーク アイコンを挿入します。](media/northwind-orders-canvas-part2/save-01.png)

    [**確認**](controls/control-shapes-icons.md)アイコンが表示されます、左上隅にある、既定で、他のコントロール可能性がありますが難しく、アイコンを検索します。

    > [!div class="mx-imgBorder"]
    > ![既定の場所でアイコン](media/northwind-orders-canvas-part2/save-02.png)

1. **ホーム** タブで、変更、**色**白、アイコンのサイズを変更、およびタイトル バーの右端近くに移動するアイコンのプロパティ。

    > [!div class="mx-imgBorder"]
    > ![色、サイズ、および保存の場所の構成 アイコン](media/northwind-orders-canvas-part2/save-03.png)

1. **ツリー ビュー**ウィンドウで、フォームの名前があることを確認します。 **Form1**、アイコンの設定と**OnSelect**プロパティをこの式に。

    ```powerapps-dot
    SubmitForm( Form1 )
    ```

    > [!div class="mx-imgBorder"]
    > ![保存アイコンの OnSelect プロパティ](media/northwind-orders-canvas-part2/save-04.png)

    ユーザーが、アイコンを選択すると、 [ **SubmitForm** ](functions/function-form.md)関数は、フォームでの任意の値を変更を収集し、データ ソースに送信します。 ドットは、画面の上部に年 3 月、データが送信され、プロセスが完了したら、注文のギャラリーが変更を反映します。

1. 設定アイコンの**DisplayMode**に次の式のプロパティ。

    ```powerapps-dot
    If( Form1.Unsaved, DisplayMode.Edit, DisplayMode.Disabled )
    ```

    > [!div class="mx-imgBorder"]
    > ![アイコンの DisplayMode プロパティを設定します。](media/northwind-orders-canvas-part2/save-05.png)

    アイコンは無効になりに表示されます、フォームのすべての変更が保存されている場合、 **DisabledColor**、次に設定します。

1. 設定アイコンの**DisabledColor**プロパティをこの値にします。

    ```powerapps-dot
    Gray
    ```

    > [!div class="mx-imgBorder"]
    > ![アイコンの DisabledColor プロパティを設定します。](media/northwind-orders-canvas-part2/save-06.png)

    ユーザーは、無効であるユーザーが別の変更を行うまでは淡色表示されるチェック アイコンを選択して、注文に変更を保存できます。

    > [!div class="mx-imgBorder"]
    > ![変更の保存](media/northwind-orders-canvas-part2/save-submit.gif)

## <a name="add-a-cancel-icon"></a>[キャンセル] アイコンを追加します。

1. **挿入**] タブで [**アイコン** > **キャンセル**:

    > [!div class="mx-imgBorder"]
    > ![[キャンセル] アイコンを追加します。](media/northwind-orders-canvas-part2/save-07.png)

    アイコンが表示されます、左上隅にある、既定で、他のコントロール可能性がありますが難しく、アイコンを検索します。

    > [!div class="mx-imgBorder"]
    > ![既定の場所で [キャンセル] アイコン](media/northwind-orders-canvas-part2/save-08.png)

1. **ホーム**アイコンの変更 タブで、**色**プロパティを白のアイコンのサイズを変更、チェック マーク アイコンの左側に移動します。

    > [!div class="mx-imgBorder"]
    > ![色、サイズ、および [キャンセル] アイコンの場所を変更します。](media/northwind-orders-canvas-part2/save-09.png)

1. 設定は [キャンセル] アイコンの**OnSelect**に次の式のプロパティ。

    ```powerapps-dot
    ResetForm( Form1 )
    ```

    > [!div class="mx-imgBorder"]
    > ![[キャンセル] アイコンの OnSelect プロパティを設定します。](media/northwind-orders-canvas-part2/save-10.png)

    [ **ResetForm** ](functions/function-form.md)関数が元の状態に戻りますフォーム内のすべての変更を破棄します。

1. 設定は [キャンセル] アイコンの**DisplayMode**に次の式のプロパティ。

    ```powerapps-dot
    If( Form1.Unsaved Or Form1.Mode = FormMode.New, DisplayMode.Edit, DisplayMode.Disabled )
    ```

    > [!div class="mx-imgBorder"]
    > ![[キャンセル] アイコンの DisplayMode プロパティを設定します。](media/northwind-orders-canvas-part2/save-11.png)

    この数式は、1 つのチェック マーク アイコンから多少は異なります。 すべての変更が保存されているかは、フォームで、キャンセル アイコンが無効になっている**新規**モードで、次に有効にします。 その場合は、 **ResetForm**新しいレコードを破棄します。

1. 設定は [キャンセル] アイコンの**DisabledColor**プロパティをこの値にします。

    ```powerapps-dot
    Gray
    ```

    > [!div class="mx-imgBorder"]
    > ![DisabledColor プロパティの [キャンセル] アイコンを設定します。](media/northwind-orders-canvas-part2/save-12.png)

    ユーザーが注文に変更をキャンセルでき、チェック、および [キャンセル] アイコンが無効になり、すべての変更が保存されている場合は淡色表示。

    > [!div class="mx-imgBorder"]
    > ![保存して、変更をキャンセルします。](media/northwind-orders-canvas-part2/save-cancel.gif)

## <a name="add-an-add-icon"></a>追加アイコンを追加します。

1. **挿入**] タブで [**アイコン** > **追加**します。

    > [!div class="mx-imgBorder"]
    > ![追加アイコンを挿入します。](media/northwind-orders-canvas-part2/save-13.png)

    **追加**アイコンが表示されます、左上隅で、既定で、他のコントロールがしづらくなるを検索します。

    > [!div class="mx-imgBorder"]
    > ![追加アイコンの既定の場所](media/northwind-orders-canvas-part2/save-14.png)

1. **ホーム**タブで、設定、**色**白、アイコンのサイズを変更し、キャンセル アイコンの左側に移動するには、追加アイコンのプロパティ。

    > [!div class="mx-imgBorder"]
    > ![色、サイズ、および追加アイコンの場所を変更します。](media/northwind-orders-canvas-part2/save-15.png)

1. 設定の追加アイコンの**OnSelect**に次の式のプロパティ。

    ```powerapps-dot
    NewForm( Form1 )
    ```

    > [!div class="mx-imgBorder"]
    > ![追加アイコンの OnSelect プロパティを設定します。](media/northwind-orders-canvas-part2/save-15b.png)

    [ **NewForm** ](functions/function-form.md)関数は、形式で空のレコードを示します。  

1. 設定の追加アイコンの**DisplayMode**に次の式のプロパティ。

    ```powerapps-dot
    If( Form1.Unsaved Or Form1.Mode = FormMode.New, DisplayMode.Disabled, DisplayMode.Edit )
    ```

    > [!div class="mx-imgBorder"]
    > ![DisplayMode プロパティの追加アイコンを設定します。](media/northwind-orders-canvas-part2/save-16.png)

    数式には、これらの条件下で [追加] アイコンが無効にします。

    - ユーザーが変更を行ったがしない保存またはキャンセル、チェックし、[キャンセル] アイコンから反対の動作ですが。
    - ユーザーは、追加アイコンを選択しますは変更しません。

1. 設定の追加アイコンの**DisabledColor**プロパティをこの値にします。

    ```powerapps-dot
    Gray
    ```

    > [!div class="mx-imgBorder"]
    > ![DisabledColor プロパティの追加アイコンを設定します。](media/northwind-orders-canvas-part2/save-17.png)

    ユーザーは、変更を加えない、保存または変更した内容を取り消す場合、注文を作成できます。 (ユーザーがこのアイコンを選択することはできません再び選択が 1 つまたは複数の変更を保存したりそれらの変更をキャンセルするまで)。

    > [!div class="mx-imgBorder"]
    > ![注文を作成します。](media/northwind-orders-canvas-part2/save-new.gif)

> [!NOTE]
> 作成して、注文を保存する場合は、新しい注文を表示する順序ギャラリーで下へスクロールする必要があります。 合計料金は、注文詳細をまだ追加していないため、その必要はありません。

## <a name="add-a-trash-icon"></a>ごみ箱アイコンを追加します。

1. **挿入**] タブで [**アイコン** > **ごみ箱**します。

    > [!div class="mx-imgBorder"]
    > ![ごみ箱アイコンを挿入します。](media/northwind-orders-canvas-part2/save-18.png)

    **ごみ箱**アイコンが表示されます、左上隅で、既定で、他のコントロールがしづらくなるを検索します。

    > [!div class="mx-imgBorder"]
    > ![ごみ箱アイコンの既定の場所](media/northwind-orders-canvas-part2/save-19.png)

1. **ホーム** タブで、変更、ごみ箱アイコンの**色**プロパティを白のアイコンのサイズを変更、追加アイコンの左側に移動します。

    > [!div class="mx-imgBorder"]
    > ![色、サイズ、および、ごみ箱アイコンの場所を変更します。](media/northwind-orders-canvas-part2/save-20.png)

1. ごみ箱アイコンの設定**OnSelect**に次の式のプロパティ。

    ```powerapps-dot
    Remove( Orders, Gallery1.Selected )
    ```

    > [!div class="mx-imgBorder"]
    > ![ごみ箱アイコンの OnSelect プロパティを設定します。](media/northwind-orders-canvas-part2/save-21.png)

    [**削除**](functions/function-remove-removeif.md)関数は、データ ソースからレコードを削除します。 この数式では、関数は、注文ギャラリーで選択されているレコードを削除します。 ごみ箱のアイコンは、フォームは、ユーザーが簡単に数式を削除するレコードを識別するために、レコードの詳細についてを示しているために、概要フォーム (注文のギャラリーとは異なる) に表示されます。

1. ごみ箱アイコンの設定**DisplayMode**に次の式のプロパティ。

    ```powerapps-dot
    If( Form1.Mode = FormMode.New, DisplayMode.Disabled, DisplayMode.Edit )
    ```

    > [!div class="mx-imgBorder"]
    > ![ごみ箱アイコンの DisplayMode プロパティを設定します。](media/northwind-orders-canvas-part2/save-22.png)

    この数式は、ユーザーがレコードを作成する場合、ごみ箱アイコンを無効にします。 ユーザーが、レコードを保存するまで、**削除**関数に削除するレコードがありません。

1. ごみ箱アイコンの設定**DisabledColor**プロパティをこの値にします。

    ```powerapps-dot
    Gray
    ```

    > [!div class="mx-imgBorder"]
    > ![ごみ箱アイコンの DisabledColor プロパティを設定します。](media/northwind-orders-canvas-part2/save-23.png)

    ユーザーは、注文を削除できます。

    > [!div class="mx-imgBorder"]
    > ![注文を削除します。](media/northwind-orders-canvas-part2/save-delete.gif)

## <a name="summary"></a>まとめ

要約をユーザーが表示され、各注文の概要を編集し、これらの要素を使用したフォームが追加されます。

- データを表示するフォームを**注文**エンティティ。**Form1.DataSource =** `Orders`
- 形式と注文のギャラリーの間の接続:**Form1.Item =** `Gallery1.Selected`
- 別のコントロールを**Order number**フィールド。**テキストの表示**
- 従業員の画像を表示する多対一のリレーションシップ、**従業員**データ カード。 `DataCardValue1.Selected.Picture`
- 注文に変更を保存するアイコン: `SubmitForm( Form1 )`
- 注文に変更をキャンセル アイコン: `ResetForm( Form1 )`
- 注文を作成するアイコン: `NewForm( Form1 )`
- 注文を削除するアイコン: `Remove( Orders, Gallery1.Selected )`

## <a name="next-step"></a>次のステップ

次のトピックでは、注文ごとに製品を表示するもう 1 つのギャラリーを追加しますを使用して、詳細な情報を変更します、 [**パッチ**](functions/function-patch.md)関数。

> [!div class="nextstepaction"]
> [詳細のギャラリーを作成します。](northwind-orders-canvas-part3.md)

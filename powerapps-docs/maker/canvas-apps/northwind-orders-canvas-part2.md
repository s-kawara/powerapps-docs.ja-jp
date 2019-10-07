---
title: キャンバスアプリで概要フォームを作成する |Microsoft Docs
description: Northwind Traders のデータを管理するためのキャンバスアプリに概要フォームを作成する
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 04/25/2019
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: d151249caebdb2a6f142943074a409bc626ff662
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "71995860"
---
# <a name="create-a-summary-form-in-a-canvas-app"></a>キャンバスアプリで概要フォームを作成する

Northwind Traders データベースで架空のデータを管理するためのキャンバスアプリで概要フォームを作成する手順について説明します。 このトピックは、Common Data Service でリレーショナルデータに対するビジネスアプリケーションを構築する方法について説明するシリーズの一部です。 最適な結果を得るには、次のトピックを参照してください。

1. [注文ギャラリーを作成](northwind-orders-canvas-part1.md)します。
2. 概要フォームを作成します (**このトピック**)。
3. [詳細ギャラリーを作成](northwind-orders-canvas-part3.md)します。

> [!div class="mx-imgBorder"]
> 画面領域の @no__t 0Definition @ no__t-1

## <a name="prerequisites"></a>前提条件

1. [Northwind Traders データベースとアプリをインストール](northwind-install.md)します。
1. Northwind Traders 用[キャンバスアプリの概要](northwind-orders-canvas-overview.md)を確認します。
1. [注文ギャラリー](northwind-orders-canvas-part1.md)を自分で作成するか、既にそのギャラリーが含まれている**Northwind Orders (キャンバス)-Begin Part 2**アプリを開きます。

## <a name="add-a-title-bar"></a>タイトル バーを追加する

アプリの上部でタイトルバーを作成します。タイトルバーには、このトピックの最後にある操作ボタンが表示されます。

1. **ツリービュー**ペインで、 **[Screen1]** を選択して、誤って注文ギャラリーにコントロールを追加しないようにします。

    > [!div class="mx-imgBorder"]
    > ![Select Screen1 in the Tree view pane @ no__t-1

1. **[挿入]** タブで、 **[ラベル]** を選択して[**ラベル**](controls/control-text-box.md)コントロールを挿入します。

    > [!div class="mx-imgBorder"]
    > ![Insert @ no__t-1 を挿入します。

    新しいラベルは、ギャラリーの上に1回だけ表示されます。 ギャラリーの各項目に表示される場合は、ラベルの最初のインスタンスを削除し、画面が選択されていることを確認し (前の手順で説明)、もう一度ラベルを挿入します。

1. 画面の上部に表示されるように、新しいラベルを移動してサイズを変更します。

    > [!div class="mx-imgBorder"]
    > ![Move @ no__t-1

1. ラベルのテキストをダブルクリックし、「 **Northwind Orders**」と入力します。

    別の方法として、数式バーの**Text**プロパティを変更して、同じ結果を得ることもできます。

    > [!div class="mx-imgBorder"]
    > ![Change バーのテキストを変更する @ no__t-1

1. **[ホーム]** タブで、次のようにラベルの書式を設定します。
    - フォントサイズを24ポイントに増やします。
    - テキストを太字にします。
    - テキストを白にします。
    - テキストを中央揃えにします。
    - 背景に濃い青の塗りつぶしを追加します。

    > [!div class="mx-imgBorder"]
    > [ホーム] タブの @no__t 0 の書式設定オプション @ no__t-1

## <a name="add-an-edit-form-control"></a>編集フォームコントロールを追加する

このセクションでは、ユーザーがギャラリーで選択した任意の順序の概要を表示するコントロールを追加します。

1. **[挿入]** タブで、次のように[**編集フォーム**](controls/control-form-detail.md)コントロールを挿入します。

    > [!div class="mx-imgBorder"]
    > ![Add form コントロールを追加する @ no__t-1

    既定では、フォームが左上隅に表示され、他のコントロールが見つけづらくなる可能性があります。

    > [!div class="mx-imgBorder"]
    > 既定の場所 @ no__t で @no__t 0Edit フォームコントロール

1. フォームを移動してサイズを変更すると、タイトルバーの下に画面の右上隅が表示されます。

    > [!div class="mx-imgBorder"]
    > ![Move フォームコントロールの移動とサイズ変更 @ no__t-1

1. 数式バーで、フォームの**DataSource**プロパティを次の値に設定します。

    ```powerapps-dot
    Orders
    ```

    > [!div class="mx-imgBorder"]
    > ![Set form コントロール @ no__t-1 の DataSource プロパティを設定します。

    右側の **[プロパティ]** タブでも同じプロパティを設定できますが、この方法を使用すると、不要なフィールドがフォームに追加されます。 数式バーを使用すると、フォームは空のままになります。

## <a name="add-and-arrange-fields"></a>フィールドの追加と配置

1. 右端の近くにある **[プロパティ]** タブで、 **[フィールドの編集]** を選択して **[フィールド]** ウィンドウを開きます。

    > [!div class="mx-imgBorder"]
    > ![Open フィールド] ウィンドウを開きます。 @ no__t-1

1. **[フィールド]** ウィンドウで **[フィールドの追加]** を選択し、 **[Customer]** および **[Employee]** フィールドのチェックボックスをオンにします。

    > [!div class="mx-imgBorder"]
    > ![Add フィールドと Employee フィールドを編集フォームコントロール @ no__t-1 に追加します。

1. これらのフィールドが表示されるまで下にスクロールし、チェックボックスをオンにします。

    - **備考**
    - **注文日**
    - **注文番号**
    - **注文の状態**
    - **支払日**

    > [!div class="mx-imgBorder"]
    > ![Add form コントロール @ no__t-1 に5つのフィールドを追加します。

1. **フィールド**ウィンドウの下部にある **[追加]** を選択し、 **[フィールド]** ウィンドウを閉じます。

    このフォームには、7つのフィールドが表示されます。

    > [!div class="mx-imgBorder"]
    > @no__t 0Edit フォームコントロールには、7つのフィールド @ no__t-1 が表示されます。

    > [!NOTE]
    > いずれかのフィールドに赤色のエラーアイコンが表示されている場合は、データがソースから取り出されたときに問題が発生した可能性があります。 このエラーを解決するには、データを更新します。
    >
    > 1. **[ビュー]** タブで **[データソース]** を選択します。
    > 1. **データ**ペインで **[データソース]** を選択します。
    > 1. **[Orders]** の横にある省略記号 (...) を選択し、 **[更新]** を選択して、**データ**ペインを閉じます。
    >
    > 顧客名または従業員名のコンボボックスに引き続きエラーが表示される場合は、各ボックスの**プライマリテキスト**と**searchfield**を選択し、**データ**ペインを開きます。 [Customer] ボックスでは、両方のフィールドを**nwind_company**に設定する必要があります。 [Employee] ボックスでは、両方のフィールドを**nwind_lastname**に設定する必要があります。

1. フォームを選択した状態で、右端の近くにある **[プロパティ]** タブで、フォームの列の数を3から12に変更します。

    この手順では、フィールドを配置する際の柔軟性が向上します。

    > [!div class="mx-imgBorder"]
    > ![Change フォームコントロールの列数 @ no__t-1

    多くの UI デザインは、1、2、3、4、6、12の各コントロールの行に均等に対応できるため、12列のレイアウトに依存しています。 このトピックでは、1、2、または4つのコントロールを含む行を作成します。

1. 他のコントロールと同様にハンドルをドラッグして、フィールドの移動とサイズ変更を行います。各行には、これらのデータカードが指定した順序で含まれます。

    - 最初の行:**注文番号**、**注文の状態**、**注文日**、および**支払日**
    - 2番目の行:**顧客**と**従業員**
    - 3番目の行:**備考**

    > [!NOTE]
    > **メモ**、**顧客**、および**従業員**のデータカードを配置する前に拡張する方が簡単な場合があります。

    > [!div class="mx-imgBorder"]
    > @no__t、フィールドの移動とサイズ変更 @ no__t-1

    フォームでフィールドを配置する方法の詳細については、次を参照してください。[キャンバスアプリのデータフォームレイアウトについて](working-with-form-layout.md)説明します。

## <a name="hide-time-controls"></a>時間コントロールの非表示

この例では、日付フィールドの時間部分は必要ありません。このレベルの粒度によってユーザーがあいまいになる可能性があるためです。 これらのコントロールを削除すると、それらのコントロールに依存する数式で、日付の値を更新したり、データカード内の別のコントロールの位置を決定したりするときに問題が発生する可能性があります。 代わりに、**表示**されるプロパティを設定して、時間コントロールを非表示にします。

1. **[ツリービュー]** ペインで、 **[Order Date]** データカードを選択します。

    カードには名前が異なる場合がありますが、**注文日**が含まれています。

1. Shift キーを押しながら、 **Order Date**データカードの [時]、[分]、および [コロン区切り] の各コントロールを選択します。

    > [!div class="mx-imgBorder"]
    > ![Select Date card @ no__t-1 の時間コントロールを選択します。

1. コントロールの**Visible**プロパティを**false**に設定します。

    選択したコントロールはすべて、次の形式で表示されなくなります。

    > [!div class="mx-imgBorder"]
    > ![Set プロパティを false に設定します。 ](media/northwind-orders-canvas-part2/form-10.png)

1. 日付の[**選択**](controls/control-date-picker.md)コントロールのサイズを変更して、完全な日付を表示します。

    > [!div class="mx-imgBorder"]
    > ![Resize picker コントロールのサイズを変更する @ no__t-1

    次に、 **[有料の日付]** フィールドの最後のいくつかの手順を繰り返します。

1. **[ツリービュー]** ウィンドウで、 **[有料日付]** データカードの時間コントロールを選択します。

    > [!div class="mx-imgBorder"]
    > ![ の有料の日付カードでの時間制御 @ no__t-1

1. 選択したコントロールの**Visible**プロパティを**false**に設定します。

    > [!div class="mx-imgBorder"]
    > ![Set プロパティを false に設定します。 ](media/northwind-orders-canvas-part2/form-13.png)

1. **クレジット**カードの日付の選択のサイズを変更します。

    > [!div class="mx-imgBorder"]
    > ![Resize picker コントロールのサイズを変更する @ no__t-1

## <a name="connect-the-order-gallery"></a>注文ギャラリーに接続する

1. **ツリービュー**ペインで、フォームを折りたたんで、注文ギャラリーの名前を簡単に見つけます。次に、必要に応じて、名前を**gallery1.selected**に変更します。

1. 概要フォームの**Item**プロパティを次の式に設定します。

    ```powerapps-dot
    Gallery1.Selected
    ```

    > [!div class="mx-imgBorder"]
    > ![Set no__t-1 という形式の項目プロパティを設定します。

    このフォームには、アプリのユーザーが一覧で選択した順序の概要が表示されます。

    > [!div class="mx-imgBorder"]
    > ![Select no__t-1 の形式で概要を表示するには、一覧の順序を選択します。

## <a name="replace-a-data-card"></a>データカードを交換する

**注文番号**は、レコードを作成するときに自動的に割り当て Common Data Service れる識別子です。 既定では、このフィールドには[**テキスト入力**](controls/control-text-input.md)コントロールがありますが、ユーザーがこのフィールドを編集できないようにラベルに置き換えることになります。

1. フォームを選択し、右端の **[プロパティ]** タブで **[フィールドの編集]** を選択し、 **[Order number]** フィールドを選択します。

    > [!div class="mx-imgBorder"]
    > ![Select number フィールド @ no__t-1 を選択します。

1. コントロールの**種類**の一覧を開きます。

    > [!div class="mx-imgBorder"]
    > ![Open type * * list @ no__t-1 を開きます。

1. [テキストデータの**表示**] カードを選択します。

    > [!div class="mx-imgBorder"]
    > ![Select * View text * * data card @ no__t-1 を選択します。

1. **[フィールド]** ウィンドウを閉じます。

    ユーザーは、注文番号を変更できなくなります。

    > [!div class="mx-imgBorder"]
    > ![Order number は読み取り専用 @ no__t

1. **[ホーム]** タブで、順序番号のフォントサイズを20ポイントに変更して、フィールドを見つけやすくします。

    > [!div class="mx-imgBorder"]
    > ![Change number のフォントサイズを変更する @ no__t-1

## <a name="use-a-many-to-one-relationship"></a>多対一のリレーションシップを使用する

**Orders**エンティティには**Employees**エンティティとの多対一のリレーションシップがあります。各従業員は多数の注文を作成できますが、各注文は1人の従業員にのみ割り当てることができます。 ユーザーが[**コンボボックス**](controls/control-combo-box.md)コントロールで従業員を選択すると、 **選択し**たプロパティによって、 **Employees**エンティティからの従業員のレコード全体が提供されます。 その結果、ユーザーがコンボボックスで選択した任意の従業員の画像を表示するように[**イメージ**](controls/control-image.md)コントロールを構成できます。

1. [ **Employee** data] カードを選択します。

    > [!div class="mx-imgBorder"]
    > ![Select データカード @ no__t-1 を選択します。

1. 右端の近くにある **[詳細設定**] タブで、データカードのロックを解除して、以前に読み取り専用であった数式を編集できるようにします。

    > [!div class="mx-imgBorder"]
    > ![Unlock data card @ no__t-1 のロックを解除します。

1. データカードで、次のように、コンボボックスの幅を狭くして、従業員の写真用の領域を確保します。

    > [!div class="mx-imgBorder"]
    > ![Resize ボックスコントロールのサイズを変更する @ no__t-1

1. **[挿入]** タブで、[**メディア** > **イメージ**] を選択します。

    > [!div class="mx-imgBorder"]
    > ![Insert @ no__t-1

    画像がデータカードに表示され、それに合わせて拡大されます。

    > [!div class="mx-imgBorder"]
    > ![Employee データカードと Image control @ no__t-1

1. イメージのサイズを変更し、コンボボックスの右側に移動します。

    > [!div class="mx-imgBorder"]
    > ![Move コントロールの移動とサイズ変更 @ no__t-1

1. 画像の**image**プロパティを次の数式に設定します。必要に応じて、Datacシャー値の最後の数値を置き換えます。

    ```powerapps-dot
    DataCardValue7.Selected.Picture
    ```

    > [!div class="mx-imgBorder"]
    > ![Set の Image プロパティを設定する @ no__t-1

    選択した従業員の画像が表示されます。

1. Alt キーを押したまま、コンボボックスで別の従業員を選択して、画像も変更されていることを確認します。

    > [!div class="mx-imgBorder"]
    > ![Select の画像 @ no__t-1 を表示するには、従業員を選択します

## <a name="add-a-save-icon"></a>[保存] アイコンを追加する

1. **ツリービュー**ペインで **[Screen1]** を選択し、@no__t の **[挿入]** を選択**し @no__t-** 5 の**チェック**ボックスをオンにします。

    > [!div class="mx-imgBorder"]
    > ![Insert チェックマークアイコン @ no__t-1

    既定では、[**チェック**](controls/control-shapes-icons.md)アイコンが左上隅に表示されます。他のコントロールでは、アイコンの検索が困難になる場合があります。

    > [!div class="mx-imgBorder"]
    > @no__t 既定の場所 @ no__t-1

1. **[ホーム]** タブで、アイコンの **[色]** プロパティを白に変更し、アイコンのサイズを変更して、タイトルバーの右端近くに移動します。

    > [!div class="mx-imgBorder"]
    > ![Configure アイコン @ no__t-1 の色、サイズ、および場所を構成します。

1. **ツリービュー**ペインで、フォームの名前が**Form1**であることを確認し、アイコンの**onselect**プロパティを次の数式に設定します。

    ```powerapps-dot
    SubmitForm( Form1 )
    ```

    > [!div class="mx-imgBorder"]
    > ![Set アイコンの OnSelect プロパティを設定します @ no__t-1

    ユーザーがアイコンを選択すると、 [**submitform**](functions/function-form.md)関数は、フォーム内の変更された値を収集し、データソースに送信します。 データが送信されると画面の上部に3月のドットが表示され、注文ギャラリーには、プロセスが完了した後の変更が反映されます。

1. アイコンの**DisplayMode**プロパティを次の数式に設定します。

    ```powerapps-dot
    If( Form1.Unsaved, DisplayMode.Edit, DisplayMode.Disabled )
    ```

    > [!div class="mx-imgBorder"]
    > ![Set の DisplayMode プロパティ @ no__t-1 を設定します。

    フォーム内のすべての変更が保存されている場合、アイコンは無効になり、 **DisabledColor**に表示されます。このアイコンは次に設定します。

1. アイコンの**DisabledColor**プロパティを次の値に設定します。

    ```powerapps-dot
    Gray
    ```

    > [!div class="mx-imgBorder"]
    > ![Set の DisabledColor プロパティ @ no__t-1 を設定します。

    ユーザーは、チェックアイコンを選択して、注文への変更を保存できます。このアイコンは、ユーザーが別の変更を行うまで無効になり、淡色表示になります。

    > [!div class="mx-imgBorder"]
    > ![ 保存の変更 @ no__t-1

## <a name="add-a-cancel-icon"></a>[キャンセル] アイコンを追加する

1. **[挿入]** タブで、[**アイコン** > **キャンセル**] を選択します。

    > [!div class="mx-imgBorder"]
    > ![Add cancel アイコン @ no__t-1

    既定では、アイコンが左上隅に表示されます。他のコントロールでは、アイコンの検索が困難になる場合があります。

    > [!div class="mx-imgBorder"]
    > ![Cancel アイコン (既定の場所 @ no__t)

1. **[ホーム]** タブで、アイコンの **[色]** プロパティを白に変更し、アイコンのサイズを変更して、チェックアイコンの左側に移動します。

    > [!div class="mx-imgBorder"]
    > ![Change アイコンの色、サイズ、位置を変更します。 @ no__t-1

1. キャンセルアイコンの**Onselect**プロパティを次の数式に設定します。

    ```powerapps-dot
    ResetForm( Form1 )
    ```

    > [!div class="mx-imgBorder"]
    > ![Set アイコンの OnSelect プロパティ @ no__t-1 を設定します。

    [**Resetform**](functions/function-form.md)関数は、フォーム内のすべての変更を破棄します。これにより、元の状態に戻ります。

1. 取り消しアイコンの**DisplayMode**プロパティを次の数式に設定します。

    ```powerapps-dot
    If( Form1.Unsaved Or Form1.Mode = FormMode.New, DisplayMode.Edit, DisplayMode.Disabled )
    ```

    > [!div class="mx-imgBorder"]
    > ![Set アイコンの DisplayMode プロパティ @ no__t-1 を設定します。

    この数式は、チェックアイコンとは少し異なります。 すべての変更が保存されているか、フォームが**新しい**モードである場合、[キャンセル] アイコンは無効になっています。これは、次に有効にします。 その場合、 **Resetform**は新しいレコードを破棄します。

1. キャンセルアイコンの**DisabledColor**プロパティを次の値に設定します。

    ```powerapps-dot
    Gray
    ```

    > [!div class="mx-imgBorder"]
    > ![Set アイコンの DisabledColor プロパティ @ no__t-1 を設定します。

    ユーザーは注文に対する変更を取り消すことができ、すべての変更が保存されている場合、[確認] および [キャンセル] アイコンは無効になり、淡色表示になります。

    > [!div class="mx-imgBorder"]
    > @no__t による変更の保存と取り消し @ no__t-1

## <a name="add-an-add-icon"></a>追加アイコンを追加する

1. **[挿入]** タブで、[**アイコン**@no__t-**2] を選択します**。

    > [!div class="mx-imgBorder"]
    > @no__t、追加アイコン @ no__t-1 を挿入します。

    既定では、 **[追加]** アイコンが左上隅に表示されます。他のコントロールでは、検索が困難になる場合があります。

    > [!div class="mx-imgBorder"]
    > ![Default アイコン @ no__t-1

1. **ホーム** タブで、追加 アイコンの **色** プロパティを白に設定し、アイコンのサイズを変更して、キャンセル アイコンの左側に移動します。

    > [!div class="mx-imgBorder"]
    > ![Change アイコン @ no__t-1 の色、サイズ、位置を変更します。

1. 追加アイコンの**Onselect**プロパティを次の数式に設定します。

    ```powerapps-dot
    NewForm( Form1 )
    ```

    > [!div class="mx-imgBorder"]
    > ![Set アイコンの OnSelect プロパティ @ no__t-1 を設定します。

    [**NewForm**](functions/function-form.md)関数は、フォームに空のレコードを表示します。  

1. 追加 アイコンの  **DisplayMode** プロパティを次の数式に設定します。

    ```powerapps-dot
    If( Form1.Unsaved Or Form1.Mode = FormMode.New, DisplayMode.Disabled, DisplayMode.Edit )
    ```

    > [!div class="mx-imgBorder"]
    > ![Set アイコンの DisplayMode プロパティ @ no__t-1 を設定します。

    この数式は、次の条件下で [追加] アイコンを無効にします。

    - ユーザーは変更を行いますが、保存もキャンセルもされません。これは、[チェック] アイコンと [キャンセル] アイコンの反対の動作です。
    - ユーザーは [追加] アイコンを選択しますが、変更は行われません。

1. [追加] アイコンの**DisabledColor**プロパティを次の値に設定します。

    ```powerapps-dot
    Gray
    ```

    > [!div class="mx-imgBorder"]
    > ![Set アイコンの DisabledColor プロパティ @ no__t-1 を設定します。

    ユーザーが変更を加えない場合、または変更を保存またはキャンセルする場合は、注文を作成できます。 (ユーザーがこのアイコンを選択した場合、1つまたは複数の変更を行ってから変更を保存またはキャンセルするまで、このアイコンを再度選択することはできません)。

    > [!div class="mx-imgBorder"]
    > ![Create @ no__t-1 を作成します。

> [!NOTE]
> 注文を作成して保存する場合は、注文ギャラリーを下にスクロールして新しい注文を表示しなければならない場合があります。 まだ注文の詳細を追加していないため、合計料金はかかりません。

## <a name="add-a-trash-icon"></a>ごみ箱アイコンを追加する

1. **[挿入]** タブで、[**アイコン** > **ごみ箱**] を選択します。

    > [!div class="mx-imgBorder"]
    > ![Insert 箱を挿入するアイコン @ no__t-1

    既定では、**ごみ箱**アイコンが左上隅に表示されます。他のコントロールでは、検索が困難になる場合があります。

    > [!div class="mx-imgBorder"]
    > ![Default アイコン @ no__t-1

1. **[ホーム]** タブで、ごみ箱アイコンの**Color**プロパティを白に変更し、アイコンのサイズを変更して、[追加] アイコンの左側に移動します。

    > [!div class="mx-imgBorder"]
    > ![Change アイコンの色、サイズ、位置を変更します @ no__t-1

1. ごみ箱アイコンの**Onselect**プロパティを次の数式に設定します。

    ```powerapps-dot
    Remove( Orders, Gallery1.Selected )
    ```

    > [!div class="mx-imgBorder"]
    > ![Set アイコンの OnSelect プロパティ @ no__t-1 を設定します。

    [**Remove**](functions/function-remove-removeif.md)関数は、データソースからレコードを削除します。 この数式では、order ギャラリーで選択したレコードが関数によって削除されます。 フォームにはレコードに関する詳細が表示されるので、[ごみ箱] アイコンは (注文ギャラリーではなく) 概要フォームの近くに表示されるので、ユーザーは、数式によって削除されるレコードをより簡単に識別できます。

1. ごみ箱アイコンの**DisplayMode**プロパティを次の数式に設定します。

    ```powerapps-dot
    If( Form1.Mode = FormMode.New, DisplayMode.Disabled, DisplayMode.Edit )
    ```

    > [!div class="mx-imgBorder"]
    > ![Set アイコンの DisplayMode プロパティ @ no__t-1 を設定します。

    この数式は、ユーザーがレコードを作成している場合にごみ箱アイコンを無効にします。 ユーザーがレコードを保存するまで、**削除関数には削除**するレコードがありません。

1. ごみ箱アイコンの**DisabledColor**プロパティを次の値に設定します。

    ```powerapps-dot
    Gray
    ```

    > [!div class="mx-imgBorder"]
    > ![Set アイコンの DisabledColor プロパティ @ no__t-1 を設定します。

    ユーザーは注文を削除できます。

    > [!div class="mx-imgBorder"]
    > ![ 番目の注文を削除する @ no__t-1

## <a name="summary"></a>まとめ

要約すると、ユーザーが各注文の概要を表示および編集できるフォームを追加し、次の要素を使用しました。

- **Orders**エンティティのデータを表示するフォーム:**Form1. DataSource =** `Orders`
- フォームと注文ギャラリー間の接続:**Form1. Item =** `Gallery1.Selected`
- **Order number**フィールドの代替コントロール:**テキストの表示**
- 従業員の写真を**employee**データカードに表示する多対一のリレーションシップ: `DataCardValue1.Selected.Picture`
- 変更を注文に保存するアイコン: `SubmitForm( Form1 )`
- 順序の変更をキャンセルするアイコン: `ResetForm( Form1 )`
- 注文を作成するためのアイコン: `NewForm( Form1 )`
- 注文を削除するアイコン: `Remove( Orders, Gallery1.Selected )`

## <a name="next-step"></a>次のステップ

次のトピックでは、各注文に製品を表示する別のギャラリーを追加し、 [**Patch**](functions/function-patch.md)関数を使用してそれらの詳細を変更します。

> [!div class="nextstepaction"]
> [詳細ギャラリーを作成する](northwind-orders-canvas-part3.md)

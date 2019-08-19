---
title: キャンバス アプリの項目の一覧を表示する | Microsoft Docs
description: ギャラリーを使用して、キャンバス アプリの項目の一覧を表示し、条件を指定して一覧をフィルター処理します。
author: emcoope-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 09/28/2017
ms.author: emcoope
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: f45948bc16f036669a09ed2c566c60440d24a797
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61528120"
---
# <a name="show-a-list-of-items-in-powerapps"></a>PowerApps の項目の一覧の表示

キャンバス アプリに **[ギャラリー](controls/control-gallery.md)** コントロールを追加して、任意のデータ ソースからの項目の一覧を表示します。 このトピックでは、データ ソースとして Excel を使用します。 **[テキスト入力](controls/control-text-input.md)** コントロールのフィルター条件に一致する項目のみを表示するように**ギャラリー** コントロールを構成して、一覧をフィルター処理します。

## <a name="prerequisites"></a>前提条件

- PowerApps で[コントロールを追加して構成する](add-configure-controls.md)方法について確認します。

- サンプル データを設定するには、次の処理を行います。
    1. [この Excel ファイル](https://az787822.vo.msecnd.net/documentation/get-started-from-data/FlooringEstimates.xlsx)をダウンロードして、チュートリアルのサンプル データを取得します。

    2. Excel ファイルを OneDrive for Business などの[クラウド ストレージ アカウント](connections/cloud-storage-blob-connections.md)にアップロードします。

- 空のアプリを開きます。
    1. [PowerApps にサインインします](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)。

    1. **[自分のアプリを作成する]** で **[キャンバス アプリを一から作成]** を選択します。

    1. アプリに名前を指定し、 **[電話]** を選択し、 **[作成]** を選択します。

    1. **[PowerApps Studio へようこそ]** ダイアログ ボックスが表示されたら、 **[スキップ]** を選択します。

    1. Excel ファイル内の **FlooringEstimates** テーブルへの[接続を追加](add-data-connection.md)します。

## <a name="add-a-gallery-to-a-blank-screen"></a>空の画面にギャラリーを追加します。

1. **挿入** タブで **ギャラリー**、し、**垂直**します。

    ![垂直方向のギャラリーを追加します。](./media/add-gallery/gallery-dropdown.png)

1. **プロパティ**オープンの右側のウィンドウのタブ、**項目**、一覧表示し、 **Flooring Estimates**します。

    ![床材見積もり](./media/add-gallery/select-layout.png)

1. (省略可能) **レイアウト** 一覧で、別のオプションを選択します。

## <a name="add-a-gallery-in-a-screen"></a>画面のギャラリーを追加します。

1. **ホーム** タブで **新しい画面** > **リスト画面** を選択します。

    **ギャラリー** コントロールと検索バーなどの他のコントロールを含む画面が表示されます。

1. ギャラリーの **Items** プロパティを `FlooringEstimates` に設定します。

    **ギャラリー** コントロールに、サンプル データが表示されます。

    ![データの表示](./media/add-gallery/show-data-default.png)

## <a name="add-a-control-to-the-gallery-control"></a>ギャラリー コントロールにコントロールを追加する
その他のカスタマイズを実行する前に、 **ギャラリー** コントロールのレイアウトが目的に最も合致するコントロールであることを確認してください。 そこから、  **ギャラリー** テンプレートを変更して、 **ギャラリー** コントロール内のすべてのデータの表示方法を決定します。

1. **ギャラリー** コントロールの下部付近をクリックまたはタップしてテンプレートを選択し、左上隅にある鉛筆アイコンを選択します。

    ![ギャラリー テンプレートの編集](./media/add-gallery/edit-item.png)

2. テンプレートを選択した状態で、 **[ラベル](controls/control-text-box.md)** コントロールを追加し、テンプレート内の他のコントロールと重ならないように、追加したコントロールを移動し、サイズを変更します。

    ![ラベルの追加](./media/add-gallery/add-text-box.png)

3. ギャラリーを選択し、**編集**横に**フィールド**上、**プロパティ**右側のウィンドウのタブ。

4. この手順の最初の方で追加したラベルを選択して、 **[データ]** ウィンドウに強調表示されたリストを表示します。

    ![ドロップダウン リストの表示](./media/add-gallery/open-dropdown.png)

5. このリストで **[価格]** をクリックまたはタップします。

    **ギャラリー** コントロールに新しい値が表示されます。

    ![最終ギャラリー](./media/add-gallery/final-gallery.png)

## <a name="filter-and-sort-a-gallery"></a>フィルターおよび並べ替えギャラリー
**ギャラリー** コントロールの **[Items](controls/properties-core.md)** プロパティで、表示する項目を指定します。 この手順でベースのフィルター条件に、どのような順序で表示するレコードも決定されるようにプロパティを構成します。

![検索ボックスと並べ替え アイコン](./media/add-gallery/text-search-box.png)

1. **ギャラリー** コントロールの **[Items](controls/properties-core.md)** プロパティを次の数式に設定します。

    ```powerapps-dot
    Sort
        (If
            (IsBlank(TextSearchBox1.Text),
            FlooringEstimates,
            Filter(
                FlooringEstimates,
                TextSearchBox1.Text in Text(Name)
            )
        ),
        Name,
        If(
            SortDescending1,
            SortOrder.Descending,
            SortOrder.Ascending
        )
    )
    ```

    この数式内の関数について詳しくは、「[数式のリファレンス](formula-reference.md)」をご覧ください。

1. 検索ボックスをダブルクリックし、その中に製品名の一部またはすべてを入力します。

    フィルター条件を満たす項目のみが表示されます。

1. Alt キーを押しながらには、1 回以上並べ替えアイコンを選択、並べ替え順序を切り替える。

    レコードは、昇順と降順の製品名に基づいてアルファベット順の順序を切り替えます。

## <a name="highlight-the-selected-item"></a>選択した項目を強調表示する
**ギャラリー** コントロールの **TemplateFill** プロパティをこの例に似た式に設定しますが、必要に応じて異なる色を指定できます。

**If(ThisItem.IsSelected, LightCyan, White)**

## <a name="change-the-default-selection"></a>既定の選択を変更する
**ギャラリー** コントロールの **Default** プロパティを、既定で選択するレコードに設定します。 たとえば、 **FlooringEstimates** データソースの 5 番目の項目を指定できます。

**Last(FirstN(FlooringEstimates, 5))**

この例では、**FlooringEstimates** データ ソースの **Hardwood** カテゴリにある、最初の項目を指定します。

**First(Filter(FlooringEstimates, Category = "Hardwood"))**

## <a name="next-steps"></a>次の手順
[フォーム](working-with-forms.md)と[数式](working-with-formulas.md)を使用する方法について確認しておきます。

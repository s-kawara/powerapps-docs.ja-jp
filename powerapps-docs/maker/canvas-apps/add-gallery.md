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
ms.openlocfilehash: f5daff973e3d6a90c6ca7748e0684a7a68c23226
ms.sourcegitcommit: 90245baddce9d92c3ce85b0537c1ac1cf26bf55a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2019
ms.locfileid: "57799021"
---
# <a name="show-a-list-of-items-in-powerapps"></a>PowerApps の項目の一覧の表示

キャンバス アプリに**[ギャラリー](controls/control-gallery.md)** コントロールを追加して、任意のデータ ソースからの項目の一覧を表示します。 このトピックでは、データ ソースとして Excel を使用します。 **[テキスト入力](controls/control-text-input.md)** コントロールのフィルター条件に一致する項目のみを表示するように**ギャラリー** コントロールを構成して、一覧をフィルター処理します。

## <a name="prerequisites"></a>前提条件

* PowerApps で[コントロールを追加して構成する](add-configure-controls.md)方法について確認します。

* サンプル データを設定するには、次の処理を行います。
    1. [この Excel ファイル](https://az787822.vo.msecnd.net/documentation/get-started-from-data/FlooringEstimates.xlsx)をダウンロードして、チュートリアルのサンプル データを取得します。

    2. Excel ファイルを OneDrive for Business などの[クラウド ストレージ アカウント](connections/cloud-storage-blob-connections.md)にアップロードします。

## <a name="add-a-gallery-control"></a>ギャラリー コントロールを追加する
1. PowerApps を開き、左端近くにある **[新規]** をクリックまたはタップします。

2. **[空のアプリ]** タイルで、**[携帯電話レイアウト]** をクリックまたはタップします。

3. **[PowerApps Studio へようこそ]** ダイアログ ボックスで、**[スキップ]** をクリックまたはタップします。

4. Excel ファイル内の **FlooringEstimates** テーブルへの[接続を追加](add-data-connection.md)します。

5. (省略可能) 既定の画面に**ギャラリー** コントロールを追加します。このためには、**[挿入]** タブをクリックまたはタップするか、**[ギャラリー]** をクリックまたはタップして、空 (空白) の、または既定のコントロール セットを含む**ギャラリー** コントロールをクリックまたはタップします。

    これらのオプションには、水平方向または垂直方向にスクロールする**ギャラリー** コントロールなどがあります。 各項目のコンテンツの量に応じてそのサイズを自動的に調整する**ギャラリー** コントロールを追加することもできます。

    ![ギャラリーを追加する](./media/add-gallery/gallery-dropdown.png)

6. **[ホーム]** タブで、**[新しい画面]** をクリックまたはタップします。

    空の画面、スクロールできる画面、**ギャラリー** コントロールを含む画面、またはフォームを含む画面を追加することができます。

7. **[リスト画面]** をクリックまたはタップして、**ギャラリー** コントロールや、検索バーなどのコントロールを含む画面を追加します。

    > [!NOTE]
   > 新しい画面または既存の画面に**ギャラリー** コントロールを追加するには、**ギャラリー** コントロールの下部付近をクリックまたはタップして選択し、右側のウィンドウで **[FlooringEstimates]** をクリックまたはタップしてから、**[データ]** ウィンドウで別のレイアウトをクリックまたはタップします。 このチュートリアルの場合、既定のレイアウトをそのまま使用します。

    ![ギャラリーのレイアウトを選択する](./media/add-gallery/select-layout.png)

8. 追加した画面で**ギャラリー** コントロールをクリックまたはタップします。

9. 右側のウィンドウの **[プロパティ]** タブで、**[CustomGallerySample]** をクリックまたはタップします。

10. **[データ]** ウィンドウで、**[CustomGallerySample]** をクリックまたはタップしてから、**[FlooringEstimates]** をクリックまたはタップします。

    ![データソースの選択](./media/add-gallery/choose-data.png)

    **ギャラリー** コントロールに、サンプル データが表示されます。

    ![データの表示](./media/add-gallery/show-data-default.png)

    並べ替えと検索は、このトピックの後半で構成します。

## <a name="add-a-control-to-the-gallery-control"></a>ギャラリー コントロールにコントロールを追加する
カスタマイズを行う前に、**ギャラリー** コントロールのレイアウトを決定します。 **ギャラリー** コントロール内のコントロールの最初のセットはテンプレートで、これにより、**ギャラリー** コントロール内のすべてのデータがどのように表示されるかを指定します。

1. **ギャラリー** コントロールの下部付近をクリックまたはタップしてから、左上隅にある鉛筆アイコンをクリックまたはタップして、テンプレートを選択します。

    ![ギャラリー テンプレートの編集](./media/add-gallery/edit-item.png)

2. テンプレートを選択した状態で、**[ラベル](controls/control-text-box.md)** コントロールを追加し、テンプレート内の他のコントロールと重ならないように、追加したコントロールを移動し、サイズを変更します。

    ![ラベルの追加](./media/add-gallery/add-text-box.png)
3. テンプレートを選択し、右側のウィンドウで **[FlooringEstimates]** をクリックまたはタップして、**[データ]** ウィンドウを開きます。

4. この手順の最初の方で追加したラベルを選択して、**[データ]** ウィンドウに強調表示されたリストを表示します。

    ![ドロップダウン リストの表示](./media/add-gallery/open-dropdown.png)

5. このリストで **[価格]** をクリックまたはタップします。

    ![ラベル バインディングの変更](./media/add-gallery/change-binding.png)

    **ギャラリー** コントロールに新しい値が表示されます。

    ![最終ギャラリー](./media/add-gallery/final-gallery.png)

## <a name="filter-the-gallery-control"></a>ギャラリー コントロールをフィルター処理する
**ギャラリー** コントロールの **[Items](controls/properties-core.md)** プロパティで、表示する項目を指定します。 この手順では、製品名に **TextSearchBox1** 内のテキストを含む項目のみが**ギャラリー** コントロールに表示されるように、このプロパティを構成します。

![テキスト検索ボックス](./media/add-gallery/text-search-box.png)

1. **ギャラリー** コントロールの下部付近をクリックまたはタップしてギャラリー コントロールを選択します。

2. **[詳細設定]** タブで、**ギャラリー** コントロールの **[Items](controls/properties-core.md)** プロパティを次の数式に設定します。

    **If(IsBlank(TextSearchBox1.Text), FlooringEstimates, Filter(FlooringEstimates, TextSearchBox1.Text in Text(Name)))**

    この数式内の関数について詳しくは、「[数式のリファレンス](formula-reference.md)」をご覧ください。

3. 検索ボックスに、製品名の一部またはすべてを入力します。

    **ギャラリー** コントロールに、フィルター条件を満たす項目のみが表示されます。

## <a name="sort-the-gallery-control"></a>ギャラリー コントロールを並べ替える
**ギャラリー** コントロールの **[Items](controls/properties-core.md)** プロパティで、項目を表示する順序を指定します。 この手順では、**ImageSortUpDown1** で設定された項目の順序で項目が**ギャラリー** コントロールに表示されるように、このプロパティを構成します。

![並べ替えのイメージ](./media/add-gallery/image-sorting.png)

1. **ギャラリー** コントロールの **[Items](controls/properties-core.md)** プロパティを次の数式に設定します。

    **Sort(If(IsBlank(TextSearchBox1.Text), FlooringEstimates, Filter(FlooringEstimates, TextSearchBox1.Text in Text(Name))), Name, If(SortDescending1, SortOrder.Descending, SortOrder.Ascending))**

2. 並べ替えアイコンを選択して、**ギャラリー** コントロールの並べ替え順序を製品名順に変更します。

**ギャラリー** コントロールの並べ替え*および*フィルター処理を行うには、次のようにします。

* この数式の *DataSource* の 2 つのインスタンスを、使用するデータ ソースの名前に置き換えます。

* *ColumnName* の 2 つのインスタンスを、並べ替えおよびフィルター処理に使用する列の名前に置き換えます。

**Sort(If(IsBlank(TextSearchBox1.Text),** *DataSource*, **Filter(** *DataSource*, **TextSearchBox1.Text in Text(** *ColumnName* **))),** *ColumnName*, **If(SortDescending1, SortOrder.Descending, SortOrder.Ascending))**

## <a name="highlight-the-selected-item"></a>選択した項目を強調表示する
**ギャラリー** コントロールの **TemplateFill** プロパティを、次の例のような式に設定します。

**If(ThisItem.IsSelected, LightCyan, White)**

## <a name="change-the-default-selection"></a>既定の選択を変更する
**ギャラリー** コントロールの **Default** プロパティを、既定で選択するレコードに設定します。 たとえば、**FlooringEstimates** データ ソースの 5 番目の項目を指定します。

**Last(FirstN(FlooringEstimates, 5))**

この例では、**FlooringEstimates** データ ソースの **Hardwood** カテゴリにある、最初の項目を指定します。

**First(Filter(FlooringEstimates, Category = "Hardwood"))**

## <a name="next-steps"></a>次の手順
[フォーム](working-with-forms.md)と[数式](working-with-formulas.md)を使用する方法について確認しておきます。

---
title: コントロールを追加および構成する | Microsoft Docs
description: ツールバー、[プロパティ] タブ、数式バーなどからコントロールを直接追加および構成するための詳細な手順です。
documentationcenter: na
author: aftowen
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: conceptual
ms.component: canvas
ms.date: 07/10/2017
ms.author: anneta
ms.openlocfilehash: 90689d708d5b86d243647a14282c6599e51f7450
ms.sourcegitcommit: 8bd4c700969d0fd42950581e03fd5ccbb5273584
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="add-and-configure-a-control-in-powerapps"></a>PowerApps でコントロールを追加および構成する
アプリへのさまざまな UI 要素の追加や、要素の外観と動作の構成を、ツールバー、**[プロパティ]** タブ、数式バーなどから直接行います。 これらの UI 要素はコントロールと呼ばれ、構成する内容はプロパティと呼ばれます。

## <a name="prerequisites"></a>前提条件
1. PowerApps に[サインアップ](../signup-for-powerapps.md)し、[インストール](http://aka.ms/powerappsinstall)して開きます。その後、サインアップに使用したのと同じ資格情報を入力してサインインします。

2. PowerApps Studio の **[File (ファイル)]** メニュー (画面左側) の **[New (新規)]** をクリックまたはタップします。

    ![[File (ファイル)] メニューの [New (新規)] オプション](./media/add-configure-controls/file-new.png)

3. **[空のアプリ]** タイルで、**[携帯電話レイアウト]** をクリックまたはタップします。

    ![アプリを最初から作成する](./media/add-configure-controls/blank-app.png)

4. クイック ツアーの開始を求められたら、**[Next (次へ)]** をクリックまたはタップし、PowerApps インターフェイスの基本事項について確認します (または、**[Skip (スキップ)]** をクリックまたはタップします)。

    ![クイック ツアーの最初の画面](./media/add-configure-controls/quick-tour.png)

    クイック ツアーは後からいつでも開始できます。右上隅の疑問符アイコンをクリックまたはタップし、**[Take the intro tour (クイック ツアーの開始)]** をクリックまたはタップしてください。

## <a name="add-a-control"></a>コントロールを追加する
ツールバーの **[Insert (挿入)]** タブをクリックまたはタップし、カテゴリをクリックまたはタップし、目的のコントロールをクリックまたはタップすることにより、さまざまなカテゴリにコントロールを追加できます。 ここでは、追加できるコントロールの種類と、コントロールの種類ごとの場所を理解するために、各カテゴリのコントロールを確認します。

**[挿入]** タブで、これらのカテゴリのいずれかをクリックまたはタップした後、追加するコントロールをクリックまたはタップします。

**テキスト**: ラベル、テキスト入力、HTML テキスト、ペン入力<br>
**コントロール**: ボタン、ドロップ ダウン、日付の選択、リスト ボックス、チェック ボックス、ラジオ、トグル、スライダー、評価、タイマー<br>
**ギャラリー**: 縦、横、高さ (伸縮可能)、縦方向 (空)、横方向 (空)、高さ (伸縮可能、空)<br>
**データ テーブル**<br>
**フォーム**: 編集、表示、エンティティ フォーム<br>
**メディア**: 画像、カメラ、バーコード、ビデオ、オーディオ、マイク、画像の追加<br>
**グラフ**: 縦棒グラフ、折れ線グラフ、円グラフ<br>
**[Icons (アイコン)]**

> [!TIP]
> コントロールのためにより多くの領域が必要な場合、[別の画面を追加](add-screen-context-variables.md)します。

## <a name="configure-a-control-directly"></a>コントロールを直接、構成する
この手順では、**ラベル** コントロールを追加および構成しますが、同じ原則の多くを他のコントロールに応用できます。

1. **[挿入]** タブをクリックまたはタップし、**[ラベル]** をクリックまたはタップします。

    ![[Insert (挿入)] タブ](./media/add-configure-controls/insert-text-box.png)

    コントロールを追加するときに、既定で選択されます。 クリックまたはタップすることによって、既存のコントロールを選択することもできます。 コントロールを選択すると、そのコントロールは選択ボックスで囲まれ、選択したコントロールを構成できるよう、UI の他の領域が変化します。 たとえば、**ラベル** コントロールを選択すると、このようになります。

    ![選択されたラベル](./media/add-configure-controls/selected-text-box.png)

    > [!IMPORTANT]
> 別のコントロールまたは画面の空の領域を選択している状態でコントロールを選択すると、最初の要素は選択解除されます。
2. **ラベル** コントロールの幅を狭くするには、選択ボックスの右端にあるハンドルを左にドラッグします  (中央のハンドルは、表示を拡大する場合にのみ表示されます)。

    ![サイズが変更されたラベル](./media/add-configure-controls/shorter-text-box.png)

     後で説明するように、コントロールの **[[Height (高さ)]](controls/properties-size-location.md)**、**[[Width (幅)]](controls/properties-size-location.md)**、または両方のプロパティを変更してサイズを変更することもできます。

3. **ラベル** コントロールを移動するには、選択ボックス自体をドラッグします (または、後で説明するように、**[[X]](controls/properties-size-location.md)**、**[[Y]](controls/properties-size-location.md)**、または両方のプロパティを変更します)。

4. **ラベル** コントロールに表示されるテキストをトリプル クリックして「**Hello, world**」と入力します。

    ![カスタムのテキストが入力されたラベル](./media/add-configure-controls/change-text-directly.png)

     後で説明するように、このコントロールの **[[Text (テキスト)]](controls/properties-core.md)** プロパティを設定してこのテキストを変更することもできます。

## <a name="configure-a-control-from-the-toolbar"></a>ツールバーからコントロールを構成する
ツールバーからコントロールを構成することにより、コントロールを直接構成する場合よりも幅広いオプションを指定できます。

1. **ラベル** コントロールを選択した状態で、ツールバーの **[ホーム]** タブをクリックまたはタップします。

    ![[Home (ホーム)] タブ](./media/add-configure-controls/home-tab.png)

2. **[Fill (塗りつぶし)]** をクリックまたはタップし、アクアマリンなどの色をクリックまたはタップします。

    ![[Fill (塗りつぶし)] オプション](./media/add-configure-controls/fill-option.png)

    **ラベル** コントロールに選択が反映されます。

    ![アクアマリンに塗りつぶされたラベル](./media/add-configure-controls/change-fill.png)

3. フォント ファミリとテキストのサイズを変更します (たとえば、18 ポイントの  Georgia に)。

    ![フォント コントロール](./media/add-configure-controls/font-size.png)

    **ラベル** コントロールに選択が反映されます。

    ![18 ポイント Georgia](./media/add-configure-controls/change-font.png)

4. **[ラベル]** タブをクリックまたはタップし、**[VerticalAlign]** をクリックまたはタップし、**[上]** をクリックまたはタップします。

    ![[Text box (テキスト ボックス)] タブ](./media/add-configure-controls/text-box-tab.png)

    **ラベル** コントロールに選択が反映されます。

    ![テキストをボックスの上端に揃えたラベル](./media/add-configure-controls/change-align.png)

## <a name="configure-a-control-from-the-properties-tab"></a>[プロパティ] タブでコントロールを構成する
**[プロパティ]** タブを使用して、数式を記述することなくコントロールを構成できます。 この手順では、もう 1 つの**ラベル** コントロールを追加および構成しますが、同じ原則の多くを他のコントロールに応用できます。

1. このトピックで前述したように、もう 1 つの**ラベル** コントロールを追加します。

2. 新しいコントロールを選択して、右側のウィンドウにある **[プロパティ]** タブをクリックまたはタップします。

    ![[プロパティ] パネル](./media/add-configure-controls/properties-panel.png)

3. **[テキスト]** ボックスに「**Properties tab**」と入力します。

    ![[プロパティ] パネルのラベル テキスト](./media/add-configure-controls/properties-panel-text.png)

    入力したテキストが**ラベル** コントロールに表示されます。

    ![[プロパティ] パネルのキャンバス テキスト](./media/add-configure-controls/properties-panel-canvas-text.png)

4. **[プロパティ]** パネルの**塗りつぶし**アイコンをクリックまたはタップして、色をクリックまたはタップします。

    ![[プロパティ] パネルの色テキスト](./media/add-configure-controls/properties-panel-color.png)

    **ラベル** コントロールに選択が反映されます。

    ![[プロパティ] パネルのキャンバス色](./media/add-configure-controls/properties-panel-canvas-color.png)

5. [プロパティ] パネルの **Color** プロパティをクリックまたはタップします。

    ![[プロパティ] パネルのプロパティ](./media/add-configure-controls/properties-panel-property.png)

    **Color** プロパティの値が数式バーで強調表示されます。

    ![[プロパティ] パネルのプロパティ式](./media/add-configure-controls/properties-panel-property-expression.png)

6. コントロールをクリックまたはタップしてから [削除] を押し、2 つ目の**ラベル** コントロールを削除します。

## <a name="configure-a-control-in-the-formula-bar"></a>数式バーでコントロールを構成する
数式バーを使用すると、**[プロパティ]** タブまたはツールバーからは直接設定できないプロパティを設定できます。 たとえば、ユーザーがコントロールをクリックまたはタップせずポイントしたときに表示されるヒントを設定できます。 アプリの能力を高める複雑な式を指定することもできます。

これまでの説明の中で行った変更のたびに、構成したコントロールの[プロパティ](reference-properties.md)の値が更新されています。

* コントロールのサイズを変更したときは、コントロールの **[[Width (幅)]](controls/properties-size-location.md)** プロパティを変更しました。
* コントロールを移動したときは、コントロールの **[[X]](controls/properties-size-location.md)** および **[[Y]](controls/properties-size-location.md)** プロパティを変更しました。
* コントロールに表示されるテキストを変更したときは、コントロールの **[[Text (テキスト)]](controls/properties-core.md)** プロパティを変更しました。

コントロールを **[プロパティ]** タブまたはツールバーで直接構成する代わりに、プロパティの一覧でプロパティを選択してから数式バーで値を指定すると、プロパティの値を更新できます。 この方法により、プロパティをアルファベット順に検索したり、より多くの種類の値を指定したりできます。

1. 残りの**ラベル** コントロールを選択して、プロパティ リストの **[[Text]](controls/properties-core.md)** をクリックまたはタップし、数式バーに「**"My Company Name"**」(引用符も含めます) と入力します。

    ![ラベル内のリテラル文字列](./media/add-configure-controls/text-literal.png)

    テキストの文字列を引用符で囲むことで、入力したとおりに文字列が扱われる必要があることを指定します。 プロパティの値を数式に設定することもできます。

2. **ラベル** コントロールを選択した状態で、プロパティの一覧にある **[[Text]](controls/properties-core.md)** をクリックまたはタップし、数式バーに **Today()** と入力します (引用符なし)。

    コントロールは、現在の日付を表示します。

    ![Today 関数](./media/add-configure-controls/today-function.png)

    > [!TIP]
> 日付と時刻を計算できるのに加え、さまざまな方法で[日付と時刻を書式設定](show-text-dates-times.md)できます。

## <a name="configure-two-controls-to-interact-with-each-other"></a>相互作用するように 2 つのコントロールを構成する
この手順では、チェック ボックスを追加した後、チェック ボックスがオンのときにのみ表示されるように既存のラベルを構成します。

1. **[Insert (挿入)]** タブをクリックまたはタップします。

    ![[Insert (挿入)] タブ](./media/add-configure-controls/insert-tab.png)

2. **[Controls (コントロール)]** をクリックまたはタップし、**[Check box (チェック ボックス)]** をクリックまたはタップします。

    ![チェック ボックスを挿入する](./media/add-configure-controls/insert-check-box.png)

3. **ラベル** コントロールの下に表示されるように**チェック ボックス** コントロールを移動し、**チェック ボックス** コントロールの **[[Text]](controls/properties-core.md)** プロパティを設定して、「**Show text**」と表示されるようにします。

    ![チェック ボックスを構成する](./media/add-configure-controls/configure-check-box.png)

4. 引き続き**チェック ボックス** コントロールを選択した状態で、**[プロパティ]** タブの真上にあるコントロール名をクリックまたはタップし、「**MyCheckbox**」と入力します。

    ![チェック ボックスの名前を変更する](./media/add-configure-controls/properties-panel-rename.png)

5. **ラベル** コントロールをクリックまたはタップして選択します。

6. **[プロパティ]** タブで、**[Visible]** プロパティをクリックまたはタップします。

    ![[Visible (表示する)] プロパティ](./media/add-configure-controls/properties-panel-visible-property.png)

7. 数式バーで、「**true**」を削除し、次の式を入力するか貼り付けます。

    **If(MyCheckbox.Value = true, true, false)**

    この **[If 関数](functions/function-if.md)** は、チェック ボックスがオンのときにのみラベルが表示されることを指定します。 チェック ボックスをオフにしたので、**ラベル** コントロールは表示されなくなります (選択ボックスを除いて)。

    ![[Visible (表示する)] の数式](./media/add-configure-controls/visible-formula.png)

8. **チェック ボックス** コントロールをクリックまたはタップして選択ボックスをコントロールに追加し、コントロールをもう一度クリックまたはタップしてチェック マークを追加します。

    **ラベル**が再び表示されます。

    ![チェック ボックスをオンにするとラベルが表示される](./media/add-configure-controls/show-text.png)

9. **ラベル** コントロールを非表示にするには、**チェック ボックス** コントロールをオフにします。

    ![チェック ボックスをオフにするとラベルが非表示になる](./media/add-configure-controls/hide-text.png)

この例は基本的なものですが、単純なものから複雑なものまで、1 つ以上の[数式](formula-reference.md)を構築することによってアプリの動作と外観を構成できます。

## <a name="rename-a-screen-or-a-control"></a>画面またはコントロールの名前を変更する
画面またはコントロールの名前を変更することにより、読みやすく保守しやすい数式を構築できます。

1. 名前を変更する画面またはコントロールをクリックまたはタップします。

2. 右側のウィンドウで (**[プロパティ]** タブの真上にある) コントロール名をクリックまたはタップし、好きな名前を入力します。

    ![チェック ボックスの名前を変更する](./media/add-configure-controls/properties-panel-rename.png)

## <a name="find-and-select-a-screen-or-a-control"></a>画面またはコントロールを検索して選択する
画面またはコントロールが非表示である場合や別のコントロールと重複している場合でも、左側のペインで検索することにより、画面またはコントロールを検索して選択できます。 このペインには、アプリの各画面のサムネイルまたは各画面の階層表示と、各画面に含まれるコントロールが表示されます。

* **サムネイルと階層表示を切り替えるには**、ペインの右上隅にあるアイコンをクリックまたはタップします。

    ![表示の切り替え](./media/add-configure-controls/toggle-view.png)

* **コントロールを検索するには**、1 文字以上の文字を入力すると、入力したテキストを含むコントロール名が強調表示されます。

    検索結果をクリックまたはタップすると、アプリ内でそのコントロールが選択されます。

    ![ツリー ビューでの検索](./media/add-configure-controls/search.png)

* **画面の上下への移動、複製、削除、または名前変更を行うには**、画面を右クリック (あるいは画面の横の省略記号をクリックまたはタップ) して、目的のオプションをクリックまたはタップします。

    ![ツリー ビューのコンテキスト メニュー](./media/add-configure-controls/context.png)

* **コントロールのコピー/貼り付け、削除、または名前変更を行うには**、コントロールを右クリック (あるいはコントロールの横の省略記号をクリックまたはタップ) して、目的のオプションをクリックまたはタップします。

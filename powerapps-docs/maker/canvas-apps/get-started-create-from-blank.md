---
title: アプリを最初から作成する | Microsoft Docs
description: 皆さんの日々の業務を支援するデータの管理アプリを、個々の UI 要素と動作を設定して一から作成します。
services: ''
suite: powerapps
documentationcenter: na
author: AFTOwen
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/16/2016
ms.author: anneta
ms.openlocfilehash: efc965d607198ed6366f3390960ccdf44b2ea210
ms.sourcegitcommit: 078ba325480147e6e4da61e319ed53219f1c5cfc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2018
---
# <a name="create-an-app-from-scratch"></a>アプリを最初から作成する
さまざまなデータ ソースからいずれかを選んで自分だけのアプリをゼロから作成しましょう。必要であればデータ ソースは後から追加できます。 それぞれの UI 要素には、思い描いた目的とワークフローに最適な結果が得られるよう、外観と動作を指定します。 この方法は、[アプリを自動的に生成する](get-started-create-from-data.md)よりもかなり時間がかかりますが、経験豊富なアプリ作成者は、自分のニーズに合わせて最適なアプリを構築することができます。

このチュートリアルの手順では、2 つの画面を持ったアプリを作成します。 1 つは、一連のレコードをユーザーが閲覧するための画面です。

![一連のデータをユーザーがスクロールするための画面](./media/get-started-create-from-blank/first-screen-final.png)

もう 1 つは、ユーザーがレコードを作成したり、レコードのフィールドを更新したり、レコード全体を削除したりするための画面です。

![ユーザーがデータを追加または更新するための画面](./media/get-started-create-from-blank/changescreen-final.png)

## <a name="prerequisites"></a>前提条件
独自の Excel ファイルを使って、このチュートリアルの一般的な概念だけを確認できます。 ただし、Excel ファイル内のデータは、テーブルとして書式設定されている必要があります。 詳細については、「[Excel でテーブルを書式設定する](how-to-excel-tips.md)」をご覧ください。

以下の手順に厳密に従うには、最初に次のサンプル データを使って Excel ファイルを作成します。

1. このデータをコピーし、Excel ファイルに貼り付けます。

   | Start Day | Start Time | Volunteer 1 | Volunteer 2 |
   | --- | --- | --- | --- |
   | Saturday |10am-noon |Vasquez |Kumashiro |
   | Saturday |noon-2pm |Ice |Singhal |
   | Saturday |2pm-4-pm |Myk |Mueller |
   | Sunday |10am-noon |Li |Adams |
   | Sunday |10am-noon |Singh |Morgan |
   | Sunday |10am-noon |Batye |Nguyen |

2. そのデータを **Schedule** という名前のテーブルとして書式設定し、PowerApps が情報を解析できるようにします。

    詳細については、「[Excel でテーブルを書式設定する](how-to-excel-tips.md)」をご覧ください。

3. ファイルを **eventsignup.xls** という名前で保存してから、OneDrive などの[クラウド ストレージ アカウント](connections/cloud-storage-blob-connections.md)にアップロードします。

4. PowerApps を初めて利用する場合:

   * [コントロールを追加してそのプロパティを設定](add-configure-controls.md)する方法を確認します。コントロールの体裁と動作は、そのプロパティによって決まります。
   * [画面を追加して名前を変更](add-screen-context-variables.md)する方法について確認します。

## <a name="create-a-blank-app-and-connect-to-data"></a>空のアプリを作成してデータに接続する
1. PowerApps Studio の **[ファイル]** メニュー (画面左側) の **[新規]** をクリックまたはタップします。

    ![[ファイル] メニューの [新規] オプション](./media/get-started-create-from-blank/file-new.png)

2. **[空のアプリ]** タイルで、**[携帯電話レイアウト]** をクリックまたはタップします。

    ![データからアプリを作成するためのオプション](./media/get-started-create-from-blank/create-from-blank.png)

3. 意思確認のメッセージが表示されたら、クイック ツアーに進んで PowerApps の主な領域を確認します。不要であれば **[Skip (スキップ)]** をクリックまたはタップしてください。

    ![クイック ツアー](./media/get-started-create-from-blank/quick-tour.png)

    クイック ツアーは後からいつでも開始できます。画面左上隅の疑問符アイコンをクリックまたはタップし、**[Take the intro tour (クイック ツアーの開始)]** をクリックしてください。

4. 左側のナビゲーション バーで、右上のアイコンをクリックまたはタップしてサムネイル表示に切り替えます。

    ![表示の切り替え](./media/get-started-create-from-blank/toggle-view.png)

5. 右側のウィンドウで **[データ ソースの追加]** をクリックまたはタップします。

    ![データ ソースの追加](./media/get-started-create-from-blank/add-data-source.png)

6. 次の手順のいずれかを実行します。

   * 既にクラウド ストレージ アカウントへの接続がある場合は、それをクリックまたはタップします。
   * まだクラウド ストレージ アカウントへの接続がない場合は、**[Add Connection (接続の追加)]**、該当するアカウントの種類、**[Connect (接続)]** の順にクリックまたはタップします。資格情報を求められた場合は、必要な情報を入力してください。

7. **[Choose an Excel file (Excel ファイルの選択)]** で **eventsignup.xlsx** を参照してクリックまたはタップします。

    ![使用する Excel ファイルの指定](./media/get-started-create-from-blank/select-excel-file.png)

8. **[Choose a table (テーブルの選択)]** の **[Schedule (スケジュール)]** チェック ボックスをオンにし、**[Connect (接続)]** をクリックまたはタップします。

    ![使用する Excel テーブルの指定](./media/get-started-create-from-blank/select-table.png)

    これまでに追加したデータ ソースは、右側のウィンドウの **[Data sources (データ ソース)]** タブに表示されます。

    ![接続されているデータ ソースの表示](./media/get-started-create-from-blank/data-connect.png)

    このチュートリアルで使用するデータ ソースは 1 つのみですが、後から他のデータ ソースを追加することもできます。

## <a name="show-the-data"></a>データの表示
1. **[ホーム]** タブで、**[新しい画面]** をクリックまたはタップし、**[リスト画面]** をクリックまたはタップします。

    ![見出し、サブタイトル、本文要素から成るレイアウトを追加](./media/get-started-create-from-blank/add-gallery.png)

    画面が追加され、いくつかの既定のコントロールが表示されます (検索ボックスや**[ギャラリー](controls/control-gallery.md)** コントロールなど)。 ギャラリーは、検索ボックスの下の画面全体に広がる領域になります。

2. ギャラリー内の任意の場所 (矢印以外) をクリックまたはタップします (検索ボックスの直下など)。

    ![ギャラリーを選択](./media/get-started-create-from-blank/select-gallery.png)

3. 右側のウィンドウで、**[レイアウト]** リストを開き、タイトル、サブタイトル、および本文のみを表示するオプションをクリックまたはタップします。

    ![ギャラリーを選択](./media/get-started-create-from-blank/select-layout.png)

4. プロパティ一覧で **[Items](controls/properties-core.md)** をクリックまたはタップし、次の式をコピーして、数式バーに貼り付けます。

    **SortByColumns(Search(Schedule, TextSearchBox1.Text, "Volunteer_x0020_1"), "Volunteer_x0020_1", If(SortDescending1, SortOrder.Descending, SortOrder.Ascending))**

    プロパティ リストの場所がわからない場合は、「[コントロールを追加および構成する](add-configure-controls.md)」を参照してください。

    > [!NOTE]
> 名前にスペースが使われている列を含む Excel または SharePoint データ ソースの場合、PowerApps ではスペースを **"\_x0020\_"** として表示します。 この例では、**"Volunteer 1"** 列は数式で **"Volunteer_x0020_1"**のように表示されます。

    このギャラリーには、**Schedule** テーブルからのデータが表示されます。

    ![既定のギャラリーに表示される Schedule データ](./media/get-started-create-from-blank/show-data-default.png)

    このギャラリーは、検索ボックスにユーザーが入力したテキストに基づいてフィルタリングすることができます。 ユーザーが検索ボックスに文字を入力すると、その文字を **Volunteer 1** フィールドに含んでいるレコードだけがギャラリーに表示されます。

    並べ替えボタンが備わっており、**Volunteer 1** 列のデータに基づいてレコードを並べ替えることができます。 そのボタンをユーザーがクリックまたはタップすると、並べ替え順が昇順または降順に切り替わります。

    その数式には、**Sort**、**If**、**IsBlank**、**Filter**、**Text** 関数が含まれます。 これらおよびその他の関数に関する詳細については、[数式の参照](formula-reference.md)をご覧ください、

5. 検索ボックスに **i** と入力し、並べ替えボタンを 1 回 (または奇数回) クリックまたはタップします。

    ギャラリーに、これらの結果が表示されます。

    ![ギャラリーの並べ替えとフィルター処理](./media/get-started-create-from-blank/sort-filter.png)

    詳細情報: **[並べ替え](functions/function-sort.md)**、**[フィルター](functions/function-filter-lookup.md)**、[その他](formula-reference.md)

6. 画面上部の**[ラベル](controls/control-text-box.md)** コントロールをクリックまたはタップして選択します。

    ![タイトル バーの選択](./media/get-started-create-from-blank/select-title-bar.png)

7. プロパティ一覧で **[Text](controls/properties-core.md)** をクリックまたはタップし、次のテキストをコピーして、数式バーに貼り付けます。<br>
   **"View Records"**

    ![タイトル バーの変更](./media/get-started-create-from-blank/change-title-bar.png)

## <a name="create-the-changescreen-and-its-banner"></a>ChangeScreen とそのバナーの作成
1. **Screen1** を削除し、**Screen2** の名前を **ViewScreen**に変更します。

    ![画面の名前変更](./media/get-started-create-from-blank/rename-screen.png)

2. 画面を追加し、**ChangeScreen** という名前に変更します。

    ![画面の追加と名前の変更](./media/get-started-create-from-blank/add-screen.png)

3. **[挿入]** タブの **[テキスト]** をクリックまたはタップし、**[[ラベル]](controls/control-text-box.md)** をクリックまたはタップします。

4. 追加したばかりの**ラベル** コントロールを次のように構成します。

   * その **Text** プロパティを次の数式に設定します。
     <br>**"Change record"**

   * その **Fill** プロパティを次の数式に設定します。
     <br>**RGBA(62, 96, 170, 1)**。

   * その **Color** プロパティを次の数式に設定します。
     <br>**RGBA(255, 255, 255, 1)**

   * その **Align** プロパティを **Center** に設定します。
   * その **X** プロパティを **0** に設定します。

   * その **Width** プロパティを **640** に設定します。
     **ラベル** コントロールに変更が反映されます。

     ![ChangeScreen とバナー](./media/get-started-create-from-blank/change-screen-blank.png)

## <a name="add-and-configure-a-form"></a>フォームの追加と構成
1. **[挿入]** タブの **[フォーム]** をクリックまたはタップし、**[編集]** をクリックまたはタップします。

2. 画面の大部分を覆うようにフォームを移動してサイズを変更します。

    ![フォームを追加する](./media/get-started-create-from-blank/add-form.png)

    既定では、フォームの名前が **Form1** になります。ただし、既にフォームを追加して削除した後である場合は例外です。 その場合は、フォームの名前を **Form1** に変更してください。

3. **Form1** の **[DataSource](controls/control-form-detail.md)** プロパティを **Schedule** に設定します。

4. **Form1** の **Item** プロパティを次の式に設定します。
   <br>**BrowseGallery1.Selected**

5. 右側のウィンドウで、各フィールドのチェックボックスをクリックまたはタップして表示状態にします。

    ![フォーム上にフィールドを表示する](./media/get-started-create-from-blank/schedule-checkbox.png)

6. フォームの下部に表示される **[カスタム カードの追加]** をクリックまたはタップします。

    ![カスタム カードの追加](./media/get-started-create-from-blank/add-custom-card.png)

7. 新しいカードに**[ラベル](controls/control-text-box.md)** コントロールを追加します。

8. 新しいコントロールの **[AutoHeight](controls/control-text-box.md)** プロパティを **true** に設定し、その **[Text](controls/properties-core.md)** プロパティに次の式を設定します。
   <br>**Form1.Error**

    フォームでエラーが発生した場合は、このラベルに表示されます。

9. 左側のナビゲーション バーで **ChangeScreen** のサムネイルをクリックまたはタップして選択します。

10. **[挿入]** タブで、**[アイコン]** をクリックまたはタップし、**戻り矢印**を追加するオプションをクリックまたはタップしてから、画面の左下隅にその矢印を移動します。

11. この矢印の **[OnSelect](controls/properties-core.md)** プロパティに次の式を設定します。

     **ResetForm(Form1);Navigate(ViewScreen,ScreenTransition.None)**

      ユーザーが矢印をクリックまたはタップすると、**[Navigate](functions/function-navigate.md)** 関数によって **ViewScreen** が開きます。

12. フォームの下に **[Button](controls/control-button.md)** コントロールを追加し、その **[Text](controls/properties-core.md)** プロパティに **"Save"** を設定します。

     ![保存ボタンの追加](./media/get-started-create-from-blank/add-save-button.png)

13. ボタンの **[OnSelect](controls/properties-core.md)** プロパティに次の式を設定します。

    **SubmitForm(Form1); If(Form1.ErrorKind = ErrorKind.None, Navigate(ViewScreen, ScreenTransition.None))**

    このボタンをユーザーがクリックまたはタップすると、データ ソースへの変更が **[SubmitForm](functions/function-form.md)** 関数によって保存され、再び **ViewScreen** が表示されます。

14. 画面下部に、もう 1 つボタンを追加して、その **[Text](controls/properties-core.md)** プロパティに **"Remove"** を設定し、さらに **[OnSelect](controls/properties-core.md)** プロパティに次の式を設定します。

    **Remove(Schedule,BrowseGallery1.Selected);<br>If(IsEmpty(Errors(Schedule)),Navigate(ViewScreen,ScreenTransition.None))**

    このボタンをユーザーがクリックまたはタップすると、**[Remove](functions/function-remove-removeif.md)** 関数によってレコードが削除され、再び **ViewScreen** が表示されます。

15. **Remove** ボタンの **[Visible](controls/properties-core.md)** プロパティに次の式を設定します。
    <br>**Form1.Mode=FormMode.Edit**

    ユーザーがレコードを作成するとき、この手順によって **Remove** ボタンが非表示になります。

    完成した **ChangeScreen** の例を次に示します。

    ![完成した ChangeScreen](./media/get-started-create-from-blank/changescreen-final.png)

## <a name="set-navigation-from-viewscreen"></a>ViewScreen からのナビゲーションの設定
1. 左側のナビゲーション バーで **ViewScreen** のサムネイルをクリックまたはタップします。

    ![ViewScreen を開く](./media/get-started-create-from-blank/select-viewscreen.png)

2. ギャラリーの先頭レコードの **[右矢印]** をクリックまたはタップします。

    ![右矢印](./media/get-started-create-from-blank/next-arrow.png)

3. この矢印の **[OnSelect](controls/properties-core.md)** プロパティに次の式を設定します。

    **Navigate(ChangeScreen,ScreenTransition.None)**

4. 右上隅にあるプラス記号のアイコンをクリックまたはタップします。

    ![レコードを追加](./media/get-started-create-from-blank/add-record.png)

5. 選択したアイコンの **[OnSelect](controls/properties-core.md)** プロパティに次の式を設定します。

    **NewForm(Form1);Navigate(ChangeScreen,ScreenTransition.None)**`

     このアイコンをユーザーがクリックまたはタップすると、レコードを作成しやすいように各フィールドが空の状態で **ChangeScreen** が表示されます。

## <a name="run-the-app"></a>アプリの実行
アプリをカスタマイズするときは、このセクションで説明する手順に従い、プレビュー モードでアプリを実行して変更をテストしてください。

1. 左側のナビゲーション バーで一番上のサムネイルをクリックまたはタップし、**[ViewScreen]** を選択します。

    ![ViewScreen を選択](./media/get-started-create-from-blank/select-viewscreen.png)

2. F5 キーを押して (または右上隅の**プレビュー** アイコンをクリックまたはタップして) プレビュー モードを開始します。

    ![プレビュー モードを開始](./media/get-started-create-from-blank/open-preview.png)

3. レコードの右矢印をクリックまたはタップすると、そのレコードの詳細が表示されます。

4. **ChangeScreen** の 1 つ以上のフィールドの情報に変更を加え、**[保存]** をクリックまたはタップして変更を保存するか、または **[削除]** をクリックまたはタップしてレコードを削除します。

5. Esc キーを押して (またはタイトル バーの下にある閉じるアイコンをクリックまたはタップして) プレビュー モードを終了します。

    ![プレビュー モードの終了](./media/get-started-create-from-blank/close-preview.png)

## <a name="next-steps"></a>次の手順
* 他のデバイスから実行できるように、Ctrl + S キーを押してアプリをクラウドに保存する。
* 他のユーザーが実行できるように[アプリを共有](share-app.md)する。
* [ギャラリー](add-gallery.md)、[フォーム](add-form.md)、[式](working-with-formulas.md)についてさらに理解を深める。

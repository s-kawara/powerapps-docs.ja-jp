---
title: Excel アプリを最初から作成する | Microsoft Docs
author: AFTOwen
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 04/23/2018
ms.author: anneta
ms.openlocfilehash: 267480158d7e44afd06962779b98c0468436841a
ms.sourcegitcommit: dfa0e1a7981814e15e6ca4720e2a5f930e859db1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2018
ms.locfileid: "39022610"
---
# <a name="create-an-excel-app-from-scratch"></a>Excel アプリを最初から作成する
Excel データを基にしてテーブルとして書式設定された独自のアプリを最初から作成した後、必要に応じて、他のソースからデータを追加します。 このチュートリアルの手順では、2 つの画面を持ったアプリを作成します。 1 つは、一連のレコードをユーザーが閲覧するための画面です。 もう 1 つは、ユーザーがレコードを作成したり、レコードのフィールドを更新したり、レコード全体を削除したりするための画面です。 この方法は、[アプリを自動的に生成する](get-started-create-from-data.md)よりかなり時間がかかりますが、経験豊富なアプリ作成者は、自分のニーズに合わせて最適なアプリを構築することができます。

## <a name="prerequisites"></a>前提条件
このチュートリアルの手順に厳密に従うには、最初に次のサンプル データを使って Excel ファイルを作成します。

1. このデータをコピーし、Excel ファイルに貼り付けます。

    | StartDay | StartTime | Volunteer | Backup |
    | --- | --- | --- | --- |
    | Saturday |10am-noon |Vasquez |Kumashiro |
    | Saturday |noon-2pm |Ice |Singhal |
    | Saturday |2pm-4-pm |Myk |Mueller |
    | Sunday |10am-noon |Li |Adams |
    | Sunday |10am-noon |Singh |Morgan |
    | Sunday |10am-noon |Batye |Nguyen |

2. そのデータを **Schedule** という名前のテーブルとして書式設定し、PowerApps が情報を解析できるようにします。

    詳細については、「[Excel でテーブルを書式設定する](how-to-excel-tips.md)」をご覧ください。

3. ファイルを **eventsignup.xls** という名前で保存してから、ファイルを閉じ、OneDrive などの[クラウド ストレージ アカウント](connections/cloud-storage-blob-connections.md)にアップロードします。

> [!IMPORTANT]
> 独自の Excel ファイルを使って、このチュートリアルの一般的な概念だけを確認できます。 ただし、Excel ファイル内のデータは、テーブルとして書式設定されている必要があります。 詳細については、「[Excel でテーブルを書式設定する](how-to-excel-tips.md)」をご覧ください。

## <a name="open-a-blank-app"></a>空のアプリを開く
1. [PowerApps](http://web.powerapps.com) にサインインします。

    ![PowerApps ホーム ページ](./media/get-started-create-from-blank/sign-in.png)

    携帯電話や他のデバイス (タブレットなど) 用のアプリを最初から設計できます。 このトピックでは、携帯電話用のアプリの設計について説明します。

1. **[このようなアプリを作成します]** の下で、**[空白から開始]** タイルの上にポインターを移動し、電話アイコンを選んで、**[このアプリを作成]** を選びます。

    ![空白アプリのタイル](./media/get-started-create-from-blank/blank-app.png)

    PowerApps Studio で、携帯電話用の空のアプリが作成されます。

1. **[PowerApps Studio へようこそ]** ダイアログ ボックスが開いたら、**[スキップ]** を選びます。

## <a name="connect-to-data"></a>データに接続する
1. 画面の中央で **[データに接続]** を選びます。

1. **[データ]** ウィンドウで、クラウド ストレージ アカウントへの接続が表示される場合は、それを選びます。 それ以外の場合は、次の手順で接続を追加します。

    1. **[新しい接続]** を選び、お使いのクラウド ストレージ アカウントのタイルを選んで、**[作成]** を選びます。
    2. メッセージが表示されたら、そのアカウントの資格情報を指定します。

1. **[Excel ファイルの選択]** で、**eventsignup** の最初の何文字かを入力するか貼り付けて、一覧をフィルター処理し、アップロードしたファイルを選びます。

1. **[テーブルの選択]** で、**Schedule** のチェック ボックスをオンにして、**[接続]** を選びます。

## <a name="create-the-view-screen"></a>表示画面を作成する

1. **[ホーム]** タブで、**[新しい画面]** の横にある下向き矢印を選んで画面の種類の一覧を開き、**[リスト画面]** を選びます。

    ![リスト画面を追加する](./media/get-started-create-from-blank/add-list-screen.png)

    画面が追加され、いくつかの既定のコントロールが表示されます (検索ボックスや**[ギャラリー](controls/control-gallery.md)** コントロールなど)。 ギャラリーは、検索ボックスの下の画面全体に広がる領域になります。

2. 中央の近くをクリックまたはタップしてギャラリーを選びます。

    ギャラリーの周囲にハンドルの付いた選択ボックスが表示されます。

    ![リスト画面を追加する](./media/get-started-create-from-blank/select-gallery.png)

3. 右側のウィンドウで **[CustomGallerySample]** を選んで **[データ]** ウィンドウを開きます。

    ![[データ] ウィンドウを開く](./media/get-started-create-from-blank/custom-gallery-sample.png)

4. **[データ ソース]** で下向き矢印を選んでアプリのデータ ソースの一覧を開き、**Schedule** を選びます。

    ![データ ソースを選ぶ](./media/get-started-create-from-blank/select-schedule.png)

5. **[レイアウト]** で下向き矢印を選んでレイアウトの一覧を開き、**[タイトル、サブタイトル、本文]** を選びます。

    ![レイアウトを選択する](./media/get-started-create-from-blank/select-layout.png)

6. **[Title2]** で、表示される列を **Backup** から **Volunteer** に変更します。

     ![ラベルの列を変更する](./media/get-started-create-from-blank/change-title2.png)

7. 右上の [閉じる] アイコンを選んで、**[データ]** ウィンドウを閉じます。

    ギャラリーに各ボランティアの名前と、そのボランティアのシフトの日時が表示されます。

    ![ギャラリーの並べ替えられていない Schedule データ](./media/get-started-create-from-blank/show-data-unsorted.png)

8. ギャラリーを選び、プロパティの一覧に **[Items](controls/properties-core.md)** と表示されることを確認します。

    数式バーで示されているように、そのプロパティの値は **Schedule** です。

    ![ギャラリーの並べ替えられていない Schedule データ](./media/get-started-create-from-blank/set-property.png)

9. 次の式をコピーして数式バーに貼り付けることで、**Items** プロパティの値を変更します。

    **SortByColumns(Search(Schedule, TextSearchBox1.Text, "Volunteer"), "Volunteer", If(SortDescending1, SortOrder.Descending, SortOrder.Ascending))**

    ギャラリーにボランティア名のアルファベット順でデータが表示されます。

    ![ギャラリーの並べ替えられた Schedule データ](./media/get-started-create-from-blank/show-data-sorted.png)

    ユーザーは、この式の **SortByColumns** 関数と **Search** 関数に基づいて、ボランティア名でギャラリーを並べ替えたりフィルター処理したりできます。

   - ユーザーが検索ボックスに文字を入力すると、**Volunteer** フィールドにその文字が含まれるレコードだけがギャラリーに表示されます。
   - ユーザーが並べ替えボタンを選ぶと、ギャラリーのレコードは **Volunteer** フィールドの値に基づいて (ユーザーがボタンを選んだ回数に応じて) 昇順または降順に並べ替えられます。

     これらの関数とその他の関数の詳細については、[数式の参照に関するページ](formula-reference.md)をご覧ください、

10. 検索ボックスに「**i**」と入力し、クリックまたはタップして並べ替えボタンを選んでから、もう 1 回 (または、さらに奇数回) ボタンを選びます。

     ギャラリーに、これらの結果が表示されます。

     ![ギャラリーの並べ替えとフィルター処理](./media/get-started-create-from-blank/sort-filter.png)

11. 検索ボックスからすべてのテキストを消去します。

12. 画面上部の**[ラベル](controls/control-text-box.md)** コントロールを選び、**[Title]** を「**View records**」に置き換えます。

     ![タイトル バーの変更](./media/get-started-create-from-blank/change-title-bar.png)

## <a name="create-the-change-screen"></a>変更画面を作成する
1. **[ホーム]** タブで、**[新しい画面]** の横の下向き矢印を選び、**[フォーム画面]** を選びます。

     ![フォーム画面を追加する](./media/get-started-create-from-blank/add-form-screen.png)

1. 追加した画面で、**[データに接続]** を選んで **[データ]** ウィンドウを開き、データ ソースを **Schedule** に設定します。

1. **[フィールド]** で、すべてのチェック ボックスをオンにしてすべてのフィールドをフォームに表示します。

     ![フィールドを表示する](./media/get-started-create-from-blank/show-fields.png)

1. **Volunteer** フィールドを上にドラッグして、フィールドの一覧の先頭に表示されるようにします。

     ![フィールドの順序を変更する](./media/get-started-create-from-blank/reorder-fields.png)

1. フォームを選び、次の式を数式バーに入力するか貼り付けて、その **Item** プロパティに設定します。<br>**BrowseGallery1.Selected**

1. 画面上部の**[ラベル](controls/control-text-box.md)** コントロールを選び、**[Title]** を「**Change records**」に置き換えます。

    ![タイトル バーの変更](./media/get-started-create-from-blank/change-title-bar2.png)

## <a name="delete-and-rename-screens"></a>画面の削除と名前の変更
1. 左のナビゲーション バーで、**Screen1** の省略記号 [...] を選び、**[削除]** を選びます。

    ![画面の削除](./media/get-started-create-from-blank/delete-screen.png)

1. **Screen2** の省略記号 [...] を選んで **[名前の変更]** を選び、「**ViewScreen**」と入力するか貼り付けます。

1. **Screen3** の省略記号 [...] を選んで **[名前の変更]** を選び、「**ChangeScreen**」と入力するか貼り付けます。

## <a name="configure-icons-on-the-view-screen"></a>表示画面のアイコンを構成する
1. **ViewScreen** 画面の上部で、円形の矢印アイコンを選びます。

    ![レコードを追加](./media/get-started-create-from-blank/refresh-icon.png)

1. そのアイコンの **OnSelect** プロパティに次の式を設定します。<br>**Refresh(Schedule)**

    ユーザーがこのアイコンを選ぶと、**Schedule** からのデータが Excel ファイルのデータで更新されます。

    この関数とその他の関数について詳しくは、[数式のリファレンス](formula-reference.md)をご覧ください。

1. **ViewScreen** の右上隅で、プラス アイコンを選びます。

    ![レコードを追加](./media/get-started-create-from-blank/add-record.png)

1. そのアイコンの **OnSelect** プロパティに次の式を設定します。<br>**NewForm(EditForm1);Navigate(ChangeScreen,ScreenTransition.None)**

    このアイコンをユーザーが選ぶと、レコードを作成しやすいように各フィールドが空の状態で **ChangeScreen** が表示されます。

1. ギャラリーの最初のレコードの右向き矢印を選びます。

    ![矢印を選ぶ](./media/get-started-create-from-blank/select-arrow.png)

1. 矢印の **OnSelect** プロパティに次の式を設定します。<br>**EditForm(EditForm1); Navigate(ChangeScreen, ScreenTransition.None)**

    ユーザーがこのアイコンを選ぶと、**ChangeScreen** の各フィールドに選んだレコードのデータが表示され、ユーザーはいっそう簡単にレコードを編集または削除できます。

## <a name="configure-icons-on-the-change-screen"></a>変更画面のアイコンを構成する
1. **ChangeScreen** で、左上隅の "x" アイコンを選びます。

    ![[キャンセル] アイコン](./media/get-started-create-from-blank/cancel-icon.png)

1. そのアイコンの **OnSelect** プロパティに次の式を設定します。<br>**ResetForm(EditForm1);Navigate(ViewScreen, ScreenTransition.None)**

    ユーザーがこのアイコンを選ぶと、ユーザーがこの画面で行ったすべての変更が破棄されて、表示画面が開きます。

1. 右上隅にあるチェックマーク アイコンを選びます。

    ![チェックマーク アイコン](./media/get-started-create-from-blank/checkmark-icon.png)

1. チェックマークの **OnSelect** プロパティに次の式を設定します。<br>**SubmitForm(EditForm1); Navigate(ViewScreen, ScreenTransition.None)**

    ユーザーがこのアイコンを選ぶと、ユーザーがこの画面で行ったすべての変更が保存されて、表示画面が開きます。

1. **[挿入]** タブで **[アイコン]** を選んでから、**ごみ箱**アイコンを選びます。

1. 新しいアイコンの **Color** プロパティを **White** に設定し、新しいアイコンをチェックマーク アイコンの隣に移動します。

    ![[ごみ箱] アイコン](./media/get-started-create-from-blank/trash-icon.png)

1. ごみ箱アイコンの **OnSelect** プロパティに次の式を設定します。<br>**Remove(Schedule, BrowseGallery1.Selected); Navigate(ViewScreen, ScreenTransition.None)**

    ユーザーがこのアイコンを選ぶと、選ばれているレコードがデータ ソースから削除され、表示画面が開きます。

## <a name="test-the-app"></a>アプリケーションをテストする
1. **ViewScreen** を選んだ後、F5 キーを押して (または右上隅の**プレビュー** アイコンを選んで) プレビューを開きます。

    ![プレビュー モードを開始](./media/get-started-create-from-blank/open-preview.png)

1. レコードを追加します。

1. 追加したレコードを更新してから、変更を保存します。

1. 追加したレコードを更新してから、変更を取り消します。

1. 追加したレコードを削除します。

1. Esc キーを押して (または右上隅の閉じるアイコンを選んで)、プレビュー モードを閉じます。

## <a name="next-steps"></a>次の手順
* 他のデバイスから実行できるように、Ctrl + S キーを押してアプリをクラウドに保存する。
* 他のユーザーが実行できるように[アプリを共有](share-app.md)する。
* 標準フォームを作らずにデータを管理できる、**Patch** などの[関数](working-with-formulas.md)について詳しく学習してください。

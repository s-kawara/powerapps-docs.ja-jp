---
title: Common Data Service for Apps を使用してキャンバス アプリを最初から作成する | Microsoft Docs
description: PowerApps で、Common Data Service for Apps のレコードを追加、更新、削除するキャンバス アプリを作成します。
author: AFTOwen
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 03/18/2018
ms.author: anneta
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 710df8899fa11e46a83e4ba670c4081b04fa7bde
ms.sourcegitcommit: c1f58a16f8dcd309a1d5fc4658ca16d82c615994
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/22/2018
ms.locfileid: "51333967"
---
# <a name="create-a-canvas-app-from-scratch-using-common-data-service-for-apps"></a>Common Data Service for Apps を使用してキャンバス アプリを最初から作成する

Common Data Service for Apps に保存されているデータを、標準エンティティ (組み込み)、カスタム エンティティ (組織が作成)、またはその両方を使用して管理するキャンパス アプリを構築します。

Common Data Service からアプリを構築する場合、SharePoint、Dynamics 365、Salesforce などのデータ ソースが利用できるので、PowerApps から接続を作成する必要はありません。 アプリの両方のアクティビティで表示、管理、または使用するエンティティの指定のみが必要です。

## <a name="prerequisites"></a>前提条件

- 新規にアプリを作成する前に、[アプリを生成し](data-platform-create-app.md)、そのアプリの[ギャラリー](customize-layout-sharepoint.md)、[フォーム](customize-forms-sharepoint.md)、[カード](customize-card.md)をカスタマイズして PowerApps の基礎を詳しく理解してください。
- サンプル データを使用してデータベースが作成された[環境に切り替えます](working-with-environments.md)。 適切なライセンスがある場合は、ニーズを満たす[環境を作成する](../../administrator/create-environment.md)ことができます。

## <a name="open-a-blank-app"></a>空のアプリを開く

1. [PowerApps](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) にサインインします。

1. **[Make your own app]\(独自アプリの作成\)** の下で、キャンバス アプリの **[空白から開始]** タイルの上にポインターを移動し、電話アイコン、**[このアプリを作成]** の順にクリックまたはタップします。

    ![空白アプリのタイル](./media/data-platform-create-app-scratch/start-from-blank.png)

    携帯電話やその他のデバイス (タブレットなど) 向けのアプリを新規に設計することができます。このトピックでは、携帯電話のアプリの設計に焦点を当てます。

## <a name="specify-an-entity"></a>エンティティを指定する

1. 画面中央で、**[データへの接続]** をクリックまたはタップし、**[データ]** ウィンドウで、**[Common Data Service]** 接続をクリックまたはタップします。

1. 検索ボックスに、**アカウント**の最初のいくつかの文字を入力するか貼り付けて、エンティティの一覧にフィルターを適用し、**[アカウント]** チェック ボックスをオンにして、**[接続]** をクリックまたはタップします。

    ![アカウントのエンティティを指定する](./media/data-platform-create-app-scratch/cds-connect.png)

1. 右上の [閉じる] アイコンをクリックまたはタップして、**[データ]** ウィンドウを閉じます。

## <a name="add-a-list-screen"></a>リスト画面を追加する

1. **[ホーム]** タブで、**[新しい画面]** の下向き矢印をクリックまたはタップし、**[リスト画面]** をクリックまたはタップします。

    ![リスト画面を追加する](./media/data-platform-create-app-scratch/list-screen.png)

1. 左側のナビゲーション バーで、**TemplateGalleryList1** をクリックまたはタップして選択し、**[項目]** プロパティの値を次の式に設定します。

    `SortByColumns(Search(Accounts, TextSearchBox1.Text, "name"), "name", If(SortDescending1, SortOrder.Descending, SortOrder.Ascending))`

    この数式は次のことを指定します。

   - ギャラリーは、**アカウント** エンティティからのデータを表示する必要があります。
   - ユーザーが並べ替えボタンをクリックまたはタップして並べ替え順序を切り替えるまで、データは昇順で並べ替えられる必要があります。
   - ユーザーが検索バーに 1 つ以上の文字を入力するか貼り付けた場合、ユーザーが指定した文字が名前フィールドに含まれるアカウントのみがリストに表示される必要があります。

     [これらの関数とその他の多くの関数](formula-reference.md)を使用して、アプリの表示と動作の方法を指定できます。

     ![ギャラリーの Items プロパティを設定する](./media/data-platform-create-app-scratch/gallery-items.png)

1. 「[ギャラリーのカスタマイズ](customize-layout-sharepoint.md)」の説明に従って、各アカウントの名前のみが表示されるようにギャラリーのレイアウトを設定し、**参照**という単語が表示されるようにタイトル バーを構成します。

    ![ブラウズ画面](./media/data-platform-create-app-scratch/final-browse.png)

1. 左側のナビゲーション バーで **Screen1** の上にポインターを移動し、省略記号 (...) をクリックまたはタップして、**[削除]** をクリックまたはタップします。

1. 左側のナビゲーション バーで **Screen2** の上にポインターを移動し、省略記号 (...) をクリックまたはタップして、**[名前の変更]** をクリックまたはタップします。

1. 「**BrowseScreen**」を入力または貼り付け、その画面でギャラリーの名前を **BrowseGallery** に変更します。

    ![参照画面ギャラリーの名前を変更する](./media/data-platform-create-app-scratch/rename-browse.png)

## <a name="add-a-form-screen"></a>フォーム画面を追加する

1. 前の手順の最初の手順を繰り返しますが、**リスト画面**の代わりに**フォーム画面**を追加します。

1. 右側のウィンドウの **[詳細設定] タブ**に示すように、フォームの **DataSource** プロパティを **Accounts** に設定し、**Item** プロパティを **BrowseGallery.Selected** に設定します。

    ![フォームのデータ ソースと項目のプロパティを設定する](./media/data-platform-create-app-scratch/form-datasource.png)

1. 右側のウィンドウの **[プロパティ]** タブで、**[アカウント]** をクリックまたはタップして、**[データ]** ウィンドウを開き、次のフィールドのチェックボックスをオンにします。

    - アカウント名
    - 住所 1: 番地 1
    - 住所 1: 市区町村
    - 住所 1: 郵便番号
    - 従業員数
    - 年間売上高

1. タイトル バーの **[テキスト]** プロパティを **[作成/編集]** が表示されるように設定します。

    画面に変更内容が反映されます。

    ![フォームのデータ ソースと項目のプロパティを設定する](./media/data-platform-create-app-scratch/field-list.png)

1. この画面の **FormScreen** の名前を変更します。

## <a name="configure-icons"></a>アイコンを構成する

1. **BrowseScreen** で、画面の上部付近にある円形のアイコンをクリックまたはタップし、**OnSelect** プロパティを次の式に設定します。

    `Refresh(Accounts)`

    ![アイコンを更新する](./media/data-platform-create-app-scratch/refresh-icon.png)

1. プラス記号のアイコンをクリックまたはタップし、**OnSelect** プロパティを次の式に設定します。

    `NewForm(EditForm1); Navigate(FormScreen, ScreenTransition.None)`

    ![[追加] アイコン](./media/data-platform-create-app-scratch/plus-icon.png)

1. 右を指している最初の矢印をクリックまたはタップし、**OnSelect** プロパティを次の式に設定します。

    `EditForm(EditForm1); Navigate(FormScreen, ScreenTransition.None)`

    ![[次へ] アイコン](./media/data-platform-create-app-scratch/next-icon.png)

1. **FormScreen** で、キャンセル アイコンをクリックまたはタップし、**OnSelect** プロパティを次の式に設定します。

    `ResetForm(EditForm1);Navigate(BrowseScreen, ScreenTransition.None)`

    ![[キャンセル] アイコン](./media/data-platform-create-app-scratch/cancel-icon.png)

1. チェックマーク アイコンをクリックまたはタップし、**OnSelect** プロパティを次の式に設定します。

    `SubmitForm(EditForm1); Navigate(BrowseScreen, ScreenTransition.None)`

    ![チェックマーク アイコン](./media/data-platform-create-app-scratch/checkmark-icon.png)

1. **[挿入]** タブで、**[アイコン]** をクリックまたはタップし、**[ごみ箱]** アイコンをクリックまたはタップします。

1. **[ごみ箱]** アイコンの **Color** プロパティを **White** に設定し、**OnSelect** プロパティを次の式に設定します。

    `Remove(Accounts, BrowseGallery.Selected); Navigate(BrowseScreen, ScreenTransition.None)`

    ![[ごみ箱] アイコン](./media/data-platform-create-app-scratch/trash-icon.png)

## <a name="test-the-app"></a>アプリケーションをテストする

1. 左側のナビゲーション バーで、**BrowseScreen** を選択し、F5 キーを押して (または右上隅の再生アイコンをクリックまたはタップして) プレビューを開きます。

    ![プレビューを開く](./media/data-platform-create-app-scratch/open-preview.png)

1. 一覧の昇順と降順の並べ替え順を切り替え、各アカウントの名前の特定の文字によって一覧をフィルター処理します。

1. アカウントを追加し、追加したアカウントを編集し、アカウントを更新して変更をキャンセルし、アカウントを削除します。

## <a name="next-steps"></a>次の手順

- [ソリューションにこのアプリをリンク](add-app-solution.md)することにより、たとえば、別の環境にデプロイしたり、AppSource に発行できるようになります。
- [1 つまたは複数のサンプル アプリを開き](open-and-run-a-sample-app.md)、作成可能なさまざまな種類のアプリを調べます。

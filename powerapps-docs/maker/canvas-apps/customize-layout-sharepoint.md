---
title: ギャラリーのカスタマイズのためのチュートリアル | Microsoft Docs
description: このチュートリアルでは、PowerApps で生成されたアプリのギャラリーを含む、既定の参照画面をカスタマイズします。
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
ms.date: 03/11/2018
ms.author: anneta
ms.openlocfilehash: 30ec6be11b40e01dddfe09cf0ac8af0ed3a8a437
ms.sourcegitcommit: 59785e9e82da8f5bd459dcb5da3d5c18064b0899
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2018
---
# <a name="tutorial-customize-a-gallery-in-powerapps"></a>チュートリアル: PowerApps でのギャラリーのカスタマイズ
このチュートリアルでは、PowerApps で生成されたアプリのギャラリーを含む、既定の参照画面をカスタマイズします。 カスタマイズしなくても、既定のアプリを使用してデータを管理することができますが、次に示す変更を加えるとさらに強力で使いやすくなります。

> [!div class="checklist"]
> * レイアウトを変更する
> * 表示されるデータを変更する
> * フィルター処理および並べ替えの列を設定する
> * フィルター処理および並べ替えをテストする
> * タイトルを変更する
> * スクロールバーを表示する

このチュートリアルでは、[Common Data Service for Apps](../common-data-service/data-platform-intro.md) から生成されたアプリを使用して作業を開始しますが、同じ概念は、SharePoint、Excel、その他のデータ ソースから生成されたアプリに適用されます。 

PowerApps のライセンスを持っていない場合は、[無料でサインアップ](../signup-for-powerapps.md)できます。

## <a name="prerequisites"></a>前提条件
このチュートリアルを開始する前に、Common Data Service for Apps から[アプリを 1 つ生成してください](data-platform-create-app.md)。

## <a name="open-the-generated-app"></a>生成されたアプリを開く
1. [PowerApps](https://web.powerapps.com) にサインインし、左端近くにある **[アプリ]** をクリックまたはタップします。

    ![PowerApps ホーム ページ](./media/customize-layout-sharepoint/sign-in.png)

1. 生成したアプリを見つけ、右端近くにある省略記号アイコン (**...**) をクリックまたはタップします。

    ![アプリの一覧](./media/customize-layout-sharepoint/open-for-edit.png)

1. 表示されるメニューで、アプリを編集するオプションをクリックまたはタップします。 

## <a name="customize-the-gallery"></a>ギャラリーのカスタマイズ
1. 参照画面で、アカウントの一覧の最初の項目を除く任意の項目をクリックまたはタップします。

    この手順では、アカウントの一覧を表示する**ギャラリー** コントロールを選択します。

    ![選択されているギャラリー](./media/customize-layout-sharepoint/select-gallery.png)

1. 右側のウィンドウで、**[データ]** ラベルの右にある、**[アカウント]** をクリックまたはタップします。

    ![**データ** ウィンドウを開く](./media/customize-layout-sharepoint/open-data-pane.png)

1. **[データ]** ウィンドウで、下矢印をクリックまたはタップして、**[レイアウト]** のオプションの一覧を表示します。

    ![レイアウト オプションを表示する](./media/customize-layout-sharepoint/show-layouts.png)

1. オプションの一覧で、タイトルのみを表示するオプションをクリックまたはタップします。

    ![タイトルのみのレイアウトを選択する](./media/customize-layout-sharepoint/choose-layout.png)

1. **[データ]** ウィンドウで、下矢印をクリックまたはタップして、タイトルのオプションの一覧を表示します。

    ![タイトルのみのレイアウトを選択する](./media/customize-layout-sharepoint/show-title-options.png)

1. オプションの一覧で、**[名前]** をクリックまたはタップし、**ギャラリー** コントロールにデータを表示します。

    ![最終ギャラリー](./media/customize-layout-sharepoint/final-gallery.png)


## <a name="set-the-sort-and-search-columns"></a>並べ替え列と検索列の設定
1. 前のセクションの説明に従って**ギャラリー** コントロールを選択します。

    ![ギャラリーを選択](./media/customize-layout-sharepoint/select-gallery-title.png)

2. 左上隅のプロパティ一覧に **Items** が表示されていることを確認します。

    ![Items プロパティ](./media/customize-layout-sharepoint/items-property.png)

    このプロパティの値は数式バーに表示され、ギャラリーのデータ ソースに加え、フィルター列と並べ替え列を判別します。

1. 数式バーで、**emailaddress1** と **name** の両方のインスタンスを置き換え、各インスタンスを囲む二重引用符は保持します。

    数式は、この例と一致する必要があります。

    ![Items プロパティの数式](./media/customize-layout-sharepoint/items-value.png)

    **name** の最初のインスタンスは、ユーザーが一覧をフィルター処理して、ユーザーが検索バーに入力したテキストがアカウント名に含まれるレコードのみを表示できることを指定します。 2 つ目の **name** のインスタンスは、ユーザーがアルファベット順にリストを並べ替えできることを指定します。 これらの関数とその他の関数の詳細については、[数式の参照に関するページ](formula-reference.md)をご覧ください、

## <a name="test-sorting-and-searching"></a>並べ替えと検索のテスト
1. F5 キーを押して (または右上隅の再生ボタンをクリックまたはタップして) プレビュー モードを開始します。

    ![プレビュー モードを開始](./media/customize-layout-sharepoint/open-preview.png)

1. 参照セクションの右上隅にある並べ替えボタンを少なくとも 1 回クリックまたはタップして、アルファベットに基づく表示順を昇順または降順に変更します。

    ![並べ替えボタンのテスト](./media/customize-layout-sharepoint/sort-button.png)

1. [検索] ボックスに、「**k**」と入力し、名前に入力した文字が含まれるアカウントのみを表示します。

    ![検索バーのテスト](./media/customize-layout-sharepoint/test-filter.png)

1. 検索バーからテキストをすべて削除し、Esc キーを押して (または PowerApps のタイトル バーの "*下*" にある閉じるアイコンをクリックまたはタップして) プレビュー モードを終了します。

## <a name="change-the-title-of-the-screen"></a>画面のタイトルの変更
1. 画面のタイトルをクリックまたはタップして選択します。

    ![画面タイトルを選択](./media/customize-layout-sharepoint/select-title.png)

1. プロパティの一覧に **Text** が表示されていることを確認し、数式バーに「**Browse**」と二重引用符で囲んで入力します。

    ![画面タイトルの更新](./media/customize-layout-sharepoint/change-screen-title.png)

    画面に変更内容が反映されます。

    ![新しい画面タイトル](./media/customize-layout-sharepoint/new-screen-title.png)

## <a name="show-a-scroll-bar"></a>スクロールバーを表示する
ユーザーがタッチ画面またはマウス ホイールを使用していない場合、ユーザーがコントロール上にマウス ポインターを置いたときにスクロール バーが表示されるように**ギャラリー** コントロールを構成します。 このように、ユーザーは画面にすべてのアカウントを同時に表示できない場合でも、すべてのアカウントを表示できます。

1. 最初の手順の説明に従って**ギャラリー** コントロールを選択します。

    ![ギャラリーを選択](./media/customize-layout-sharepoint/select-gallery-sorted.png)

1. **[ギャラリー]** タブで、**[スクロール バーを表示]** をクリックまたはタップし、そのプロパティの値が **true** に変更されたことを確認します。 

    ![スクロール バーの表示](./media/customize-layout-sharepoint/show-scrollbar.png)

## <a name="next-steps"></a>次の手順
このチュートリアルでは、生成されたアプリの**ギャラリー** コントロールと既定の参照画面のタイトルをカスタマイズしました。 詳細を表示し、アカウントを作成または更新するための既定の画面をカスタマイズすることもできます。 それらの画面には、**表示フォーム** コントロールと**編集フォーム** コントロールが含まれ、たとえば、表示されるデータの種類と表示の順序を変更できます。

> [!div class="nextstepaction"]
> [フォームをカスタマイズ](customize-forms-sharepoint.md)
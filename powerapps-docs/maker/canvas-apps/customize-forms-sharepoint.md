---
title: キャンバス アプリでフォームをカスタマイズする | Microsoft Docs
description: PowerApps で、キャンバス アプリのフォームに、どのデータを、どのような順番で、どのコントロールに表示するかを指定します。
author: AFTOwen
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 03/17/2018
ms.author: anneta
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 1a6465a00f135489d594bad75b8a25942e05dd25
ms.sourcegitcommit: f84095d964fe1fe5cc5290e5edbee284bd768e1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "58870933"
---
# <a name="customize-a-canvas-app-form-in-powerapps"></a>PowerApps でキャンバス アプリのフォームをカスタマイズする

キャンバス アプリでは、最も重要なデータを、ユーザーが簡単に理解して更新できるよう、最も見やすい直感的な順序で表示されるように、**表示フォーム** コントロールと**編集フォーム** コントロールをカスタマイズできます。

それぞれのフォームは、少なくとも 1 つのカードで構成され、データ ソースから取得された特定の列のデータが個々のカードに表示されます。 このトピックの手順に従うことで、フォームに表示するカードを指定したり、フォーム内でカードの位置を上げ下げしたりできます。

キャンバス pps を使い慣れていない場合を参照してください。[キャンバス アプリとは?](getting-started.md)します。

## <a name="prerequisites"></a>前提条件

Common Data Service から[アプリを生成](data-platform-create-app.md)し、そのアプリで[ギャラリーをカスタマイズ](customize-layout-sharepoint.md)します。

## <a name="show-and-hide-cards"></a>カードの表示と非表示

1. サインインする[PowerApps](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)、しを生成してカスタマイズしたアプリを開きます。

1. 左側のナビゲーション バーに入力するか貼り付けます**D** 、要素のリストをフィルター処理して選択し、検索バーで**DetailForm1**します。

    > [!div class="mx-imgBorder"]
    > ![詳細画面を選択します。](./media/customize-forms-sharepoint/select-detailform.png)

1. 右側のウィンドウの **[プロパティ]** タブで **[フィールドの編集]** を選択して、**[フィールド]** ウィンドウを開きます。

    > [!div class="mx-imgBorder"]
    > ![開いているフィールド ウィンドウ](./media/customize-forms-sharepoint/edit-fields.png)

1. など、フィールドを非表示に**説明**上にポインターを合わせると、表示される省略記号 (...) を選択し、選択して、**削除**します。

    > [!div class="mx-imgBorder"]
    > ![フィールドの一覧](./media/customize-forms-sharepoint/hide-fields.png)

1. フィールドを選択して表示**フィールドの追加**の入力または検索ボックスは、フィールドのチェック ボックスをオンや選択し、フィールドの名前の最初のいくつかの文字を貼り付ける**追加**します。

    > [!div class="mx-imgBorder"]
    > ![フィールドの一覧](./media/customize-forms-sharepoint/show-field.png)

## <a name="reorder-the-cards"></a>カードの並べ替え

1. **フィールド**ウィンドウで、ドラッグ、**アカウント名**フィールドをフィールドの一覧の一番上にします。

    内のカード**DetailForm1**変更が反映されます。

    > [!div class="mx-imgBorder"]
    > ![並べ替え後のカード](./media/customize-forms-sharepoint/reordered-card.png)

1. (省略可能)このシーケンスに、他のカードの順序を変更します。

    - アカウント名
    - 従業員数
    - 年間売上高
    - メインの電話
    - 住所 1: 番地 1
    - 住所 1: 番地 2
    - 住所 1: 市区町村
    - 住所 1: 郵便番号

1. 左側のナビゲーション バーに入力するか貼り付けます**Ed**検索バーで、 **EditForm1**をオンにします。

1. 前の手順とこれを繰り返して、**EditForm1** のフィールドが **DetailForm1** のフィールドと一致するようにします。

## <a name="run-the-app"></a>アプリの実行

1. 左側のナビゲーション バーに入力するか貼り付けます**Br**検索バーで、 **BrowseScreen1**をオンにします。

1. F5 キーを押して (または右上隅の**プレビュー** アイコンをクリックして) プレビュー モードを開きます。

    > [!div class="mx-imgBorder"]
    > ![プレビュー アイコン](./media/customize-forms-sharepoint/open-preview.png)

1. 右上隅でレコードを追加するプラス アイコンを選択します。 **EditScreen1**します。

    > [!div class="mx-imgBorder"]
    > ![レコードを追加します。](./media/customize-forms-sharepoint/add-record.png)

1. 追加しに戻って変更を保存するには、右上隅にあるチェック マーク アイコンを選択し、どのようなデータ**BrowseScreen1**します。

    > [!div class="mx-imgBorder"]
    > ![レコードを保存します。](./media/customize-forms-sharepoint/save-record.png)

1. 内のアイテムに関する詳細を表示用に作成した項目の矢印を選択**DetailScreen1**します。

    > [!div class="mx-imgBorder"]
    > ![右矢印](./media/customize-forms-sharepoint/right-arrow.png)

1. 右上隅でのレコードを更新する編集アイコンを選択**EditScreen1**します。

    > [!div class="mx-imgBorder"]
    > ![レコードを編集します。](./media/customize-forms-sharepoint/edit-record.png)

1. 1 つまたは複数のフィールドの情報を変更しに戻って変更を保存するには、右上隅にあるチェック マークを選択**DetailScreen1**します。

    > [!div class="mx-imgBorder"]
    > ![変更を保存します。](./media/customize-forms-sharepoint/save-record.png)

1. 右上隅の近くには、更新したレコードを削除してに戻るには、ごみ箱アイコンを選択します。 **BrowseScreen1**します。

    > [!div class="mx-imgBorder"]
    > ![レコードを削除します。](./media/customize-forms-sharepoint/delete-record.png)

1. Esc キーを押して (または左上隅の近くにある閉じるアイコンを選択して) プレビュー モードを終了します。

## <a name="next-steps"></a>次の手順

- アプリを[保存して公開](save-publish-app.md)します。
- アプリの[カードをカスタマイズ](customize-card.md)します。
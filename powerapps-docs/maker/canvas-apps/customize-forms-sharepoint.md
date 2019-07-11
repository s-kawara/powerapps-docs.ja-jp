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
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61560678"
---
# <a name="customize-a-canvas-app-form-in-powerapps"></a>PowerApps でキャンバス アプリのフォームをカスタマイズする

キャンバス アプリでは、**ディスプレイフォーム** コントロールと**編集フォーム** コントロールをカスタマイズすることで、最も重要なデータを最も見やすい直感的な順序で表示されるようにして、ユーザーが簡単にデータを理解し更新できるようにします。

それぞれのフォームは、少なくとも 1 つのカードで構成され、データ ソースから取得された特定の列のデータが個々のカードに表示されます。 このトピックの手順に従うことで、フォームに表示するカードを指定したり、フォーム内でカードの位置を上げ下げしたりできます。

キャンバス アプリを使い慣れていない場合は、[キャンバス アプリとは?](getting-started.md)を参照してください。

## <a name="prerequisites"></a>前提条件

Common Data Service から[アプリを生成](data-platform-create-app.md)し、そのアプリで[ギャラリーをカスタマイズ](customize-layout-sharepoint.md)します。

## <a name="show-and-hide-cards"></a>カードの表示と非表示

1. [PowerApps](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) にサインインしてから、生成してカスタマイズしたアプリを開きます。

1. 左側のナビゲーション バーの検索バーに **D** を入力するか貼り付け、要素のリストをフィルター処理し、**DetailForm1** を選択します。

    > [!div class="mx-imgBorder"]
    > ![詳細画面を選択します。](./media/customize-forms-sharepoint/select-detailform.png)

1. 右側のウィンドウの **[プロパティ]** タブで **[フィールドの編集]** を選択して、**[フィールド]** ウィンドウを開きます。

    > [!div class="mx-imgBorder"]
    > ![開いているフィールド ウィンドウ](./media/customize-forms-sharepoint/edit-fields.png)

4. **[Description]説明**上にポインターを合わせると表示される省略記号 (...) を選択し、**[Remove]削除**を選択します。

    > [!div class="mx-imgBorder"]
    > ![フィールドの一覧](./media/customize-forms-sharepoint/hide-fields.png)

5. **[Add field] (フィールドの追加)**を選択し、検索ボックスにフィールド名の最初の数文字を入力するか貼り付けて、フィールドのチェックボックスをオンにしてから、**[Add] (追加)** を選択し、フィールドを表示します。

    > [!div class="mx-imgBorder"]
    > ![フィールドの一覧](./media/customize-forms-sharepoint/show-field.png)

## <a name="reorder-the-cards"></a>カードの並べ替え

1. **フィールド**ウィンドウで、**[Account Name] アカウント名**フィールドをフィールド一覧の一番上にドラッグします。

    **DetailForm1**のカードに、変更が反映されます。

    > [!div class="mx-imgBorder"]
    > ![並べ替え後のカード](./media/customize-forms-sharepoint/reordered-card.png)

2. (省略可能) 他のカードを次の順序で並び替えます。

    - アカウント名
    - 従業員数
    - 年間売上高
    - メインの電話
    - 住所 1: 番地 1
    - 住所 1: 番地 2
    - 住所 1: 市区町村
    - 住所 1: 郵便番号

1. 左側のナビゲーション バーの検索バーに **Ed** と入力するか貼り付けて、**EditForm1** を選択します。

4. **EditForm1** のフィールドが **DetailForm1** のフィールドと一致するように、前の操作手順を繰り返します。

## <a name="run-the-app"></a>アプリの実行

1. 左側のナビゲーション バーの検索バーに **Br** と入力するか貼り付けて、**BrowseScreen1** を選択します。

1. F5 キーを押して (または右上隅の**プレビュー** アイコンをクリックして) プレビュー モードを開きます。

    > [!div class="mx-imgBorder"]
    > ![プレビュー アイコン](./media/customize-forms-sharepoint/open-preview.png)

1. 右上隅にあるプラス アイコンを選択して、**EditScreen1** にレコードを追加します。

    > [!div class="mx-imgBorder"]
    > ![レコードを追加します。](./media/customize-forms-sharepoint/add-record.png)

4. 必要なデータを追加してから、右上隅にあるチェック マーク アイコンを選択して変更内容を保存し、**BrowseScreen1** に戻ります。

    > [!div class="mx-imgBorder"]
    > ![レコードを保存します。](./media/customize-forms-sharepoint/save-record.png)

5. 作成したばかりのアイテムの矢印を選択すると、**DetailScreen1** にそのアイテムの詳細が表示されます。

    > [!div class="mx-imgBorder"]
    > ![右矢印](./media/customize-forms-sharepoint/right-arrow.png)

6. 右上隅の編集アイコンを選択して、**EditScreen1** のレコードを更新します。

    > [!div class="mx-imgBorder"]
    > ![レコードを編集します。](./media/customize-forms-sharepoint/edit-record.png)

7. 1 つまたは複数のフィールドの情報を変更してから、右上隅にあるチェック マークを選択して変更内容を保存し、**DetailScreen1** に戻ります。

    > [!div class="mx-imgBorder"]
    > ![変更を保存します。](./media/customize-forms-sharepoint/save-record.png)

8. 右上隅の近くのごみ箱アイコンを選択して、更新したばかりのレコードを削除し、**BrowseScreen1** に戻ります。

    > [!div class="mx-imgBorder"]
    > ![レコードを削除します。](./media/customize-forms-sharepoint/delete-record.png)

1. Esc キーを押して (または左上隅の近くにある閉じるアイコンを選択して) プレビュー モードを終了します。

## <a name="next-steps"></a>次の手順

- アプリを[保存して公開](save-publish-app.md)します。
- アプリの[カードをカスタマイズ](customize-card.md)します。

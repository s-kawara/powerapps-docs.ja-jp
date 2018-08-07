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
ms.openlocfilehash: 14ea731907624f882ae117a09c7f799a25389fe6
ms.sourcegitcommit: e3f5a2bef64085d02aec82e62ff94ae8a4d01d24
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/02/2018
ms.locfileid: "39471445"
---
# <a name="customize-a-canvas-app-form-in-powerapps"></a>PowerApps でキャンバス アプリのフォームをカスタマイズする

キャンバス アプリでは、最も重要なデータを、ユーザーが簡単に理解して更新できるよう、最も見やすい直感的な順序で表示されるように、**表示フォーム** コントロールと**編集フォーム** コントロールをカスタマイズできます。

それぞれのフォームは、少なくとも 1 つのカードで構成され、データ ソースから取得された特定の列のデータが個々のカードに表示されます。 このトピックの手順に従うことで、フォームに表示するカードを指定したり、フォーム内でカードの位置を上げ下げしたりできます。

PowerApps の基本的な事柄については、「[PowerApps の概要](getting-started.md)」を参照してください。

## <a name="prerequisites"></a>前提条件

Common Data Service から[アプリを生成](data-platform-create-app.md)し、そのアプリで[ギャラリーをカスタマイズ](customize-layout-sharepoint.md)します。

## <a name="show-and-hide-cards"></a>カードの表示と非表示

1. [PowerApps](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) にサインインします。

    ![PowerApps サイトのホーム ページ](./media/customize-forms-sharepoint/sign-in.png)


1. 生成してカスタマイズしたアプリを開きます。

1. 左側のナビゲーション バーで、要素の一覧をフィルター処理するために検索バーに「**D**」と入力するか貼り付け、**DetailForm1** をクリックするかタップして選択します。

    ![詳細画面を選択](./media/customize-forms-sharepoint/select-detailform.png)

1. 右側のウィンドウで、**[アカウント]** をクリックするかタップして、**[データ]** ウィンドウを表示します。

    ![データ ウィンドウの表示](./media/customize-forms-sharepoint/show-data-pane.png)

1. **[データ]** ウィンドウで、**[取引先責任者]**、**[説明]**、および **[住所 1: 建物名]** チェックボックスをオフにして、それらのフィールドを非表示にします。

    ![フィールドの一覧](./media/customize-forms-sharepoint/hide-fields.png)

1.  **[データ]** ウィンドウで **[住所 1: 郵便番号]** チェックボックスをオンにして、そのフィールドを表示します。

    ![フィールドの一覧](./media/customize-forms-sharepoint/show-field.png)

## <a name="reorder-the-cards"></a>カードの並べ替え
1. **[データ]** ウィンドウで、**[アカウント名]** フィールドを一覧の一番上にドラッグします。

    ![カードの移動](./media/customize-forms-sharepoint/move-card.png)

    **DetailForm1** 内のカードにも同じ変更が反映されます。

    ![並べ替え後のカード](./media/customize-forms-sharepoint/reordered-card.png)

1. その他のカードをこの順序に並べ替えます。

    - アカウント名
    - 住所 1: 建物名
    - 住所 1: 市区町村
    - 住所 1: 郵便番号
    - 従業員数
    - 年間売上高

1. 左ナビゲーション バーの検索バーに、「**Ed**」と入力するか貼り付け、**EditForm1** をクリックまたはタップして選択します。

1. 前の手順とこれを繰り返して、**EditForm1** のフィールドが **DetailForm1** のフィールドと一致するようにします。

## <a name="run-the-app"></a>アプリの実行
1. 左側のナビゲーション バーで、「**Br**」と入力するか貼り付け、**BrowseScreen1** をクリックするかタップして選択します。

2. F5 キーを押して (または右上隅の**プレビュー** アイコンをクリックして) プレビュー モードを開きます。

    ![プレビュー アイコン](./media/customize-forms-sharepoint/open-preview.png)

3. 右上隅のプラス アイコンをクリックまたはタップして、**EditScreen1** でレコードを追加します。

    ![レコードを追加](./media/customize-forms-sharepoint/add-record.png)

4. 必要なデータを追加し、右上隅のチェックマーク アイコンをクリックまたはタップして変更を保存して、**BrowseScreen1** に戻ります。

    ![レコードの保存](./media/customize-forms-sharepoint/save-record.png)

5. 今作成した項目の矢印をクリックまたはタップして、その詳細を **DetailScreen1** に表示します。  

    ![右矢印](./media/customize-forms-sharepoint/right-arrow.png)

6. 右上隅の編集アイコンをクリックまたはタップして、**EditScreen1** でレコードを更新します。

    ![レコードを編集](./media/customize-forms-sharepoint/edit-record.png)

7. 少なくとも 1 つのフィールドの情報を変更し、右上隅のチェック マークをクリックまたはタップして SharePoint リストに変更内容を保存し、**DetailScreen1** に戻ります。  

    ![変更を保存](./media/customize-forms-sharepoint/save-record.png)

8. 右上隅にあるごみ箱アイコンをクリックまたはタップして、先ほど更新したレコードを削除し、**BrowseScreen1** に戻ります。

    ![レコードを削除](./media/customize-forms-sharepoint/delete-record.png)

9. Esc キーを押して (または左上隅にある閉じるアイコンをクリックまたはタップして) プレビュー モードを終了します。

## <a name="next-steps"></a>次の手順
- アプリを[保存して公開](save-publish-app.md)します。
- アプリの[カードをカスタマイズ](customize-card.md)します。

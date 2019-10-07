---
title: キャンバス アプリでフォームをカスタマイズする | Microsoft Docs
description: PowerApps で、キャンバス アプリのフォームに、どのデータを、どのような順番で、どのコントロールに表示するかを指定します。
author: tapanm-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 03/17/2018
ms.author: tapanm
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 67e7e0074259731bb1d3c50474e8020e3f4fcf1b
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "71993173"
---
# <a name="customize-a-canvas-app-form-in-powerapps"></a>PowerApps でキャンバス アプリのフォームをカスタマイズする

キャンバス アプリでは、最も重要なデータを、ユーザーが簡単に理解して更新できるよう、最も見やすい直感的な順序で表示されるように、**表示フォーム** コントロールと**編集フォーム** コントロールをカスタマイズできます。

それぞれのフォームは、少なくとも 1 つのカードで構成され、データ ソースから取得された特定の列のデータが個々のカードに表示されます。 このトピックの手順に従うことで、フォームに表示するカードを指定したり、フォーム内でカードの位置を上げ下げしたりできます。

Canvas-pps に慣れていない場合は、「[キャンバスアプリとは](getting-started.md)」を参照してください。

## <a name="prerequisites"></a>前提条件

Common Data Service から[アプリを生成](data-platform-create-app.md)し、そのアプリで[ギャラリーをカスタマイズ](customize-layout-sharepoint.md)します。

## <a name="show-and-hide-cards"></a>カードの表示と非表示

1. [PowerApps](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)にサインインし、生成してカスタマイズしたアプリを開きます。

1. 左側のナビゲーションバーで、検索バーに「 **D** 」と入力するか貼り付けて、要素の一覧をフィルター処理し、 **[DetailForm1]** を選択します。

    > [!div class="mx-imgBorder"]
    > ![Select details screen @ no__t-1

1. 右側のウィンドウの **[プロパティ]** タブで **[フィールドの編集]** を選択して、 **[フィールド]** ウィンドウを開きます。

    > [!div class="mx-imgBorder"]
    > ![Open fields pane @ no__t-1

1. **説明**などのフィールドを非表示にするには、そのフィールドにカーソルを合わせ、表示される省略記号 (...) を選択し、 **[削除]** を選択します。

    > [!div class="mx-imgBorder"]
    > ![List @ no__t-1

1. フィールドを表示するには、 **[フィールドの追加]** を選択し、検索ボックスにフィールド名の最初の数文字を入力または貼り付け、フィールドのチェックボックスをオンにして、 **[追加]** を選択します。

    > [!div class="mx-imgBorder"]
    > ![List @ no__t-1

## <a name="reorder-the-cards"></a>カードの並べ替え

1. **[フィールド]** ウィンドウで、 **[アカウント名]** フィールドをフィールドの一覧の一番上にドラッグします。

    **DetailForm1**のカードには、変更が反映されています。

    > [!div class="mx-imgBorder"]
    > @no__t 0 で並べ替えられるカード @ no__t-1

1. optional他のカードを次の順序に並べ替えます。

    - アカウント名
    - 従業員数
    - 年間売上高
    - メインの電話
    - 住所 1: 番地 1
    - 住所 1: 番地2
    - 住所 1: City
    - 住所 1: 郵便番号

1. 左側のナビゲーションバーで、検索バーに「 **Ed** 」と入力するか貼り付け、 **[EditForm1]** を選択して選択します。

1. 前の手順とこれを繰り返して、**EditForm1** のフィールドが **DetailForm1** のフィールドと一致するようにします。

## <a name="run-the-app"></a>アプリの実行

1. 左側のナビゲーションバーで、検索バーに「 **Br** 」と入力するか貼り付け、 **[BrowseScreen1]** を選択して選択します。

1. F5 キーを押して (または右上隅の**プレビュー** アイコンをクリックして) プレビュー モードを開きます。

    > [!div class="mx-imgBorder"]
    > ![Preview アイコン @ no__t

1. 右上隅にあるプラスアイコンを選択して、 **EditScreen1**にレコードを追加します。

    > [!div class="mx-imgBorder"]
    > ![Add record @ no__t-1

1. 任意のデータを追加し、右上隅のチェックマークアイコンを選択して変更を保存し、 **BrowseScreen1**に戻ります。

    > [!div class="mx-imgBorder"]
    > ![Save レコード @ no__t

1. 作成した項目の矢印を選択して、 **DetailScreen1**内のその項目に関する詳細を表示します。

    > [!div class="mx-imgBorder"]
    > ![Right arrow @ no__t

1. 右上隅にある [編集] アイコンを選択して、 **EditScreen1**のレコードを更新します。

    > [!div class="mx-imgBorder"]
    > ![Edit record @ no__t-1

1. 1つまたは複数のフィールドの情報を変更し、右上隅のチェックマークを選択して変更を保存し、 **DetailScreen1**に戻ります。

    > [!div class="mx-imgBorder"]
    > ![Save changes @ no__t-1

1. 右上隅にあるごみ箱アイコンを選択して、更新したばかりのレコードを削除し、 **BrowseScreen1**に戻ります。

    > [!div class="mx-imgBorder"]
    > ![Delete レコード @ no__t

1. Esc キーを押して (または左上隅の閉じるアイコンを選択して) プレビューモードを終了します。

## <a name="next-steps"></a>次の手順

- アプリを[保存して公開](save-publish-app.md)します。
- アプリの[カードをカスタマイズ](customize-card.md)します。
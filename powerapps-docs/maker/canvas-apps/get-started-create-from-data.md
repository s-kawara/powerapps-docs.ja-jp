---
title: Excel からキャンバス アプリを生成する | Microsoft Docs
description: PowerApps を使用し、クラウド ストレージ アカウントに格納されている Excel ファイルを使用して自動的にキャンバス アプリを生成する
author: AFTOwen
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 01/14/2019
ms.author: anneta
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 7ab85f09ebf88c30b35c963242895cd74ca6a966
ms.sourcegitcommit: b987589e946cacc86b806a0bd49b9b544ea489dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/15/2019
ms.locfileid: "54297598"
---
# <a name="generate-a-canvas-app-from-excel-in-powerapps"></a>PowerApps で Excel からキャンバス アプリを生成する

このトピックでは、PowerApps で、Excel テーブルからのデータを使用して最初のキャンバス アプリを自動的に生成します。 Excel ファイルを選択して、アプリを生成し、生成したアプリを実行します。 生成されたすべてのアプリには、レコードの参照、レコードの詳細の表示、レコードの作成または更新のための画面が含まれています。 アプリを生成して、Excel のデータを使用して作業用アプリをすばやく入手することができ、その後でニーズに合わせてアプリをカスタマイズできます。 

Excel ファイルは、OneDrive、Dropbox、Google Drive などのクラウドストレージ アカウントに置かれている必要があります。 このトピックでは、OneDrive for Business を使用します。

PowerApps のライセンスを持っていない場合は、[無料でサインアップ](../signup-for-powerapps.md)できます。

## <a name="prerequisites"></a>前提条件

このトピックの内容に正確に従うには、Excel で [Flooring Estimates](https://az787822.vo.msecnd.net/documentation/get-started-from-data/FlooringEstimates.xlsx) ファイルをダウンロードし、[クラウド ストレージ アカウント](connections/cloud-storage-blob-connections.md)に保存します。

> [!IMPORTANT]
> ご自身の Excel ファイルを使用するには、データがテーブルとして書式設定されている必要があります。 詳しくは、「[テーブルの書式設定](how-to-excel-tips.md)」をご覧ください。 

## <a name="generate-the-app"></a>アプリを生成する

1. [PowerApps](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) にサインインします。

1. **[Make your own app]\(独自アプリの作成\)** の下の **[Start from data]\(データから開始\)** にポインターを合わせ、**[このアプリの作成]** を選択します。

    ![アプリを作成するためのオプション](./media/get-started-create-from-data/start-from-data.png)

1. **[データを使用して開始]** の下で、クラウド ストレージ アカウントのタイルで **[電話レイアウト]** をクリックまたはタップします。

    ![アプリを作成するためのオプション](./media/get-started-create-from-data/odfb-tile.png)

1. メッセージが表示されたら、**[接続]** をクリックまたはタップし、そのアカウントの資格情報を指定します。

1. **[Choose an Excel file (Excel ファイルの選択)]** で **FlooringEstimates.xlsx** を参照してクリックまたはタップします。 

1. **[Choose a table (テーブルの選択)]** で **[FlooringEstimates]** をクリックまたはタップし、**[Connect (接続)]** をクリックまたはタップします。

    ![アプリを作成するためのオプション](./media/get-started-create-from-data/choose-table.png)

## <a name="run-the-app"></a>アプリの実行

1. F5 キーを押して (または右上隅の再生アイコンをクリックまたはタップして) プレビューを開始します。

    ![プレビューを開く](./media/get-started-create-from-data/open-preview.png)

1. 右上隅にある並べ替えアイコンをクリックまたはタップして、並べ替え順序を切り替えます。

    ![並べ替えアイコン](./media/get-started-create-from-data/sort-icon.png)

1. 検索ボックスに文字を入力するか貼り付けて一覧をフィルタリングします。

    たとえば、入力または貼り付けます**ハニー**文字列が、製品の名前、カテゴリ、または概要に表示されることを唯一のレコードを表示します。

    ![フィルターの例](./media/get-started-create-from-data/filter-example.png)

1. レコードを追加します。

    1. 正符号アイコンを選択します。

        ![プラス記号のアイコン](./media/get-started-create-from-data/plus-icon.png)

    1. 任意のデータを追加し、変更を保存するチェック マーク アイコンを選択します。

        ![[保存] アイコン](./media/get-started-create-from-data/save-icon.png)

1. レコードを編集します。

    1. 編集するレコードの矢印を選択します。

        ![右矢印](./media/get-started-create-from-data/next-arrow.png)

    1. 鉛筆アイコンを選択します。

        ![鉛筆のアイコン](./media/get-started-create-from-data/pencil-icon.png)

    1. 1 つまたは複数のフィールドを更新し、し、変更を保存するチェック マーク アイコンを選択します。

        ![[保存] アイコン](./media/get-started-create-from-data/save-icon.png)

        代わりに、変更を破棄する、キャンセル アイコンを選択します。

1. レコードを削除します。

    1. 削除するレコードの横にある矢印を選択します。

        ![右矢印](./media/get-started-create-from-data/next-arrow.png)

    1. ごみ箱アイコンを選択します。

        ![[ごみ箱] アイコン](./media/get-started-create-from-data/trash-icon.png)

## <a name="next-steps"></a>次の手順

ニーズに合わせて既定のブラウザー画面をカスタマイズします。 たとえば、ソートし、カテゴリまたは概要ではない、製品名だけで一覧をフィルター処理できます。

> [!div class="nextstepaction"]
> [既定のブラウザー画面のカスタマイズ](customize-layout-sharepoint.md).

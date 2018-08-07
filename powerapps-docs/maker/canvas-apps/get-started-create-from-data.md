---
title: Excel からキャンバス アプリを生成する | Microsoft Docs
description: PowerApps を使用し、クラウド ストレージ アカウントに格納されている Excel ファイルを使用して自動的にキャンバス アプリを生成する
author: AFTOwen
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 03/18/2018
ms.author: anneta
ms.openlocfilehash: f6051ca8348e8417302f49261d7ccac56a8aa9c9
ms.sourcegitcommit: e3f5a2bef64085d02aec82e62ff94ae8a4d01d24
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/02/2018
ms.locfileid: "39470088"
---
# <a name="generate-a-canvas-app-from-excel-in-powerapps"></a>PowerApps で Excel からキャンバス アプリを生成する

このトピックでは、PowerApps で、Excel テーブルからのデータを使用して最初のキャンバス アプリを自動的に生成します。 Excel ファイルを選択して、アプリを生成し、生成したアプリを実行します。 生成されたすべてのアプリには、レコードの参照、レコードの詳細の表示、レコードの作成または更新のための画面が含まれています。 アプリを生成して、Excel のデータを使用して作業用アプリをすばやく入手することができ、その後でニーズに合わせてアプリをカスタマイズできます。 

Excel ファイルは、OneDrive、Dropbox、Google Drive などのクラウドストレージ アカウントに置かれている必要があります。 このトピックでは、OneDrive for Business を使用します。

PowerApps のライセンスを持っていない場合は、[無料でサインアップ](../signup-for-powerapps.md)できます。

## <a name="prerequisites"></a>前提条件 ##
このトピックの内容に正確に従うには、Excel で [Flooring Estimates](https://az787822.vo.msecnd.net/documentation/get-started-from-data/FlooringEstimates.xlsx) ファイルをダウンロードし、[クラウド ストレージ アカウント](connections/cloud-storage-blob-connections.md)に保存します。

> [!IMPORTANT]
> ご自身の Excel ファイルを使用するには、データがテーブルとして書式設定されている必要があります。 詳しくは、「[テーブルの書式設定](how-to-excel-tips.md)」をご覧ください。 

## <a name="generate-the-app"></a>アプリを生成する
1. [PowerApps](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) にサインインします。

    ![PowerApps ホーム ページ](./media/get-started-create-from-data/sign-in.png)

1. **[このようなアプリを作成します]** の下の **[Start from data]\(データから開始\)** にポインターを合わせ、**[このアプリの作成]** を選択します。

    ![アプリを作成するためのオプション](./media/get-started-create-from-data/make-this-app.png)

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

1. プラス アイコンをクリックまたはタップしてレコードを追加し、必要なデータを追加し、チェックマーク アイコンをクリックまたはタップして変更を保存します。

1. 追加したレコードの横にある矢印をクリックまたはタップし、鉛筆アイコンをクリックまたはタップしてレコードを編集し、1 つ以上のフィールドを更新し、チェックマーク アイコンをクリックまたはタップして変更を保存します。

1. 追加したレコードの横にある矢印をクリックまたはタップし、鉛筆アイコンをクリックまたはタップしてレコードを編集し、1 つ以上のフィールドを更新し、キャンセル アイコンをクリックまたはタップして変更を破棄します。

1. 追加したレコードの横にある矢印をクリックまたはタップし、ごみ箱アイコンをクリックまたはタップしてレコードを削除します。

## <a name="next-steps"></a>次の手順
ニーズに合わせて既定のブラウザー画面をカスタマイズします。 たとえば、カテゴリではなく製品名で一覧を並べ替えるかフィルター処理できます。

> [!div class="nextstepaction"]
> [既定のブラウザー画面をカスタマイズします](customize-layout-sharepoint.md)。
---
title: Excel へのイメージの追加 | Microsoft Docs
description: クラウド ストレージ アカウントで Excel にイメージ ファイルとペン描画を追加する手順
author: AFTOwen
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 10/25/2016
ms.author: anneta
ms.openlocfilehash: cc3609991ffb68f6846cb73b7ccfa37227d0c8e7
ms.sourcegitcommit: dfa0e1a7981814e15e6ca4720e2a5f930e859db1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2018
ms.locfileid: "39019488"
---
# <a name="add-images-to-excel-from-powerapps"></a>PowerApps から Excel へのイメージの追加
ユーザーがファイルのイメージを表示、追加、または削除したり、**ペン** コントロールを使用して描画したりできるアプリを自動的に作成します。 アプリは、作成してクラウド ストレージ アカウントにアップロードする Excel ファイルに基づきます。

## <a name="prerequisites"></a>前提条件

* [コントロールの追加と構成](add-configure-controls.md)に慣れている。
* [テーブルとしての Excel データの構成](https://support.office.com/article/Format-an-Excel-table-6789619F-C889-495C-99C2-2F971C0E2370?ui=en-US&rs=en-US&ad=US)に慣れている。
* Excel ファイルを格納できる、クラウド ストレージ アカウント (Dropbox、OneDrive、Google Drive など) への [PowerApps の接続](add-data-connection.md)。

## <a name="create-the-data-source-and-the-app"></a>データ ソースとアプリの作成
1. Excel で、隣接しており、2 つの空のセルのすぐ上にある 2 つのセル (A1 と B1 など) に**キャプション**と**イメージ [image]** を追加します。
2. 更新したセルと、そのセルのすぐ下にあるセルをテーブルとして書式設定し、そのテーブルに名前 (**Images** など) を付けます。
   
    ![テーブルの作成](./media/add-images-to-excel/create-table.png)
3. ファイル (**ImageDemo** など) を保存し、クラウド ストレージ アカウントにアップロードします。
4. PowerApps で、(アプリをまだ開いていない場合は左端にある) **[ファイル]** メニューの **[新規]** をクリックまたはタップし、クラウド ストレージ アカウントのタイルの **[携帯電話レイアウト]** をクリックまたはタップします。
   
    ![クラウド ストレージ アカウントの選択](./media/add-images-to-excel/select-account.png)
5. **[Excel ファイルの選択]** で、作成したファイルをクリックまたはタップします。
   
    ![ブックの選択](./media/add-images-to-excel/select-workbook.png)
6. **[テーブルの選択]** で、作成したテーブルをクリックまたはタップし、**[接続]** をクリックまたはタップします。
   
    ![テーブルの選択](./media/add-images-to-excel/select-table.png)
7. クイック ツアーが表示された場合は、それを実行するか、**[スキップ]** をクリックまたはタップします。
   
    ![クイック ツアーの最初の画面](./media/add-images-to-excel/quick-tour.png)

## <a name="add-an-image-from-a-file"></a>ファイルからのイメージの追加
1. F5 キーを押して (または右上隅の再生ボタンをクリックまたはタップして) プレビュー モードを開始し、右上隅のプラス記号のアイコンをクリックまたはタップします。
   
    ![プラス記号のアイコン](./media/add-images-to-excel/plus-icon.png)
2. **[キャプション]** ボックスに、追加するイメージ ファイルの簡単な説明を入力または貼り付け、その下をクリックまたはタップしてファイルを指定します。
3. **[開く]** ダイアログ ボックスで、追加するファイルを参照し、そのファイルをクリックまたはタップして **[開く]** をクリックまたはタップします。
   
    ![キャプションとイメージの追加](./media/add-images-to-excel/add-image.png)
4. 右上隅にあるチェックマーク アイコンをクリックまたはタップして、変更を保存します。
   
    ![変更を保存](./media/add-images-to-excel/checkmark-icon.png)
5. 最後の 3 つの手順を繰り返して必要な数のイメージを追加し、Esc キーを押して既定のワークスペースに戻ります。
6. (省略可能) 各イメージのキャプションを示す**ラベル** コントロールのいずれかを削除します。

## <a name="add-a-drawing"></a>描画の追加
1. 左側のナビゲーション バーで **EditScreen1** をクリックまたはタップして表示し、イメージ カードをクリックまたはタップして選択します。
   
    ![イメージ カードの選択](./media/add-images-to-excel/select-card.png)
2. 右側のウィンドウで、イメージ カードのカード セレクターをクリックまたはタップし、**[メモの追加]** をクリックまたはタップします。
   
    ![メモの追加](./media/add-images-to-excel/add-notes.png)
3. 左側のナビゲーション バーで **BrowseScreen1** をクリックまたはタップして表示し、プレビュー モードを開始します。
4. 右上隅にあるプラス記号のアイコンをクリックまたはタップし、キャプションを追加して、**ペン** コントロールでイメージを描画します。
   
    ![図の描画](./media/add-images-to-excel/draw-picture.png)
5. 右上隅にあるチェックマーク アイコンをクリックまたはタップして、変更を保存します。
   
    ![変更を保存](./media/add-images-to-excel/checkmark-icon.png)
6. 最後の 2 つの手順を繰り返して必要な数の描画を追加し、Esc キーを押して既定のワークスペースに戻ります。


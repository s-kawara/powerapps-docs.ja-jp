---
title: キャンバス アプリのテーブルからレコードを表示、編集、または追加する | Microsoft Docs
description: データ ソース内のテーブルのレコードを表示、編集、または追加するには、キャンバス アプリ フォームを使用します。
author: karthik-1
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 10/06/2017
ms.author: sharik
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 853f54448b3cf29ebd108299ca69cc96ce51be19
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "42854815"
---
# <a name="show-edit-or-add-a-record-from-a-table-in-powerapps"></a>PowerApps でテーブルのレコードを表示、編集、または追加する

レコード内のすべてのフィールドを表示するには、キャンバス アプリで**[フォームを表示](controls/control-form-detail.md)** コントロールを追加および構成します。 レコード内のフィールドを編集 (またはレコードを追加) して、変更内容をデータ ソースに保存するには、キャンバス アプリで**[フォームを編集](controls/control-form-detail.md)** コントロールを追加および構成します。

## <a name="prerequisites"></a>前提条件

* PowerApps で[コントロールを追加して構成する](add-configure-controls.md)方法について確認します。
* [この Excel ファイル](https://az787822.vo.msecnd.net/documentation/get-started-from-data/FlooringEstimates.xlsx)をダウンロードして、チュートリアルのサンプル データを取得します。
* Excel ファイルを OneDrive for Business などの[クラウド ストレージ アカウント](connections/cloud-storage-blob-connections.md)にアップロードします。
* 新規または既存のアプリで、Excel ファイル内の **FlooringEstimates** テーブルに[接続を追加します](add-data-connection.md)。
* 既存のアプリを使用している場合は、[画面を追加します](add-screen-context-variables.md)。

## <a name="add-a-form-and-show-data"></a>フォームを追加し、データを表示する
1. **[ドロップ ダウン](controls/control-drop-down.md)** コントロールを追加し、**ChooseProduct** という名前を付け、**[Items](controls/properties-core.md)** プロパティを以下の値に設定します。

    **FlooringEstimates.Name**

    > [!NOTE]
   > コントロールの追加、コントロールの名前変更、およびプロパティの設定の方法がわからない場合は、「[Add and configure controls (コントロールの追加と構成)](add-configure-controls.md)」を参照してください。

    一覧に、データ ソースから取得した床材製品の名前が表示されます。

2. **フォームの編集**コントロールを追加し、それを **ChooseProduct** の下に移動して、フォームが画面の大部分を占めるようにサイズ変更します。

    ![フォームを追加する](./media/add-form/add-a-form.png)

    > [!NOTE]
   > このトピックでは**フォームを編集**コントロールについて説明していますが、同様の原則が**フォームを表示**コントロールにも当てはまります。

3. フォームの **[DataSource](controls/control-form-detail.md)** プロパティを **FlooringEstimates** に設定し、**[Item](controls/control-form-detail.md)** プロパティを次の数式に設定します。

   **First(Filter(FlooringEstimates, Name=ChooseProduct.Selected.Value))**

   この式では、フォームの構成が完了した後、**ChooseProduct** でユーザーが選択したレコードが表示されるように指定しています。

4. **[データ]** ウィンドウで、各フィールドのチェックボックスをクリックまたはタップして表示状態にします。

    > [!NOTE]
   > **[データ]** ウィンドウが閉じている場合、左側のウィンドウでフォームを選択し、右側のウィンドウで **[データ]** をクリックまたはタップして開いてください。

    ![フォーム上にフィールドを表示する](./media/add-form/checkbox.png)

5. **[データ]** ウィンドウで、**[名前]** エントリを一覧の先頭にドラッグします。

    ![カードを移動する](./media/add-form/drag-field.png)

    **フォームを編集**コントロールに変更内容が反映されます。

    ![先頭にある名前](./media/add-form/move-card-form.png)

## <a name="set-the-card-type-for-a-field"></a>フィールドにカードの種類を設定する
1. フォームを選択したまま、**[データ]** ウィンドウで **[価格]** のカード セレクターをクリックまたはタップします。

    ![カード セレクターを選択する](./media/add-form/price-card2.png)

2. 下にスクロールし、**View text** オプションをクリックまたはタップして、フィールドを読み取り専用にします。

    ![View text](./media/add-form/view-text.png)

    フォームに変更内容が反映されます。

    ![読み取り専用番号](./media/add-form/read-only.png)  

## <a name="edit-form-only-save-changes"></a>(編集フォームのみ) 変更を保存する
1. 左側のウィンドウで、フォームを選択し、省略記号 (...) をクリックまたはタップします。

   ![フォームを選択する](./media/add-form/select-form.png)

2. **[名前の変更]** をクリックまたはタップして、フォーム **EditForm** の名前を変更します。

3. **[ボタン](controls/control-button.md)** コントロールを追加し、**[Text](controls/properties-core.md)** プロパティを **Save** に設定します。

    ![保存ボタンの追加](./media/add-form/save-button.png)  

4. **Save** ボタンの **[OnSelect](controls/properties-core.md)** プロパティを次の数式に設定します。

   **SubmitForm(EditForm)**

5. 右上隅の再生ボタンを選択するか、F5 キーを押して、プレビュー モードを開きます。

    ![プレビュー モードを開始](./media/add-form/open-preview.png)

6. 製品の名前を変更し、先ほど作成した **Save** ボタンをクリックまたはタップします。

    **[SubmitForm](functions/function-form.md)** 関数によって、変更内容がフォームの構成に使用したデータ ソースに保存されます。

7. (省略可能) 閉じるアイコンを選択して (または Esc キーを押して) プレビューを終了します。

    ![プレビューを終了する](./media/add-form/close-preview.png)

## <a name="next-steps"></a>次の手順
[フォーム](working-with-forms.md)と[数式](working-with-formulas.md)についてさらに理解を深める。

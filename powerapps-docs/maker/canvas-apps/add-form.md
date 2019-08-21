---
title: 表示、編集、またはキャンバス アプリでレコードを追加 |Microsoft Docs
description: データ ソース内のテーブルのレコードを表示、編集、または追加するには、キャンバス アプリ フォームを使用します。
author: emcoope-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 10/06/2017
ms.author: emcoope
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: e94aa48ed3fba1b4591e196e3b81d3fb0f76666f
ms.sourcegitcommit: 4ed29d83e90a2ecbb2f5e9ec5578e47a293a55ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63321444"
---
# <a name="show-edit-or-add-a-record-in-a-canvas-app"></a>キャンバス アプリでレコードを表示、編集、追加

キャンバス アプリを追加して構成を **[表示](controls/control-form-detail.md)** も追加して構成する、レコードのすべてのフィールドを表示するコントロールをフォーム、 **[編集](controls/control-form-detail.md)** レコード内のフィールドを編集フォーム コントロールは、レコードを追加し、変更内容をデータ ソースに保存します。

## <a name="prerequisites"></a>前提条件

- PowerApps で[コントロールを追加して構成する](add-configure-controls.md)方法について確認します。
- [この Excel ファイル](https://az787822.vo.msecnd.net/documentation/get-started-from-data/FlooringEstimates.xlsx)をダウンロードして、チュートリアルのサンプル データを取得します。
- Excel ファイルを OneDrive for Business などの[クラウド ストレージ アカウント](connections/cloud-storage-blob-connections.md)にアップロードします。
- 携帯電話用のアプリを作成または開き、Excel ファイル内のテーブル **FlooringEstimages** テーブルに [接続を追加する](add-data-connection.md)。

    タブレット アプリにフォームを追加することもできますが、フォームには既定で 3 つの列があるため、このトピックには一致しません。

- 既存のアプリを開いた場合、 [画面を追加します](add-screen-context-variables.md) 。

## <a name="add-a-form-and-show-data"></a>フォームを追加し、データを表示する
1. 空の画面を追加、 **[ドロップダウン](controls/control-drop-down.md)** 制御、および名前を付けます**ChooseProduct**します。

    > [!NOTE]
   > コントロールの追加、コントロールの名前変更、およびプロパティの設定の方法がわからない場合は、「[Add and configure controls (コントロールの追加と構成)](add-configure-controls.md)」を参照してください。

1. 右側のペインの **プロパティ** タブで **Items** を `FlooringEstimates` に **Value** を `Name` に設定します。

    ![フォームの Items プロパティを設定します。](./media/add-form/items-property.png)

    一覧に、データ ソースから取得した床材製品の名前が表示されます。

1. **編集** フォーム コントロールを追加し、 **ChooseProduct** の下に移動し、フォームのサイズを変更して画面の大部分をカバーします。

    ![フォームを追加する](./media/add-form/add-a-form.png)

    > [!NOTE]
   > このトピックでは、 **編集** フォーム コントロールについて説明しますが、同様の原則が、 **ディスプレイ** フォーム コントロールにも適用されます。

1. フォームの設定 **[DataSource](controls/control-form-detail.md)** プロパティを**FlooringEstimates**とその **[項目](controls/control-form-detail.md)** プロパティをこの数式では:

    `First(Filter(FlooringEstimates, Name=ChooseProduct.Selected.Value))`

   この式では、フォームの構成が完了した後、**ChooseProduct** でユーザーが選択したレコードが表示されるように指定しています。

1. 右側のペインの **プロパティ** タブで、 **フィールドの編集** を選択します。

    ![フィールドを編集します。](./media/add-form/edit-fields.png)

1. **[フィールド]** ウィンドウで **[フィールドの追加]** を選択し、各フィールドのチェック ボックスをオンにし、 **[追加]** を選択します。

    ![フィールドを追加します。](./media/add-form/add-fields.png)

1. 横にある省略記号 (...) を選択します。**フィールドの追加**を選択します**すべて折りたたむ**、し、ドラッグ**名前**一覧の先頭にします。

    ![フィールドに移動します。](./media/add-form/move-field.png)

    **編集** フォーム コントロールには、変更が反映されます。

    ![フォームを表示します。](./media/add-form/show-form1.png)

## <a name="set-the-card-type-for-a-field"></a>フィールドにカードの種類を設定する
1. **フィールド** ペインで、下向きの矢印を選択して **価格[Price]** フィールドを展開します。

1. 開く、**コントロール型**、一覧表示し、**スライダーの編集**します。

    ![スライダーを編集します。](./media/add-form/edit-slider.png)

    フォームで、**価格**フィールド、**スライダー**コントロールの代わりに、**テキスト入力**コントロール。

1. (省略可能) **概要[Overview]** フィールドのコントロールを **複数行テキストの編集** コントロールに変更するには、同じ手順です。

## <a name="edit-form-only-save-changes"></a>(編集フォームのみ) 変更を保存する

1. フォームの名前を **EditForm** に変更します。

1. **[[ボタン]](controls/control-button.md)** コントロールを追加し、 **[OnSelect](controls/properties-core.md)** プロパティに次の式を設定します。

   `SubmitForm(EditForm)`

1. F5 キーを押してプレビューを開き、製品の名前を変更して作成したボタンを選択します。

    **[SubmitForm](functions/function-form.md)** 関数は、データ ソースに変更を保存します。

1. (省略可能)Esc キーを押して (または右上隅にある閉じるアイコンを選択して) プレビューを終了します。

## <a name="next-steps"></a>次の手順
[フォーム](working-with-forms.md)と[数式](working-with-formulas.md)についてさらに理解を深める。

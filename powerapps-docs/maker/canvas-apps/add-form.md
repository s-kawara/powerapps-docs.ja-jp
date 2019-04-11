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
ms.sourcegitcommit: 5c098a62f66a2f33418967fdce9363bd529e0fc1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2019
ms.locfileid: "58581026"
---
# <a name="show-edit-or-add-a-record-in-a-canvas-app"></a>表示、編集、またはキャンバス アプリでレコードを追加

キャンバス アプリを追加して構成を **[表示](controls/control-form-detail.md)** も追加して構成する、レコードのすべてのフィールドを表示するコントロールをフォーム、 **[編集](controls/control-form-detail.md)** レコード内のフィールドを編集フォーム コントロールは、レコードを追加し、変更内容をデータ ソースに保存します。

## <a name="prerequisites"></a>前提条件

- PowerApps で[コントロールを追加して構成する](add-configure-controls.md)方法について確認します。
- [この Excel ファイル](https://az787822.vo.msecnd.net/documentation/get-started-from-data/FlooringEstimates.xlsx)をダウンロードして、チュートリアルのサンプル データを取得します。
- Excel ファイルを OneDrive for Business などの[クラウド ストレージ アカウント](connections/cloud-storage-blob-connections.md)にアップロードします。
- 作成するか、スマート フォン用のアプリを開きます[接続を追加する](add-data-connection.md)を**FlooringEstimates** Excel ファイル内のテーブル。

    タブレット アプリにフォームを追加することができますが、このトピックでは、フォームが既定で 3 つの列を持つために一致しません。

- 既存のアプリを開いた場合[画面を追加する](add-screen-context-variables.md)にします。

## <a name="add-a-form-and-show-data"></a>フォームを追加し、データを表示する
1. 空の画面を追加、 **[ドロップダウン](controls/control-drop-down.md)** 制御、および名前を付けます**ChooseProduct**します。

    > [!NOTE]
   > コントロールの追加、コントロールの名前変更、およびプロパティの設定の方法がわからない場合は、「[Add and configure controls (コントロールの追加と構成)](add-configure-controls.md)」を参照してください。

1. **プロパティ**右側のウィンドウのタブ設定**項目**に`FlooringEstimates`と**値**に`Name`します。

    ![フォームの Items プロパティを設定します。](./media/add-form/items-property.png)

    一覧に、データ ソースから取得した床材製品の名前が表示されます。

1. 追加、**編集**コントロールをフォームの下に移動**ChooseProduct**、し、画面の大部分をカバーするためのフォームのサイズを変更します。

    ![フォームを追加する](./media/add-form/add-a-form.png)

    > [!NOTE]
   > このトピックで説明します、**編集**フォームのコントロールが、同様の原則を適用する、**表示**フォーム コントロール。

1. フォームの設定 **[DataSource](controls/control-form-detail.md)** プロパティを**FlooringEstimates**とその **[項目](controls/control-form-detail.md)** プロパティをこの数式では:

    `First(Filter(FlooringEstimates, Name=ChooseProduct.Selected.Value))`

   この式では、フォームの構成が完了した後、**ChooseProduct** でユーザーが選択したレコードが表示されるように指定しています。

1. **プロパティ**選択の右側のウィンドウのタブ**フィールドを編集**します。

    ![フィールドを編集します。](./media/add-form/edit-fields.png)

1. **[フィールド]** ウィンドウで **[フィールドの追加]** を選択し、各フィールドのチェック ボックスをオンにし、**[追加]** を選択します。

    ![フィールドを追加します。](./media/add-form/add-fields.png)

1. 横にある省略記号 (...) を選択します。**フィールドの追加**を選択します**すべて折りたたむ**、し、ドラッグ**名前**一覧の先頭にします。

    ![フィールドに移動します。](./media/add-form/move-field.png)

    **編集**フォーム コントロールには、変更が反映されます。

    ![フォームを表示します。](./media/add-form/show-form1.png)

## <a name="set-the-card-type-for-a-field"></a>フィールドにカードの種類を設定する
1. **フィールド**ウィンドウで、展開、**価格**フィールドで、下向きの矢印を選択します。

1. 開く、**コントロール型**、一覧表示し、**スライダーの編集**します。

    ![スライダーを編集します。](./media/add-form/edit-slider.png)

    フォームで、**価格**フィールド、**スライダー**コントロールの代わりに、**テキスト入力**コントロール。

1. (省略可能)コントロールを変更するのと同じ手順、**概要**フィールドを**複数行のテキストを編集**コントロール。

## <a name="edit-form-only-save-changes"></a>(編集フォームのみ) 変更を保存する

1. フォームの名前を変更**EditForm**します。

1. **[[ボタン]](controls/control-button.md)** コントロールを追加し、**[OnSelect](controls/properties-core.md)** プロパティに次の式を設定します。

   `SubmitForm(EditForm)`

1. F5 キーを押してプレビューを開き、製品の名前を変更して作成したボタンを選択します。

    **[SubmitForm](functions/function-form.md)** 関数は、データ ソースに変更を保存します。

1. (省略可能)Esc キーを押して (または右上隅にある閉じるアイコンを選択して) プレビューを終了します。

## <a name="next-steps"></a>次の手順
[フォーム](working-with-forms.md)と[数式](working-with-formulas.md)についてさらに理解を深める。

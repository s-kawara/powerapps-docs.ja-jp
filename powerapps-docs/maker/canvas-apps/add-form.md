---
title: キャンバスアプリでレコードを表示、編集、または追加する |Microsoft Docs
description: データ ソース内のテーブルのレコードを表示、編集、または追加するには、キャンバス アプリ フォームを使用します。
author: emcoope-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 10/06/2017
ms.author: emcoope
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: ed7493dcc9c2ef5f0b84052a11dbadb0947af38e
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "71994266"
---
# <a name="show-edit-or-add-a-record-in-a-canvas-app"></a>キャンバスアプリでレコードを表示、編集、または追加する

キャンバスアプリでは、レコード内のすべてのフィールドを表示するための **[表示](controls/control-form-detail.md)** フォームコントロールを追加して構成することもできます。また、[フォームの **[編集](controls/control-form-detail.md)** ] コントロールを追加および構成して、レコード内のフィールドを編集したり、レコードを追加したり、変更内容をデータソースに保存したりすることもできます。

## <a name="prerequisites"></a>前提条件

- PowerApps で[コントロールを追加して構成する](add-configure-controls.md)方法について確認します。
- [この Excel ファイル](https://az787822.vo.msecnd.net/documentation/get-started-from-data/FlooringEstimates.xlsx)をダウンロードして、チュートリアルのサンプル データを取得します。
- Excel ファイルを OneDrive for Business などの[クラウド ストレージ アカウント](connections/cloud-storage-blob-connections.md)にアップロードします。
- スマートフォン用のアプリを作成または開き、Excel ファイルの**FlooringEstimates**テーブルに[接続を追加](add-data-connection.md)します。

    タブレットアプリにフォームを追加できますが、フォームには既定で3つの列があるため、このトピックは一致しません。

- 既存のアプリを開いた場合は、[画面を追加](add-screen-context-variables.md)します。

## <a name="add-a-form-and-show-data"></a>フォームを追加し、データを表示する
1. 空の画面で、 **[ドロップダウン](controls/control-drop-down.md)** コントロールを追加し、 **[product]** という名前を指定します。

    > [!NOTE]
   > コントロールの追加、コントロールの名前変更、およびプロパティの設定の方法がわからない場合は、「[Add and configure controls (コントロールの追加と構成)](add-configure-controls.md)」を参照してください。

1. 右側のペインの **[プロパティ]** タブで、 **[項目]** を [`FlooringEstimates`] に設定し、 **[値]** を [`Name`] に設定します。

    ![フォームの Items プロパティを設定する](./media/add-form/items-property.png)

    一覧に、データ ソースから取得した床材製品の名前が表示されます。

1. **編集**フォームコントロールを追加し、 **[product]** の下に移動して、画面の大部分をカバーするようにフォームのサイズを変更します。

    ![フォームを追加する](./media/add-form/add-a-form.png)

    > [!NOTE]
   > このトピックでは、フォームの**編集**コントロールについて説明しますが、同様の原則が**表示**フォームコントロールにも適用されます。

1. フォームの **[DataSource](controls/control-form-detail.md)** プロパティを**FlooringEstimates**に設定し、 **[Item](controls/control-form-detail.md)** プロパティを次の数式に設定します。

    `First(Filter(FlooringEstimates, Name=ChooseProduct.Selected.Value))`

   この式では、フォームの構成が完了した後、**ChooseProduct** でユーザーが選択したレコードが表示されるように指定しています。

1. 右側のペインの **[プロパティ]** タブで、 **[フィールドの編集]** を選択します。

    ![フィールドの編集](./media/add-form/edit-fields.png)

1. **[フィールド]** ウィンドウで **[フィールドの追加]** を選択し、各フィールドのチェック ボックスをオンにし、 **[追加]** を選択します。

    ![フィールドの追加](./media/add-form/add-fields.png)

1. **[追加フィールド]** の横にある省略記号 (...) を選択し、 **[すべて折りたたみ]** を選択し、 **[名前]** を一覧の一番上にドラッグします。

    ![フィールドの移動](./media/add-form/move-field.png)

    **編集**フォームコントロールには、変更が反映されます。

    ![フォームの表示](./media/add-form/show-form1.png)

## <a name="set-the-card-type-for-a-field"></a>フィールドにカードの種類を設定する
1. **[フィールド]** ウィンドウで、下矢印を選択して **[Price]** フィールドを展開します。

1. **[コントロールの種類]** の一覧を開き、 **[スライダーの編集]** を選択します。

    ![スライダーの編集](./media/add-form/edit-slider.png)

    フォームの**Price**フィールドには、**テキスト入力**コントロールではなく、**スライダー**コントロールが表示されます。

1. optional同じプロセスに従って、 **[概要]** フィールドのコントロールを **[複数行テキストの編集]** コントロールに変更します。

## <a name="edit-form-only-save-changes"></a>(編集フォームのみ) 変更を保存する

1. フォームの名前を**editform**に変更します。

1. **[[ボタン]](controls/control-button.md)** コントロールを追加し、 **[OnSelect](controls/properties-core.md)** プロパティに次の式を設定します。

   `SubmitForm(EditForm)`

1. F5 キーを押してプレビューを開き、製品の名前を変更して、作成したボタンを選択します。

    **[Submitform](functions/function-form.md)** 関数は、データソースへの変更を保存します。

1. optionalEsc キーを押して (または右上隅の閉じるアイコンを選択して) プレビューを終了します。

## <a name="next-steps"></a>次の手順
[フォーム](working-with-forms.md)と[数式](working-with-formulas.md)についてさらに理解を深める。

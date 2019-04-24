---
title: 作成し、キャンバス アプリでのコレクションの更新 |Microsoft Docs
description: キャンバス アプリでコレクションを作成、コレクションに項目を追加およびそこから 1 つまたはすべての項目を削除
author: aftowen
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 01/28/2019
ms.author: anneta
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 6089063e2478c95bb5bfbc5926608d85552cea40
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61561623"
---
# <a name="create-and-update-a-collection-in-a-canvas-app"></a>作成し、キャンバス アプリでコレクションを更新

コレクションを使用して、アプリでユーザーを管理するデータを格納します。 コレクションは、製品一覧で製品など、類似した項目のグループです。 さまざまな種類のコレクションなどの変数の詳細については。[キャンバス アプリの変数について](working-with-variables.md)します。

## <a name="prerequisites"></a>前提条件

- PowerApps に[サインアップ](../signup-for-powerapps.md)し、サインアップに使用したのと同じ資格情報を入力して[サインイン](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)します。
- PowerApps で、アプリを作成するか既存のアプリを開きます。
- PowerApps で[コントロールを構成する](add-configure-controls.md)方法について確認します。

## <a name="create-a-multicolumn-collection"></a>複数列のコレクションを作成します。

1. PowerApps Studio では、追加、**テキスト入力**コントロール。

    ![テキスト入力コントロールを挿入します。](./media/create-update-collection/add-textbox.png)

1. 左側のナビゲーション ウィンドウで、省略記号を選択して、コントロールの名前を変更選択**の名前を変更**、」と入力し、 **ProductName**します。

    ![コントロールの名前を変更します。](./media/create-update-collection/rename-textbox.png)

1. 追加、**ドロップダウン**コントロール。

    ![ドロップダウン リストを追加します。](./media/create-update-collection/add-dropdown.png)

1. 名前の変更、**ドロップダウン**コントロール**色**、ことを確認し、**項目**プロパティがプロパティの一覧で選択されています。

    ![Items プロパティ](./media/create-update-collection/items-property.png)

1. 数式バーで置き換えます**DropDownSample**この式を使用します。

    `["Red","Green","Blue"]`

1. 追加、**ボタン**設定、制御、**テキスト**プロパティを **"Add"**、設定とその**OnSelect**プロパティをこの式に。

    ```powerapps-dot
    Collect(
        ProductList,
        {
            Product: ProductName.Text,
            Color: Colors.Selected.Value
        }
    )
    ```

1. F5 キーを押して、テキストを入力**ProductName**でオプションを選択して**色**、し、**追加**します。

    ![アプリのプレビュー](./media/create-update-collection/preview-add.png)

1. さらに、少なくとも 2 回、前の手順を繰り返して、Esc キーを押します。

1. **ファイル**メニューの **コレクション**を作成したコレクションを表示します。

    ![コレクションを表示します。](./media/create-update-collection/show-collection.png)

## <a name="show-a-collection"></a>コレクションを表示します。

1. 垂直方向の追加**ギャラリー**コントロール。

    ![縦方向のギャラリーの追加](./media/create-update-collection/add-gallery.png)

1. ギャラリーの設定**項目**プロパティを **[productlist]** します。

1. **データ**ウィンドウで、字幕のフィールドに設定する**色**、タイトル フィールドを設定および**製品**します。

    ![ギャラリーのアイテムのプロパティを設定し、表示されるフィールドを変更](./media/create-update-collection/configure-gallery.png)

1. 閉じる、**データ**ウィンドウで、ギャラリーを選択し、設定、**レイアウト**フィールドを**タイトルとサブタイトル**します。

    ![ギャラリーのアイテムのプロパティを設定し、表示されるフィールドを変更](./media/create-update-collection/change-layout.png)

    画面には、この例に似ています。

    ![最初の画面例](./media/create-update-collection/screen-example1.png)

## <a name="remove-one-or-all-items"></a>1 つまたはすべての項目を削除します。

1. クリックすると、ギャラリーの下部の近くをタップまたはクリックしてまたは左上隅の鉛筆アイコンをタップしてギャラリー テンプレートを選択します。

    ![ギャラリー テンプレートを選択します。](./media/create-update-collection/select-template.png)

1. 追加、**ごみ箱**アイコン ギャラリー テンプレートにします。

    ![ごみ箱アイコンを追加します。](./media/create-update-collection/trash-icon.png)

1. 設定アイコンの**OnSelect**に次の式のプロパティ。

    `Remove(ProductList, ThisItem)`

1. ギャラリーの外部ボタンを追加、設定、**テキスト**プロパティを **"Clear"**、設定とその**OnSelect**プロパティをこの式に。

    `Clear(ProductList)`

1. Alt キーを押しながら選択、**ごみ箱**、コレクションからその項目を削除するか選択する項目のアイコン、**クリア**コレクションからすべての項目を削除するボタン。

## <a name="put-a-sharepoint-list-into-a-collection"></a>SharePoint リストをコレクションに挿入する

1. [SharePoint リストへの接続を作成します](connections/connection-sharepoint-online.md#create-a-connection)。

1. ボタンを追加して、その **[OnSelect](controls/properties-core.md)** プロパティをこの関数に設定し、以下の *ListName* を SharePoint リストの名前に置き換えます。<br>

    `Collect(MySPCollection, ListName)`

    この関数では、**MySPCollection** という名前の、SharePoint リストと同じデータを含むコレクションを作成します。

1. Alt キーを押しながら、ボタンを選択します。

1. (省略可能)作成したコレクションをプレビューするには、選択**コレクション**上、**ファイル**メニュー。

ギャラリーで (日付、選択、およびユーザー) などの SharePoint リストからデータを表示する方法については。[ギャラリーのリスト内の列を表示する](connections/connection-sharepoint-online.md#show-list-columns-in-a-gallery)します。 (ドロップダウン リスト、日付の選択、およびユーザー ピッカー) を持つフォームでデータを表示する方法については。[フォームおよびフォームの表示コントロールを編集](controls/control-form-detail.md)します。

## <a name="next-steps"></a>次の手順

- レビュー、[リファレンス トピック](functions/function-clear-collect-clearcollect.md)の**収集**関数。
- 使用してコレクション内のデータの整形方法を説明します、 [AddColumns、DropColumns、RenameColumns、および ShowColumns](functions/function-table-shaping.md)関数。

---
title: バーコードをスキャンする | Microsoft Docs
description: UPC や Codabar などのさまざまな種類のバーコードをスキャンします
author: AFTOwen
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 10/23/2016
ms.author: anneta
ms.openlocfilehash: befc72b875f7876bc0f9f907a094f0d97314c03c
ms.sourcegitcommit: dfa0e1a7981814e15e6ca4720e2a5f930e859db1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2018
ms.locfileid: "39023323"
---
# <a name="scan-a-barcode-in-powerapps"></a>PowerApps でバーコードをスキャンする
ざまな種類のバーコードをスキャンするアプリを作成し、カメラ付きのデバイス (携帯電話など) で実行します。 バーコードで表現されている数値が**ラベル** コントロールに表示され、そのデータをさまざまな[データ ソース](connections-list.md)にアップロードできます。

PowerApps の基本的な事柄については、「[PowerApps の概要](getting-started.md)」を参照してください。

## <a name="known-limitations"></a>既知の制限
* バーコードのサイズは、少なくとも高さ 1" (2.5cm)、幅 1.5" (4cm) が必要です。
* 携帯電話でバーコードをスキャンするには、携帯電話を縦向きに保持し、バーコードから 7" (18cm) から 10" (25cm) 離れた位置でゆっくりと動かします。
* 長い種類のバーコード (15 個以上の文字を持つことができる I2of5 など) は切り捨てられるか正しい結果を得られない可能性があります。特にバーコードが明確に印刷されていない場合はこれが発生します。
* iPhone と Android デバイスでは、**バーコード** コントロールの**高さ**プロパティを指定できますが、幅は固定の縦横比によって決まります。
* **バーコード** コントロールの**スキャン レート** プロパティは、**35** 以下に設定しなければならない場合があります。
* iOS を実行しているデバイスでメモリ不足の発生を遅らせるには、**バーコード** コントロールの**高さ**プロパティを **700** (またはそれ以下) に、**スキャン レート** プロパティを **30** に設定します。
* デバイスがメモリ不足になり、アプリがフリーズした場合は、アプリを再起動します。

## <a name="create-a-blank-app"></a>空のアプリを作成する
1. [PowerApps にサインアップ](../signup-for-powerapps.md)し、次の*いずれか一方*の操作を行います。

2. カメラ付きのデバイスで、[PowerApps](https://create.powerapps.com) をブラウザーで開きます。

3. **[Start with a blank canvas or template]** (空のキャンバスまたはテンプレートから開始する) の下の **[空のアプリ]** タイルで **[携帯電話レイアウト]** をクリックまたはタップします。

    ![アプリを最初から作成する](./media/scan-barcode/create-from-blank.png)

4. PowerApps を初めて使用する場合は、クイック ツアーで PowerApps の基本事項を確認できます (不要であれば、**[スキップ]** をクリックまたはタップします)。

    ![クイック ツアーの開始画面](./media/scan-barcode/quick-tour.png)

    > [!NOTE]
   > クイック ツアーは後からいつでも開始できます。右上隅の疑問符アイコンをクリックまたはタップし、**[Take the intro tour (クイック ツアーの開始)]** をクリックまたはタップしてください。

## <a name="add-a-barcode-control"></a>バーコード コントロールの追加
1. **[挿入]** タブで **[メディア]** をクリックまたはタップし、**[バーコード]** をクリックまたはタップします。

    ![バーコード スキャナーの追加](./media/scan-barcode/add-scanner.png)

2. **バーコード** コントロールが選択ボックス (コントロールのサイズを変更するためのハンドル付き) によって囲まれていることを確認します。

    ![選択ボックス](./media/scan-barcode/selection-box.png)

3. **[ホーム]** タブで **[Barcode1]** をクリックまたはタップし、**[名前の変更]** の下に「**MyScanner**」と入力するか貼り付けます。

    > [!TIP]
   > 追加する最初の**バーコード** コントロールは、既定で **Barcode1** という名前になります。 そのコントロールを削除して別の**バーコード** コントロールを追加した場合は、既定で **Barcode2** という名前が付きます。 名前を手動で変更するときは、数式でコントロールが正しい名前で参照されることを確認してください。

    ![バーコード コントロールの名前の変更](./media/scan-barcode/rename-barcode.png)

## <a name="add-a-text-input-control"></a>テキスト入力コントロールを追加する
1. **[挿入]** タブで **[テキスト]** をクリックまたはタップし、**[テキスト入力]** をクリックまたはタップします。

    **[挿入]** タブが表示されない場合は、PowerApps ウィンドウを最大化します。

    ![テキスト入力コントロールの追加](./media/scan-barcode/add-text-input.png)

2. (サイズ変更ハンドルではなく) 選択ボックスを**テキスト入力** コントロールを囲むようにドラッグして、**MyScanner** の下に表示します。

    ![選択ボックスで囲まれたラベル](./media/scan-barcode/move-input-text.png)

3. **テキスト入力**コントロールを選択した状態で、プロパティの一覧に **[既定]** が表示されていることを確認し、数式バーに「**MyScanner.Text**」と入力するか貼り付けます。

    ![ラベル コントロールのテキスト プロパティ](./media/scan-barcode/default-text.png)

## <a name="change-the-barcode-type"></a>バーコードの種類を変更する
1. **[挿入]** タブで **[コントロール]** をクリックまたはタップし、**[ドロップダウン]** をクリックまたはタップします。

    ![ドロップダウン リストの追加](./media/scan-barcode/insert-dropdown.png)

2. **ドロップダウン** コントロールを移動させて、画面上の他のコントロールの下に表示されるようにします。

    ![ドロップダウン リストの移動](./media/scan-barcode/move-dropdown.png)

3. **ドロップダウン** コントロールを選択した状態で、プロパティの一覧に **[項目]** が表示されていることを確認し、数式バーに次のテキスト文字列を入力するか貼り付けます。<br>
    **[Codabar, Code128, Code39, Ean, I2of5, Upc]**

    ![ドロップダウン リストの項目プロパティの設定](./media/scan-barcode/items-property.png)

4. **[ホーム]** タブで、**ドロップダウン** コントロールの名前を「**ChooseType**」に変更します。

    ![ドロップダウン リストの名前変更](./media/scan-barcode/rename-dropdown.png)

5. **[MyScanner]** をクリックするかタップして選択し、プロパティの一覧に **[BarcodeType]** が表示されていることを確認し、数式バーに次のテキスト文字列を入力するか貼り付けます。<br>
    **ChooseType.Selected.Value**

## <a name="test-the-app"></a>アプリケーションをテストする
1. F5 キーを押して (または右上隅の再生ボタンをクリックまたはタップして) プレビュー モードを開始します。

    ![プレビュー モードを開始](./media/scan-barcode/open-preview.png)

2. **ラベル** コントロールにバーコードの数値要素が表示されるまで、デバイスのカメラの前でバーコードを保持します。

    数値要素が表示されない場合は、**BarcodeType** の一覧の別のオプションで試してみます。 それでも適切なデータが表示されない場合は、**入力テキスト** コントロールに適切な数値を入力します。

## <a name="next-steps"></a>次の手順
* [データ ソースにアプリを接続](add-data-connection.md)し、ユーザーが結果を保存できるように **[Patch](functions/function-patch.md)** 関数を構成します。
* **[ドロップダウン](controls/control-drop-down.md)** コントロールを追加し、ユーザーがスキャンするバーコードの種類を選択できるように構成します。
* **[スライダー](controls/control-slider.md)**  コントロールを追加し、ユーザーが**バーコード** コントロールのスキャン レートと高さを調節できるように構成します。

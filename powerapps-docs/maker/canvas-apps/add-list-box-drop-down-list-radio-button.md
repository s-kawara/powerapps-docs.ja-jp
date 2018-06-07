---
title: リスト ボックス、ドロップダウン リスト、ラジオ ボタンを追加する | Microsoft Docs
description: PowerApps で複数選択オプションを作成または構成する
documentationcenter: ''
author: lonu
manager: kfile
editor: ''
ms.service: powerapps
ms.devlang: na
ms.topic: conceptual
ms.component: canvas
ms.date: 10/23/2016
ms.author: lonu
ms.openlocfilehash: 1fbaf4f9d740084a1ed0d630b94d1cd41713ba03
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "31825558"
---
# <a name="add-a-list-box-a-drop-down-list-or-radio-buttons"></a>リスト ボックス、ドロップダウン リスト、ラジオ ボタンを追加する
PowerApps には、複数選択オプションと単一選択オプションがあります。リスト ボックス、ドロップダウン リスト、ラジオ ボタンなどです。 このトピックでは、これらのコントロールを追加し、**テーブル**式を利用してリストを作成します。 ある項目がリストで選択されると、他のコントロールが更新されます。

[!INCLUDE [app-customization-requirements](../../includes/app-customization-requirements.md)]

## <a name="add-a-list-box"></a>リスト ボックスを追加する
1. **[挿入]** タブで **[コントロール]** を選択し、**[リスト ボックス]** を選択します。  

    ![][2]  

2. **リスト ボックス** コントロールの名前を **MyListBox** に変更します。  

    ![][3]

3. その **[Items](controls/properties-core.md)** プロパティを次の式に設定します。  
   ```["circle","triangle","rectangle"]```  <br/>

    デザイナーは次のようになります。

    ![][4]

4. **[挿入]** タブで **[アイコン]** を選択し、円を選択し、それを**リスト ボックス** コントロールの下に移動します。

    ![][5]  

5. 三角形と四角形を追加し、**リスト ボックス** コントロールの下に図形を並べます。

    ![][6]  

6. 次の図形の **[Visible](controls/properties-core.md)** プロパティを次の関数に設定します。  

   | 図形 | 設定する Visible 関数 |
   | --- | --- |
   | 円 |```If("circle" in MyListBox.SelectedItems.Value, true)``` |
   | 三角形 |```If("triangle" in MyListBox.SelectedItems.Value, true)``` |
   | 四角形 |```If("rectangle" in MyListBox.SelectedItems.Value, true)``` |

7. 作成したものをプレビューします ![][1]。 **リスト ボックス** コントロールでさまざまな図形を選択します。 選択した図形のみが表示されます。 Esc を押すか、**X** を選択して自分の画面に戻ります。

以上の手順では、式を利用し、**リスト ボックス** コントロールの項目リストを作成しました。 **リスト ボックス** コントロールで選択した内容に基づき、さまざまな図形が表示されます。 これは自分の作業内の他の要素に適用できます。 たとえば、**リスト ボックス** コントロールを利用し、製品の画像や説明などを表示できます。

## <a name="add-radio-buttons"></a>ラジオ ボタンを追加する
1. **[ホーム]** タブで **[新しい画面]** を選択します。

2. **[挿入]** タブで **[コントロール]** を選択し、**ラジオ** を選択します。

    ![][10]  

3. **ラジオ** コントロールの名前を **Choices** に変更し、その **[Items](controls/properties-core.md)** プロパティをこの式に設定します。  
   ```["red","green","blue"]```  <br/>

    ![][12]  

    必要に応じて、すべてのオプションが表示されるようにコントロールのサイズを変更します。

4. **[挿入]** タブで **[アイコン]** を選択し、円を選択します。

5. 円の **[Fill](controls/properties-color-border.md)** プロパティを次の関数に設定します。  
   ```If(Choices.Selected.Value = "red", RGBA(192, 0, 0, 1), Choices.Selected.Value = "green", RGBA(0, 176, 80, 1), Choices.Selected.Value = "blue", RGBA(0, 32, 96, 1))```  

    この数式では、選択したラジオ ボタンに基づいて円の色が変わります。

6. この例のように **ラジオ** コントロールの下に円を移動します。

    ![][14]  

7. 作成したものをプレビューします ![][1]。 別のラジオ ボタンを選択すると、円の色が変わります。 Esc を押すか、**X** を選択して自分の画面に戻ります。

## <a name="add-a-drop-down-list"></a>ドロップダウン リストを追加する
1. 画面を追加し、**ドロップダウン** コントロールを追加します。

    ![][15]  

2. コントロールの名前を **DDChoices** に変更し、その **[Items](controls/properties-core.md)** プロパティをこの式に設定します。<br>
   **["red","green","blue"]**

3. 円を追加し、**ドロップダウン** コントロールの下にそれを移動し、円の **[Fill](controls/properties-color-border.md)** プロパティをこの式に設定します。  
   ```If(DDChoices.Selected.Value = "red", RGBA(192, 0, 0, 1), DDChoices.Selected.Value = "green", RGBA(0, 176, 80, 1), DDChoices.Selected.Value = "blue", RGBA(0, 32, 96, 1))```

4. 作成したものをプレビューします ![][1]。 別のオプションを選択すると、円の色が変わります。

[1]: ./media/add-list-box-drop-down-list-radio-button/preview.png
[2]: ./media/add-list-box-drop-down-list-radio-button/listbox.png
[3]: ./media/add-list-box-drop-down-list-radio-button/renamelistbox.png
[4]: ./media/add-list-box-drop-down-list-radio-button/itemslistbox.png
[5]: ./media/add-list-box-drop-down-list-radio-button/circle.png
[6]: ./media/add-list-box-drop-down-list-radio-button/allshapes.png
[10]: ./media/add-list-box-drop-down-list-radio-button/radiobutton.png
[12]: ./media/add-list-box-drop-down-list-radio-button/itemsradio.png
[14]: ./media/add-list-box-drop-down-list-radio-button/radiocircle.png
[15]: ./media/add-list-box-drop-down-list-radio-button/dropdown.png

---
title: コレクションの作成と更新 | Microsoft Docs
description: PowerApps でコレクションを作成し、既存のコレクションに列を追加します
documentationcenter: ''
author: lonu
manager: kfile
editor: ''
ms.service: powerapps
ms.devlang: na
ms.topic: conceptual
ms.component: canvas
ms.date: 11/30/2015
ms.author: lonu
ms.openlocfilehash: 26cf15054a1cf5d00bda0e2f265ed242cb21421c
ms.sourcegitcommit: 8bd4c700969d0fd42950581e03fd5ccbb5273584
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="create-and-update-a-collection-in-your-app"></a>アプリのコレクションの作成と更新
コレクションを使用すると、アプリで使用できるデータを格納できます。 コレクションとは、類似の項目で構成されるグループです。 たとえば、MyImages というコレクションを作成して、企業が販売する製品の画像をすべてそこに格納することができます。 PowerApps では、MyImages コレクションを追加できるほか、これらの製品の画像をすべて表示するアプリを作成することができます。 別の例では、製品と各製品の価格を一覧表示する PriceList コレクションを作成できます。

コレクションは PowerApps 内で作成して使用できます。 それでは、始めましょう。

### <a name="prerequisites"></a>前提条件
* PowerApps に[サインアップ](../signup-for-powerapps.md)し、[インストール](http://aka.ms/powerappsinstall)して開きます。その後、サインアップに使用したのと同じ資格情報を入力してサインインします。
* PowerApps で、アプリを作成するか既存のアプリを開きます。
* PowerApps で[コントロールを構成する](add-configure-controls.md)方法について確認します。
* この記事の手順では、サンプルの入力データとして [PriceList.zip](http://pwrappssamples.blob.core.windows.net/samples/PriceList.zip) ファイルを使用します。 この zip ファイルには、Excel に変換できる XML ファイルが含まれています。 変換できなくても、.zip ファイル内のファイルは PowerApps によって自動的に読み取られ、正常にインポートされます。 このサンプル データをダウンロードして使用することも、独自のデータをインポートすることもできます。

## <a name="create-a-single-column-collection"></a>単一列コレクションの作成
次の手順では、Collect 関数を使用してアプリ内でコレクションを作成する方法と、コレクションに項目を追加する方法について説明します。

1. アプリを開きます。
2. **[挿入]** タブで、**[テキスト]**、**[テキスト入力]** の順に選択します。  
   ![][1]  
3. 左上隅で **[Text1]** を選択し、コントロールの名前を「**Destinations**」に変更します。  
   ![][2]  
4. **[挿入]** タブで **[ボタン]** を選択し、ボタン コントロールをデザイナーに追加します。 ドロップダウン リストで **[OnSelect](controls/properties-core.md)** プロパティを表示します。 それを次の関数に設定します。  
   
    ```Collect(Destinations, Destination!Text)```
   
    これは次のようになります。  
    ![][3]  
5. ボタン テキストを選択し、「**Add**」と入力します。  
   ![][5]  
6. **[Add]** ボタンを選択し、テキスト コントロールの下に移動します。 ボタンは好きな場所に移動できます。  
   ![][6]  

上記の手順では、Collect 関数を使用して、**Destinations** という名前のコレクションを作成しました。 さらに、ボタン コントロールを追加しました。このボタンを選択すると、コレクションに新しい項目が追加されます。 ここで、作成した内容を確認します。

1. プレビューを選択します。  
   ![][7]  
2. 都市名をボックスに入力し、**[Add]** ボタンを選択します。
3. さらにいくつかの都市名を入力します。その都度、**[Add]** ボタンを選択します。
4. **Esc** キーを押してプレビュー ウィンドウを閉じます。
5. Destinations コレクションと入力したテキスト値を確認します。 **[ファイル]** タブで **[コレクション]** を選択します。 入力したテキストが表示されます。  
   ![][8]

#### <a name="extra-credit"></a>追加の手順
ここで、Destinations コレクションをリスト ボックスに関連付けます。

1. デザイナーに戻ります。
2. **[挿入]** タブで **[コントロール]** を選択し、**[リスト ボックス]** を選択します。  
   ![][22]  
3. 見やすいようにリスト ボックスを移動します。 その **[Items](controls/properties-core.md)** プロパティを次の式に設定します。  
   ```Destinations!Value```  <br/>
   
    この設定を行うと、Destinations コレクションで先ほど入力した項目が自動的にリスト ボックスに設定されます。  
   ![][4]  

変更をプレビューします (![][7])。 リスト ボックスに、入力した各都市が表示されます。 テキスト入力コントロールで新しい都市を入力し、**[追加]** ボタンを選択します。 リスト ボックスは自動的に更新されて、入力した新しい都市が表示されます。

## <a name="create-a-multi-column-collection"></a>複数列コレクションの作成
次の手順では、Collect 関数を使用してアプリ内のコレクションを作成する方法と、コレクションに複数の行を追加する方法について説明します。

1. **[ホーム]** タブで新しい画面を開きます。
2. **[挿入]** タブで、**[テキスト]**、**[テキスト入力]** の順に選択します。
3. テキスト コントロールの名前を「**City**」に変更します。  
   ![][9]  
4. もう 1 つテキスト入力コントロールを挿入し、名前を「**States**」に変更します。
5. City と States の両方のテキスト コントロールを見やすいように移動します。  
   ![][10]  
   
    > [!NOTE]
> "Text Input (テキスト入力)" は、画像のように "City" または "State" などに置き換えることができます。  
6. **[挿入]** タブの **[ボタン]** を選択します。 その **[OnSelect](controls/properties-core.md)** プロパティを次の関数に設定します。  
   ```Collect(Destinations, {Cities:City!Text, States:States!Text})```  
   
    これは次のようになります。  
    ![][11]  
   
    > [!NOTE]
> この関数は、このコレクションに列を追加する際にも使用できます。 たとえば、国を表すテキスト入力コントロールをもう 1 つ追加して、Countries 列を追加することができます。
   
    `Collect(Destinations, {Cities:City!Text, States:States!Text}, {Countries:Country!Text})`
7. ボタン コントロールの名前を「**AddCityStateButton**」に変更し、その **[Text](controls/properties-core.md)** プロパティを **Add City and State** に設定します。  
   ![][12]  

上記の手順では、**City** 列と **States** 列を **Destinations** コレクションに追加しました。 ボタン コントロールを使用すると、これらの新しいテキスト項目がコレクションに追加されます。 ここで、作成した内容を確認します。

1. プレビューを選択します。  
   ![][7]  
2. City ボックスと State ボックスにテキストを入力し、**[Add City and State]** ボタンを選択します。
3. さらにいくつかの都市と州を追加します。
4. **Esc** キーを押してプレビュー ウィンドウを閉じます。
5. Destinations コレクションに追加した項目を確認するには、**[ファイル]** タブを選択し、**[コレクション]** を選択します。  
   ![][13]

## <a name="add-columns-to-a-collection"></a>コレクションへの列の追加
このチュートリアルにはいくつかのセクションがあります。 このチュートリアルを完了すると、コレクションにデータをインポートする方法、価格表のデータを表示するギャラリーの作成方法、製品の数量を決定するスライダー コントロールの使用方法がわかるようになります。

### <a name="import-the-price-list-and-create-the-collection"></a>価格表のインポートとコレクションの作成
1. [PriceList](http://pwrappssamples.blob.core.windows.net/samples/PriceList.zip) zip ファイルをダウンロードします。
2. **[ホーム]** タブで新しい画面を追加します。
3. **[挿入]** タブで **[コントロール]** を選択し、**[インポート]** を選択します。  
   ![][14]  
4. **[Action (操作)]** タブで **OnSelect** を選択します。 次の関数を入力します。  
   
    ```Collect(PriceList, Import1!Data)```  
5. アプリをプレビューします。 **[Import Data (データをインポート)]** ボタンを選択し、PriceList.zip ファイルを選択して、**[開く]** を選択します。
6. プレビュー ウィンドウを閉じます。
7. **[ファイル]** タブを選択し、**[コレクション]** を選択します。 インポートした PriceList 項目が一覧表示されます。  
   ![][15]

### <a name="add-the-gallery-to-show-the-collection-items"></a>コレクション項目を表示するギャラリーの追加
1. デザイナーに戻ります。
2. **[挿入]** タブで **[ギャラリー]** を選択し、**[カスタム ギャラリー]** まで下へスクロールして、**[縦]** を選択します。    
   ![][16]  
3. ギャラリーの名前を **PriceGallery** に変更し、**[Items](controls/properties-core.md)** プロパティを **PriceList** に設定します。  
   ![][18]  
4. **[Import Data (データをインポート)]** コントロールの下に PriceList ギャラリーを移動します。 ギャラリーの枠線を選択し、クリック アンド ドラッグを使用して、3 つの四角形が見えるようにギャラリーのサイズを変更します。
5. ギャラリーの最初の四角形を選択し、3 つのラベルを追加します (**[挿入]** タブ、**[ラベル]** の順に選択)。
6. ラベルのサイズを変更し、最初の四角形の上部に 1 列に並べます。 ギャラリーは次のようになります。  
   ![][19]
7. 各ラベルの **[Text](controls/properties-core.md)** プロパティを次の式に設定します。  
   
   | ラベル | Text プロパティの設定 |
   | --- | --- |
   | Label1 |``ThisItem!Name`` |
   | Label2 |``Text(ThisItem!Price, "$#")`` |
   | Label3 |``ThisItem!Maker`` |
   
    この設定を行うと、PriceList コレクション内の名前、価格、メーカーの値でラベルが自動的に更新されます。
8. ラベルとギャラリーのサイズを変更して余分なスペースをなくします。 画面は次のようになります。  
   ![][17]

### <a name="add-the-quantity-slider-and-update-the-collection"></a>数量のスライダーの追加とコレクションの更新
1. **[挿入]** メニューで **[コントロール]** を選択し、**[スライダー]** を選択します。 スライダーの名前を **OrderQty** に変更し、ギャラリーの下に移動します。
2. ボタンを追加してその **[Text](controls/properties-core.md)** プロパティを **Add** に設定し、**OrderQty** スライダーの下に移動します。 アプリは次のようになります。  
   ![][20]
3. **[Add]** ボタンの **[OnSelect](controls/properties-core.md)** プロパティを次の式に設定します。  
   
    ```Collect(OrderList, {Name:PriceGallery!Selected!Name, Qty:OrderQty!Value, Cost:OrderQty!Value*LookUp(PriceList, PriceGallery!Selected!Name in Name, Price)});SaveData(OrderList, "orderfile")```  
   
    > [!NOTE]
> 後でこのボタンを選択し、**OrderList** という名前のコレクションを作成して保存します。 このコレクションには、ギャラリーに入力する製品名、スライダーで選択する数量、その数量と製品の価格を掛けて計算される総コストが含まれます。
4. **[画面]** タブを選択し、**[OnVisible](controls/control-screen.md)** プロパティを次の式に設定します。  
   
    ```If(IsEmpty(PriceList), LoadData(PriceList, "pricefile"));If(IsEmpty(OrderList), LoadData(OrderList, "orderfile"))```

ここで、作成した内容を確認します。

1. **プレビュー**を開きます。
2. ギャラリーで製品を選択し、スライダーを目的の数量に移動して、**[Add]** ボタンを選択します。  
   
   > [!IMPORTANT]
   > 製品を選択しても、この製品を選択したことを示すように強調表示されません。 強調表示の機能はギャラリーの作成時に追加しませんでした。 製品をクリックすると製品が選択されることを把握しておいてください。  
   > 
   > 
3. これらの手順を繰り返し、さらにいくつかの製品を追加します。 **Esc** キーを押してプレビュー ウィンドウを閉じます。
4. **[ファイル]** タブで **[コレクション]** を選択し、作成した **OrderList** コレクションのプレビューを表示します。  
   ![][21]

> [!TIP]
> 注文リストからすべての項目を削除するには、ボタンを追加し、その **[Text](controls/properties-core.md)** プロパティを **Clear** に設定して、**[OnSelect](controls/properties-core.md)** プロパティを次の式に設定します。  
> ```Clear(OrderList);SaveData(OrderList, "orderfile")```  
> 項目を 1 つずつ削除するには、ギャラリーの **OrderList** コレクションを表示し、そのギャラリーのラベルの **[OnSelect](controls/properties-core.md)** プロパティを次の式に設定します。  
> ```Remove(OrderList, ThisItem);SaveData(OrderList, "orderfile")```
> 
> 

## <a name="tips-and-tricks"></a>ヒントとコツ
* いつでもプレビュー ボタン (![][7]) を選択して、グラフを表示したり、グラフのデータがどのように表示されるかを確認したりできます。
* アプリの設計時に、コントロールのサイズを変更したり、クリック アンド ドラッグでコントロールを移動したりできます。

## <a name="what-you-learned"></a>学習した内容
このトピックでは次の操作を行いました。

* Collect() 関数を使用して、アプリ内にコレクションを作成しました。
* ボタン コントロールを追加しました。このボタンを選択すると、コレクションに新しい項目が追加されます。
* リスト ボックスを使用してコレクションに項目を追加しました。
* スライダー コントロールを追加してコレクション内の項目を更新しました。

[1]: ./media/create-update-collection/insertmenu-inputtext.png
[2]: ./media/create-update-collection/renametext.png
[3]: ./media/create-update-collection/buttononselect.png
[4]: ./media/create-update-collection/listboxpreview.png
[5]: ./media/create-update-collection/buttontext.png
[6]: ./media/create-update-collection/buttonundertext.png
[7]: ./media/create-update-collection/preview.png
[8]: ./media/create-update-collection/existingcollections.png
[9]: ./media/create-update-collection/renametext-city.png
[10]: ./media/create-update-collection/citystate.png
[11]: ./media/create-update-collection/buttononselectcitystate.png
[12]: ./media/create-update-collection/buttononcitystate.png
[13]: ./media/create-update-collection/existingcollectionscitystate.png
[14]: ./media/create-update-collection/import.png
[15]: ./media/create-update-collection/pricelistcollection.png
[16]: ./media/create-update-collection/portrait.png
[17]: ./media/create-update-collection/resizedgallery.png
[18]: ./media/create-update-collection/galleryitems.png
[19]: ./media/create-update-collection/gallerylabels.png
[20]: ./media/create-update-collection/slider.png
[21]: ./media/create-update-collection/existingcollectionsorderlist.png
[22]: ./media/create-update-collection/listbox.png

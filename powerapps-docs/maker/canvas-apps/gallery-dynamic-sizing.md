---
title: ギャラリーで異なる高さのアイテムを表示する | Microsoft Docs
description: 高さ調整可能なギャラリーを追加し、自動でギャラリーの各アイテムのコンテンツの分量に合わせるように構成する
author: fikaradz
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 04/01/2017
ms.author: fikaradz
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: b724bff09e02a3f69166b3c3357833804c8172b6
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "42834844"
---
# <a name="show-items-of-different-heights-in-a-powerapps-gallery"></a>PowerApps ギャラリーで異なる高さのアイテムを表示する
データ セットの各アイテムの同一フィールドに含まれるデータ量が異なる場合、含まれるデータを量が少ないアイテムの後にスペースを挿入しなくても、データ量が多いアイテムの全体を表示することができます。 **高さ可変**ギャラリーを追加し、次の操作を行えるように構成します。

* コンテンツに合わせて伸縮するように**ラベル** コントロールを構成する。
* 各コントロールを、上にあるコントロールのすぐ下に自動で表示されるように配置する。

このチュートリアルでは、**高さ可変**ギャラリー コントロールにフローリング製品に関するデータを表示します。 各製品画像は、概要の行数が 5 行と 2 行のどちらの場合でも概要の 5 ピクセル下に表示します。

![完成版のアプリ](./media/gallery-dynamic-sizing/dynamic-app.png)

**推奨記事**

ギャラリーにコントロールを追加したことがない場合は、このトピックの先へ進む前に[アイテムのリストの表示](add-gallery.md)に関するページを参照してください。

## <a name="add-data-to-a-blank-app"></a>空のアプリにデータを追加する
1. [この Excel ファイル](https://az787822.vo.msecnd.net/documentation/get-started-from-data/FlooringEstimates.xlsx)をダウンロードします。このファイルには、フローリング製品の名前、概要、画像へのリンクが含まれています。

    ![フローリング製品](./media/gallery-dynamic-sizing/flooring-products.png)

2. Excel ファイルを、OneDrive、Dropbox、Google Drive などのクラウドストレージ アカウントにアップロードします。

3. PowerApps Studio の **[ファイル]** メニューの **[新規]** をクリックまたはタップします。

4. **[空のアプリ]** タイルで、**[携帯電話レイアウト]** をクリックまたはタップします。

    ![[ファイル] メニューの [新規] オプション](./media/gallery-dynamic-sizing/blank-app.png)

5. Excel ファイル内の **FlooringEstimates** テーブルへの接続を追加します。

    詳細については、[接続の追加](add-data-connection.md)に関するページを参照してください。

## <a name="add-data-to-a-gallery"></a>ギャラリーにデータを追加する
1. **[挿入]** タブの **[ギャラリー]** をクリックまたはタップし、**[変動する高さ]** をクリックまたはタップします。

    ![ギャラリーを追加する](./media/gallery-dynamic-sizing/add-flexible.png)
2. 画面全体を占めるようにギャラリーのサイズを変更します。

3. ギャラリーの **[Items](controls/properties-core.md)** プロパティを **FlooringEstimates** に設定します。

## <a name="show-the-product-names"></a>製品名を表示する
1. ギャラリーの左上隅にある鉛筆アイコンをクリックまたはタップして、ギャラリー テンプレートを選択します。

    ![鉛筆のアイコン](./media/gallery-dynamic-sizing/edit-template.png)

2. ギャラリー テンプレートを選択した状態で、**[ラベル](controls/control-text-box.md)** コントロールを追加します。

3. **ラベル** コントロールの **Text** プロパティに次の式を設定します。<br>
   **ThisItem.Name**

    ![ラベルの追加](./media/gallery-dynamic-sizing/add-text-box.png)

## <a name="show-the-product-overviews"></a>製品の概要を表示する
1. ギャラリー テンプレートを選択した状態で、別の**ラベル** コントロールを追加し、1 番目の**ラベル** コントロールの下に移動させます。  

2. 2 番目の**ラベル** コントロールの **Text** プロパティに、次の式を設定します。<br> **ThisItem.Overview**

3. 2 番目の**ラベル** コントロールを選択した状態で、**[コンテンツ]** タブの名前タグ アイコンをクリックまたはタップし、コントロールの名前を **OverviewText** (概要テキスト) に変更します。

    ![ラベルの名前を変更する](./media/gallery-dynamic-sizing/rename-text-box.png)

4. **OverviewText** ボックスの **AutoHeight** プロパティを **true** に設定します。

    この手順により、ボックスがそのコンテンツに合わせて伸縮するようになります。

      ![テキストの高さの自動設定](./media/gallery-dynamic-sizing/autoheight-text.png)

## <a name="show-the-product-images"></a>製品画像を表示する
1. テンプレートのサイズを、高さが 2 倍になるように変更します。

    アプリの作成時にテンプレートへコントロールを追加しやすくなりました。この変更はアプリの実行時の見た目に影響しません。

2. ギャラリー テンプレートを選択した状態で、**[イメージ](controls/control-image.md)** コントロールを追加し、**OverviewText** ボックスの下に移動させます。

3. **イメージ** コントロールの **Image** プロパティに次の式を設定します。<br>
    **ThisItem.Image**

4. 次の式のように、**OverviewText** ボックスの位置とサイズを基に**イメージ** コントロールの **[Y](controls/properties-core.md)** プロパティを設定します。
   <br>**OverviewText.Y + OverviewText.Height + 5**

    ![完成版のアプリ](./media/gallery-dynamic-sizing/final-app.png)

他のコントロールを追加する場合も考え方は同じです。各コントロールの **Y** プロパティを、その上にあるコントロールの **Y** プロパティと **Height** プロパティに基づいて設定します。

## <a name="next-steps"></a>次の手順
[ギャラリー](working-with-forms.md) コントロールと[数式](working-with-formulas.md)の使用方法について確認してください。

---
title: グラフの作成 | Microsoft Docs
description: さまざまなカテゴリのデータを折れ線グラフ、円グラフ、棒グラフで表示します
author: lonu
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 10/23/2016
ms.author: lonu
ms.openlocfilehash: 5fecc52a5100f2ed0d045fd0ebdc3834f83d5b39
ms.sourcegitcommit: 0e9af8cace2bdc04750f4c5a70a3c4af8e3d2292
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/22/2018
ms.locfileid: "39195912"
---
# <a name="show-data-in-a-line-pie-or-bar-chart-in-powerapps"></a>PowerApps でデータを折れ線グラフ、円グラフ、棒グラフで表示する
折れ線グラフ、円グラフ、棒グラフを使ってデータを表示することができます。 グラフを扱うとき、インポートするデータは次のような構造になっている必要があります。

* 各系列が先頭行に入力されていること。
* ラベルが左端の列に入力されていること。

たとえば、データは次のようになっている必要があります。

![][9]

これらのグラフは PowerApps 内で作成し、使用することができます。 それでは、始めましょう。

## <a name="prerequisites"></a>前提条件
* PowerApps に[サインアップ](../signup-for-powerapps.md)し、サインアップに使用したのと同じ資格情報で[サインイン](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)します。
* [テンプレート](get-started-test-drive.md)、[データ](get-started-create-from-data.md)、または[ゼロ](get-started-create-from-blank.md)からアプリを作成します。
* PowerApps で[コントロールを構成する](add-configure-controls.md)方法について確認します。
* [ChartData.zip](http://pwrappssamples.blob.core.windows.net/samples/ChartData.zip) をダウンロードします。このファイルには、サンプル データが XML ファイルとして格納されています。 このトピックの手順に従って直接アプリにインポートしてください。 または .zip ファイルを展開し、XML ファイルを Excel で開いて、[クラウド ストレージ アカウント](connections/cloud-storage-blob-connections.md)に保存します。

## <a name="import-the-sample-data"></a>サンプル データをインポートする
以降の手順では、**ProductRevenue** という名前のコレクションにサンプル データをインポートします。

1. **[挿入]** タブで **[コントロール]** を選択し、**[インポート]** を選択します。  

    ![][11]  

2. このコントロールの **[OnSelect](controls/properties-core.md)** プロパティを次の関数に設定します。  

   ```Collect(ProductRevenue, Import1.Data)```

3. F5 を押してプレビュー モードで開き、**[データのインポート]** ボタンを選択します。

4. **[開く]** ダイアログ ボックスで ChartData.zip を選択し、**[開く]** を選択して Esc キーを押します。

5. **[ファイル]** メニューの **[コレクション]** を選択します。

    ProductRevenue コレクションが、インポートしたグラフ データと共に表示されます。

    ![][1]  

   > [!NOTE]
   > インポート コントロールの目的は、Excel と同様のデータをインポートしてコレクションを作成することです。 インポート コントロールによってデータがインポートされるのは、アプリの作成時とアプリのプレビュー時です。 現在、アプリの発行時には、データはインポートされません。
   >

6. Esc キーを押して既定のワークスペースに戻ります。

## <a name="add-a-pie-chart"></a>円グラフを追加する
1. **[挿入]** タブの **[グラフ]** を選択し、**[円グラフ]** を選択します。

2. **[データのインポート]** ボタンの下に円グラフを移動します。

3. 円グラフ コントロールで、円グラフの中心を選択します。   

    ![][10]

4. 円グラフの **[Items](controls/properties-core.md)** プロパティを式 `ProductRevenue.Revenue2014` に設定します。

    ![][2]  

    円グラフに、2014 年の売上データが表示されます。

    ![][3]  

## <a name="add-a-bar-chart-to-display-your-data"></a>棒グラフを追加してデータを表示する
今度は、この ProductRevenue コレクションを棒グラフで表示してみましょう。

1. **[ホーム]** タブでスクリーンを追加します。

2. **[挿入]** タブの **[グラフ]** を選択し、**[縦棒グラフ]** を選択します。

3. 縦棒グラフの中心を選択します。 縦棒グラフの **[Items](controls/properties-core.md)** プロパティを ```ProductRevenue``` に設定します。

    ![][12]  

    縦棒グラフに、2012 年の売上データが表示されます。

    ![][4]  

4. 縦棒グラフの中央の正方形を選択します。

    ![][5]

5. **[グラフ]** タブで **[系列の数]** を選択し、数式バーに「**3**」と入力します。

    ![][6]  

    縦棒グラフに、3 年間にわたる各製品の売上データが表示されます。

    ![][7]  

[1]: ./media/use-line-pie-bar-chart/productrevenuecollection.png
[2]: ./media/use-line-pie-bar-chart/itemsexpression.png
[3]: ./media/use-line-pie-bar-chart/piechart.png
[4]: ./media/use-line-pie-bar-chart/columnchart.png
[5]: ./media/use-line-pie-bar-chart/columnchartseries.png
[6]: ./media/use-line-pie-bar-chart/columnchartseriesfunction.png
[7]: ./media/use-line-pie-bar-chart/columnchartthreeyears.png
[8]: ./media/use-line-pie-bar-chart/preview.png
[9]: ./media/use-line-pie-bar-chart/tableformat.png
[10]: ./media/use-line-pie-bar-chart/middlepiechart.png
[11]: ./media/use-line-pie-bar-chart/import.png
[12]: ./media/use-line-pie-bar-chart/itemscolumnchart.png

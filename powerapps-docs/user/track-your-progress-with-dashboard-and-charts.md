---
title: モデル駆動型アプリでダッシュボードとグラフを使用して進行状況を追跡する |MicrosoftDocs
ms.custom: ''
author: mduelae
manager: kvivek
ms.service: powerapps
ms.component: pa-user
ms.topic: conceptual
ms.date: 10/4/2019
ms.author: mduelae
ms.reviewer: ''
ms.assetid: ''
search.audienceType:
- enduser
search.app:
- PowerApps
- D365CE
- D365CE
ms.openlocfilehash: e9d046c49a2a91aaf5c65094d446ae09f41572f9
ms.sourcegitcommit: 4c35aedde46380d5438687ae6f61a3b0cc7e7e2f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2019
ms.locfileid: "71969083"
---
# <a name="track-your-progress-with-dashboards-and-charts"></a>ダッシュボードとグラフを使って進行状況を追跡する

ダッシュボードは、アプリデータのコレクションを取得し、主要業績評価指標 (KPI) やその他の重要なデータを読みやすい対話型のグラフやグラフに表示するための洞察を提供します。 ダッシュボードは、すべてのレコードの種類で使用できます。

> [!div class="mx-imgBorder"]
> ![ダッシュボード](media/Dashboard.png "ダッシュボード") 

-  別のダッシュボードレイアウトを表示するには、ダッシュボードの名前の横にある下矢印を選択し、目的のレイアウトを選択します。
-  既定のダッシュボードを選択するには、目的のダッシュボードを表示し、画面の上部にある **[既定値として設定]** を選択します。

   > [!div class="mx-imgBorder"]
   > ダッシュボードの追加また![は変更](media/add_dashboard.png "ダッシュボードの追加または変更") 

## <a name="create-a-new-dashboard"></a>新しいダッシュボードを作成する

1. 新しいダッシュボードを作成するには、 **[Dynamics 365 ダッシュボードの作成]** を選択します。 

   > [!div class="mx-imgBorder"]
   > 新しい![ダッシュボードを追加]する(media/new_dashboard.png "新しいダッシュボード")を追加する
   
2. ダッシュボードのレイアウトを選択し、 **[作成]** を選択します。  

   > [!div class="mx-imgBorder"]
   > ダッシュボードを![作成]する(media/create_dashboard.png "ダッシュボードを")作成する
 
3. ダッシュボードの名前を入力します。 
4. ダッシュボードの各領域に必要なものを追加します。 たとえば、グラフを追加してみましょう。 

   > [!div class="mx-imgBorder"]
   > ![グラフの]追加グラフ(media/add_chart.png "の")追加
 
 5. グラフの**レコードの種類**を選択します。
 6. グラフ内のデータが表示される**ビュー**を選択します。
 7. グラフを選択し、 **[追加]** を選択します。
 8. ダッシュボードへのコンポーネントの追加を続行し、完了したら **[保存]** を選択します。 
 
作成したダッシュボードは、使用可能なダッシュボードのドロップダウンメニューに表示されます。

## <a name="use-charts"></a>グラフを使用する 

グラフを使用すると、目標を追跡する方法を簡単に確認できます。 また、対話型であるため、グラフの領域をクリックまたはタップして詳細情報を表示できます。

-   グラフの上にマウスポインターを置くと、グラフのその領域についての簡単な情報を示すツールヒントが表示されます。
-   グラフの領域をクリックすると、グラフ内のデータに関する詳細を含むグリッドビューが表示されます。
-   グラフを展開するに**は、[** ![グラフの]展開]、[グラフビューの(media/expandviewbutton.png "展開")] の順に展開します。
-   グラフのレコードを表示したり、グラフを更新したりするには、[![その他のコマンド]] を選択し、レコードの **[更新]** または **[レコードの表示]** を(media/MoreButton.png "選択します")。
     
     > [!div class="mx-imgBorder"]
     > Powerapps(media/ViewOfCharts.png "でのグラフの powerapps ビュー") ![でのグラフの表示]  
       

**グラフビューを変更する**
 
グラフビューを変更すると、特定の期間内に開かれた営業案件など、データのさまざまな内訳が表示されます。 グラフビューを変更するには、グリッドページでビューセレクターを選択します。

たとえば、[すべての営業案件] を選択し、別のビューを選択すると、グラフとグリッドの両方が更新されます。

> [!div class="mx-imgBorder"]
> ![Powerapps でのグラフビューの変更](media/ChangeChartView.png "powerapps でのグラフビューの変更")

## <a name="known-issues"></a>既知の問題  
グラフデザイナーでは、特定の計算フィールドに order by を追加することはサポートされていないため、エラーが発生します。  この原因となった計算フィールドは、別の計算フィールド、関連エンティティフィールド、またはエンティティのローカルフィールドを使用します。




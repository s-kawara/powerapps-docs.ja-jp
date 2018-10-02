---
title: PowerApps でモデル駆動型アプリ システム グラフを作成または編集 | MicrosoftDocs
description: グラフを作成または編集する方法を学習する
ms.custom: ''
ms.date: 05/23/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - PowerApps
author: Mattp123
ms.assetid: e02d58f7-6b1c-4a51-b801-a4d9f24729c5
caps.latest.revision: 29
ms.author: matp
manager: kvivek
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="create-a-model-driven-app-system-chart"></a>モデル駆動型アプリ システム グラフを作成する

このトピックでは、システム グラフの作成方法について説明します。 システム グラフは、組織所有のグラフであり、アプリを実行しているデータを読み取るためのアクセス権を持つユーザーはだれでも使用できるようになります。 システム グラフは、特定のアプリ ユーザーに割り当てたり共有したりすることはできません。  
  
1. [PowerApps](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) サイトで、**モデル駆動型** (ナビゲーション ウィンドウの左下) を選択します。  

     ![モデル駆動型の設計モード](media/model-driven-switch.png)

    > [!IMPORTANT]
    > **モデル駆動型** デザイン モードがない場合は、[環境の作成](https://docs.microsoft.com/powerapps/administrator/create-environment)が必要となることがあります。     
  
2. **データ**を展開して**エンティティ**を選択し、目的のエンティティを選択して**グラフ** タブを選択します。  
  
3.  ツール バーで、**グラフの追加** を選択します。  
  
4.  グラフの種類およびデータをグラフに表示する方法を指定します。  
  
    -   *取引先企業ごとの従業員数*など、グラフの名前を入力します。  
  
    -   **フィールドの選択** ドロップダウンで次の作業を行います。 
        - **フィールドの選択** の **系列** 軸ドロップダウンで **従業員数**などのフィールドを選択します。  
        - **フィールドの選択** の **カテゴリ** 軸ドロップダウンで、**取引先企業名** などのフィールドを選択します。
  
    -   *この縦棒グラフには、取引先企業名ごとに従業員数が表示されます* など、グラフの目的を識別できる説明を追加します。 

    > [!div class="mx-imgBorder"] 
    > ![グラフの例](media/sample-chart.png)
  
5.  **保存して閉じる**を選択します。  

## <a name="next-steps"></a>次のステップ  
[ダッシュボードの作成または編集](create-edit-dashboards.md)

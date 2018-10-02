---
title: PowerApps でモデル駆動型アプリ ビューを作成または編集 | MicrosoftDocs
description: ビューを作成または編集する方法を学習する
ms.custom: ''
ms.date: 06/11/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - powerapps
author: Mattp123
ms.assetid: bd1d393d-16ea-40ac-8136-26643c37dd2a
caps.latest.revision: 25
ms.author: matp
manager: kvivek
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="create-or-edit-a-model-driven-app-view"></a>モデル駆動型アプリ ビューを作成または編集する

<a name="BKMK_CreatingAndEditingViews"></a>   

 このトピックでは、新しい共有ビューを作成します。 既存のビューも編集します。  
  
### <a name="create-a-new-view"></a>ビューの新規作成  
  
1.  [PowerApps](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) サイトで、**モデル駆動型** (ナビゲーション ウィンドウの左下) を選択します。  

    ![モデル駆動型の設計モード](media/model-driven-switch.png)

    > [!IMPORTANT]
    > **モデル駆動型** デザイン モードがない場合は、[環境の作成](https://docs.microsoft.com/powerapps/administrator/create-environment)が必要となることがあります。 

2.  **データ**を展開して**エンティティ**を選択し、**取引先企業**エンティティを選択して**ビュー** タブを選択します。 

3.  ツール バーで、**ビューの追加** を選択します。  

4.  **ビューのプロパティ** ダイアログ ボックスで、**25 人以上の従業員がいる取引先企業**などの**名前**を指定し、必要に応じてビューの**説明**を入力して **OK** を選択します。

    > [!div class="mx-imgBorder"] 
    > ![プロパティの表示](media/view-properties.png)
  
5.  [タスク] の右側のウィンドウで、**列の追加** を選択し、**列の追加** ダイアログ ボックスで **従業員数** を選択して **OK** を選択します。  

    > [!div class="mx-imgBorder"] 
    > ![[従業員数] 列](media/column-no-employees.png)
  
6. [タスク] の右側のウィンドウで、**フィルター条件の編集** を選択して、[フィルター条件の編集] ダイアログ ボックスで **従業員数** を選択し、**以上** を選択して **25** と入力します。  

    > [!div class="mx-imgBorder"] 
    > ![フィルター条件の編集](media/edit-filter-criteria.png)

7.  **OK** を選択して **フィルター条件の編集** ダイアログ ボックスを閉じ、ビュー エディターの **保存して閉じる** を選択します。  
  
8.  ビューが PowerApps サイトの **ビュー** タブから使用できるようになり、アプリに追加できるようになったことに注意してください。
  
### <a name="edit-a-view"></a>ビューの編集  
  
1.  PowerApps サイトの **ビュー** タブから、**従業員数** ビューを選択します。
  
2.  ビューの **名前** を **アリゾナ州の 25 人以上の従業員を持つ従業員数** に変更して、**OK** を選択します。  

3.  [タスク] の右側のウィンドウで、**列の追加** を選択し、**列の追加** ダイアログ ボックスで **住所 1: 市区町村** を選択して **OK** を選択します。  

4. [タスク] の右側のウィンドウで、**フィルター条件の編集** を選択して、[フィルター条件の編集] ダイアログ ボックスで 2 番目のフィルター句を追加します。 **住所 2: 都道府県** を選択して **等しい** を選択し、**アリゾナ州** と入力します。 

    > [!div class="mx-imgBorder"] 
    > ![住所 2: 都道府県](media/column-address-2-state.png)

5. **OK** を選択して **フィルター条件の編集** ダイアログ ボックスを閉じ、ビュー エディターの **保存して閉じる** を選択します。  
  

## <a name="create-a-new-view-from-an-existing-view"></a>既存のビューからの新しいビューの作成  
 ビューを編集する手順に従います。ただし、**保存して閉じる**の代わりに、**名前を付けて保存**を選択し、ビューの新しい**名前**と**説明**を入力します。  
 
### <a name="next-steps"></a>次のステップ
[列の選択および構成](choose-and-configure-columns.md)  
  
[フィルター条件の編集](edit-filter-criteria.md)  
  
[並べ替えを構成する](configure-sorting.md)  

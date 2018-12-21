---
title: キャンバス アプリに画面を追加し、画面間を移動する | Microsoft Docs
description: PowerApps でキャンバス アプリに画面を追加し、[次へ] 矢印と [戻る] 矢印を使用して画面間を移動する
author: emcoope-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 07/10/2017
ms.author: emcoope
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: c0c4e14b2f4a7db81dcdd51dd75a45d3cac4da68
ms.sourcegitcommit: 6851486b8a44d76b6d87837952b7a7f38a8752b6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/18/2018
ms.locfileid: "53570353"
---
# <a name="add-a-screen-to-a-canvas-app-and-navigate-between-screens"></a>キャンバス アプリに画面を追加し、画面間を移動する

複数の画面があるキャンバス アプリを作成し、ユーザーが画面間を移動するための方法を追加します。

## <a name="prerequisites"></a>前提条件

* [コントロールを構成する](add-configure-controls.md)方法を確認しておきます。
* アプリを作成するか、開いておきます。

## <a name="add-and-rename-a-screen"></a>画面を追加し、名前を変更する

1. **[ホーム]** タブで、**[新しい画面]** をクリックまたはタップします。

    ![[ホーム] タブの画面追加オプション](./media/add-screen-context-variables/add-screen.png)

2. 右側のウィンドウで、(**[プロパティ]** タブの真上にある) 画面名をクリックまたはタップし、「**Source**」という新しい名前を入力します。

    ![既定の画面の名前を変更する](./media/add-screen-context-variables/name-source-screen.png)

3. 別の画面を追加し、**Target** という名前を付けます。

    ![左側のナビゲーション バーの 2 つの画面](./media/add-screen-context-variables/two-screens-in-nav.png)

## <a name="add-navigation"></a>ナビゲーションを追加する
1. **Source** 画面が選択されている状態で、**[挿入]** タブを開き、**[アイコン]** をクリックまたはタップし、**[次へ矢印]** をクリックまたはタップします。  

    ![[挿入] タブの図形オプション](./media/add-screen-context-variables/add-next-arrow.png)

2. (省略可能) 画面の右下隅に表示されるように矢印を移動します。

3. 矢印が選択されている状態で、**[アクション]** タブをクリックまたはタップし、**[移動]** をクリックまたはタップします。

    矢印の **[OnSelect](controls/properties-core.md)** プロパティが **Navigate** 関数に自動的に設定されます。  

    ![Navigate 関数に設定された OnSelect プロパティ](./media/add-screen-context-variables/onselect-default.png)

    ユーザーが矢印をクリックまたはタップすると、**Target** 画面がフェードインします。

4. **Target** 画面で、**[戻る矢印]** を追加し、その **[OnSelect](controls/properties-core.md)** プロパティをこの式に設定します。
   <br>**Navigate(Source, ScreenTransition.Fade)**

5. プレビュー モードを開き (![](./media/add-screen-context-variables/preview.png) または F5 を押し)、追加した矢印をクリックまたはタップして画面を切り替えます。

6. **Esc** キーを押して既定のワークスペースに戻ります。

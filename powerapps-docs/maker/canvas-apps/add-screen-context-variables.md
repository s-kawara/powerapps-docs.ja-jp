---
title: キャンバス アプリに画面を追加し、画面間を移動する | Microsoft Docs
description: PowerApps でキャンバス アプリに画面を追加し、[次へ] 矢印と [戻る] 矢印を使用して画面間を移動する
author: emcoope-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 02/03/2019
ms.author: emcoope
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: b6f83d21b2964dac7c4925d45efdf11a3a1e6b02
ms.sourcegitcommit: 4ed29d83e90a2ecbb2f5e9ec5578e47a293a55ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63321382"
---
# <a name="add-a-screen-to-a-canvas-app-and-navigate-between-screens"></a>キャンバス アプリに画面を追加し、画面間を移動する

複数の画面があるキャンバス アプリを作成し、ユーザーが画面間を移動するための方法を追加します。

## <a name="add-and-rename-a-screen"></a>画面を追加し、名前を変更する

1. **ホーム** タブで **新しい画面** を選択し、追加する画面の種類を選択します。

    ![[ホーム] タブの画面追加オプション](./media/add-screen-context-variables/add-screen.png)

2. 右側のウィンドウで、(**プロパティ** タブのすぐ上にある)画面の名前を選択し、**Source[ソース]** と入力します。

    ![既定の画面の名前を変更する](./media/add-screen-context-variables/name-source-screen.png)

3. 別の画面を追加し、**Target[ターゲット]** という名前を付けます。

    ![左側のナビゲーション バーの 2 つの画面](./media/add-screen-context-variables/two-screens-in-nav.png)

## <a name="reorder-screens"></a>画面の順序を変更します。

上へ移動またはダウンが表示されたら、省略記号ボタンを選択する画面で、左側のナビゲーション バーをポイントし、**上へ移動**または**を下へ移動**します。

![画面の順序を変更します。](./media/add-screen-context-variables/reorder-screen.png)

> [!NOTE]
> アプリが開かれると、コントロールの階層リストの上部にある画面は、通常最初表示されます。 ただし、 **[OnStart](controls/control-screen.md)** プロパティを **[Navigate](functions/function-navigate.md)** 関数を含む式に設定することで、別の画面を指定できます。

## <a name="add-navigation"></a>ナビゲーションを追加する

1. **Source[ソース]** 画面を選択した状態で、 **挿入** タブを開き、 **アイコン** を選択してから **次へ** 矢印を選択します。  

    ![[挿入] タブの図形オプション](./media/add-screen-context-variables/add-next-arrow.png)

2. (省略可能) 画面の右下隅に表示されるように矢印を移動します。

3. 矢印を選択したままの状態で、 **アクション** タブを選択してから **Navigate[移動]** を選択します。

    矢印の **[OnSelect](controls/properties-core.md)** プロパティが自動的に **Navigate** 関数に設定されます。

    ![Navigate 関数に設定された OnSelect プロパティ](./media/add-screen-context-variables/onselect-default.png)

    ユーザーが、矢印を選択すると、**Target[ターゲット]** 画面がフェードインします。

4. **Target** 画面で、 **[戻る]** 矢印を追加し、その **[OnSelect](controls/properties-core.md)** プロパティをこの式に設定します。

    `Navigate(Source, ScreenTransition.Fade)`

5. Alt キーを押しながら各画面の矢印を選択して画面間を切り替えます。

## <a name="more-information"></a>詳細

[画面コントロールのリファレンス](controls/control-screen.md)
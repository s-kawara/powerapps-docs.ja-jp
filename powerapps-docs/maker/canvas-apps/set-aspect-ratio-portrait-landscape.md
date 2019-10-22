---
title: キャンバス アプリの画面のサイズと向きを変更する | Microsoft Docs
description: PowerApps でキャンバス アプリの画面のサイズと向きなどの設定を変更するための詳しい手順
author: evchaki
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 11/07/2018
ms.author: evchaki
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 1d3bd48f658e31f795ca3489fa1973c48da94a22
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "71995633"
---
# <a name="change-screen-size-and-orientation-of-a-canvas-app-in-powerapps"></a>PowerApps でキャンバス アプリの画面のサイズと向きを変更する
キャンバス アプリは、その画面のサイズと向きを変更することでカスタマイズできます。

## <a name="prerequisites"></a>前提条件

アプリを作成するか、編集用に開き、 **[ファイル]** メニューの **[アプリの設定]** を選択します。

## <a name="change-screen-size-and-orientation"></a>スクリーンのサイズと向きを変更する
1. **[App settings (アプリ設定)]** で **[Screen size + orientation (画面のサイズと向き)]** を選択します。

    ![アプリの画面のサイズと向きを変更するためのオプション](./media/set-aspect-ratio-portrait-landscape/size-orientation.png)

1. **[方向]** ボックスの一覧で、 **[縦]** または **[横]** を選択します。

1. (タブレットアプリのみ) **[縦横比]** で、次のいずれかの手順を実行します。

    - このアプリのターゲットデバイスに一致する比率を選択します。
    - 独自のサイズを設定するには **[カスタム]** を選択し、50 ~ 3840 の範囲の幅を指定し、50 ~ 2160 の高さを指定します。

    ![タブレット アプリの縦横比の変更](./media/set-aspect-ratio-portrait-landscape/aspect-tablet.png)
    
1. **[拡大縮小]** で、 **[オン**] または **[オフ]** を指定します。

    この設定は既定でオンになっているので、デバイスの使用可能な領域に合わせてアプリの画面のサイズが変更されます。 この設定が on の場合、アプリの**width**プロパティは**designwidth**に一致し、アプリの**高さ**は**designwidth**と一致します。

    この設定をオフにすると、アプリは、実行されているデバイスの縦横比に合わせて調整され、使用可能なすべての領域を占有します。 アプリは拡張されず、結果として画面により多くの情報が表示される場合があります。

    この設定をオフにすると、**ロックの縦横比**は自動的にオフになり、無効になります。 また、すべての画面の**Width**プロパティが `Max(App.Width, App.DesignWidth)` に設定され、 **Height**プロパティが `Max(App.Height, App.DesignHeight)` に設定されているので、アプリが実行されているウィンドウの大きさを追跡できます。 この変更により、さまざまなデバイスとウィンドウのサイズに応答するアプリを作成できます。 詳細情報:[応答性の高いレイアウトの作成](create-responsive-layout.md)

1. **[Lock aspect ratio (縦横比を固定する)]** で、 **[On (オン)]** または **[Off (オフ)]** を指定します。

    この設定をオンにすると、デバイスに関係なく、手順 2. および 3. で指定した画面の向きと縦横比が維持されます。 たとえば、web ブラウザーで実行されている電話アプリでは、電話の比率が保持されます。ウィンドウを埋めるのではなく、両側にダークバーが表示されます。

    この設定がオフの場合、アプリは、実行されているデバイスの縦横比に合わせて調整されます (必要に応じて UI がゆがめられます)。

1. **[Lock orientation (向きを固定する)]** で、 **[On (オン)]** または **[Off (オフ)]** を指定します。

    アプリの向きをロックすると、指定した向きが保持されます。 アプリが異なる向きのデバイスで実行されている場合、アプリが正しく表示されないため、望ましくない結果が表示されることがあります。 アプリの向きのロックを解除すると、アプリが実行されているデバイスの画面の向きに合わせて調整されます。

    **[詳細設定**] の [**アプリの埋め込みユーザーエクスペリエンスを有効**にする] を有効にすることで、アプリの向きを変更することもできます。 この機能は、アプリが埋め込まれているときにアプリを左揃えにし、ホストしているキャンバスの背景色を白に変更します。

1. **[Apply (適用)]** を選択して変更を保存します。

## <a name="next-step"></a>次のステップ
**[File (ファイル)]** メニューの **[Save (保存)]** を選択して、新しい設定でアプリを再発行します。
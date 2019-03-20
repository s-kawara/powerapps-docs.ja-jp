---
title: キャンバス アプリの画面のサイズと向きを変更する | Microsoft Docs
description: PowerApps でキャンバス アプリの画面のサイズと向きなどの設定を変更するための詳しい手順
author: evchaki
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 11/07/2018
ms.author: evchaki
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: c4d9f648a4519ef30887d8d0739d7dc3d940555b
ms.sourcegitcommit: 0dbbf53aea319e53edadc1d3a9efa5728856ebd8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58172681"
---
# <a name="change-screen-size-and-orientation-of-a-canvas-app-in-powerapps"></a>PowerApps でキャンバス アプリの画面のサイズと向きを変更する
キャンバス アプリは、その画面のサイズと向きを変更することでカスタマイズできます。

## <a name="prerequisites"></a>前提条件

アプリを作成または編集に関しては、1 つを開き、選択**アプリ設定**上、**ファイル**メニュー。

## <a name="change-screen-size-and-orientation"></a>スクリーンのサイズと向きを変更する
1. **[App settings (アプリ設定)]** で **[Screen size + orientation (画面のサイズと向き)]** を選択します。

    ![アプリの画面のサイズと向きを変更するためのオプション](./media/set-aspect-ratio-portrait-landscape/size-orientation.png)

1. **向き**一覧で、**縦**または**ランドス ケープ**します。

1. (タブレット アプリのみ)**縦横比**、次の手順のいずれかを実行します。

    - このアプリのターゲット デバイスに一致する比率を選択します。
    - 選択**カスタム**に独自のサイズを設定し、50 3840 50 2160 間の高さと幅を指定します。

    ![タブレット アプリの縦横比の変更](./media/set-aspect-ratio-portrait-landscape/aspect-tablet.png)
    
1. **に合わせてスケール**、どちらかを指定**で**または**オフ**します。

    この設定は既定では、デバイスで使用可能な領域に合わせてアプリの画面のサイズを変更するためです。 この設定がアプリの **幅**プロパティと一致するその**DesignWidth**とアプリの**高さ**と一致するその**が追加されます**。

    この設定を無効にした場合、アプリがデバイスが実行されているすべての利用可能な領域を占めるの縦横比を調整します。 アプリでは、拡張し、結果として、画面の詳細情報を表示できます。

    この設定が入っていないときに**縦横比をロック**が自動的に無効になり、無効になっています。 さらに、**幅**すべての画面のプロパティに設定されて`Max(App.Width, App.DesignWidth)`とその**高さ**プロパティに設定されて`Max(App.Height, App.DesignHeight)`アプリが実行されているウィンドウのサイズを追跡できるようにします。 この変更により、さまざまなデバイスやウィンドウのサイズに対応するアプリを作成できます。 詳細情報:[レスポンシブ レイアウトを作成します。](create-responsive-layout.md)

1. **[Lock aspect ratio (縦横比を固定する)]** で、**[On (オン)]** または **[Off (オフ)]** を指定します。

    この設定では、アプリは、画面の向きと手順 2. および 3. は、どのデバイスでもで指定した縦横比を保持します。 たとえば、web ブラウザーで実行されている電話アプリは、ウィンドウの入力ではなく、それぞれの側に黒いバーを表示する電話番号の比率を保持します。

    この設定がオフの場合、アプリが実行されている (および必要な場合は、UI を変形) デバイスの縦横比を調整します。

1. **[Lock orientation (向きを固定する)]** で、**[On (オン)]** または **[Off (オフ)]** を指定します。

    アプリの向きをロックする場合、アプリには、印刷の向きを指定するが保持されます。 アプリが画面が異なる向きでのデバイスで実行している場合、アプリが正しく表示されないと、予想外の結果を表示することがあります。 アプリの向きのロックを解除する場合が実行されているデバイスの画面の向きを調整します。

    有効にすると、アプリの向きを変更することも**有効にするアプリのユーザー エクスペリエンスを埋め込む**で**詳細設定**します。 この機能の左上は、埋め込まれているし、ホスティング キャンバスの背景色を白に変更する場合に、アプリを配置します。

1. **[Apply (適用)]** を選択して変更を保存します。

## <a name="next-step"></a>次のステップ
**[File (ファイル)]** メニューの **[Save (保存)]** を選択して、新しい設定でアプリを再発行します。
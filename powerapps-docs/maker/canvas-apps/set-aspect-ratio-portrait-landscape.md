---
title: キャンバス アプリの画面のサイズと向きを変更する | Microsoft Docs
description: PowerApps でキャンバス アプリの画面のサイズと向きなどの設定を変更するための詳しい手順
author: lonu
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 10/16/2016
ms.author: lonu
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: ab41707c06faa11dd2e1d519b72fb35ff6b9914a
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "42835585"
---
# <a name="change-screen-size-and-orientation-of-a-canvas-app-in-powerapps"></a>PowerApps でキャンバス アプリの画面のサイズと向きを変更する
キャンバス アプリは、その画面のサイズと向きを変更することでカスタマイズできます。

## <a name="prerequisites"></a>前提条件
1. アプリを作成するか、編集するために開きます。

2. **[ファイル]** メニューの **[アプリ設定]** をクリックまたはタップします。

## <a name="change-screen-size-and-orientation"></a>スクリーンのサイズと向きを変更する
1. **[アプリ設定]** の **[画面のサイズと向き]** をクリックまたはタップします。

    ![アプリの画面のサイズと向きを変更するためのオプション](./media/set-aspect-ratio-portrait-landscape/size-orientation.png)

2. **[方向]** の一覧で、**[縦]** または **[横]** をクリックまたはタップします。

3. (タブレット アプリのみ) **[縦横比]** でこのアプリのターゲット デバイスに一致する比率をクリックまたはタップします。

    ![タブレット アプリの縦横比の変更](./media/set-aspect-ratio-portrait-landscape/aspect-tablet.png)

4. **[Lock aspect ratio (縦横比を固定する)]** で、**[On (オン)]** または **[Off (オフ)]** を指定します。

    縦横比を固定すると、スマートフォンに適した縦横比がアプリで保持されます。 別の種類のデバイスでアプリが実行されている場合、アプリの表示は正しく行われず、望ましくない結果が表示される可能性があります。 縦横比の固定を解除すると、アプリが実行されているデバイスの縦横比に合うように自動的に調整されます。

5. **[Lock orientation (向きを固定する)]** で、**[On (オン)]** または **[Off (オフ)]** を指定します。

    アプリの向きを固定すると、指定した向きがアプリで保持されます。 画面の向きが異なるデバイスでアプリが実行されている場合、アプリの表示は正しく行われず、望ましくない結果が表示される可能性があります。 アプリの向きの固定を解除すると、アプリが実行されているデバイスの画面の向きに合うように自動的に調整されます。

6. **[Apply (適用)]** を選択して変更を保存します。

## <a name="next-step"></a>次のステップ
**[File (ファイル)]** メニューの **[Save (保存)]** を選択して、新しい設定でアプリを再発行します。

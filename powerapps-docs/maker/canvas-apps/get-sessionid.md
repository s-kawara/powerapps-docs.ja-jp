---
title: セッション ID またはキャンバス アプリ ID を取得する | Microsoft Docs
description: PowerApps でのトラブルシューティングのためにセッション ID またはキャンバス アプリ ID を取得する方法
author: tapanm-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 06/18/2018
ms.author: tapanm
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 11f749f241f978ebd94e460833e98cca894fe7fa
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "71990199"
---
# <a name="get-a-session-id-or-a-canvas-app-id"></a>セッション ID またはキャンバス アプリ ID を取得する
PowerApps で作成したキャンバス アプリに問題が発生した場合、問題のセッション ID、アプリ ID、またはその両方を Microsoft に提供すると、問題をより効果的にトラブルシューティングできます。

## <a name="get-the-session-id"></a>セッション ID を取得する

### <a name="when-editing-an-app"></a>アプリケーションを編集する場合
1. 左上隅にある **[ファイル]** を選択します。

1. **[アカウント]** を選択します。

1. **[診断]** の下で、 **[セッションの詳細]** を選択します。

    ![PowerApps Studio からセッション ID を取得する](media/get-sessionid/studio.png)

### <a name="when-running-an-app-in-a-browser"></a>アプリケーションをブラウザーで実行する場合
1. 右上隅にある歯車アイコンを選択します。

1. **[セッションの詳細]** を選択します。

    ![ブラウザーからセッション ID を取得する](media/get-sessionid/browser.png)

### <a name="when-running-an-app-on-a-phone-or-a-tablet"></a>アプリケーションをスマートフォンまたはタブレットで実行する場合
1. 右にスワイプします。

1. **[セッションの詳細]** をタップします。

    ![ブラウザーからセッション ID を取得する](media/get-sessionid/mobile.png)

### <a name="when-running-an-embedded-app-or-form"></a>埋め込みのアプリケーションまたはフォームを実行する場合
1. 次の手順のいずれかを実行します。

    - Alt キーを押しながら、アプリケーションまたはフォームを右クリックします。
    - アプリケーションまたはフォームを、2 本の指で 1 から 2 秒間タップして離します。

1. **[セッションの詳細]** を選択します。

    ![埋め込みのアプリケーションからセッション ID を取得する](media/get-sessionid/embedded.png)

## <a name="get-an-app-id"></a>アプリケーション ID を取得する
1. [PowerApps にサインインします](https://powerapps.microsoft.com)。

1. 左の端にある **[アプリ]** を選択します。

1. トラブルシューティングしているアプリの省略記号 ( **. . .** ) を選択し、 **[詳細]** を選択します。

    ![アプリの詳細の表示](./media/get-sessionid/details.png)

    そのアプリケーションの **[詳細]** ウィンドウの下部に、アプリケーション ID が表示されます。

    ![詳細からのアプリ ID のコピー](./media/get-sessionid/app-id.png)

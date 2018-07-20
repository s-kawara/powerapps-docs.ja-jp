---
title: カードのカスタマイズ | Microsoft Docs
description: PowerApps の詳細または編集フォームに表示される既定のコントロールを変更します。
author: AFTOwen
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 03/18/2018
ms.author: anneta
ms.openlocfilehash: 56a46493ef15eff7d65d19f12affb2a58dbba0b6
ms.sourcegitcommit: dfa0e1a7981814e15e6ca4720e2a5f930e859db1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2018
ms.locfileid: "39023438"
---
# <a name="customize-a-card-in-powerapps"></a>PowerApps でカードをカスタマイズする
基本的なカスタマイズ (カードのロック解除を伴わないカスタマイズ) は、コントロールの変更などによって行います。 高度なカスタマイズは、カードのロックを解除し、既定では利用できないコントロールをカードに追加するなどして行います。

概要については、「[Understand data cards (データ カードについて)](working-with-cards.md)」をご覧ください。

## <a name="prerequisites"></a>前提条件

* [コントロールを追加して構成](add-configure-controls.md)する方法について学ぶ。
* このトピックは、概念全般を理解する目的でのみご覧いただいても、これらのトピックの各手順を完全に実行していただいてもかまいません。

  1. [アプリを生成します](data-platform-create-app.md)。
  2. [そのギャラリーをカスタマイズします](customize-layout-sharepoint.md)。
  3. [フォームをカスタマイズします](customize-forms-sharepoint.md)。

## <a name="customize-a-locked-card"></a>ロックされたカードのカスタマイズ
この手順では、カードのロックを解除せずに、**[テキスト入力](controls/control-text-input.md)** コントロールを**[スライダー](controls/control-slider.md)** コントロールで置き換えます。

1. [PowerApps](http://web.powerapps.com) にサインインします。

    ![PowerApps のホーム ページ](./media/customize-card/sign-in.png)

1. 生成およびカスタマイズしたアプリを開いて、**EditForm1** を選択し、右側のウィンドウで **[アカウント]** を選択して **[データ]** ウィンドウを開きます。

1. フィールドの一覧で、**[従業員数]** の下向き矢印を選択し、**[スライダーの編集]** を選択します。

    ![番号カードのオプションのドロップダウン リスト](./media/customize-card/card-selector.png)

    画面に変更内容が反映されます。

    ![スライダー コントロールと EditForm1](./media/customize-card/add-slider.png)

## <a name="unlock-and-customize-a-card"></a>カードのロック解除とカスタマイズ
この手順では、カードのロックを解除し、**[トグル](controls/control-toggle.md)** コントロールを**[チェックボックス](controls/control-check-box.md)** コントロールで置き換えます。

1. **EditForm1** で、**[マーケティング資料の送付]** フィールドを表示します。

    ![[マーケティング資料の送付] フィールドを表示する](./media/customize-card/show-field.png)

2. カードが選択された状態で、右側のウィンドウの上部にある **[詳細]** をクリックまたはタップし、ロック アイコンをクリックまたはタップして、カードのロックを解除します。

    ![[マーケティング資料の送付] フィールドを表示する](./media/customize-card/unlock-card.png)

1. カードで、**トグル**コントロールを削除し、**チェックボックス** コントロールを追加して、新しいコントロールに「**chkMktg**」と名前を付けます。

    ![トグルをチェックボックスに置き換える](./media/customize-card/add-checkbox.png)

1. 更新したカードを選択します。

    ![カードを選択](./media/customize-card/select-card.png)

1. 右側のペインで、**[詳細]** タブがまだ表示されていることを確認し、**[その他のオプション]** をクリックまたはタップします。

    ![[その他のオプション] ボタン](./media/customize-card/more-options.png)

1. カードの **[更新]** プロパティの値を次の式に変更します。
<br>`chkMktg.Value`

1. そのカードのエラー メッセージの **Y** プロパティの値を次の式に変更します。<br>
`chkMktg.Y + chkMktg.Height`

    ![新しいカードのエラー メッセージを選択する](./media/customize-card/select-error.png)

1. **chkMktg** の **[テキスト]** プロパティの値を **[はい]** に変更します。

    画面に変更が反映され、エラーが解決されます。

    ![エラーの解決の最終画面](./media/customize-card/final-screen.png)

## <a name="next-steps"></a>次の手順
これでアプリを生成し、ギャラリー、フォーム、カードをカスタマイズする方法の基礎を理解したので、[独自のアプリを新規に作成する](data-platform-create-app-scratch.md)ことができます。

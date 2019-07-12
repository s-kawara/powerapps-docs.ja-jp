---
title: キャンバス アプリでカードのカスタマイズ |Microsoft Docs
description: 変更の詳細のカードに表示される既定のコントロールまたはキャンバス アプリでのフォームの編集
author: AFTOwen
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 03/18/2018
ms.author: anneta
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: ddc1c677ed95caf10d8cd6e0e7e12e6aaf88a0f5
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61559875"
---
# <a name="customize-a-card-in-a-canvas-app"></a>キャンバス アプリでカードをカスタマイズします。

基本的なカスタマイズ (カードのロック解除を伴わないカスタマイズ) は、コントロールの変更などによって行います。 高度なカスタマイズは、カードのロックを解除し、既定では利用できないコントロールをカードに追加するなどして行います。

概要については、「[Understand data cards (データ カードについて)](working-with-cards.md)」をご覧ください。

## <a name="prerequisites"></a>前提条件

- [コントロールを追加して構成](add-configure-controls.md)する方法について学ぶ。
- 一般的な概念のみ、このトピックを確認するまたはこれらのトピックの手順を完了している場合、ステップ バイ ステップに従ってできます。

    1. [アプリを生成します](data-platform-create-app.md)。
    1. [そのギャラリーをカスタマイズします](customize-layout-sharepoint.md)。
    1. [フォームをカスタマイズします](customize-forms-sharepoint.md)。

## <a name="customize-a-locked-card"></a>ロックされたカードのカスタマイズ

この手順では、カードロックを解除せずに、 **[テキスト入力](controls/control-text-input.md)** コントロールを **[スライダー](コントロール/管理-slider.md** コントロールに置き換えます。

1. 生成してカスタマイズしたアプリで、左側のナビゲーションバーの **EditForm1** を選択し、右側のペインの**プロパティ**タブで**フィールドを編集**を選択します。

1. フィールドの一覧で、**Number of Employees** の下向き矢印を選択してから、**コントロールの種類**のリストを開きます。

    > [!div class="mx-imgBorder"]
    > ![数値カードのオプションのドロップダウン リスト](./media/customize-card/card-selector.png)

1. **スライダーの編集**を選択します。

    画面に変更内容が反映されます。

    > [!div class="mx-imgBorder"]
    > ![スライダー コントロールと EditForm1](./media/customize-card/add-slider.png)

## <a name="unlock-and-customize-a-card"></a>カードのロック解除とカスタマイズ

この手順では、カードのロックを解除して、追加した**スライダー** コントロールの**最大**のプロパティを更新します。

1. **EditForm1** で、**Number of Employees** カードの**スライダー** コントロールを選択します。

    > [!div class="mx-imgBorder"]
    > ![スライダーを選択します。](./media/customize-card/select-slider.png)

1. **詳細設定**  タブの右側のウィンドウには、カードのロックを解除するロック アイコンを選択します。

    > [!div class="mx-imgBorder"]
    > ![カードのロックを解除します。](./media/customize-card/lock-icon.png)

1. **スライダー**コントロールの**最大**プロパティを 10,000 に設定します。

    > [!div class="mx-imgBorder"]
    > ![詳細設定 タブで、Max プロパティ](./media/customize-card/max-property.png)

    **スライダー** コントロールは、より正確な値を示します。

    > [!div class="mx-imgBorder"]
    > ![スライダーの範囲:0-10,000](./media/customize-card/final-slider.png)

## <a name="next-steps"></a>次の手順

これでアプリを生成し、ギャラリー、フォーム、カードをカスタマイズする方法の基礎を理解したので、[独自のアプリを新規に作成する](data-platform-create-app-scratch.md)ことができます。
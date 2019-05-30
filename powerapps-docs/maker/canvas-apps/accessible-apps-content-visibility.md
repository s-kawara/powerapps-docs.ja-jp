---
title: キャンバス アプリでの支援技術からコンテンツを非表示 |Microsoft Docs
description: 目が見えるユーザーにのみ、またはキャンバス アプリについてのみ、スクリーン リーダー ユーザーにのみコンテンツを表示するための手法
author: tahoon-ms
ms.service: powerapps
ms.topic: article
ms.custom: canvas
ms.date: 10/22/2018
ms.author: tahoon
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: c680767bc6a56f0596eba03dd555c1c9a0205346
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61550090"
---
# <a name="show-or-hide-content-from-assistive-technologies-for-canvas-apps"></a>キャンバス アプリの支援技術からコンテンツを非表示

ほとんどの場合は、すべてのユーザーは、すべてのコンテンツにアクセスできる必要がありますが、目が見えるユーザーにのみ、またはスクリーン リーダー ユーザーにのみコンテンツを表示したい場合があります。 たとえば、目が見えるユーザーに明らかなの折れ線グラフの傾向の説明にアクセスする唯一のスクリーン リーダー ユーザーをする可能性があります。 それに隣接するラベルが説明されている場合、スクリーン リーダー ユーザーからアイコンを非表示にする場合があります。 アイコンをもう 1 つの説明は不必要に冗長になります。

## <a name="hide-content-from-all-users"></a>すべてのユーザーからコンテンツを非表示にします。

* 設定 **[Visible](controls/properties-core.md)** を false にします。

## <a name="hide-content-from-sighted-users-and-show-it-to-screen-reader-users"></a>ユーザーの目が見えるからコンテンツを非表示にして、スクリーン リーダー ユーザーに表示

これらの手法のいずれかを使用します。

* 設定 **[サイズ](controls/properties-text.md)** を 0 にします。
* 設定 **[幅](controls/properties-size-location.md)** と **[高さ](controls/properties-size-location.md)** を 1 にします。
* 設定 **[X](controls/properties-size-location.md)** 、  **[Y](controls/properties-size-location.md)** 、または両方のプロパティ、コントロールが画面外にできるようにします。
* 設定 **[色](controls/properties-color-border.md)** と関連プロパティを透過的になります。
* 四角形の位置 **[図形](controls/control-shapes-icons.md)** コンテンツ、およびセット上 **[入力](controls/properties-color-border.md)** 画面の背景色と同じ色にします。

> [!NOTE]
> ユーザーなど、対話型のコントロールにアクセスするキーボードを使って引き続き、 **[ボタン](controls/control-button.md)** 場合でも、前の一覧に、手法の 1 つを使用して非表示にします。 設定 **[TabIndex](controls/properties-accessibility.md)** を Tab キーを押して、コントロールにアクセスできないようにする場合は-1。

## <a name="hide-content-from-screen-reader-users-and-show-it-to-sighted-users"></a>スクリーン リーダー ユーザーからコンテンツを非表示にして、目が見えるユーザーに表示

* **[イメージ](controls/control-image.md)** 、 **[アイコン](controls/control-shapes-icons.md)** 、および **[図形](controls/control-shapes-icons.md)** コントロールの設定 **[AccessibleLabel](controls/properties-accessibility.md)** を空の文字列""です。

## <a name="next-steps"></a>次の手順

について[アクセシビリティ プロパティ](controls/properties-accessibility.md)キャンバス アプリ内のコントロール。

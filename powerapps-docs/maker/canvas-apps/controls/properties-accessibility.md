---
title: アクセシビリティのプロパティのキャンバス アプリ |Microsoft Docs
description: TabIndex、Tooltip などのプロパティに関する参照情報
author: fikaradz
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 01/26/2017
ms.author: fikaradz
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 5fa8b6fecdf690114cbf6a0945f2dfec66b067c3
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61560417"
---
# <a name="accessibility-properties-for-canvas-apps"></a>キャンバス アプリのアクセシビリティのプロパティ

障碍のあるユーザーに適したコントロールを備えた、別の方法での操作を提供するためのプロパティを構成します。

## <a name="properties"></a>プロパティ

**AccessibleLabel** – スクリーン リーダー用のラベルです。 画像、アイコン、および図形コントロールの値を空にすると、スクリーン リーダーにはコントロールが表示されなくなり、装飾として扱われます。

**Live** – スクリーン リーダーはコンテンツへの変更を通知する必要があります。 のみ使用できます、 **[ラベル](control-text-box.md)** コントロール。

* 設定すると**オフ**、スクリーン リーダーは変更を発表します。
* 設定すると**礼儀**、スクリーン リーダーが話していたときに発生した変更を通知する前に言うと、スクリーン リーダーが終了します。
* 設定すると**Assertive**、スクリーン リーダーの割り込み自体をスクリーン リーダーが話していたときに発生した変更を発表します。

学習方法[ライブ リージョンでの動的な変更を発表](../accessible-apps-live-regions.md)します。

**TabIndex** – 他のコントロールに関連するキーボード ナビゲーションの順序です。

既定値 0 は、コントロールの XY 座標に基づいて、既定のタブの順序を指定します。  0 より大きな値を設定すると、コントロールのタブの順序が、既定値が設定されているすべてのコントロールの前に移動されます。  TabIndex 値 2 が設定されているコントロールは、TabIndex 値 3 以上が設定されているコントロールに優先します。

フォームやギャラリーなどのコントロールのコンテナーは、コンテナー外のコントロールに進む前に、コンテナーのすべての要素を常にタブ処理することに注意してください。  コンテナーのタブの順序は、子コントロールの TabIndex の最小値です。

TabIndex を -1 に設定すると、コントロールへのタブのアクセスが無効になります。画像、アイコン、および図形の場合は、非インタラクティブ要素となります。

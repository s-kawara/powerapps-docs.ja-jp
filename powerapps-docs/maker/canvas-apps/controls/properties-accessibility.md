---
title: アクセシビリティのプロパティ | Microsoft Docs
description: TabIndex、Tooltip などのプロパティに関する参照情報
author: fikaradz
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 01/26/2017
ms.author: fikaradz
ms.openlocfilehash: 59cc231dfc461a2301de90a7a995ec2ec82790cb
ms.sourcegitcommit: dfa0e1a7981814e15e6ca4720e2a5f930e859db1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2018
ms.locfileid: "39022932"
---
# <a name="accessibility-properties-in-powerapps"></a>PowerApps のアクセシビリティのプロパティ
障碍のあるユーザーに適したコントロールを備えた、別の方法での操作を提供するためのプロパティを構成します。

### <a name="properties"></a>プロパティ
**AccessibleLabel** – スクリーン リーダー用のラベルです。 画像、アイコン、および図形コントロールの値を空にすると、スクリーン リーダーにはコントロールが表示されなくなり、装飾として扱われます。

**TabIndex** – 他のコントロールに関連するキーボード ナビゲーションの順序です。

既定値 0 は、コントロールの XY 座標に基づいて、既定のタブの順序を指定します。  0 より大きな値を設定すると、コントロールのタブの順序が、既定値が設定されているすべてのコントロールの前に移動されます。  TabIndex 値 2 が設定されているコントロールは、TabIndex 値 3 以上が設定されているコントロールに優先します。

フォームやギャラリーなどのコントロールのコンテナーは、コンテナー外のコントロールに進む前に、コンテナーのすべての要素を常にタブ処理することに注意してください。  コンテナーのタブの順序は、子コントロールの TabIndex の最小値です。

TabIndex を -1 に設定すると、コントロールへのタブのアクセスが無効になります。画像、アイコン、および図形の場合は、非インタラクティブ要素となります。

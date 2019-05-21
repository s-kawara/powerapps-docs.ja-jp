---
title: 'バーコード スキャナー コントロール: リファレンス |Microsoft Docs'
description: プロパティや例については、バーコード スキャナー コントロールに関するなどの情報
author: fikaradz
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.date: 11/25/2018
ms.author: fikaradz
ms.reviewer: anneta
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 9a4b2c941b5e28c462b85d3c6d54404746e22d04
ms.sourcegitcommit: 8d0ba2ec0c97be91d1350180dd6881c14dec8f2d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2019
ms.locfileid: "65517336"
---
# <a name="barcode-scanner-control-for-canvas-apps"></a>キャンバス アプリのバーコード スキャナー コントロール

バーコード、QR コード、および Android または iOS デバイスでデータの行列のコードをスキャンします。 Web ブラウザーでサポートされていません。

## <a name="description"></a>説明

コントロールでは、Android または iOS デバイスでネイティブのスキャナーが開きます。 スキャナーでは、バーコード、QR コードの場合、またはデータ行列のコードとビューに自動的に検出します。 コントロールは、web ブラウザーでスキャンをサポートしていません。

コントロールには、QR コード、データのマトリックス コード、およびこれらの種類のバーコードがサポートされています。

- UPC A
- UPC E
- EAN 協会 8
- EAN 協会 13
- コード 39
- CODE 128
- ITF
- PDF 417

## <a name="key-properties"></a>主要なプロパティ

**値**– 最後にスキャンされたコードのテキスト値を含むプロパティを出力します。

**テキスト**-スキャナーをアクティブにするボタンに表示されるテキスト。

**OnScan** – バーコードが正常にスキャンされたときに、アプリの応答方法。

## <a name="additional-properties"></a>その他のプロパティ

**[BorderColor](properties-color-border.md)** – コントロールの境界線の色です。

**[BorderStyle](properties-color-border.md)** – コントロールの境界線を **Solid** (実線)、**Dashed** (破線)、**Dotted** (点線)、**None** (なし) のいずれに指定します。

**[BorderThickness](properties-color-border.md)** – コントロールの境界線の太さです。

**[DisplayMode](properties-core.md)** – コントロールで、ユーザー入力を許可するか (**Edit**)、データの表示のみを許可するか (**View**)、許可しないか (**Disabled**) を設定します。

**FlashlightEnabled** -、懐中電灯は、スキャナーを開いたときに自動的に有効かどうか。

**[高さ](properties-size-location.md)** – スキャナーをアクティブにするボタンの高さ。

**PreferFrontCamera** -、前面カメラは、使用可能な場合、スキャンの使用があるかどうか。

**[Tooltip](properties-core.md)** – ポインターをコントロールに合わせたときに表示される説明テキストです。

**型**-最後に成功したスキャンで検出されたコードの種類。

**[Visible](properties-core.md)** – コントロールを表示するか非表示にするかを指定します。

**[幅](properties-size-location.md)** – スキャナーをアクティブにするボタンの幅。

**[X](properties-size-location.md)** – コントロールの左端とその親コンテナー (親コンテナーがない場合は画面) の左端間の距離です。

**[Y](properties-size-location.md)** – コントロールの上端とその親コンテナー (親コンテナーがない場合は画面) の上端間の距離です。

## <a name="accessibility-guidelines"></a>アクセシビリティのガイドライン
同じガイドライン、 **[ボタン](control-button.md)** にコントロールを適用、**バーコード スキャナー**制御、スキャンを起動するボタンがあるためです。

### <a name="visual-alternatives"></a>ビジュアルの代替手段
* バーコード スキャナーは、スキャン結果を表示しないようにボタンです。 スキャン結果を表示する、 **[ラベル](control-text-box.md)** コントロール。 ラベルの設定 **[テキスト](properties-core.md)** プロパティをバーコード スキャナーの**値**プロパティ。 ラベルの設定 **[Live](properties-accessibility.md)** プロパティを**礼儀**変更のスクリーン リーダー ユーザーに通知されるようにします。 この変更により、スキャンされた値がビジュアルの機能に関係なく、全員にアクセスできます。

* カメラ、バーコード ポイントが視覚的、自動車の障碍のあるユーザーお勧めします。 別の形式の入力などの追加を検討してください、 **[テキスト入力](control-text-input.md)** ユーザー バーコードを入力するためのコントロール。

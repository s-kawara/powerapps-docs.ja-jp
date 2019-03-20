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
ms.openlocfilehash: 961f8908014ef9cd85eadacb97a7c1dfc7e52b25
ms.sourcegitcommit: eef2d6d9a9c7f5c8a44b9734817f59dc0eac3ecf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/07/2019
ms.locfileid: "57800999"
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

**[Tooltip](properties-core.md)** – ポインターをコントロールに合わせたときに表示される説明テキストです。

**型**-最後に成功したスキャンで検出されたコードの種類。

**[Visible](properties-core.md)** – コントロールを表示するか非表示にするかを指定します。

**[幅](properties-size-location.md)** – スキャナーをアクティブにするボタンの幅。

**[X](properties-size-location.md)** – コントロールの左端とその親コンテナー (親コンテナーがない場合は画面) の左端間の距離です。

**[Y](properties-size-location.md)** – コントロールの上端とその親コンテナー (親コンテナーがない場合は画面) の上端間の距離です。

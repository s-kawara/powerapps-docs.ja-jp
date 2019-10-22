---
title: デバイス |Microsoft Docs
description: ''
keywords: ''
ms.author: nabuthuk
author: Nkrb
manager: kvivek
ms.date: 10/01/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a0f9abc5-c605-4433-bf5a-f8253eeeda3b
ms.openlocfilehash: 0558004b889df59c168cfe9bdcfc7b5b5414fc02
ms.sourcegitcommit: b8148ec3324b7ffed9fa5a28ea1f4df7e444a081
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72347339"
---
# <a name="device"></a>ドライブ

[!INCLUDE [device-description](includes/device-description.md)]

> [!IMPORTANT]
> デバイス API メソッドを使用する場合は、マニフェストファイルの[機能使用法](../manifest-schema-reference/feature-usage.md)ノードで、これらのメソッドの使用法を宣言する必要があります。

## <a name="syntax"></a>構文

`context.device`

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー)

## <a name="methods"></a>メソッド

|B | Description |
| ------------- |-------------|
|[captureAudio](device/captureaudio.md)|[!INCLUDE [captureaudio-description](device/includes/captureaudio-description.md)]|
|[キャプチャイメージ](device/captureimage.md)|[!INCLUDE [captureimage-description](device/includes/captureimage-description.md)]|
|[captureVideo](device/capturevideo.md)|[!INCLUDE [capturevideo-description](device/includes/capturevideo-description.md)]|
|[getBarcodeValue](device/getbarcodevalue.md)|[!INCLUDE [getbarcodevalue-description](device/includes/getbarcodevalue-description.md)]|
|[getCurrentPosition](device/getcurrentposition.md)|[!INCLUDE [getcurrentposition-description](device/includes/getcurrentposition-description.md)]|
|[ファイルの候補](device/pickfile.md)|[!INCLUDE [pickfile-description](device/includes/pickfile-description.md)]|

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネントフレームワーク API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../overview.md)
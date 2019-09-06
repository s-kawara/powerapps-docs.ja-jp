---
title: CaptureImage | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
author: Nkrb
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1d9c0063-add2-4002-acab-1be07ca1f6b6
---

# <a name="captureimage"></a>captureImage

[!INCLUDE[./includes/captureimage-description.md](./includes/captureimage-description.md)]

## <a name="syntax"></a>構文

`captureImage(options)`

## <a name="parameters"></a>パラメーター

| パラメーター名|型|必須出席者|説明|
| ------------- |----|--------|-----------|
|`options`|`object`|いいえ|画像を取り込むオプション。|

## <a name="return-value"></a>戻り値

種類: `Promise<FileObject>`

[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise) と [ファイル](https://developer.mozilla.org/docs/Web/API/File) を参照してください。

## <a name="remarks"></a>備考

`options` パラメーター オブジェクトは以下のプロパティを持ちます:

|Name|型|説明|
| ---|----|-----------|
|`allowEdit`|`boolean`|保存する前に画像を編集するかを指定します|
|`height`|`number`|取り込む画像の高さ|
|`preferFrontCamera`|`boolean`|デバイスの前部カメラを使用して画像を取り込むかを指定します。|
|`quality`|`number`|パーセントで表した画像ファイルの画質|
|`width`|`number`|取り込む画像の幅|


### <a name="related-topics"></a>関連トピック

[デバイス](../device.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../../overview.md)
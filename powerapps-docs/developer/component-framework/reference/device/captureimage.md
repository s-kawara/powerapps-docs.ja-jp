---
title: キャプチャイメージ |Microsoft Docs
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
ms.assetid: 1d9c0063-add2-4002-acab-1be07ca1f6b6
ms.openlocfilehash: e642af17e02334b45041df87386885536e1810af
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72345683"
---
# <a name="captureimage"></a>captureImage

[!INCLUDE[./includes/captureimage-description.md](./includes/captureimage-description.md)]

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリ

## <a name="syntax"></a>構文

`context.device.captureImage(options)`

## <a name="parameters"></a>パラメーター

| パラメーター名|種類|必須|Description|
| ------------- |----|--------|-----------|
|`options`|`Object`|いいえ|イメージをキャプチャするためのオプション。|

## <a name="return-value"></a>戻り値

種類: `Promise<FileObject>`

[Promise](https://developer.mozilla.org/docs/Web/JavaScript/reference/Global_Objects/Promise)と[FileObject](../fileobject.md)を見る

## <a name="remarks"></a>」

@No__t_0 parameter オブジェクトには、次のプロパティがあります。

|名前|種類|Description|
| ---|----|-----------|
|`allowEdit`|`Boolean`|保存する前にイメージを編集するかどうかを示します。|
|`height`|`Number`|キャプチャするイメージの高さ。|
|`preferFrontCamera`|`Boolean`|デバイスの前面カメラを使用してイメージをキャプチャするかどうかを示します。|
|`quality`|`Number`|イメージファイルの品質 (パーセント)。|
|`width`|`Number`|キャプチャするイメージの幅。|


### <a name="related-topics"></a>関連トピック

[ドライブ](../device.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../../overview.md)
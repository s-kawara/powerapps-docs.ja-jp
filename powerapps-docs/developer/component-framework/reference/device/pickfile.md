---
title: PickFile | Microsoft Docs
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
ms.assetid: aae27c64-33c4-47f1-b833-4c04161c01e2
---

# <a name="pickfile"></a>pickFile

[!INCLUDE[./includes/pickfile-description.md](./includes/pickfile-description.md)]

## <a name="syntax"></a>構文

`pickFile(options)`

## <a name="parameters"></a>パラメーター

| パラメーター名|型|必須出席者|説明|
| ------------- |----|--------|-----------|
|`options`|`object`|いいえ|ファイルを選択するオプション。|

## <a name="return-value"></a>戻り値

種類: `Promise<File[]>`

[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise) と [ファイル](https://developer.mozilla.org/docs/Web/API/File) を参照してください。

## <a name="remarks"></a>備考

`options` パラメーター オブジェクトは以下のプロパティを持ちます:

|Name|型|説明|
|--|--|--|
|`accept`|`string`|選択する画像ファイルの種類。 有効な値は、"audio"、"video"、または "image" です|
|`allowMultipleFiles`|`boolean`|複数ファイルの選択を許可するかを示します|
|`maximumAllowedFileSize`|`number`|選択するファイルの最大サイズ。|


### <a name="related-topics"></a>関連トピック

[デバイス](../device.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../../overview.md)
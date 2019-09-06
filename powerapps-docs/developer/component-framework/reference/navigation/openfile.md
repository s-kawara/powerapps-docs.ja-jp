---
title: openFile | Microsoft Docs
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
ms.assetid: ae94e467-d12c-4a74-96f0-05a09e03c5f8
---
# <a name="openfile"></a>openFile

[!INCLUDE [openfile-description](includes/openfile-description.md)]

## <a name="syntax"></a>構文

`openFile(file, options)`

## <a name="parameters"></a>パラメーター

| パラメーター名|型|必須出席者|説明|
| ------------- |----|--------|-----------|
|ファイル|`FileObject`|はい|開くファイルを記述するオブジェクト。FileObject には以下の属性があります: <br/>- **fileContent**: `string`。 ファイルの内容です。 <br/>- **fileName**: `string`。 ファイルの名前。<br/>- **fileSize**: `number`。 ファイルのサイズ (KB) です。 <br/>- **mimeType**: `string`。 ファイルの MIME の種類。|

## <a name="return-value"></a>戻り値

種類: `Promise`

## <a name="remarks"></a>備考

[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise) と [ファイル](https://developer.mozilla.org/docs/Web/API/File) を参照してください。


### <a name="related-topics"></a>関連トピック

[ナビゲーション](../navigation.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../../overview.md)
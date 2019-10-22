---
title: ファイルの候補 |Microsoft Docs
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
ms.assetid: aae27c64-33c4-47f1-b833-4c04161c01e2
ms.openlocfilehash: a36731edc7ee5cc8edede499fc791595bc00bc8c
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72344625"
---
# <a name="pickfile"></a>pickFile

[!INCLUDE[./includes/pickfile-description.md](./includes/pickfile-description.md)]

## <a name="syntax"></a>構文

`context.device.pickFile(options)`

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリ

## <a name="parameters"></a>パラメーター

| パラメーター名|種類|必須|Description|
| ------------- |----|--------|-----------|
|`options`|`Object`|いいえ|ファイルを選択するためのオプション。|

## <a name="return-value"></a>戻り値

種類: `Promise<FileObject[]>`

[Promise](https://developer.mozilla.org/docs/Web/JavaScript/reference/Global_Objects/Promise)と[FileObject](../fileobject.md)を見る

## <a name="remarks"></a>」

@No__t_0 parameter オブジェクトには、次のプロパティがあります。

|名前|種類|Description|
|--|--|--|
|`accept`|`String`|選択するイメージファイルの種類。 有効な値は、 *audio*、 *video*、または*image*です。|
|`allowMultipleFiles`|`Boolean`|複数のファイルを選択できるようにするかどうかを示します|
|`maximumAllowedFileSize`|`Number`|選択されるファイルの最大サイズ|


### <a name="related-topics"></a>関連トピック

[ドライブ](../device.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../../overview.md)
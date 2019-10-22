---
title: openFile |Microsoft Docs
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
ms.assetid: ae94e467-d12c-4a74-96f0-05a09e03c5f8
ms.openlocfilehash: 5de6eefb37450fde50127829f2a922252d08a4fb
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72342693"
---
# <a name="openfile"></a>openFile

[!INCLUDE [openfile-description](includes/openfile-description.md)]

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリ

## <a name="syntax"></a>構文

`context.navigation.openFile(file, options)`

## <a name="parameters"></a>パラメーター

| パラメーター名|種類|必須|Description|
| ------------- |----|--------|-----------|
|拡張子|`FileObject`|はい|開くファイルを記述するオブジェクト。FileObject には、次の属性があります。 <br/>- **filecontent**`String`。 ファイルの内容。 <br/>- **fileName**: `String`。 ファイルの名前。<br/>-  の**サイズ**: `Number`。 ファイルのサイズ (KB 単位)。 <br/>-  の**mime**: `String`。 ファイルの MIME の種類。|
|オプション|`Object`|いいえ|ファイルを開くか保存するかを記述するオブジェクト。 オブジェクトには、次の属性があります。 <br/>- **openMode**: を開くには1を指定します。2を保存します。 
このパラメーターを指定しない場合、既定では 1 (open) が渡されます。 このパラメーターは、統合インターフェイスでのみサポートされています。|

## <a name="return-value"></a>戻り値

種類: `Promise`

## <a name="remarks"></a>」

[Promise](https://developer.mozilla.org/docs/Web/JavaScript/reference/Global_Objects/Promise)と[FileObject](../fileobject.md)を見る


### <a name="related-topics"></a>関連トピック

[ナビゲーション](../navigation.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../../overview.md)
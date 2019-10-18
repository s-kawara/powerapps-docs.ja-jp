---
title: openWebResource |Microsoft Docs
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
ms.assetid: 27a1e54c-71fe-450f-8f84-b4cc125970bf
ms.openlocfilehash: 577c26dd87149fabebafe32b77395029ef4df335
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72342256"
---
# <a name="openwebresource"></a>openWebResource

[!INCLUDE [openwebresource-description](includes/openwebresource-description.md)]

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリ

## <a name="syntax"></a>構文

`context.navigation.openWebResource(name, options, data)`

## <a name="parameters"></a>パラメーター

| パラメーター名|種類|必須|Description|
| ------------- |----|--------|-----------|
|指定|`String`|はい|開く HTML web リソースの名前。|
|オプション|`OpenWebResourceOptions`|いいえ|Web リソースを開くためのウィンドウオプションです。 OpenWebResourceOptions には、次の属性があります。<br/>-  の**高さ**: `Number` します。 結果ページをピクセル単位で表示するウィンドウの高さ。<br/>- **幅**: `Number`。 結果ページを表示するウィンドウの幅 (ピクセル単位)。<br/>**Openinnewwindow**: `Boolean` を -  します。 新しいウィンドウで web リソースを開くかどうかを示します。|
|データ|`String`|いいえ|データパラメーターに渡されるデータ。

### <a name="related-topics"></a>関連トピック

[ナビゲーション](../navigation.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../../overview.md)
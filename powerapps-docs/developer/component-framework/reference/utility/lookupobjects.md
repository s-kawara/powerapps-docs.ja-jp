---
title: いいね。Microsoft Docs
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
ms.assetid: d213b401-cfc4-44df-b55c-f040fb6d7072
ms.openlocfilehash: 0dca29df3537389decefe2584d2fc931cea8979c
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72341152"
---
# <a name="lookupobjects"></a>lookupObjects

[!INCLUDE [lookupobjects-description](includes/lookupobjects-description.md)]

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリ

## <a name="syntax"></a>構文

`context.utils.lookupObjects(lookupOptions)`

## <a name="parameters"></a>パラメーター

| パラメーター名|種類|必須|Description|
| ------------- |----|--------|-----------|
|LookupOptions|`UtilityApi.LookupOptions`|はい|参照ダイアログを開くためのオプションを定義します。 LookupOptions には、次の属性があります。<br/>**allowmultiselect**の - : `Boolean`。 参照によって複数の項目を選択できるかどうかを示します。<br/>- **Defaultentitytype**: `String` です。 使用する既定のエンティティ型。<br/>- **defaultViewId**: `String`。 使用する既定のビュー。<br/>- **Entitytypes**: `String[]`。 表示するエンティティ型。<br/>- **viewid**: `String[]`。 ビューピッカーで使用できるビュー。 システムビューのみがサポートされています (ユーザービューではありません)。|

## <a name="return-value"></a>戻り値

型: [Promise](https://developer.mozilla.org/docs/Web/JavaScript/reference/Global_Objects/Promise) <[Entityreference](../entityreference.md)[] >


### <a name="related-topics"></a>関連トピック

[ユーティリティ](../utility.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../../overview.md)
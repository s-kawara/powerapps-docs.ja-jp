---
title: getTimeZoneOffsetMinutes |Microsoft Docs
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
ms.assetid: 86290d20-7dbb-4932-adaa-31121ae7a3f6
ms.openlocfilehash: bc621299b19b1387225b8532ee03ff65e0e6471f
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72341014"
---
# <a name="gettimezoneoffsetminutes"></a>getTimeZoneOffsetMinutes

[!INCLUDE [gettimezoneoffsetminutes-description](includes/gettimezoneoffsetminutes-description.md)]

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリ

## <a name="syntax"></a>構文

`context.usersettings.getTimeZoneOffsetMinutes(date)`

## <a name="parameters"></a>パラメーター

| パラメーター名|種類|必須|Description|
| ------------- |----|--------|-----------|
|予定|`Date`|はい|utc からのオフセットを取得する日付。|

## <a name="return-value"></a>戻り値

種類: `Number` の説明: タイムゾーンのオフセット (分単位)。


### <a name="related-topics"></a>関連トピック

[ユーザー設定](../usersettings.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../../overview.md)
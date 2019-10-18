---
title: formatTime |Microsoft Docs
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
ms.assetid: 148964b5-106e-4f2e-8038-9086d29dc54f
ms.openlocfilehash: cc2c7dfdbe9952d69dcda9fdd4c813965f539478
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72343337"
---
# <a name="formattime"></a>formatTime

[!INCLUDE [formattime-description](includes/formattime-description.md)]

## <a name="syntax"></a>構文

`context.formatting.formatTime(value, behavior);`

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー)

## <a name="parameters"></a>パラメーター

| パラメーター名|種類|必須|Description|
| ------------- |----|--------|-----------|
|値|`Date`|はい|書式設定する日付。|
|挙動|`DateTimeFieldBehavior`|はい|書式設定する datetime オブジェクトの動作。 @No__t_0 には、次の属性があります。<br/>-  `None =0`: 不明な DateTime の動作 <br/>-  `UserLocal =1`: ユーザーのローカル時間を尊重します。 UTC として格納された日付<br/>-  の `TimeZoneIndependent =3`: UTC に変換せずに格納された日付と時刻|

## <a name="return-value"></a>戻り値

種類: `string`


### <a name="related-topics"></a>関連トピック

[形式](../formatting.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../../overview.md)
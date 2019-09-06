---
title: formatTime | Microsoft Docs
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
ms.assetid: 148964b5-106e-4f2e-8038-9086d29dc54f
---

# <a name="formattime"></a>formatTime

[!INCLUDE [formattime-description](includes/formattime-description.md)]

## <a name="syntax"></a>構文

`formatTime(value, behavior)`

## <a name="parameters"></a>パラメーター

| パラメーター名|型|必須出席者|説明|
| ------------- |----|--------|-----------|
|値|`Date`|はい|書式設定する日付。|
|動作|`DateTimeFieldBehavior`|はい|書式設定する日時オブジェクトの動作。 `DateTimeFieldBehavior` には次のような属性があります:<br/>- `None =0`: 不明な DateTime の動作 <br/>- `UserLocal =1`: ユーザーの現地時間を尊重します。 UTC で保存された日付<br/>- `TimeZoneIndependent =3`: UTC に変換せずに保存された日付と時刻|

## <a name="return-value"></a>戻り値

種類: `string`


### <a name="related-topics"></a>関連トピック

[形式](../formatting.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../../overview.md)
---
title: UserSettings | Microsoft Docs
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
ms.assetid: c237ff96-9268-4068-9d61-aea0bdc79fc2
---

# <a name="usersettings"></a>usersettings

[!INCLUDE[cc-beta-prerelease-disclaimer](../../../includes/cc-beta-prerelease-disclaimer.md)]

[!INCLUDE [usersettings-description](includes/usersettings-description.md)]

## <a name="properties"></a>プロパティ

## <a name="dateformattinginfo"></a>dateFormattingInfo

サーバーから取得した日付書式情報。

**種類**: `DateFormattingInfo`

## <a name="isrtl"></a>isRTL

それが右から左に書く言語かどうか

**種類**: `boolean`

## <a name="languageid"></a>languageId

現在のユーザーの言語 ID

**種類**: `number`

## <a name="numberformattinginfo"></a>numberFormattingInfo

サーバーから取得した数値書式情報。

**種類**: `NumberFormattingInfo`

## <a name="securityroles"></a>securityRoles

現在のユーザー ロール

**種類**: `string[]`

## <a name="userid"></a>userId

現在のユーザーの ID

**種類**: `string`

## <a name="username"></a>userName

現在のユーザー名

**種類**: `string`

## <a name="methods"></a>メソッド

|方法 | 説明 | 
| ------|-------------|
|[getTimeZoneOffsetMinutes](usersettings/gettimezoneoffsetminutes.md)|[!INCLUDE [gettimezoneoffsetminutes-description](usersettings/includes/gettimezoneoffsetminutes-description.md)]|

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークの API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../overview.md)
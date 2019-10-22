---
title: UserSettings | Microsoft Docs
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
ms.assetid: c237ff96-9268-4068-9d61-aea0bdc79fc2
ms.openlocfilehash: 5325091d8f82ffd98cfc4e5fdab4e0228a5d541e
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72341037"
---
# <a name="usersettings"></a>UserSettings

[!INCLUDE [usersettings-description](includes/usersettings-description.md)]

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリ

## <a name="properties"></a>プロパティ

### <a name="dateformattinginfo"></a>Date書式化情報

サーバーから取得された日付の書式設定情報。

**種類**: [date書式化情報](dateformattinginfo.md)

### <a name="isrtl"></a>isRTL

言語が右から左の場合に true を返します。

**種類**: `boolean`

### <a name="languageid"></a>languageId

現在のユーザーの言語 id。

**種類**: `number`

### <a name="numberformattinginfo"></a>数値の書式情報

サーバーから取得した数値の書式設定情報。

**種類**: 数値[書式情報](numberformattinginfo.md)

### <a name="securityroles"></a>securityRoles

現在のユーザーロール。

**種類**: `string[]`

### <a name="userid"></a>userId

現在のユーザーの id。

**種類**: `string`

### <a name="username"></a>userName

現在のユーザーのユーザー名。

**種類**: `string`

## <a name="methods"></a>メソッド

|B | Description | 
| ------|-------------|
|[getTimeZoneOffsetMinutes](usersettings/gettimezoneoffsetminutes.md)|[!INCLUDE [gettimezoneoffsetminutes-description](usersettings/includes/gettimezoneoffsetminutes-description.md)]|

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネントフレームワーク API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../overview.md)
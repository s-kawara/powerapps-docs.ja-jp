---
title: DateFormattingInfo | Microsoft Docs
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
ms.assetid: 4e7d43fb-b6b7-4f1d-89e3-0b8157c9d2d9
ms.openlocfilehash: fb6dc5c67cc0ea031ab4e264d282458163ee46a0
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72344832"
---
# <a name="dateformattinginfo"></a>DateFormattingInfo

[!INCLUDE [context-description](includes/dateformattinginfo-description.md)]

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリ

## <a name="properties"></a>プロパティ

### <a name="abbreviateddaynames"></a>abbreviatedDayNames

{"Sun"、"Mon"、"火曜"、"水曜日"、"Thu"、"金曜"、"Sat"}

**種類**: `string`

### <a name="abbreviatedmonthgenitivenames"></a>abbreviatedMonthGenitiveNames

{"Jan"、"Feb"、"Mar"、"Apr"、"may"、"6"、"7 月"、"8 月"、"Sep"、"Oct"、"11 月"、"Dec"、""}

**種類**: `string[]`

### <a name="abbreviatedmonthnames"></a>Datetimeformatinfo.abbreviatedmonthnames

{"Jan"、"Feb"、"Mar"、"Apr"、"may"、"6"、"7 月"、"8 月"、"Sep"、"Oct"、"11 月"、"Dec"、""}

**種類**: `string[]`

### <a name="amdesignator"></a>amDesignator 子

使い慣れ

**種類**: `string`

### <a name="calendar"></a>カレンダー

**種類**: `object`

@No__t_0 オブジェクトには、次のプロパティが含まれています。

|名前|種類|Description|
|--|--|--|
|`algorithmType`|`number`|1|
|`calendarType`|`number`|1|
|`maxSupportedDateTime`|`Date`|"/日付 (253402300799999)/"|
|`minSupportedDateTime`|`Date`|"/日付 (-62135568000000)/"|
|`twoDigitYearMax`|`number`|2029|

### <a name="calendarweekrule"></a>calendarWeekRule

**種類**: `number`

### <a name="dateseparator"></a>dateSeparator

"/"

**種類**: `string`

### <a name="daynames"></a>Datetimeformatinfo.daynames

{"日曜日"、"Monday"、"火曜日"、"水曜日"、"木曜日"、"金曜"、"土曜日"}

**種類**: `string[]`

### <a name="firstdayofweek"></a>firstDayOfWeek

**種類**: `number`

@No__t_0 プロパティは、次のいずれかの値に設定できます。

|Value|通用|
|--|--|
|0|Sunday|
|1|月曜日|
|2|日付|
|3|毎週|
|4|(木)|
|5|月曜|
|6|Saturday|

### <a name="fulldatetimepattern"></a>Datetimeformatinfo.fulldatetimepattern

"dddd, MMMM d, yyyy h:mm: ss tt"

**種類**: `string`

### <a name="longdatepattern"></a>Datetimeformatinfo.longdatepattern

dddd, MMMM d, yyyy "

**種類**: `string`

### <a name="longtimepattern"></a>Datetimeformatinfo.longtimepattern

"hh: mm: ss tt"

**種類**: `string`

### <a name="monthdaypattern"></a>Datetimeformatinfo.monthdaypattern

"MMMM dd"

**種類**: `string`

### <a name="monthgenitivenames"></a>月の Geniti・ベンダー

{"January", "2 月", "3 月",... "December", ""}

**種類**: `string[]`

### <a name="monthnames"></a>monthNames

{"January", "2 月", "3 月",... "December", ""}

**種類**: `string[]`

### <a name="pmdesignator"></a>Datetimeformatinfo.amdesignator

PM

**種類**: `string`

### <a name="shortdatepattern"></a>Datetimeformatinfo.shortdatepattern

"M/d/yyyy"

**種類**: `string`

### <a name="shorttimepattern"></a>Datetimeformatinfo.shorttimepattern

"h:mm tt"

**種類**: `string`

### <a name="shortestdaynames"></a>shortestDayNames

{"Su"、"Mo"、"Tu"、"i"、"Th"、"Fr"、"Sa"}

**種類**: `string[]`

### <a name="sortabledatetimepattern"></a>Datetimeformatinfo.sortabledatetimepattern

yyyy'-'mm'-'dd't'hh-' MM'-' Dd' T' HH ': ' MM ': ' ss "

**種類**: `string`

### <a name="timeseparator"></a>timeSeparator

":"

**種類**: `string`

### <a name="universalsortabledatetimepattern"></a>System.globalization.datetimeformatinfo.universalsortabledatetimepattern

"yyyy'-'mm'-'dd't'hh-' MM'-' dd HH ': ' MM ': ' Ss' Z '"

**種類**: `string`

### <a name="yearmonthpattern"></a>Datetimeformatinfo.yearmonthpattern

"MMMM yyyy"

**種類**: `string`


### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネントフレームワーク API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../overview.md)
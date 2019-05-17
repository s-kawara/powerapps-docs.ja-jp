---
title: DateFormattingInfo | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4e7d43fb-b6b7-4f1d-89e3-0b8157c9d2d9
---

# <a name="dateformattinginfo"></a>DateFormattingInfo

[!INCLUDE [context-description](includes/dateformattinginfo-description.md)]

## <a name="abbreviateddaynames"></a>abbreviatedDayNames

{ "日", "月", "火", "水", "木", "金", "土" }

**種類**: `string`

## <a name="abbreviatedmonthgenitivenames"></a>abbreviatedMonthGenitiveNames

{ "1 月", "2 月", "3 月", "4 月", "5 月", "6 月", "7 月", "8 月", "9 月", "10 月", "11 月", "12 月", "" }

**種類**: `string[]`

## <a name="abbreviatedmonthnames"></a>abbreviatedMonthNames

{ "1 月", "2 月", "3 月", "4 月", "5 月", "6 月", "7 月", "8 月", "9 月", "10 月", "11 月", "12 月", "" }

**種類**: `string[]`

## <a name="amdesignator"></a>amDesignator

"午前"

**種類**: `string`

## <a name="calendar"></a>calendar

**種類**: `object`

`calendar` オブジェクトは以下のプロパティを含みます:

|Name|型|説明|
|--|--|--|
|`algorithmType`|`number`|1|
|`calendarType`|`number`|1|
|`maxSupportedDateTime`|`Date`|"/Date(253402300799999)/"|
|`minSupportedDateTime`|`Date`|"/Date(-62135568000000)/"|
|`twoDigitYearMax`|`number`|2029|

## <a name="calendarweekrule"></a>calendarWeekRule

0

**種類**: `number`

## <a name="dateseparator"></a>dateSeparator

"/"

**種類**: `string`

## <a name="daynames"></a>dayNames

{ "日曜日", "月曜日", "火曜日", "水曜日", "木曜日", "金曜日", "土曜日" }

**種類**: `string[]`

## <a name="firstdayofweek"></a>firstDayOfWeek

**種類**: `number`

`firstDayOfWeek` プロパティは以下のいずれかの値に設定することができます:

|Value|説明|
|--|--|
|0|日曜日|
|1|月曜日|
|2|火曜日|
|3|水曜日|
|4|木曜日|
|5|金曜日|
|6|土曜日|

## <a name="fulldatetimepattern"></a>fullDateTimePattern

"dddd, MMMM d, yyyy h:mm:ss tt"

**種類**: `string`

## <a name="longdatepattern"></a>longDatePattern

dddd, MMMM d, yyyy"

**種類**: `string`

## <a name="longtimepattern"></a>longTimePattern

"hh:mm:ss tt"

**種類**: `string`

## <a name="monthdaypattern"></a>monthDayPattern

"MMMM dd"

**種類**: `string`

## <a name="monthgenitivenames"></a>monthGenitiveNames

{ "1 月", "2 月", "3 月", ... "12 月", "" }

**種類**: `string[]`

## <a name="monthnames"></a>monthNames

{ "1 月", "2 月", "3 月", ... "12 月", "" }

**種類**: `string[]`

## <a name="pmdesignator"></a>pmDesignator

"午後"

**種類**: `string`

## <a name="shortdatepattern"></a>shortDatePattern

"M/d/yyyy"

**種類**: `string`

## <a name="shorttimepattern"></a>shortTimePattern

"h:mm tt"

**種類**: `string`

## <a name="shortestdaynames"></a>shortestDayNames

{ "日", "月", "火", "水", "木", "金", "土" }

**種類**: `string[]`

## <a name="sortabledatetimepattern"></a>sortableDateTimePattern

yyyy'-'MM'-'dd'T'HH':'mm':'ss"

**種類**: `string`

## <a name="timeseparator"></a>timeSeparator

":"

**種類**: `string`

## <a name="universalsortabledatetimepattern"></a>universalSortableDateTimePattern

"yyyy'-'MM'-'dd HH':'mm':'ss'Z'"

**種類**: `string`

## <a name="yearmonthpattern"></a>yearMonthPattern

"MMMM yyyy"

**種類**: `string`


### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークの API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../overview.md)
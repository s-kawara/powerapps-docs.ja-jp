---
title: Day、Month、Year、Hour、Minute、Second、および Weekday 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Day、Month、Year、Hour、Minute、Second、および Weekday 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 10/25/2016
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: ab824432833614ba5b2002375a79e7899a8d7277
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61551263"
---
# <a name="day-month-year-hour-minute-second-and-weekday-functions-in-powerapps"></a>PowerApps の Day、Month、Year、Hour、Minute、Second、および Weekday 関数
Date/Time 値の個々の要素を返します。

## <a name="description"></a>説明
**Day** 関数は、Date/Time 値の日付要素を 1 から 31 の範囲で返します。

**Month** 関数は、Date/Time 値の月要素を 1 から 12 の範囲で返します。

**Year** 関数は、Date/Time 値の年要素を 1900 以上の範囲で返します。

**Hour** 関数は、Date/Time 値の時間要素を 0 (12:00 AM) から 23 (11:00 PM) の範囲で返します。

**Minute** 関数は、Date/Time 値の分要素を 0 から 59 の範囲で返します。

**Second** 関数は、Date/Time 値の秒要素を 0 から 59 の範囲で返します。

**Weekday** 関数は、Date/Time 値の曜日を返します。  既定では、結果の範囲は 1 (日曜日) から 7 (土曜日) です。  次のように、Microsoft Excel Weekday 関数コードまたは StartOfWeek 列挙値で、別の範囲を指定できます。

| Excel コード | StartOfWeek 列挙型 | 説明 |
| --- | --- | --- |
| **1**、**17** |**StartOfWeek.Sunday** |1 (日曜日) から 7 (土曜日) までの数値。  既定値。 |
| **2**、**11** |**StartOfWeek.Monday** |1 (月曜日) から 7 (日曜日) までの数値。 |
| **3** |**StartOfWeek.MondayZero** |0 (月曜日) から 6 (日曜日) までの数値。 |
| **12** |**StartOfWeek.Tuesday** |1 (火曜日) から 7 (月曜日) までの数値。 |
| **13** |**StartOfWeek.Wednesday** |1 (水曜日) から 7 (火曜日) までの数値。 |
| **14** |**StartOfWeek.Thursday** |1 (木曜日) から 7 (水曜日) までの数値。 |
| **15** |**StartOfWeek.Friday** |1 (金曜日) から 7 (木曜日) までの数値。 |
| **16** |**StartOfWeek.Saturday** |1 (土曜日) から 7 (金曜日) までの数値。 |

どの関数も数値を返します。

詳細については、[日付と時刻の操作](../show-text-dates-times.md)に関するページを参照してください。

## <a name="syntax"></a>構文
**Day**( *DateTime* )<br>**Month**( *DateTime* )<br>**Year**( *DateTime* )<br>**Hour**( *DateTime* )<br>**Minute**( *DateTime* )<br>**Second**( *DateTime* )

* *DateTime* - 必須。  操作する Date/Time 値。  

**Weekday**( *DateTime* [, *WeekdayFirst* ] )<br>

* *DateTime* - 必須。  操作する Date/Time 値。 
* *WeekdayFirst* - 省略可能。  週の開始日を指定する Excel コード。  指定しない場合は、1 (日曜日が開始日) が使用されます。

## <a name="examples"></a>例
次の例では、現在の時刻は **2015 年 4 月 9 日木曜日**の**午後 3 時 59 分 37 秒**です。

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Year(&nbsp;Now()&nbsp;)** |現在の時刻と日付の年要素を返します。 |2015 |
| **Month(&nbsp;Now()&nbsp;)** |現在の時刻と日付の月要素を返します。 |4 |
| **Day(&nbsp;Now()&nbsp;)** |現在の時刻と日付の日付要素を返します。 |9 |
| **Hour(&nbsp;Now()&nbsp;)** |現在の時刻と日付の時間要素を返します。 |15 |
| **Minute(&nbsp;Now()&nbsp;)** |現在の時刻と日付の分要素を返します。 |59 |
| **Second(&nbsp;Now()&nbsp;)** |現在の時刻と日付の分要素を返します。 |37 |
| **Weekday(&nbsp;Now()&nbsp;)** |既定の週開始日 (日曜日) を使用して、現在の時刻と日付の曜日要素を返します。 |5 |
| **Weekday(&nbsp;Now(),&nbsp;14&nbsp;)** |週開始日として木曜日を指定する Excel コードを使用して、現在の時刻と日付の曜日要素を返します。 |1 |
| **Weekday(&nbsp;Now(),&nbsp;StartOfWeek.Wednesday&nbsp;)** |週開始日として水曜日を指定する **StartOfWeek** 列挙型を使用して、現在の時刻と日付の曜日要素を返します。 |2 |


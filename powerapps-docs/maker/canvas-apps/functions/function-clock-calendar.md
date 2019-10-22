---
title: Calendar および Clock 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Calendar および Clock 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 11/07/2015
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: a4b3540d8a7d499d4da1206f70298ea4a2541b16
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "71985435"
---
# <a name="calendar-and-clock-functions-in-powerapps"></a>PowerApps の Calendar および Clock 関数
現在のロケールのカレンダーおよび時計の情報を取得します。

## <a name="description"></a>説明
**Calendar** 関数と **Clock** 関数は、現在のロケールに関する情報を取得する関数です。

これらの関数を使用して、現在のユーザーの言語で日付と時刻を表示できます。  **Calendar** 関数と **Clock** 関数によって返される単一列テーブルは、ドロップダウン コントロールとリストボックス コントロールの **[Items](../controls/properties-core.md)** プロパティで直接使用できます。

| 関数 | 説明 |
| --- | --- |
| **Calendar.MonthsLong()** |"January" から始まる、各月の完全な名前を含む単一列テーブル。 |
| **Calendar.MonthsShort()** |January の "Jan" から始まる、各月の省略された名前を含む単一列テーブル。 |
| **Calendar.WeekdaysLong()** |"Sunday" から始まる、各曜日の完全な名前を含む単一列テーブル。 |
| **Calendar.WeekdaysShort()** |Sunday の "Sun" から始まる、各曜日の省略された名前を含む単一列テーブル。 |
| **Clock.AmPm()** |長い大文字の "AM" および "PM" の指定を含む単一列テーブル。  言語で 24 時間制を使用している場合、テーブルは空になります。 |
| **Clock.AmPmShort()** |短い大文字の "A" および "P" の指定を含む単一列テーブル。  言語で 24 時間制を使用している場合、テーブルは空になります。 |
| **Clock.IsClock24()** |対象ロケールで 24 時間制を使用しているかどうかを示すブール値。 |

**[Text](function-text.md)** 関数では、これと同じ情報を使って日付と時刻の値の書式を設定できます。  **[Language](function-language.md)** 関数は、現在の言語と地域コードを返します。

## <a name="syntax"></a>構文
**Calendar.MonthsLong**()

**Calendar.MonthsShort**()

**Calendar.WeekdaysLong**()

**Calendar.WeekdaysShort**()

**Clock.AmPm**()

**Clock.AmPmShort**()

**Clock.IsClock24**()

## <a name="examples"></a>例
1. ドロップダウン コントロールを挿入します。
2. **[Items](../controls/properties-core.md)** プロパティを次の数式に設定します。
   
   * **Calendar.MonthsLong()**
3. これで、アプリのユーザーが自分の言語で月を選択できるようになります。  **MonthsLong** を **Calendar** によって返されるいずれかの単一列テーブルに置き換えて、曜日と時刻のセレクターを作成できます。

**[Language](function-language.md)** で "en-US" が返される米国では、**Calendar** 関数で以下が返されます。

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Calendar.MonthsLong()** |戻り値には、"January" から始まる各月の完全名が含まれます。 |[ "January"、"February"、"March"、"April"、"May"、"June"、"July"、"August"、"September"、"October"、"November"、"December" ] |
| **Calendar.MonthsShort()** |戻り値には、"January" から始まる各月の省略名が含まれます。 |[ "Jan"、"Feb"、"Mar"、"Apr"、"May"、"Jun"、"Jul"、"Aug"、"Sep"、"Oct"、"Nov"、"Dec" ] |
| **Calendar.WeekdaysLong()** |戻り値には、"日曜日" から始まる各日の完全な名前が含まれます。 |[ "Sunday"、"Monday"、"Tuesday"、"Wednesday"、"Thursday"、"Friday"、"Saturday" ] |
| **Calendar.WeekdaysShort()** |戻り値には、"日曜日" から始まる、各曜日の省略名が含まれます。 |[ "Sun"、"Mon"、"Tue"、"Wed"、"Thu"、"Fri"、"Sat" ] |
| **Clock.AmPm()** |この言語では、12 時間制を使用しています。 戻り値には、大文字バージョンの完全な AM と PM の指定が含まれます。 |[ "AM", "PM" ] |
| **Clock.AmPmShort()** |この言語では、12 時間制を使用しています。 戻り値には、大文字バージョンの短い AM と PM の指定が含まれます。 |[ "A", "P" ] |
| **Clock.IsClock24()** |この言語では、12 時間制を使用しています。 |**false** |


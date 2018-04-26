---
title: Now、Today、および IsToday 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Now、Today、および IsToday 関数の参照情報
documentationcenter: na
author: gregli-msft
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: reference
ms.component: canvas
ms.date: 11/07/2015
ms.author: gregli
ms.openlocfilehash: 410e9be47b4356a97292eb5de17c5dc10885fae3
ms.sourcegitcommit: 8bd4c700969d0fd42950581e03fd5ccbb5273584
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="now-today-and-istoday-functions-in-powerapps"></a>PowerApps の Now、Today、および IsToday 関数
現在の日付と時刻を返し、日付/時刻値が今日のものかどうかをテストします。

## <a name="description"></a>説明
**Now** 関数は、現在の日付と時刻を日付/時刻値として返します。

**Today** 関数は、現在の日付を日付/時刻値として返します。 時刻部分は、午前 0 時です。 **Today** は、1 日 (今日の午前 0 時から翌日の午前 0 時まで) を通して同じ値を保持します。

**IsToday** 関数は、日付/時刻値が今日の午前 0 時から翌日の午前 0 時の間の値になっているかどうかをテストします。 この関数は、**true** または **false** のブール値を返します。

これらの関数はすべて、現在のユーザーのローカル時刻を使用します。

詳細については、[日付と時刻の操作](../show-text-dates-times.md)に関するページを参照してください。

## <a name="syntax"></a>構文
**Now**()

**Today**()

**IsToday**( *DateTime* )

* *DateTime* - 必須。  テストする日付/時刻値。

## <a name="examples"></a>例
このセクションの例では、現在の時刻が **2015 年 2 月 12 日**の**午前 3 時 59 分**、言語が **en-us** です。

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Text( Now(), "mm/dd/yyyy hh:mm:ss" )** |現在の日付と時刻を取得し、文字列として表示します。 |"02/12/2015 03:59:00" |
| **Text( Today(), "mm/dd/yyyy hh:mm:ss" )** |現在の日付のみを取得し、時刻は午前 0 時としたまま、これを文字列として表示します。 |"02/12/2015 00:00:00" |
| **IsToday( Now() )** |現在の日付と時刻が、今日の午前 0 時から翌日の午前 0 時の間であるかどうかをテストします。 |**true** |
| **IsToday( Today() )** |現在の日付が、今日の午前 0 時から翌日の午前 0 時の間であるかどうかをテストします。 |**true** |
| **Text( DateAdd( Now(), 12 ), "mm/dd/yyyy hh:mm:ss" )** |現在の日付と時刻を取得し、その結果に 12 日を加算して、文字列として表示します。 |"02/24/2015 03:59:00" |
| **Text( DateAdd( Today(), 12 ), "mm/dd/yyyy hh:mm:ss" )** |現在の日付を取得し、その結果に 12 日を加算して、文字列として表示します。 |"02/24/2015 00:00:00" |
| **IsToday( DateAdd( Now(), 12 ) )** |現在の日付と時刻に 12 日を加算した日時が今日の午前 0 時から翌日の午前 0 時の間であるかどうかをテストします。 |**false** |
| **IsToday( DateAdd( Today(), 12 ) )** |現在の日付に 12 日を加算した日付が今日の午前 0 時から翌日の午前 0 時の間であるかどうかをテストします。 |**false** |


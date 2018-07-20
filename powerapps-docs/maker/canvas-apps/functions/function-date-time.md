---
title: Date および Time 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Date および Time 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 11/07/2015
ms.author: gregli
ms.openlocfilehash: 440d7bc8a737fdc53a5c76ec80db7fcf0d515f7e
ms.sourcegitcommit: dfa0e1a7981814e15e6ca4720e2a5f930e859db1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2018
ms.locfileid: "39020103"
---
# <a name="date-and-time-functions-in-powerapps"></a>PowerApps の Date および Time 関数
日付と時刻のコンポーネントを日付/時刻値に変換します。

## <a name="description"></a>説明
**Date** 関数は、個々の Year、Month、および Day 値を Date/Time 値に変換します。  時刻部分は、午前 0 時です。

* Year が 0 以上で 1899 以下の場合は、年を計算するために、その値が 1900 に加算されます。  **70** は **1970** になります。
* Month が 1 未満か 12 を超える場合は、指定された年の始めに対してその月数が減算または加算された結果になります。
* 指定された月の日数より Day が大きい場合は、月の初日に Day の日数が加算され、翌月の対応する日付が返されます。  Day が 1 未満の場合は、その日数に 1 を加えた数が、指定された月の初日から減算されます。

**Time** 関数は、個々の Hour、Minute、および Second 値を Date/Time 値に変換します。  結果には、関連付けられている日付がありません。

文字列を値に変換する方法の情報については、**[DateValue](function-datevalue-timevalue.md)**、**[TimeValue](function-datevalue-timevalue.md)**、および **[DateTimeValue](function-datevalue-timevalue.md)** 関数を参照してください。  

詳細については、[日付と時刻の操作](../show-text-dates-times.md)に関するページも参照してください。

## <a name="syntax"></a>構文
**Date**( *Year*, *Month*, *Day* )

* *Year* - 必須。  1899 より大きい数値は、絶対値として解釈されます (1980 は 1980 として解釈されます)。0 から 1899 の範囲の数値は、1900 に対する相対値として解釈されます  (たとえば、80 は 1980 として解釈されます)。
* *Month* - 必須。  1 ～ 12 の範囲の数値。
* *Day* - 必須。 1 ～ 31 の範囲の数値。

**Time**( *Hour*, *Minute*, *Second* )

* *Hour* - 必須。  0 (12:00 AM) から 23 (11:00 PM) の範囲の数値。
* *Minute* - 必須。 0 ～ 59 の範囲の数値。
* *Second* - 必須。 0 ～ 59 の範囲の数値。

## <a name="examples"></a>例
### <a name="date"></a>Date
ユーザーが **HireYear** という名前のテキスト入力コントロールに「**1979**」、**HireMonth** という名前のテキスト入力コントロールに「**3**」、**HireDay** という名前のテキスト入力コントロールに「**17**」を入力した場合、この関数は **3/17/1979** を返します。

**Date(Value(HireYear.Text), Value(HireMonth.Text), Value(HireDay.Text))**

### <a name="time"></a>Time
ユーザーが **BirthHour** という名前のテキスト入力コントロールに「**14**」、**BirthMinute** という名前のテキスト入力コントロールに「**50**」、**BirthSecond** という名前のテキスト入力コントロールに「**24**」を入力した場合、この関数は **02:50:24 p** を返します。

**Text(Time(Value(BirthHour.Text), Value(BirthMinute.Text), Value(BirthSecond.Text)), "hh:mm:ss a/p")**


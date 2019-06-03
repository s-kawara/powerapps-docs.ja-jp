---
title: DateValue、TimeValue、および DateTimeValue 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の DateValue、TimeValue、および DateTimeValue 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 11/07/2015
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: c1f11be30f56859ede0950feebc27dd1be39d011
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61551194"
---
# <a name="datevalue-timevalue-and-datetimevalue-functions-in-powerapps"></a>PowerApps の DateValue、TimeValue、および DateTimeValue 関数
文字列内の日付、時刻、またはその両方を日付/時刻値に変換します。

## <a name="description"></a>説明
**DateValue** 関数は、日付文字列 (たとえば、"10/01/2014") を日付/時刻値に変換します。

**TimeValue** 関数は、時間文字列 (たとえば、"12:15 PM") を日付/時刻値に変換します。

**DateTimeValue** 関数は、日付および時間文字列 (たとえば、"January 10, 2013 12:13 AM") を日付/時刻値に変換します。

**DateValue** 関数は日付文字列内のすべての時刻情報を無視し、**TimeValue** 関数は時刻文字列内のすべての日付情報を無視します。

既定では、使用される言語は現在のユーザーの言語ですが、文字列が適切に解釈されるようにオーバーライドすることができます。 たとえば、"10/1/1920" が "en" では 10 月 1 日<sup></sup>と解釈され、"fr" では 1 月 10 日<sup></sup>と解釈されます。

日付は、以下の形式のいずれかである必要があります。

* MM/DD/YYYY
* DD/MM/YYYY
* DD Mon YYYY
* Month DD, YYYY

数値要素の日付、月、年、時間、分、秒から変換するには、 **[Date](function-date-time.md)** および **[Time](function-date-time.md)** 関数を参照してください。

詳細については、[日付と時刻の操作](../show-text-dates-times.md)に関するページも参照してください。

数値を変換するには、 **[Value](function-value.md)** 関数を参照してください。

## <a name="syntax"></a>構文
**DateValue**( *String* [, *Language* ])<br>**DateTimeValue**( *String* [, *Language* ])<br>**TimeValue**( *String* [, *Language* ])

* *String* - 必須。  日付、時刻、または日付と時刻の組み合わせの値を含むテキスト文字列。
* *Language* - 省略可能。  **[Language](function-language.md)** 関数から最初の 2 文字で返されるような言語文字列。  指定しない場合は、現在のユーザーのクライアントの言語が使用されます。  

## <a name="examples"></a>例
### <a name="datevalue"></a>DateValue
**[Startdate]** という名前のテキスト入力コントロールに「**10/11/2014**」と入力し、ラベルの **[Text](../controls/properties-core.md)** プロパティをこの関数に設定した場合は、次のようになります。

* **Text(DateValue(Startdate.Text), DateTimeFormat.LongDate)**
  
    コンピューターが **en** ロケールに設定されている場合、ラベルには "**Saturday, October 11, 2014**" と表示されます。
  
    > [!NOTE]
  > **DateTimeFormat** パラメーターでは、**LongDateTime** の他にもいくつかのオプションを使用することができます。 これらのオプションの一覧を表示するには、関数ボックスにパラメーターを入力し、すぐ後に感嘆符を入力します。
* **Text(DateValue(Startdate.Text, "fr"), DateTimeFormat.LongDate)**
  
    ラベルには "**Monday, November 10, 2014**" と表示されます。

同じことを **2014 年 10 月 20 日**に行った場合は、次のようになります。

* **DateDiff(DateValue(Startdate.Text), Today())**
  
    コンピューターが **en** 言語に設定されている場合、ラベルには "**9**" と表示されます。これは、10 月 11 日から 10 月 20 日までの日数を示してします。 **[DateDiff](function-dateadd-datediff.md)** 関数は、間隔を月、四半期、または年で示すこともできます。

### <a name="datetimevalue"></a>DateTimeValue
**[Start]** という名前のテキスト入力コントロールに「**10/11/2014 1:50:24.765 PM**」と入力し、ラベルの **[Text](../controls/properties-core.md)** プロパティをこの関数に設定した場合は、次のようになります。

* **Text(DateTimeValue(Start.Text), DateTimeFormat.LongDateTime)**
  
    コンピューターが "en" ロケールに設定されている場合、ラベルには "**Saturday, October 11, 2014 1:50:24 PM**" と表示されます。
  
    > [!NOTE]
  > **DateTimeFormat** パラメーターでは、**LongDateTime** の他にもいくつかのオプションを使用することができます。 これらのオプションの一覧を表示するには、関数ボックスにパラメーターを入力し、すぐ後に感嘆符を入力します。
* **Text(DateTimeValue(Start.Text, "fr"), DateTimeFormat.LongDateTime)**
  
    ラベルには "**Monday, November 10, 2014 1:50:24 PM**" と表示されます。
* **Text(DateTimeValue(Start.Text), "dddd, mmmm dd, yyyy hh:mm:ss.fff AM/PM")**
  
    コンピューターが **en** ロケールに設定されている場合、ラベルには "**Saturday, October 11, 2014 01:50:24:765 PM**" と表示されます。
  
    また、**hh:mm:ss.f** または **hh:mm:ss.ff** を指定し、時刻を最も近い 10 分の 1 または 100 分の 1 秒の位に丸めることもできます。

### <a name="timevalue"></a>TimeValue
テキスト入力コントロールに **FinishedAt** という名前を付け、ラベルの **[Text](../controls/properties-core.md)** プロパティをこの関数に設定すると、次のようになります。

**If(TimeValue(FinishedAt.Text)<TimeValue("5:00:00.000 PM"), "You made it!", "Too late!")**

* **[FinishedAt]** コントロールに「**4:59:59.999 PM**」と入力した場合、ラベルには "You made it!" と表示されます。
* **[FinishedAt]** コントロールに「**5:00:00.000 PM**」と入力した場合、ラベルには "Too late!" と表示されます。


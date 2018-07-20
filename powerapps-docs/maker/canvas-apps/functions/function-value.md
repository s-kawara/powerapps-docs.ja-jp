---
title: Value 関数 | Microsoft Docs
description: 構文を含む PowerApps の Value 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 11/07/2015
ms.author: gregli
ms.openlocfilehash: 49088dbcdf2757e14659ee5109cbc86ba68b3bb4
ms.sourcegitcommit: dfa0e1a7981814e15e6ca4720e2a5f930e859db1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2018
ms.locfileid: "39014974"
---
# <a name="value-function-in-powerapps"></a>PowerApps の Value 関数
テキスト形式の文字列を数値に変換します。

## <a name="description"></a>説明
**Value** 関数は、文字としての数字が含まれるテキスト文字列を数値に変換するものです。 ユーザーがテキストとして入力した数値に対して計算を実行する必要がある場合には、この関数を使用します。

**,** と **.** の 2 つの記号は、言語によって解釈が 異なります。  既定では、テキストは現在のユーザーの言語に従って解釈されます。  言語タグを使用すると、使用する言語を指定することができます。このとき使用するのは、**[Language](function-language.md)** 関数により返される言語タグと同じものです。

文字列の形式に関する注意事項:

* 文字列の先頭には現在の言語の通貨記号を付けることができます。  この通貨記号は無視されます。  他の言語の通貨記号は無視されません。
* 文字列の末尾には、百分率であることを示すパーセント記号 (**%**) を付けることができます。  この場合、100 で割った数字が返されます。  パーセンテージ記号と通貨記号を同時に使用することはできません。
* 文字列では指数表記も使用できます。12 x 10<sup>3</sup> を表す場合には、"12e3" という表記になります。

数が適切な形式になっていない場合には、**Value** の戻り値が "*空白*" になります。

日付や時刻の値に変換する場合には、[**DateValue**](function-datevalue-timevalue.md)、[**TimeValue**](function-datevalue-timevalue.md)、[**DateTimeValue**](function-datevalue-timevalue.md) のいずれかの関数を使用してください。

## <a name="syntax"></a>構文
**Value**( *String* [, *LanguageTag* ] )

* *String* - 必須。 数値に変換する文字列。
* *LanguageTag* - 省略可能。  文字列の解析に使用する言語タグ。  指定しなかった場合には、現在のユーザーの言語が使用されます。

## <a name="examples"></a>例
これらの式を実行しているユーザーは米国内のユーザーで、言語として英語を選択しています。  **Language** 関数は、"en-US" を返します。

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Value( "123.456" )** |既定の言語 "en-US" (アメリカ英語) を使用します。アメリカ英語では、ピリオドが小数点を表す記号として使われています。 |123.456 |
| **Value( "123.456", "es-ES" )** |"es-ES" は、スペインのスペイン語を表す言語タグです。  スペインでは、ピリオドが桁区切り記号として使われています。 |123456 |
| **Value( "123,456" )** |既定の言語 "en-US" (アメリカ英語) を使用します。アメリカ英語では、コンマが桁区切り記号として使われています。 |123456 |
| **Value( "123,456", "es-ES" )** |"es-ES" は、スペインのスペイン語を表す言語タグです。  スペインでは、コンマが小数点を表す記号として使われています。 |123.456 |
| **Value( "12.34%" )** |文字列の末尾に、この数字が百分率であることを示すパーセント記号が付いています。 |0.1234 |
| **Value( "$ 12.34" )** |現在の言語の通貨記号は無視されます。 |12.34 |
| **Value( "24e3" )** |指数表記の 12 × 10<sup>3</sup> です。 |24000 |


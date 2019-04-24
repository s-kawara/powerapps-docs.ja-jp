---
title: Replace および Substitute 関数 | Microsoft Docs
description: 構文を含む PowerApps の Replace および Substitute 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 12/02/2018
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: fca1953402c87ca13bc3560b827cde03a47a8e92
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61551608"
---
# <a name="replace-and-substitute-functions-in-powerapps"></a>PowerApps の Replace および Substitute 関数
テキストの文字列の一部を別の文字列に置換します。

## <a name="description"></a>説明
**Replace** 関数は、開始位置と長さによって、置換するテキストを識別します。  

**Substitute** 関数は、文字列を照合することで、置換するテキストを識別します。 1 つ以上の一致が見つかった場合は、それらのすべてを置き換えるか、置換するいずれかを指定することができます。

1 つの文字列を渡すと、変更された文字列が戻り値として返されます。 文字列を含む単一列[テーブル](../working-with-tables.md)を渡すと、変更された文字列の単一列テーブルが戻り値として返されます。 複数列テーブルがある場合は、[テーブルの使用](../working-with-tables.md)に関するページの説明に従って、そのテーブルを単一列テーブルにすることができます。

## <a name="syntax"></a>構文
**Replace**( *String*, *StartingPosition*, *NumberOfCharacters*, *NewString* )

* *String* - 必須。 操作の対象となる文字列。
* *StartingPosition* - 必須。 置換を開始する文字の位置。 *String* の最初の文字の位置は 1 です。
* *NumberOfCharacters* - 必須。 *String* で置換する文字の数。
* *NewString* - 必須。 置換後の文字列。 この引数の文字数は、*NumberOfCharacters* 引数とは異なっていてもかまいません。

**Substitute**( *String*, *OldString*, *NewString* [, *InstanceNumber* ] )

* *String* - 必須。 操作の対象となる文字列。
* *OldString* - 必須。 置換の対象となる文字列。
* *NewString* - 必須。 置換後の文字列。 *OldString* と *NewString* の長さは異なっていてもかまいません。
* *InstanceNumber* - 省略可能。 この引数を使用して、対象のインスタンスの指定*OldString*を置き換える*文字列*1 つ以上のインスタンスが含まれます。 この引数を指定しない場合は、すべてのインスタンスが置き換えられます。

**Replace**( *SingleColumnTable*, *StartingPosition*, *NumberOfCharacters*, *NewString* )

* *SingleColumnTable* - 必須。 操作対象となる複数の文字列の単一列テーブル。
* *StartingPosition* - 必須。 置換を開始する文字の位置。  テーブルの各文字列の最初の文字の位置は 1 です。
* *NumberOfCharacters* - 必須。 各文字列で置換する文字の数。
* *NewString* - 必須。  置換後の文字列。 この引数の文字数は、*NumberOfCharacters* 引数とは異なっていてもかまいません。

**Substitute**( *SingleColumnTable*, *OldString*, *NewString* [, *InstanceNumber* ] )

* *SingleColumnTable* - 必須。 操作対象となる複数の文字列の単一列テーブル。
* *OldString* - 必須。  置換の対象となる文字列。
* *NewString* - 必須。  置換後の文字列。 *OldString* と *NewString* の長さは異なっていてもかまいません。
* *InstanceNumber* - 省略可能。 この引数を使用して、対象のインスタンスの指定*OldString*を置き換える*文字列*1 つ以上のインスタンスが含まれます。 この引数を指定しない場合は、すべてのインスタンスが置き換えられます。

## <a name="examples"></a>例

| 数式 | 説明 | 結果 |
|---------|-------------|--------|
| **Replace( "abcdefghijk",&nbsp;6,&nbsp;5,&nbsp;"*" )** | 1 つの"abcdefghijk"の 5 文字を置き換える"*"("f") の 6 番目の文字で始まる文字。 | "abcde*k" |
| **Replace(&nbsp;"2019",&nbsp;3,&nbsp;2,&nbsp;"20"&nbsp;)** | 「20」と「2019」の最後の 2 つの文字を置き換えます。 | "2020" |
| **Replace(&nbsp;"123456",&nbsp;1,&nbsp;3,&nbsp;"_"&nbsp;)** | 「123456」の最初の 3 つの文字を 1 つの「_」文字に置き換えます。 | "_456" | 
| **Substitute(&nbsp;"Sales&nbsp;Data",&nbsp;"Sales",&nbsp;"Cost"&nbsp;)** | "Sales"の「コスト」の文字列に置換されます。 | 「コスト データ」 | 
| **Substitute( "Quarter&nbsp;1,&nbsp;2018", "1", "2", 1 )** | 「1」と「2」の最初のインスタンスのみを置き換えるため、4 番目の引数 (*インスタンス番号*) 1 で提供します。 |  「第 2、2018」 |
| **Substitute( "Quarter&nbsp;1,&nbsp;2011", "1", "2", 3 )** | 「1」と「2」の 3 番目のインスタンスのみを置き換えるため、4 番目の引数 (*インスタンス番号*) は 3 に付属します。 | 「四半期 1, 2012」 |
| **Substitute( "Quarter&nbsp;1,&nbsp;2011", "1", "2" )** | 「1」と「2」のすべてのインスタンスを置き換えるため、4 番目の引数 (*インスタンス番号*) が指定されていません。 | 「第 2、2022」 |
| **Replace(<br>[&nbsp;"Quarter&nbsp;1,&nbsp;2018",<br>"Quarter&nbsp;2,&nbsp;2011",<br>"Quarter&nbsp;4,&nbsp;2019" ],<br>9,  1, "3" )** | 「3」を単一列テーブルの各レコードの 9 番目の文字に置き換えます。 | [&nbsp;"四半期&nbsp;3、&nbsp;2018"、<br>"四半期&nbsp;3、&nbsp;2011"、<br>"四半期&nbsp;3、&nbsp;2019"&nbsp;] |
| **Substitute( <br>[&nbsp;"Qtr&nbsp;1,&nbsp;2018",<br>"Quarter&nbsp;1,&nbsp;2011",<br>"Q1,&nbsp;2019"&nbsp;],<br>"1", "3", 1 )** | ため、4 番目の引数 (*インスタンス番号*) が付属して、値 1、「1」の最初のインスタンスのみの置換「3」を持つ単一列テーブルは、各レコード。 | [&nbsp;"Qtr&nbsp;3、&nbsp;2018"、<br>"四半期&nbsp;3、&nbsp;2011"、<br>"Q3,&nbsp;2019"&nbsp;] |
| **Substitute( <br>[&nbsp;"Qtr&nbsp;1,&nbsp;2018",<br>"Quarter&nbsp;1,&nbsp;2011",<br>"Q1,&nbsp;2019"&nbsp;],<br>"1", "3" )** | ため、4 番目の引数 (*インスタンス番号*) が指定されていません、「3」を単一列テーブルの各レコードの「1」のすべてのインスタンスに置換されます。 | [&nbsp;"Qtr&nbsp;3、&nbsp;2038"、<br>"四半期&nbsp;3、&nbsp;2033"、<br>"Q3,&nbsp;2039"&nbsp;] |  
 



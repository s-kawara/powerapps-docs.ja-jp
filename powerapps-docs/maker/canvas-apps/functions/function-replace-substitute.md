---
title: Replace および Substitute 関数 | Microsoft Docs
description: 構文を含む PowerApps の Replace および Substitute 関数の参照情報
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
ms.openlocfilehash: d08cbb1ae487c7ae4423d67a499f5477a5ea263b
ms.sourcegitcommit: 8bd4c700969d0fd42950581e03fd5ccbb5273584
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="replace-and-substitute-functions-in-powerapps"></a>PowerApps の Replace および Substitute 関数
テキストの文字列の一部を別の文字列に置換します。

## <a name="description"></a>説明
**Replace** 関数は、開始位置と長さによって、置換するテキストを識別します。  

**Substitute** 関数は、文字列を照合することで、置換するテキストを識別します。  1 つ以上の一致が見つかった場合は、置換対象を指定できます。

1 つの文字列を渡すと、変更された文字列が戻り値として返されます。  文字列を含む単一列[テーブル](../working-with-tables.md)を渡すと、変更された文字列の単一列テーブルが戻り値として返されます。 複数列テーブルがある場合は、[テーブルの使用](../working-with-tables.md)に関するページの説明に従って、そのテーブルを単一列テーブルにすることができます。

## <a name="syntax"></a>構文
**Replace**( *String*, *StartingPosition*, *NumberOfCharacters*, *NewString* )

* *String* - 必須。 操作の対象となる文字列。
* *StartingPosition* - 必須。  置換を開始する文字の位置。 *String* の最初の文字の位置は 1 です。
* *NumberOfCharacters* - 必須。  *String* で置換する文字の数。
* *NewString* - 必須。  置換後の文字列。 この引数の文字数は、*NumberOfCharacters* 引数とは異なっていてもかまいません。

**Substitute**( *String*, *OldString*, *NewString* [, *InstanceNumber* ] )

* *String* - 必須。 操作の対象となる文字列。
* *OldString* - 必須。  置換の対象となる文字列。
* *NewString* - 必須。  置換後の文字列。 *OldString* と *NewString* の長さは異なっていてもかまいません。
* *InstanceNumber* - 省略可能。 既定では、*OldString* の最初のインスタンスが置換されます。 *String* に 2 つ以上のインスタンスが含まれている場合は、置換対象のインスタンスを指定できます。

**Replace**( *SingleColumnTable*, *StartingPosition*, *NumberOfCharacters*, *NewString* )

* *SingleColumnTable* - 必須。 操作対象となる複数の文字列の単一列テーブル。
* *StartingPosition* - 必須。  置換を開始する文字の位置。  テーブルの各文字列の最初の文字の位置は 1 です。
* *NumberOfCharacters* - 必須。  各文字列で置換する文字の数。
* *NewString* - 必須。  置換後の文字列。 この引数の文字数は、*NumberOfCharacters* 引数とは異なっていてもかまいません。

**Substitute**( *SingleColumnTable*, *OldString*, *NewString* [, *InstanceNumber* ] )

* *SingleColumnTable* - 必須。 操作対象となる複数の文字列の単一列テーブル。
* *OldString* - 必須。  置換の対象となる文字列。
* *NewString* - 必須。  置換後の文字列。 *OldString* と *NewString* の長さは異なっていてもかまいません。
* *InstanceNumber* - 省略可能。 既定では、*OldString* の最初のインスタンスが置換されます。 テーブルに 2 つ以上のインスタンスが含まれている場合は、置換対象のインスタンスを指定できます。


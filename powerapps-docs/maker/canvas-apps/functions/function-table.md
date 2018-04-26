---
title: Table 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Table 関数の参照情報
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
ms.openlocfilehash: 28d393d9be240b3e9ba57d108761c7a38f013b24
ms.sourcegitcommit: 8bd4c700969d0fd42950581e03fd5ccbb5273584
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="table-function-in-powerapps"></a>PowerApps の Table 関数
一時[テーブル](../working-with-tables.md)を作成します。

## <a name="description"></a>説明
**Table** 関数は、[レコード](../working-with-tables.md#records)の引数リストからテーブルを作成します。

テーブルの[列](../working-with-tables.md#columns)は、すべての引数レコードのすべてのプロパティの集合になります。 レコードに値が含まれていない列には、"*空白*" の値が追加されます。

テーブルは、文字列や数値と同様、PowerApps 内での値です。 テーブルは関数の引数として指定できるほか、関数から結果として返すことができます。 **Table** は、永続テーブルは作成しません。 その代わりに、引数で構成された一時テーブルを返します。  この一時テーブルは、別の関数の引数として指定できるほか、ギャラリーで視覚化したり、別のテーブルに埋め込んだりもできます。  詳細については、[テーブルの使用](../working-with-tables.md)に関するページを参照してください。

**[ value1, value2, ... ]** という構文を使って、単一列テーブルを作成することもできます。

## <a name="syntax"></a>構文
**Table**( *Record1* [, *Record2*, ... ] )

* *Record(s)* - 必須。 テーブルに追加するレコード。

## <a name="examples"></a>例
* リスト ボックスの **[Items](../controls/properties-core.md)** プロパティを次の数式に設定します。
  <br>**Table({Color:"red"}, {Color:"green"}, {Color:"blue"})**
  
    リスト ボックスには、オプションとしてそれぞれの色が表示されます。
* テキスト ギャラリーを追加し、その **[Items](../controls/properties-core.md)** プロパティをこの関数に設定します。<br>
  **Table({Item:"Violin123", Location:"France", Owner:"Fabrikam"}, {Item:"Violin456", Location:"Chile"})**
  
    ギャラリーには 2 つのレコードが表示されます。どちらにも、項目の場所と名前が含まれます。 所有者の名前が含まれるのは、1 つのレコードのみです。


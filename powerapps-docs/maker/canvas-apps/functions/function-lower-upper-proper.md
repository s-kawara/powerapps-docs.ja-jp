---
title: Lower 関数、Upper 関数、Proper 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Lower 関数、Upper 関数、Proper 関数の参照情報
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
ms.openlocfilehash: 72e1bd234a9cbccc24cf35723ee10bacd175b278
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "42865833"
---
# <a name="lower-upper-and-proper-functions-in-powerapps"></a>PowerApps の Lower 関数、Upper 関数、Proper 関数
テキストの文字列中の文字をすべて大文字か小文字に変換します。または、テキストの文字列中の文字を適切なケースに変換します。

## <a name="description"></a>説明
**Lower** 関数、**Upper** 関数、**Proper** 関数は、文字列中の文字の大文字小文字を変換します。

* **Lower** は、すべての大文字を小文字にします。
* **Upper** は、すべての小文字を大文字にします。
* **Proper** は、各単語の最初の文字が小文字であれば大文字にします。また、その他の文字が大文字であれば小文字に変換します。

これら 3 つの関数では、アルファベットでない文字は無視されます。

文字列を 1 つ渡した場合、その文字列の変換されたバージョンが戻り値として返されます。  文字列が含まれた単一列[テーブル](../working-with-tables.md)を渡すと、変換された文字列の単一列テーブルが戻り値として返されます。 複数列テーブルがある場合は、[テーブルの使用](../working-with-tables.md)に関するページの説明に従って、そのテーブルを単一列テーブルにすることができます。

## <a name="syntax"></a>構文
**Lower**( *String* )<br>**Upper**( *String* )<br>**Proper**( *String* )

* *String* - 必須。 変換の対象となる文字列。

**Lower**( *SingleColumnTable* )<br>**Upper**( *SingleColumnTable* )<br>**Proper**( *SingleColumnTable* )

* *SingleColumnTable* - 必須。 変換対象となる文字列が含まれている単一列テーブル。

## <a name="examples"></a>例
### <a name="single-string"></a>単一の文字列
このセクションの例では、**Author** という名前のテキスト入力コントロールを[データ ソース](../working-with-data-sources.md)として使用します。 このコントロールには、文字列 "E. E. CummINGS" が含まれています。

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Lower(&nbsp;Author.Text&nbsp;)** |文字列中のすべての大文字を小文字にします。 |"e. e. cummings" |
| **Upper(&nbsp;Author.Text&nbsp;)** |文字列中のすべての小文字を大文字にします。 |"E. E. CUMMINGS" |
| **Proper(&nbsp;Author.Text&nbsp;)** |各単語の最初の文字が小文字であれば大文字にします。また、その他の大文字の文字を小文字に変換します。 |"E. E. Cummings" |

### <a name="single-column-table"></a>単一列テーブル
このセクションの例では、次のデータが含まれている **People** データ ソースの **Address** [列](../working-with-tables.md#columns)の文字列を変換します。

![](media/function-lower-upper-proper/people-table.png)

それぞれの数式は、変換済みの文字列が含まれた単一列テーブルを返します。

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Lower( ShowColumns(&nbsp;People,&nbsp;"Address"&nbsp;) )** |小文字の文字をすべて大文字に変換します。 |<style> img { max-width:none; } </style> ![](media/function-lower-upper-proper/people-table-lower.png) |
| **Upper( ShowColumns(&nbsp;People,&nbsp;"Address"&nbsp;) )** |小文字の文字をすべて大文字に変換します。 |![](media/function-lower-upper-proper/people-table-upper.png) |
| **Proper( ShowColumns(&nbsp;People,&nbsp;"Address"&nbsp;) )** |単語の先頭の文字が小文字であれば大文字に変換します。また、その他の文字が大文字であれば小文字に変換します。 |![](media/function-lower-upper-proper/people-table-proper.png) |

### <a name="step-by-step-example"></a>ステップバイステップの例
1. **[テキスト入力](../controls/control-text-input.md)** コントロールを追加し、 **Source** という名前を付けます。
2. ラベルを追加し、その **[Text](../controls/properties-core.md)** プロパティを次の関数に設定します。<br>**Proper(Source.Text)**
3. F5 キーを押し、**Source** ボックスに 「**WE ARE THE BEST!**」と入力します。<br>ラベルには **We Are The Best!** と表示されます。


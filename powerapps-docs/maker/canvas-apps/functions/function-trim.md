---
title: Trim および TrimEnds 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Trim および TrimEnds 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 09/09/2016
ms.author: gregli
ms.openlocfilehash: 30a35425fa9abdcaa4cc5300753c111c0fb1c8d2
ms.sourcegitcommit: dfa0e1a7981814e15e6ca4720e2a5f930e859db1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2018
ms.locfileid: "39015365"
---
# <a name="trim-and-trimends-functions-in-powerapps"></a>PowerApps の Trim および TrimEnds 関数
テキストの文字列から余分なスペースを削除します。

## <a name="description"></a>説明
**Trim** 関数は、単語間の 1 つのスペースを除く、すべてのスペースをテキストの文字列から削除します。  

**TrimEnds** 関数は、テキストの文字列の先頭と末尾からすべてのスペースを削除しますが、単語間のスペースはそのまま残します。

1 つのテキスト文字列を指定した場合、いずれの関数の戻り値も、余分なスペースが削除された文字列になります。 文字列を含む単一列[テーブル](../working-with-tables.md)を指定した場合、戻り値は、トリミングされた文字列の単一列テーブルになります。 複数列テーブルがある場合は、[テーブルの使用](../working-with-tables.md)に関するページの説明に従って、そのテーブルを単一列テーブルにすることができます。

単語間のスペースを削除することにより、**Trim** は、Microsoft Excel にある同じ名前の関数と変わらなくなります。 一方、**TrimEnds** は、各文字列の先頭と末尾からのみスペースを削除するプログラミング ツールと一致します。

## <a name="syntax"></a>構文
**Trim**( *String* )<br>**TrimEnds**( *String* )

* *String* - 必須。 スペースを削除するテキスト文字列。

**Trim**( *SingleColumnTable* )<br>**TrimEnds**( *SingleColumnTable* )

* *SingleColumnTable* - 必須。 スペースを削除する文字列の単一列テーブル。

## <a name="example"></a>例

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Trim(&nbsp;"&nbsp;&nbsp;&nbsp;Hello&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;World&nbsp;&nbsp;&nbsp;"&nbsp;)** |文字列の先頭と末尾にあるすべてのスペースと文字列内の余分なスペースを削除します。 |"Hello World" |
| **TrimEnds(&nbsp;"&nbsp;&nbsp;&nbsp;Hello&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;World&nbsp;&nbsp;&nbsp;"&nbsp;)** |文字列の先頭と末尾からすべてのスペースを削除します。 |"Hello&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;World" |

次の例では、次の文字列を含む **Spaces** という名前の単一列コレクションを使用します。

![](media/function-trim/input-strings.png)

このコレクションを作成するには、**[ボタン](../controls/control-button.md)** コントロールの **OnSelect** プロパティを次の数式に設定し、プレビュー モードを開始して、ボタンをクリックまたはタップします。
<br>**ClearCollect( Spaces, [ "&nbsp;&nbsp;&nbsp;Jane&nbsp;&nbsp;&nbsp;Doe&nbsp;&nbsp;&nbsp;", "&nbsp;&nbsp;&nbsp;&nbsp;Jack&nbsp;&nbsp;&nbsp;and&nbsp;&nbsp;&nbsp;Jill", "Already&nbsp;trimmed", "&nbsp;&nbsp;&nbsp;Venus,&nbsp;&nbsp;&nbsp;Earth,&nbsp;&nbsp;&nbsp;Mars&nbsp;&nbsp;", "Oil&nbsp;and&nbsp;Water&nbsp;&nbsp;&nbsp;" ] )**

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Trim(&nbsp;Spaces&nbsp;)** |**Spaces** コレクションの各文字列の先頭と末尾にあるすべてのスペースと各文字列内の余分なスペースを削除します。 |<style> img { max-width: none } </style> ![](media/function-trim/output-trim.png) |
| **TrimEnds(&nbsp;Spaces&nbsp;)** |**Spaces** コレクションの各文字列の先頭と末尾からすべてのスペースを削除します。 |<style> img { max-width: none } </style> ![](media/function-trim/output-trimends.png) |

> [!NOTE]
> **[ファイル]** メニューの **[コレクション]** をクリックまたはタップしてコレクションを表示した場合、余分なスペースは表示されません。 文字列の長さを確認するには、**[Len](function-len.md)** 関数を使用してください。


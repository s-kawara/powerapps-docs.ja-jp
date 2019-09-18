---
title: Split 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Split 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta anneta
ms.date: 09/14/2019
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: fd331d5dd8503b072785573dc9400b8e2b581cb3
ms.sourcegitcommit: 5899d37e38ed7111d5a9d9f3561449782702a5e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71038214"
---
# <a name="split-function-in-powerapps"></a>PowerApps の Split 関数
テキスト文字列を部分文字列のテーブルに分割します。

## <a name="description"></a>説明
**Split** 関数はテキスト文字列を部分文字列のテーブルに分割します。  コンマ区切りのリスト、間にスラッシュが使用されている日付、その他適切に定義された区切り記号が使用されている状況で分割を行う場合に **Split** を使用します。  

区切り記号文字列はテキスト文字列を分割するために使用します。  区切り記号は 0、1、またはテキスト文字列全体で整合するその他の文字になります。  長さ 0 または*空の*文字列を使用すると、すべての文字が 1 つずつ分割されます。  一致する区切り文字は、結果に返されません。  区切り記号の一致が見つからない場合、テキスト文字列全体が 1 つの結果として返されます。

文字列を区切り記号なしで再結合するには、 **[Concat](function-concatenate.md)** 関数を使用します。 
 
正規表現を使用して文字列を分割するには、 **[Matchall](function-ismatch.md)** 関数を使用します。

これらの例では、1つの区切り部分文字列を抽出するために、 **[最初](function-first-last.md)** と **[最後](function-first-last.md)** の関数で**Split**を使用する方法を示しています。  多くの場合、 **[Match](function-ismatch.md)** 関数は、正規表現に慣れている方にとってより簡潔で強力な選択肢です。

## <a name="syntax"></a>構文
**Split**( *Text*, *Separator* )

* *Text* - 必須。  分割するテキスト。
* *Separator* - 必須。  文字列の分割で使用する区切り記号。  0、1、またはそれ以上の文字を指定できます。

## <a name="examples"></a>使用例

### <a name="basic-usage"></a>基本的な使用方法

| [数式] | 説明 | 結果 |
| --- | --- | --- |
| `Split( "Apples, Oranges, Bananas", "," )` |コンマ区切り記号に基づき、それぞれの果物が分割されます。  分割はコンマに基づいて実行され、その後のスペースには基づきません。そのため、"&nbsp;Oranges" および "&nbsp;Bananas" のように前にスペースが入ります。 |<style> img { max-width: none; } </style> ![](media/function-split/fruit1.png) |
| `TrimEnds( Split( "Apples, Oranges, Bananas", "," ) )` |前の例と同じですが、この場合は **Split** により生成される単一の列テーブルに対して動作している [**TrimEnds** 関数](function-trim.md)によってスペースが削除されています。 コンマの後のスペースを含む区切り記号 **",&nbsp;"** も使用できますが、スペースがない場合やスペースが 2 つある場合には正しく動作しません。 |<style> img { max-width: none; } </style> ![](media/function-split/fruit2.png) |
| `Split( "08/28/17", "/" )` |区切り記号としてスラッシュを使用して、日付を分割します。 |<style> img { max-width: none; } </style> ![](media/function-split/date.png) |

### <a name="different-delimiters"></a>区切り記号が異なる

| [数式] | 説明 | 結果 |
| --- | --- | --- |
| `Split( "Hello, World", "," )` |区切り記号としてコンマを使用して、単語を分割します。  2 番目の結果には、前にスペースが含まれています。この結果がコンマの直後の文字であるためです。 |<style> img { max-width: none; } </style> ![](media/function-split/comma.png) |
| `Split( "Hello, World", "o" )` |文字 "o" を区切り記号として使用して、文字列を分割します。 |<style> img { max-width: none; } </style> ![](media/function-split/o.png) |
| `Split( "Hello, World", "l" )` |単一の文字 "l" を区切り記号として使用して、文字列を分割します。 **Hello** の 2 つの **l** の間には文字がないため、*空白の*値が返されています。 |<style> img { max-width: none; } </style> ![](media/function-split/l.png) |
| `Split( "Hello, World", "ll" )` |二重文字 "ll" を区切り記号として使用して、文字列を分割します。 |<style> img { max-width: none; } </style> ![](media/function-split/ll.png) |
| `Split( "Hello, World", "%" )` |パーセント記号を区切り記号として使用して、文字列を分割します。 この区切り記号は文字列に表示されないため、文字列全体が 1 つの結果として返されます。 |<style> img { max-width: none; } </style> ![](media/function-split/percent.png) |
| `Split( "Hello, World", "" )` |空の文字列 (ゼロ文字) を区切り記号として使用して、文字列を分割します。 これにより、文字列の各文字が分割されます。 |<style> img { max-width: none; } </style> ![](media/function-split/none.png) |

### <a name="substring-extraction"></a>部分文字列の抽出

| [数式] | 説明 | 結果 |
| --- | --- | --- |
| `First( Split( Last( Split( "Bob Jones <bob.jones@contoso.com>", "<" ) ).Result, ">" ) ).Result` | 開始区切り記号 (<) に基づいて文字列を分割し、**最後**の区切り記号の右側に文字列を抽出します。  次に、式は、終了区切り記号 (>) に基づいて結果を分割し、区切り記号の左側にある文字列を**右**に抽出します。 | "bob.jones@contoso.com" |
| `Match( "Bob Jones <bob.jones@contoso.com>", "<(?<email>.+)>" ).email` | は、最後の例と同じ区切り記号に基づく抽出を実行しますが、代わりに**Match**関数と正規表現を使用します。 | "bob.jones@contoso.com" |


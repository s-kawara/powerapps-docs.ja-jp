---
title: Split 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Split 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta anneta
ms.date: 08/28/2017
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: b8f8dc0d354dd17fedd16524fed0f358b70839d4
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61519430"
---
# <a name="split-function-in-powerapps"></a>PowerApps の Split 関数
テキスト文字列を部分文字列のテーブルに分割します。

## <a name="description"></a>説明
**Split** 関数はテキスト文字列を部分文字列のテーブルに分割します。  コンマ区切りのリスト、間にスラッシュが使用されている日付、その他適切に定義された区切り記号が使用されている状況で分割を行う場合に **Split** を使用します。  

区切り記号文字列はテキスト文字列を分割するために使用します。  区切り記号は 0、1、またはテキスト文字列全体で整合するその他の文字になります。  長さ 0 または*空の*文字列を使用すると、すべての文字が 1 つずつ分割されます。  一致する区切り文字は、結果に返されません。  区切り記号の一致が見つからない場合、テキスト文字列全体が 1 つの結果として返されます。

文字列 (区切り記号なし) を再結合するには、**[Concat](function-concatenate.md)** 関数を使用します。 使用して、 **[MatchAll](function-ismatch.md)** (場合によっては) で文字列を分割に使用できますが、正規表現を使用して、テキスト文字列の部分を抽出する関数。 

## <a name="syntax"></a>構文
**Split**( *Text*, *Separator* )

* *Text* - 必須。  分割するテキスト。
* *Separator* - 必須。  文字列の分割で使用する区切り記号。  0、1、またはそれ以上の文字を指定できます。

## <a name="examples"></a>例

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Split( "Apples,&nbsp;Oranges,&nbsp;Bananas", "," )** |コンマ区切り記号に基づき、それぞれの果物が分割されます。  分割はコンマに基づいて実行され、その後のスペースには基づきません。そのため、"&nbsp;Oranges" および "&nbsp;Bananas" のように前にスペースが入ります。 |<style> img { max-width: none; } </style> ![](media/function-split/fruit1.png) |
| **TrimEnds( Split( "Apples,&nbsp;Oranges,&nbsp;Bananas", "," ) )** |前の例と同じですが、この場合は **Split** により生成される単一の列テーブルに対して動作している [**TrimEnds** 関数](function-trim.md)によってスペースが削除されています。 コンマの後のスペースを含む区切り記号 **",&nbsp;"** も使用できますが、スペースがない場合やスペースが 2 つある場合には正しく動作しません。 |<style> img { max-width: none; } </style> ![](media/function-split/fruit2.png) |
| **Split( "08/28/17", "/" )** |区切り記号としてスラッシュを使用して、日付を分割します。 |<style> img { max-width: none; } </style> ![](media/function-split/date.png) |
| **Split( "Hello,&nbsp;World", "," )** |区切り記号としてコンマを使用して、単語を分割します。  2 番目の結果には、前にスペースが含まれています。この結果がコンマの直後の文字であるためです。 |<style> img { max-width: none; } </style> ![](media/function-split/comma.png) |
| **Split( "Hello,&nbsp;World", "o" )** |文字 "o" を区切り記号として使用して、文字列を分割します。 |<style> img { max-width: none; } </style> ![](media/function-split/o.png) |
| **Split( "Hello,&nbsp;World", "l" )** |単一の文字 "l" を区切り記号として使用して、文字列を分割します。 **Hello** の 2 つの **l** の間には文字がないため、*空白の*値が返されています。 |<style> img { max-width: none; } </style> ![](media/function-split/l.png) |
| **Split( "Hello,&nbsp;World", "ll" )** |二重文字 "ll" を区切り記号として使用して、文字列を分割します。 |<style> img { max-width: none; } </style> ![](media/function-split/ll.png) |
| **Split( "Hello,&nbsp;World", "%" )** |パーセント記号を区切り記号として使用して、文字列を分割します。 この区切り記号は文字列に表示されないため、文字列全体が 1 つの結果として返されます。 |<style> img { max-width: none; } </style> ![](media/function-split/percent.png) |
| **Split( "Hello,&nbsp;World", "" )** |空の文字列 (ゼロ文字) を区切り記号として使用して、文字列を分割します。 これにより、文字列の各文字が分割されます。 |<style> img { max-width: none; } </style> ![](media/function-split/none.png) |


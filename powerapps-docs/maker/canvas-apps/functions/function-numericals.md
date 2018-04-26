---
title: Abs、Exp、Ln、Power および Sqrt 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Abs、Sqrt およびその他の関数の参照情報
documentationcenter: na
author: gregli-msft
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: reference
ms.component: canvas
ms.date: 09/13/2016
ms.author: gregli
ms.openlocfilehash: 15d458142bc1077b1bf55ae6e358c826f813ecb2
ms.sourcegitcommit: 8bd4c700969d0fd42950581e03fd5ccbb5273584
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="abs-exp-ln-power-and-sqrt-functions-in-powerapps"></a>PowerApps の Abs、Exp、Ln、Power および Sqrt 関数
絶対値、自然対数、平方根、および *e* または任意の数の指定した累乗の結果を計算します。

## <a name="description"></a>説明
**Abs** 関数は引数の負以外の値を返します。 数値が負の場合は、**Abs** は対応する正の値を返します。

**Exp** 関数は *e* の引数の累乗を返します。  超越数 *e* は 2.7182818... です。

**Ln** 関数は引数の自然対数 (底 *e*) を返します。

**Power** 関数は数値の累乗を返します。  この関数は、[**^** 演算子](operators.md)を使用するのに相当します。

**Sqrt** 関数はそれ自体を乗じた場合に、引数と同じになる数値を返します。

1 つの数値を渡すと、呼び出される関数に基づいて、結果が戻り値として 1 つだけ返されます。  複数の数値を含んだ単一列[テーブル](../working-with-tables.md)を渡すと、戻り値は複数の結果を含んだ単一列テーブルとなり、引数のテーブル内のレコードごとに 1 つの結果が返されます。 複数列テーブルがある場合は、[テーブルの使用](../working-with-tables.md)に関するページの説明に従って、そのテーブルを単一列テーブルにすることができます。  

引数が、未定義の値となる場合は、結果は *空白*になります。  このことは、負の数値の平方根や対数などで発生する場合があります。

## <a name="syntax"></a>構文
**Abs**( *Number* )<br>**Exp**( *Number* )<br>**Ln**( *Number* )<br>**Sqrt**( *Number* )

* *Number* - 必須。 演算する数値。

**Power**( *Base*、*Exponent* )

* *Base* - 必須。 累乗する底の値。
* *Exponent* - 必須。 底の値を累乗する指数。

**Abs**( *SingleColumnTable* )<br>**Exp**( *SingleColumnTable* )<br>**Ln**( *SingleColumnTable* )<br>**Sqrt**( *SingleColumnTable* )

* *SingleColumnTable* - 必須。 演算する複数の数値を含む単一列テーブル。

## <a name="examples"></a>例
### <a name="single-number"></a>1 つの数値
| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Abs( -55 )** |負の符号のない数値を返します。 |55 |
| **Exp( 2 )** |*e* の 2 乗、つまり *e* \* *e* を返します。 |7.389056... |
| **Ln( 100 )** |数値 100 の自然対数 (底 *e*) を返します。 |4.605170... |
| **Power( 5, 3 )** |5 の 3 乗、つまり 5 \* 5 \* 5 を返します。 |125 |
| **Sqrt( 9 )** |それ自体を乗じた結果が 9 になる数値を返します。 |3 |

### <a name="single-column-table"></a>単一列テーブル
このセクションの例では、名前が **ValueTable** で、次のデータを含む[データ ソース](../working-with-data-sources.md)を使用します。

![](media/function-numericals/values.png)

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Abs(&nbsp;ValueTable&nbsp;)** |テーブル内の各数値の絶対値を返します。 |<style> img { max-width: none } </style> ![](media/function-numericals/values-abs.png) |
| **Exp(&nbsp;ValueTable&nbsp;)** |*e* をテーブル内の各数値で累乗した値を返します。 |<style> img { max-width: none } </style> ![](media/function-numericals/values-exp.png) |
| **Ln(&nbsp;ValueTable&nbsp;)** |テーブルの各数値の自然対数を返します。 |<style> img { max-width: none } </style> ![](media/function-numericals/values-ln.png) |
| **Sqrt(&nbsp;ValueTable&nbsp;)** |テーブルの各数値の平方根を返します。 |![](media/function-numericals/values-sqrt.png) |

### <a name="step-by-step-example"></a>ステップバイステップの例
1. **[テキスト入力](../controls/control-text-input.md)** コントロールを追加し、 **Source** という名前を付けます。
2. **ラベル** コントロールを追加し、その **[Text](../controls/properties-core.md)** プロパティを次の数式に設定します。
   <br>
   **Sqrt( Value( Source.Text ) )**
3. **Source** に数値を入力し、**ラベル** コントロールに、入力した数値の平方根が表示されることを確認します。


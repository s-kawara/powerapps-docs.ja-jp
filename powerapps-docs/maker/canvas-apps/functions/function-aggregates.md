---
title: Average、Max、Min、StdevP、Sum、および VarP 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Average、Max、Min、StdevP、Sum、および VarP 関数の参照情報
documentationcenter: na
author: gregli-msft
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: reference
ms.component: canvas
ms.date: 08/15/2017
ms.author: gregli
ms.openlocfilehash: e488383acbd163383079b5078e464cab89e677ad
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "31829050"
---
# <a name="average-max-min-stdevp-sum-and-varp-functions-in-powerapps"></a>PowerApps の Average、Max、Min、StdevP、Sum、および VarP 関数
一連の数値をまとめる集計関数。

## <a name="description"></a>説明
**Average** 関数は、引数の平均 (算術平均) を計算します。

**Max** 関数は、最大値を見つけます。

**Min** 関数は、最小値を見つけます。

**Sum** 関数は、引数の合計を計算します。

**StdevP** 関数は、引数の標準偏差を計算します。

**VarP** 関数は、引数の分散を計算します。

これらの関数には、次の形式で値を指定できます。

* 個々の引数。 たとえば、**Sum( 1, 2, 3 )** は 6 を返します。
* [テーブル](../working-with-tables.md)とそのテーブルを操作する数式。  各[レコード](../working-with-tables.md#records)について、数式の値の集計が計算されます。  

[!INCLUDE [record-scope](../../../includes/record-scope.md)]

これらの関数は数値のみに対して動作します。 文字列やレコードなど、他の種類の値は無視されます。 文字列を数値に変換するには、**[Value](function-value.md)** 関数を使用します。

**Average**、**Max**、**Min**、および **Sum** 関数が、[これらの関数の委任をサポートするデータ ソース](../delegation-list.md)に使用される場合は、関数を委任できます。  ただし、**StdevP** と **VarP** は、どのデータ ソースでも委任できません。  委任がサポートされていない場合、データの最初の部分だけが取得され、関数はローカルに適用されます。  結果は完全でない場合があります。  作成時に、この制限について通知し、可能であれば委任可能な代替関数への切り替えを提案する青い点が表示されます。 詳細については、[委任の概要](../delegation-overview.md)に関する記事を参照してください。

## <a name="syntax"></a>構文
**Average**( *NumericalFormula1*, [ *NumericalFormula2*, ... ] )<br>**Max**( *NumericalFormula1*, [ *NumericalFormula2*, ... ] )<br>**Min**( *NumericalFormula1*, [ *NumericalFormula2*, ... ] )<br>**Sum**( *NumericalFormula1*, [ *NumericalFormula2*, ... ] )<br>**StdevP**( *NumericalFormula1*, [ *NumericalFormula2*, ... ] )<br>**VarP**( *NumericalFormula1*, [ *NumericalFormula2*, ... ] )

* *NumericalFormula(s)* - 必須。  操作の対象となる数値。

**Average**( *Table*, *NumericalFormula* )<br>**Max**( *Table*, *NumericalFormula* )<br>**Min**( *Table*, *NumericalFormula* )<br>**Sum**( *Table*, *NumericalFormula* )<br>**StdevP**( *Table*, *NumericalFormula* )<br>**VarP**( *Table*, *NumericalFormula* )

* *Table* - 必須。  操作の対象となるテーブル。
* *NumericalFormula* - 必須。 各レコードについて評価する数式。 この数式の結果が集計に使用されます。 数式では、テーブルの列を使用できます。

## <a name="examples"></a>例
### <a name="step-by-step"></a>ステップ バイ ステップ
**Sales** という名前の[データ ソース](../working-with-data-sources.md)に **CostPerUnit** 列と **UnitsSold** 列が含まれており、ラベルの **[Text](../controls/properties-core.md)** プロパティを次の関数に設定するとします。<br>
**Sum(Sales, CostPerUnit * UnitsSold)**

ラベルには、各レコードのこれらの列の値を乗算し、すべてのレコードの結果を加算した合計売上が表示されます。<br>![販売数と単位からの合計売上の計算](./media/function-aggregates/total-sales.png)

別の例として、**Slider1**、**Slider2**、**Slider3** という名前のスライダーがあり、ラベルの **[Text](../controls/properties-core.md)** プロパティを次の数式に設定したとします。<br>
**Sum(Slider1.Value, Slider2.Value, Slider3.Value)**

ラベルには、スライダーで設定されたすべての値の合計が表示されます。


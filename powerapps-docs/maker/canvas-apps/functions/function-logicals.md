---
title: And 関数、Or 関数、Not 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の And 関数、Or 関数、Not 関数の参照情報
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
ms.openlocfilehash: a2e62ef2aa0a52bde33ea3e40faf96889597b09b
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "31825903"
---
# <a name="and-or-and-not-functions-in-powerapps"></a>PowerApps の And 関数、Or 関数、Not 関数
比較とテストの結果を操作するためによく使用される、ブール値の論理関数について説明します。

## <a name="description"></a>説明
**And** 関数は、すべての引数が **true** の場合に **true** を返します。  **&&**[ 演算子](operators.md)は、**And** と等価です。

**Or** 関数は、引数のいずれかが **true** の場合に **true** を返します。  **||** 演算子は、**Or** と等価です。

**Not** 関数は、引数が **false** の場合は **true** を、引数が **true** の場合は **false** を返します。  **!**  演算子は、**Not** と等価です。

これらの関数では論理値が扱われます。 数または文字列をこれらの関数に直接渡すことはできません。その代わり、比較かテストを実行する必要があります。 たとえば、**x > 1** などの比較は、**x** が **1** より大きい場合に評価がブール値 **true** になる論理式です。 **x** が **1** より小さい場合、式の評価は **false** になります。

## <a name="syntax"></a>構文
**And**( *LogicalFormula1*, *LogicalFormula2* [, *LogicalFormula3*, ... ] )<br>
**Or**( *LogicalFormula1*, *LogicalFormula2* [, *LogicalFormula3*, ... ] )<br>
**Not**( *LogicalFormula* )

* *LogicalFormula(s)* - 必須。  評価と処理の対象となる論理式。

## <a name="examples"></a>例
### <a name="step-by-step"></a>ステップ バイ ステップ
次の関数を使用して、スライダーの値が 50 から 100 までの範囲に含まれるかどうかを判定します。

**Or(Slider1.Value < 50, Slider1.Value> 100)**

**Dept** [列](../working-with-tables.md#columns)と **Salary** 列が[テーブル](../working-with-tables.md)に含まれていれば、**Result** 列で次の関数を使用して、**Dept** 列の値が **HR** であるか **Salary** 列の値が **200000** より大きいすべての行に **true** と表示できます。

**Or(Dept = HR, Salary >= 200000)**

別の方法では、|| 演算子を使用して、先ほどの数式が返すのと同じ結果を得ることができます。

**Slider1.Value < 50 || Slider1.Value> 100**

**Dept = "HR" || Salary > 200000**


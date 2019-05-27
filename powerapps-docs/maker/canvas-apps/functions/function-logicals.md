---
title: And 関数、Or 関数、Not 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の And 関数、Or 関数、Not 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 05/23/2019
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 4eb020d854549b6dc8878f07ae26390523a1bc03
ms.sourcegitcommit: aa9f78c304fe46922aecfe3b3fadb6bda72dfb23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66215978"
---
# <a name="and-or-and-not-functions-in-powerapps"></a>PowerApps の And 関数、Or 関数、Not 関数

比較とテストの結果を操作するためによく使用される、ブール値の論理関数について説明します。

## <a name="description"></a>説明

**And** 関数は、すべての引数が **true** の場合に **true** を返します。

**Or** 関数は、引数のいずれかが **true** の場合に **true** を返します。

**Not** 関数は、引数が **false** の場合は **true** を、引数が **true** の場合は **false** を返します。

Excel でのように、これらの関数機能は同じです。 使用することも[演算子](operators.md)Visual Basic または JavaScript の構文を使用して、これらの同じ操作を実行します。

| 関数の表記 | Visual Basic の演算子の表記 | JavaScript の演算子の表記 |
| -------------|------------|--------|
| **And( x, y )** | **x と y** | **x & & y** |
| **Or( x, y )** | **x または y** | **x &#124; &#124; y** |
| **Not( x )** | **X ではありません。** | **!x** |

これらの関数では論理値が扱われます。 渡すことはできませんに数値または文字列。代わりに、比較またはテストを行う必要があります。 たとえば、この論理式**x > 1**ブール値に評価される**true**場合**x**がより大きい**1**します。 場合**x**がより小さい**1**、数式に**false**します。

## <a name="syntax"></a>構文

**And**( *LogicalFormula1*, *LogicalFormula2* [, *LogicalFormula3*, ... ] )<br>
**Or**( *LogicalFormula1*, *LogicalFormula2* [, *LogicalFormula3*, ... ] )<br>
**Not**( *LogicalFormula* )

- *LogicalFormula(s)* - 必須。  評価と処理の対象となる論理式。

## <a name="examples"></a>例

このセクションの例では、これらのグローバル変数を使用します。

- **a** = *false*
- **b** = *は true。*
- **x** = 10
- **y** = 100
- **s** "Hello World"を =

アプリでこれらのグローバル変数を作成するには、挿入、 [**ボタン**](../controls/control-button.md)を制御して、設定、 **OnSelect**プロパティをこの式に。

```powerapps-dot
Set( a, false ); Set( b, true ); Set( x, 10 ); Set( y, 100 ); Set( s, "Hello World" )
```

(をクリックしている間に、Alt キーを押し)、ボタンを選択し、設定、**テキスト**のプロパティを[**ラベル**](../controls/control-text-box.md)次の表の最初の列の数式を制御します。

| 数式 | 説明 | 結果 |
|---------|-------------|--------|
| **And( a, b )** | 値をテスト**a**と**b**します。  引数の 1 つは*false*関数を返しますので、 *false*します。 | *false* |
| **And b** | Visual Basic の表記を使用して、前の例と同じです。 | *false* |
| **(& a) (& a) b** | JavaScript の表記を使用して、前の例と同じです。 | *false* |
| **Or( a, b )** | 値をテスト**a**と**b**します。 引数の 1 つは*true*関数を返しますので、 *true*します。 | *true* |
| **Or b** | Visual Basic の表記を使用して、前の例と同じです。 | *true* |
| **&#124; &#124; b** | JavaScript の表記を使用して、前の例と同じです。 | *true* |
| **しない (a)** | 値をテスト**a**します。 引数が*false*、反対の結果を返します。 | *true* |
| **ありません、** | Visual Basic の表記を使用して、前の例と同じです。 | *true* |
| **!を** | JavaScript の表記を使用して、前の例と同じです。 | *true* |
| **Len(&nbsp;s&nbsp;)&nbsp;<&nbsp;20 And&nbsp;Not&nbsp;IsBlank(&nbsp;s&nbsp;)** | テストするかどうかの長さ**s** 20 より小さいされていないかどうかと、**空白**値。 長さが 20 未満、および空白値ではありません。 そのため、結果は*true*します。 | *true* |
| **または (&nbsp;Len (&nbsp;s&nbsp;)&nbsp;<&nbsp;、10 倍&nbsp;<&nbsp;100、y&nbsp;<&nbsp;100&nbsp;)** | テストかどうかの長さ**s** 、10 未満をするかどうかは**x** 、100 よりも小さいかどうかおよび**y** 100 未満。 最初と 3 番目の引数が false の場合には、2 つ目は true。 したがって、関数が返されます*true*します。 | *true* |
| **Not IsBlank(&nbsp;s&nbsp;)** | テストするかどうか**s**は*空白*、返された*false*します。 **いない**返しますが、この結果の逆*true*します。 | *true* |
---
title: Rand 関数 | Microsoft Docs
description: 構文を含む PowerApps の Rand 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 06/09/2018
ms.author: gregli
ms.openlocfilehash: 4246ce5564886402c6d785a462cdc9dd93270c81
ms.sourcegitcommit: dfa0e1a7981814e15e6ca4720e2a5f930e859db1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2018
ms.locfileid: "39021322"
---
# <a name="rand-function-in-powerapps"></a>PowerApps の Rand 関数
疑似乱数を返します。

## <a name="description"></a>説明
**Rand** 関数は、0 以上 1 未満の疑似乱数を返します。

## <a name="volatile-functions"></a>揮発性関数
**Rand** は揮発性関数です。  揮発性関数は、評価されるたびに異なる値を返します。  

データ フロー式で使うと、揮発性関数は、それが出現する数式が再評価された場合にのみ、異なる値を返します。  数式で何も変更されていない場合、アプリの実行全体を通じて同じ値を返します。

たとえば、**Label1.Text = Rand()** であるラベル コントロールは、アプリがアクティブな間は変化しません。  アプリをいったん閉じて再び開いた場合にのみ、新しい値が返ります。

関数は、何かが変更された数式の一部である場合に再評価されます。  たとえば、**Label1.Text = Slider1.Value + Rand()** であるスライダー コントロールを含むように例を変更した場合、スライダー コントロールの値が変化するたびにラベルのテキスト プロパティが再評価されて、新しい乱数が生成されます。  この例については、以下を参照してください。

[動作の数式](../working-with-formulas-in-depth.md)で使うと、動作の数式が評価されるたびに、**Rand** が評価されます。  例については、以下を参照してください。

## <a name="syntax"></a>構文
**Rand**()

## <a name="examples"></a>例

#### <a name="display-a-different-random-number-as-user-input-changes"></a>ユーザーの入力が変わると、異なる乱数を表示します。
1. **[Slider](../controls/control-slider.md)** コントロールを追加し、別の名前になっている場合は **Slider1** に名前を変更します。

1. **[Label](../controls/control-text-box.md)** コントロールを追加し、その **Text** プロパティを次の数式に設定します。

    **Slider1.Value + Rand()**

    **50** (スライダーの既定値) にランダムな小数を加えた値が、ラベルに表示されます。

    ![ラベル コントロールに 50.741 が表示された画面](media/function-rand/rand-slider-1.png)

1. Alt キーを押しながら、スライダーの値を変更します。

    スライダーの値を変更するたびに、ラベルの小数部分に異なる乱数が表示されます。

    ![4 つの異なるスライダー設定に対して 4 つの異なるランダムな小数値がラベル コントロールに表示されている 4 つの画面 (70.899、84.667、90.134、99.690)](media/function-rand/rand-slider-results.png)

#### <a name="create-a-table-of-random-numbers"></a>乱数のテーブルを作成する
1. **[[ボタン]](../controls/control-button.md)** コントロールを追加し、**[OnSelect](../controls/properties-core.md)** プロパティに次の式を設定します。

    **ClearCollect( RandomNumbers, ForAll( [ 1, 2, 3, 4, 5 ], Rand() ))**

    この式は、5 回反復して 5 つの乱数を生成するために使用される単一列のテーブルを作成します。

1. **[データ テーブル](../controls/control-data-table.md)** を追加し、その **Items** プロパティを **RandomNumbers** に設定して、**Value** フィールドを表示します。

    ![5 つの異なる小数値 0.857、0.105、0.979、0.167、0.814 を含むデータ テーブルが表示されている画面](media/function-rand/set-show-data.png)

1. Alt キーを押しながら、クリックまたはタップしてボタンを選択します。

    データ テーブルに 5 つのランダムな小数値が表示されます。

    ![5 つの異なる小数値 0.857、0.105、0.979、0.167、0.814 を含むデータ テーブルが表示されている画面](media/function-rand/rand-collection-1.png)

1. もう一度ボタンを選択すると、別の乱数のリストが表示されます。

    ![新しい 5 つの異なる小数値 0.414、0.128、0.860、0.303、0.568 を含むデータ テーブルが表示されている同じ画面](media/function-rand/rand-collection-2.png)

テーブルではなく 1 つの乱数を生成するには、**Set( RandomNumber, Rand() )** を使用します。

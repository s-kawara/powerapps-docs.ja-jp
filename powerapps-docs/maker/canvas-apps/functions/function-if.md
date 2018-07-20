---
title: If および Switch 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の If 関数および Switch 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 04/24/2017
ms.author: gregli
ms.openlocfilehash: 5293cd448d96633e2d8d2cda9dfbd6d3c162c953
ms.sourcegitcommit: dfa0e1a7981814e15e6ca4720e2a5f930e859db1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2018
ms.locfileid: "39017389"
---
# <a name="if-and-switch-functions-in-powerapps"></a>PowerApps の If および Switch 関数
セット内の条件が true かどうか (**If**)、または数式の結果がセット内のいずれかの値に一致するかどうか (**Switch**) を判断し、結果を返すかアクションを実行します。

## <a name="description"></a>説明
**If** 関数は、**true** の結果が見つかるまで、1 つ以上の条件をテストします。 このような結果が見つかった場合は、対応する値が返されます。 このような結果が見つからない場合、既定値が返されます。 どちらの場合も、返される値は、表示する文字列、評価する対象の数式、または別の形式の結果になります。

**Switch** 関数は、数式を評価し、結果が指定したシーケンス内の値に一致するかどうかを判断します。 一致が見つかった場合は、対応する値が返されます。 一致が見つからない場合は、既定値が返されます。 どちらの場合も、返される値は、表示する文字列、評価する対象の数式、または別の形式の結果になります。

**If** と **Switch** はよく似ていますが、状況に合わせて適切な関数を使用する必要があります。

* 単一の条件を評価する場合は、**If** を使用します。 この関数の最も一般的な構文は、**If**( *Condition*, *ThenResult*, *DefaultResult* ) です。これは、他のプログラミング ツールで見られる一般的な "if …  then … else …" パターンを提供します。
* 関連性のない複数の条件を評価する場合は、**If** を使用します。 PowerApps では (Microsoft Excel とは異なり)、**If** の数式を入れ子にすることなく、複数の条件を指定できます。
* 可能な複数の一致を求めて単一の条件を評価する場合は、**Switch** を使用します。 この場合、**If** も使用できますが、可能なそれぞれの一致について数式を繰り返す必要があります。

これらの関数は両方とも、2 つ以上のアクション間で分岐するために、[動作の数式](../working-with-formulas-in-depth.md)で使用できます。 アクションをトリガーする分岐は 1 つだけです。 条件と一致が順番に評価され、条件が **true** になるか一致が見つかった時点で停止します。

どの条件も *true* にならなかった場合、一致が見つからなかった場合、既定の結果を指定しなかった場合は、"**空白**" が返されます。

## <a name="syntax"></a>構文
**If**( *Condition*, *ThenResult* [, *DefaultResult* ] )<br>**If**( *Condition1*, *ThenResult1* [, *Condition2*, *ThenResult2*, ... [ , *DefaultResult* ] ] )

* *Condition(s)* – 必須。 **true** かどうかをテストする数式。 このような数式には、通常、比較[演算子](operators.md) (**<**、**>**、**=** など) と、テスト関数 (**[IsBlank](function-isblank-isempty.md)**、**[IsEmpty](function-isblank-isempty.md)** など) が含まれています。
* *ThenResult(s)* - 必須。 **true** に評価される条件について返される、対応する値。
* *DefaultResult* - 省略可能。 **true** に評価される条件がない場合に返される値。  この引数を指定しない場合は、"*空白*" が返されます。

**Switch**( *Formula*, *Match1*, *Result1* [, *Match2*, *Result2*, ... [, *DefaultResult* ] ] )

* *Formula* - 必須。 一致について評価する数式。  この数式は、1 回だけ評価されます。
* *Match(s)* - 必須。 *Formula* の結果と比較する値。  完全一致が見つかった場合、対応する *Result* が返されます。
* *Result(s)* - 必須。 完全一致が見つかった場合に返される、対応する値。
* *DefaultResult* - 省略可能。 完全一致が見つからない場合は、この値が返されます。 この引数を指定しない場合は、"*空白*" が返されます。

## <a name="examples"></a>例
### <a name="values-in-formulas"></a>数式の値
次の例では、**Slider1** という名前の**スライダー** コントロールに **25** という値が設定されています。

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **If( Slider1.Value&nbsp;=&nbsp;25, "Result1" )** |条件は **true** であり、対応する結果が返されます。 |"Result1" |
| **If( Slider1.Value&nbsp;=&nbsp;25, "Result1", "Result2" )** |条件は **true** であり、対応する結果が返されます。 |"Result1" |
| **If( Slider1.Value&nbsp;>&nbsp;1000, "Result1" )** |条件は **false** であり、*DefaultResult* が指定されていません。 |"*空白*" |
| **If( Slider1.Value&nbsp;>&nbsp;1000, "Result1", "Result2" )** |条件は **false** であり、*DefaultResult* が指定されているため、それが返されます。 |"Result2" |
| **If( Slider1.Value&nbsp;=&nbsp;25, "Result1", Slider1.Value&nbsp;>&nbsp;0, "Result2" )** |1 つ目の条件が **true** であり、対応する結果が返されます。 2 番目の条件も **true** ですが、引数リストで **true** に評価される条件よりも後にあるため、評価されません。 |"Result1" |
| **If( IsBlank(&nbsp;Slider1.Value&nbsp;), "Result1", IsNumeric(&nbsp;Slider1.Value&nbsp;), "Result2" )** |スライダーが "**空白**" ではないため、1 つ目の条件は *false* です。 スライダーの値は数値であるため、2 つ目の条件は **true** になり、対応する結果が返されます。 |"Result2" |
| **If( Slider1.Value&nbsp;>&nbsp;1000, "Result1", Slider1.Value&nbsp;>&nbsp;50, "Result2", "Result3")** |1 つ目と 2 つ目の条件は両方とも **false** であり、*DefaultResult* が指定されているため、それが返されます。 |"Result3" |
| **Switch( Slider1.Value, 25, "Result1" )** |スライダーの値は、チェックする 1 つ目の値に一致し、対応する結果が返されます。 |"Result1" |
| **Switch( Slider1.Value, 20, "Result1", 25, "Result2", 30, "Result3" )** |スライダーの値は、チェックする 2 つ目の値に一致し、対応する結果が返されます。 |"Result2" |
| **Switch( Slider1.Value, 20, "Result1", 10, "Result2", 0, "Result3", "DefaultResult" )** |スライダーの値は、チェックするどの値とも一致しません。  *DefaultResult* が指定されているため、それが返されます。 |"DefaultResult" |

### <a name="branching-in-behavior-formulas"></a>動作の数式での分岐
次の例では、**FirstName** という名前の**[テキスト入力](../controls/control-text-input.md)** コントロールに値 "John" が入力されています。

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **If( !IsBlank( FirstName.Text ), Navigate(&nbsp;Screen1, ScreenTransition.None ) )** |条件は **true** であり、**[Navigate](function-navigate.md)** 関数が実行されます。 **[IsBlank](function-isblank-isempty.md)** 関数を使用して、必要なフォーム フィールドが入力済みかどうかをテストすることができます。  **FirstName** が "[空白](function-isblank-isempty.md)" だった場合、この数式には効果がありません。 |**true**<br><br>表示が **Screen1** に変更されます。 |
| **If( IsBlank( FirstName.Text ), Navigate(&nbsp;Screen1, ScreenTransition.None ), Back() )** |**!** 演算子がない場合、条件は **false** であり、**[Navigate](function-navigate.md)** 関数は実行されません。 **[Back](function-navigate.md)** 関数が *DefaultResult* として指定されているため、それが実行されます。 |**true**<br><br>表示は、前に表示されていた画面に戻ります。 |
| **Switch( FirstName.Text, "Carlos", Navigate(&nbsp;Screen1, ScreenTransition.None ), "Kirstin", Navigate( Screen2, ScreenTransition.None ), "John", Navigate( Screen3, ScreenTransition.None ) )** |**FirstName.Text** の値は "Carlos"、"Kirstin"、"John" と、この順に比較されます。 "John" との一致が見つかり、アプリは **Screen3** に移動します。 |**true**<br><br>表示が **Screen3** に変更されます。 |

### <a name="step-by-step"></a>ステップ バイ ステップ
1. **[テキスト入力](../controls/control-text-input.md)** コントロールを追加し、**Text1** という名前を付けます (既定でその名前が付いていない場合)。
2. **[Text1]** に「**30**」と入力します。
3. **ラベル** コントロールを追加し、その **[Text](../controls/properties-core.md)** プロパティを次の数式に設定します。<br>
   **If( Value(Text1.Text) < 20, "Order MANY more!", Value(Text1.Text) < 40, "Order more!", Text1.Text )**
   
    **ラベル** コントロールに "**Order more!**" と表示されます。 これは、**Text1** の値が 20 より大きく、40 より小さいためです。
4. **[Text1]** に「**15**」と入力します。
   
    **ラベル** コントロールに "**Order MANY more!**" と表示されます。 これは、**Text1** の値が 20 より小さいためです。
5. **[Text1]** に「**50**」と入力します。
   
    **ラベル** コントロールに入力した値が表示されます (値が 40 より大きいため)。


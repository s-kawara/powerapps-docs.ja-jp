---
title: IfError 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の IfError 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 03/21/2018
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 63a837eff2944569f5f66223690b11ddcfd399f6
ms.sourcegitcommit: aa9f78c304fe46922aecfe3b3fadb6bda72dfb23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66215927"
---
# <a name="iferror-function-in-powerapps"></a>PowerApps の IfError 関数

エラーを検出し、代替値を提供するか、操作を実行します。

## <a name="description"></a>説明

> [!NOTE]
> この関数は、試験的な機能の一部であり、変更される可能性があります。 このトピックで説明する動作が使用可能な場合にのみ、*数式レベル エラー管理*機能をオンにします。 このアプリ レベルの設定では既定で無効です。 この機能をオンにするには、開く、*ファイル*] タブで [*アプリ設定*選択し、左側のメニューで*試験的機能*。 お客様のフィードバックは弊社にとって非常に重要です。ご意見を [PowerApps コミュニティ フォーラム](https://powerusers.microsoft.com/t5/Expressions-and-Formulas/bd-p/How-To)にお寄せください。

**IfError**関数が、エラーの結果が見つかるまで、1 つまたは複数の値をテストします。 関数には、エラーが検出されると、対応する値が返されます。 それ以外の場合、関数は、既定値を返します。 どちらの場合、関数を評価する数式または別の形式の結果を表示する文字列を返す可能性があります。 **IfError**関数に似ています、**場合**関数。**IfError**エラーについては、テスト中に**場合**テスト**true**します。

使用**IfError**エラー値を有効な値に置き換えます。 たとえば、0 による除算がユーザー入力が発生する場合は、この関数を使用します。 0 またはダウン ストリームの計算が続行されるように、アプリに該当する別の値に結果を置換する数式を作成します。 数式は次の例と同じくらい簡単になります。

```powerapps-dot
IfError( 1/x, 0 )
```

場合の値**x**数式は、0 のない**1/x**します。 それ以外の場合、 **1/x**エラーが生成し、式は、代わりに 0 を返します。

使用**IfError**で[動作の数式](../working-with-formulas-in-depth.md)このパターンのように、追加のアクションを実行する前に、エラーのアクションとチェックを実行します。

```powerapps-dot
IfError(
    Patch( DS1, ... ), Notify( "problem in the first action" ),
    Patch( DS2, ... ), Notify( "problem in the second action" )
)
```

問題、最初に、最初の修正プログラムが発生したかどうか**通知**それ以上の処理の実行が発生し、2 つ目の修正プログラムは実行されません。 最初の更新プログラムが成功すると、2 つ目の更新プログラムを実行し、問題、2 番目に到達した場合**通知**を実行します。

式は、すべてのエラーが検出されないし、省略可能な指定したかどうか*DefaultResult*引数、引数に指定した数値を返します。 式は、すべてのエラーが検出されない、その引数を指定していない場合は、数式の最後の*値*引数が評価されます。

## <a name="syntax"></a>構文

**IfError**( *Value1*, *Fallback1* [, *Value2*, *Fallback2*, ... [, *DefaultResult* ] ] )

* *値*- 必須。 エラー値かどうかをテストする数式。
* *Fallback(s)* - 必須。 評価する数式と一致する場合に返す値*値*引数には、エラーが返されました。
* *DefaultResult* - 省略可能。  式は、すべてのエラーが検出されない場合を評価する数式。

## <a name="examples"></a>例

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **IfError( 1, 2 )** |最初の引数では、エラーはありません。 関数を確認するその他のエラーのないありの値を返す既定値はありません。 関数は、最後を返します*値*引数が評価されます。   | 1 |
| **IfError( 1/0, 2 )** | 最初の引数は、(0 による除算) が原因のエラー値を返します。 関数は、2 番目の引数を評価し、結果として返します。 | 2 |
| **IfError( 1/0, Notify( "There was an internal problem", NotificationType.Error ) )** | 最初の引数は、(0 による除算) が原因のエラー値を返します。 関数は、2 番目の引数を評価し、ユーザーにメッセージが表示されます。 **IfError** の戻り値が **Notify** の戻り値であり、**IfError** の最初の引数 (数字) と同じ型に強制されます。 | 1 |
| **IfError( 1, 2, 3, 4, 5 )** | 最初の引数は、関数は引数がフォールバック対応の評価されませんので、エラーはありません。 3 番目の引数、関数は引数がフォールバック対応の評価されませんので、いずれか、エラーはありません。 5 番目の引数は対応するフォールバックを持たない、既定の結果です。 関数は、数式にエラーが含まれていないために、その結果を返します。 | 5 |

### <a name="step-by-step"></a>ステップ バイ ステップ

1. **[テキスト入力](../controls/control-text-input.md)** コントロールを追加し、**TextInput1** という名前を付けます (既定でその名前が付いていない場合)。

2. **[ラベル](../controls/control-text-box.md)** コントロールを追加し、**Label1** という名前を付けます (既定でその名前が付いていない場合)。

3. **Label1** の**テキスト** プロパティの数式を次のように設定します。

    **IfError( Value( TextInput1.Text ), -1 )**

4. **TextInput1** に、「**1234**」と入力します。  

    これは、Value 関数で有効な入力であるため、Label1 に **[1234]** の値が表示されます。

5. **TextInput1** に、「**ToInfinity**」と入力します。

    これは、Value 関数で有効な入力でないため、Label1 に **[-1]** の値が表示されます。  IfError で Value 関数をラップしないと、エラー値が*空白*として扱われるため、ラベルに値が表示されません。 


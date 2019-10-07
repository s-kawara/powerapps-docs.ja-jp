---
title: IfError 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の IfError 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 03/21/2018
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 992ff4ccfae533908acac96efaa117a726198334
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "71984718"
---
# <a name="iferror-function-in-powerapps"></a>PowerApps の IfError 関数

エラーを検出し、代替値を提供するか、操作を実行します。

## <a name="description"></a>説明

> [!NOTE]
> この関数は、試験的な機能の一部であり、変更される可能性があります。 このトピックで説明する動作は、*数式レベルのエラー管理*機能が有効になっている場合にのみ使用できます。 このアプリレベルの設定は、既定ではオフになっています。 この機能を有効にするには、[*ファイル*] タブを開き、左側のメニューで [*アプリの設定*] を選択し、[試験的な*機能*] を選択します。 お客様のフィードバックは弊社にとって非常に重要です。ご意見を [PowerApps コミュニティ フォーラム](https://powerusers.microsoft.com/t5/Expressions-and-Formulas/bd-p/How-To)にお寄せください。

**IfError**関数は、エラー結果が見つかるまで1つ以上の値をテストします。 関数がエラーを検出した場合、関数は対応する値を返します。 それ以外の場合、関数は既定値を返します。 どちらの場合も、関数は、表示する文字列、評価する式、または別の形式の結果を返すことがあります。 **IfError**関数は、 **If**関数に似ています。が**true**をテストする場合、 **IfError** **は**エラーをテストします。

**IfError**を使用して、エラー値を有効な値に置き換えます。 たとえば、ユーザー入力によって0除算が発生する可能性がある場合は、この関数を使用します。 数式を作成して、結果をアプリに適した0または別の値に置き換えて、ダウンストリームの計算を続行できるようにします。 数式は、次の例のように単純にすることができます。

```powerapps-dot
IfError( 1/x, 0 )
```

**X**の値が0でない場合、この数式は**1/x**を返します。 それ以外の場合、 **1/x**はエラーを生成し、数式は代わりに0を返します。

[動作の数式](../working-with-formulas-in-depth.md)で**IfError**を使用してアクションを実行し、次のパターンのように、追加のアクションを実行する前にエラーをチェックします。

```powerapps-dot
IfError(
    Patch( DS1, ... ), Notify( "problem in the first action" ),
    Patch( DS2, ... ), Notify( "problem in the second action" )
)
```

最初の修正プログラムで問題が発生した場合、最初の**通知**が実行され、それ以降の処理は行われず、2つ目の修正プログラムは実行されません。 最初の修正プログラムが成功した場合、2番目の修正プログラムが実行され、問題が発生した場合は2番目の**通知**が実行されます。

数式によってエラーが検出されず、オプションの*Defaultresult*引数を指定した場合、数式はその引数に指定した値を返します。 数式でエラーが検出されず、その引数を指定していない場合、数式は最後に評価された*値*引数を返します。

## <a name="syntax"></a>構文

**IfError**( *Value1*, *Fallback1* [, *Value2*, *Fallback2*,...[, *Defaultresult* ]])

* *Value (s)* -必須。 エラー値かどうかをテストする数式。
* *Fallback(s)* - 必須。 評価する数式と、一致する*値*の引数によってエラーが返された場合に返される値。
* *DefaultResult* - 省略可能。  数式によってエラーが検出されなかった場合に評価する数式。

## <a name="examples"></a>例

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **IfError( 1, 2 )** |最初の引数がエラーではありません。 関数には、他にチェックするエラーはなく、既定の戻り値はありません。 関数は、評価された最後の*値*引数を返します。   | 1 |
| **IfError( 1/0, 2 )** | 最初の引数は、0による除算によりエラー値を返します。 関数は、2番目の引数を評価し、結果として返します。 | 2 |
| **IfError( 1/0, Notify( "There was an internal problem", NotificationType.Error ) )** | 最初の引数は、0による除算によりエラー値を返します。 関数は、2番目の引数を評価し、ユーザーにメッセージを表示します。 **IfError** の戻り値が **Notify** の戻り値であり、**IfError** の最初の引数 (数字) と同じ型に強制されます。 | 1 |
| **IfError (1, 2, 3, 4, 5)** | 最初の引数はエラーではないため、関数はその引数に対応するフォールバックを評価しません。 3番目の引数はエラーではないため、関数はその引数に対応するフォールバックを評価しません。 5番目の引数には対応するフォールバックがなく、既定の結果が返されます。 数式にエラーが含まれていないため、関数はその結果を返します。 | 5 |

### <a name="step-by-step"></a>ステップ バイ ステップ

1. **[テキスト入力](../controls/control-text-input.md)** コントロールを追加し、**TextInput1** という名前を付けます (既定でその名前が付いていない場合)。

2. **[ラベル](../controls/control-text-box.md)** コントロールを追加し、**Label1** という名前を付けます (既定でその名前が付いていない場合)。

3. **Label1** の**テキスト** プロパティの数式を次のように設定します。

    **IfError( Value( TextInput1.Text ), -1 )**

4. **TextInput1** に、「**1234**」と入力します。  

    これは、Value 関数で有効な入力であるため、Label1 に **[1234]** の値が表示されます。

5. **TextInput1** に、「**ToInfinity**」と入力します。

    これは、Value 関数で有効な入力でないため、Label1 に **[-1]** の値が表示されます。  IfError で Value 関数をラップしないと、エラー値が*空白*として扱われるため、ラベルに値が表示されません。 


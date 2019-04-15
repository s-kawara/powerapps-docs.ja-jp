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
ms.openlocfilehash: 1bf9f3cf075441dd3264b5a2f6533671d2e08654
ms.sourcegitcommit: 4db9c763455d141a7e1dd569a50c86bd9e50ebf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2019
ms.locfileid: "57802310"
---
# <a name="iferror-function-in-powerapps"></a>PowerApps の IfError 関数
エラーを検出し、代替値を提供するか、操作を実行します。

## <a name="description"></a>説明
> [!NOTE]
> この関数は、試験的な機能の一部であり、変更される可能性があります。  ここで説明されている動作は、*数式レベル エラー管理*機能がオンになっている場合にのみ使用できます。  これはアプリ レベルの設定で、既定ではオフになっています。  この機能をオンにするには、 *[ファイル]* タブの左側のメニューで *[App settings]\(アプリ設定)*、 *[試験的な機能]* の順に移動します。  お客様のフィードバックは弊社にとって非常に重要です。ご意見を [PowerApps コミュニティ フォーラム](https://powerusers.microsoft.com/t5/Expressions-and-Formulas/bd-p/How-To)にお寄せください。

**IfError** 関数はそのすべての引数に対してエラーの値がないかを順番にテストし、エラーではない値が見つかった時点で停止します。  エラーではない値が見つかった後の引数は無視され、評価されません。

エラーの値を有効な値に置き換えるには、**IfError** を使用します。  たとえば、ユーザー入力によって 0 による除算が発生する可能性がある場合は、後続の計算が続行されるように 0 またはアプリに適した有効な値に置き換えます。

[動作の数式](../working-with-formulas-in-depth.md)の **IfError** で、操作を実行し、結果にエラーがないかを確認し、必要に応じてさらに操作を行うか、[**Notify**](function-showerror.md) でユーザーにエラー メッセージを表示します。

**IfError** のすべての引数でエラーが発生する場合は、最後の引数の値が返されます (これがエラー値になります)。 

## <a name="syntax"></a>構文
**IfError**( *Value*, *Fallback1* [, *Fallback2*, ... ] )

* *Value* - 必須。 エラー値かどうかをテストする数式。 
* *Fallback(s)* - 必須。 評価する数式と、前の引数でエラーが返された場合に返される値。  *フォールバック*引数がエラーではない値が見つかった時点までの順序で評価されます。

## <a name="examples"></a>例

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **IfError( 1, 2 )** |最初の引数は、エラーではありません。  最初の引数が返され、後続の引数は評価されません。   | 1 |
| **IfError( 1/0, 2 )** | 最初の引数は、エラー値を返します (0 による除算のため)。  2 番目の引数が評価され、エラーではない値が発生します。この値が返されます。 | 2 | 
| **IfError( 1/0, Notify( "There was an internal problem", NotificationType.Error ) )** | 最初の引数は、エラー値を返します (0 による除算のため)。  2 番目の引数が評価され、ユーザーにメッセージが表示されます。  **IfError** の戻り値が **Notify** の戻り値であり、**IfError** の最初の引数 (数字) と同じ型に強制されます。 | 1 |
| **IfError( 1/0, 1/0, 2, 1/0, 3 )** | 最初の引数は、エラー値を返します (0 による除算のため)。  2 番目の引数が評価され、やはりエラー値が生じます (別の 0 による除算)。  3 番目の引数が評価され、エラー値は返されません。この値が返されます。  4 番目と 5 番目の引数は無視されます。  | 2 |

### <a name="step-by-step"></a>ステップ バイ ステップ

1. **[テキスト入力](../controls/control-text-input.md)** コントロールを追加し、**TextInput1** という名前を付けます (既定でその名前が付いていない場合)。

2. **[ラベル](../controls/control-text-box.md)** コントロールを追加し、**Label1** という名前を付けます (既定でその名前が付いていない場合)。

3. **Label1** の**テキスト** プロパティの数式を次のように設定します。

    **IfError( Value( TextInput1.Text ), -1 )**

4. **TextInput1** に、「**1234**」と入力します。  

    これは、Value 関数で有効な入力であるため、Label1 に **[1234]** の値が表示されます。

5. **TextInput1** に、「**ToInfinity**」と入力します。

    これは、Value 関数で有効な入力でないため、Label1 に **[-1]** の値が表示されます。  IfError で Value 関数をラップしないと、エラー値が*空白*として扱われるため、ラベルに値が表示されません。 


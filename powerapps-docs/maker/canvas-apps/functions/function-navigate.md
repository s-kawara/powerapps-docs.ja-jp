---
title: Back および Navigate 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Navigate および Back 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 05/16/2019
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 8f63321b128214d14cd2f4e521d7cc1b85c7b98f
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "71984500"
---
# <a name="back-and-navigate-functions-in-powerapps"></a>PowerApps の Back および Navigate 関数

表示する画面を変更します。

## <a name="overview"></a>概要

ほとんどのアプリには、複数の画面が含まれます。  **Back** および **Navigate** 関数を使用して、表示する画面を変更します。 たとえば、ユーザーがボタンを選択したときに別の画面を表示する場合は、**Navigate** 関数が含まれた数式に、ボタンの **[OnSelect](../controls/properties-core.md)** プロパティを設定します。 その数式では、**Fade** などのビジュアルの切り替えを指定することで、画面の切り替わり方を選択できます。  

**Back** および **Navigate** で変更できるのは、表示する画面のみです。 現在表示されていない画面は、バックグラウンドで引き続き動作します。 他の画面上のコントロールのプロパティを参照する数式を作成できます。 たとえば、ユーザーは、1つの画面でスライダーの値を変更し、その値を数式で使用する別の画面に移動して、新しい画面での動作にどのように影響するかを確認できます。 ユーザーは元の画面に戻り、スライダーの値が保持されていることを確認できます。

ユーザーが画面間を移動したとき、[コンテキスト変数](../working-with-variables.md#use-a-context-variable)も保持されます。 **Navigate** を使用して、数式で表示される画面に 1 つ以上のコンテキスト変数を設定できます。これは、画面外からコンテキスト変数を設定する唯一の方法です。 このアプローチにより、画面にパラメーターを渡すことができます。 他のプログラミング ツールを使用したことがあれば、このアプローチはプロシージャにパラメーターを渡す処理に似ています。

どちらの関数も、[動作の数式](../working-with-formulas-in-depth.md)内でのみ使用できます。

## <a name="navigate"></a>Navigate

最初の引数で、表示する画面の名前を指定します。  

 2 番目の引数で、前の画面がどのように新しい画面に変化するかを指定します。

| 切り替えの引数 | 説明 | デモ |
| --- | --- | --- |
| **ScreenTransition.Cover** |新しい画面は、現在の画面を覆うように、右から左に向かってスライドします。 | ![画面の切り替え効果のアニメーション](media/function-navigate/cover.gif) |
| **ScreenTransition。右に移動** |新しい画面が表示され、左から右へ移動して、現在の画面が表示されます。 | ![画面の切り替え効果の右アニメーション](media/function-navigate/coverright.gif) |
| **ScreenTransition.Fade** |現在の画面がフェードアウトして、新しい画面が表示されます。 | ![画面の切り替え効果のフェードアニメーション](media/function-navigate/fade.gif) |
| **Screentransition. なし**(既定値) |新しい画面が現在の画面にすばやく置き換わります。 | ![画面の切り替え効果なしアニメーション](media/function-navigate/none.gif) |
| **ScreenTransition.UnCover** | 現在の画面では、右から左に向かってスライドして、新しい画面が表示されます。 | ![画面の切り替え効果を表示するアニメーション](media/function-navigate/uncover.gif) |
| **ScreenTransition。右に移動** | 現在の画面では、左から右へ移動して新しい画面が表示されます。 | ![画面の切り替え効果の右へのアニメーションの表示](media/function-navigate/uncoverright.gif) |

**Navigate** を使用して、新しい画面のコンテキスト変数を作成または更新できます。 省略可能な 3 番目の引数として、コンテキスト変数の名前 ([列](../working-with-tables.md#columns)名として) とコンテキスト変数の新しい値を含む[レコード](../working-with-tables.md#records)を渡します。  このレコードは、 **[UpdateContext](function-updatecontext.md)** 関数で使用するレコードと同じです。

前の画面の **[OnHidden](../controls/control-screen.md)** プロパティまたは新しい画面の **[OnVisible](../controls/control-screen.md)** プロパティ、あるいはその両方を設定して、切り替え時の追加の変更を実施します。 **App.ActiveScreen** プロパティが更新され、変更が反映されます。

**Navigate**は通常は**true**を返しますが、エラーが発生した場合は**false**を返します。

## <a name="back"></a>Back

**Back**関数は、最後に表示された画面に戻ります。

**Navigate**呼び出しごとに、アプリは、表示された画面と切り替え効果を追跡します。 連続する**バック**コールを使用して、ユーザーがアプリを開始したときに表示された画面にすべての方法を返すことができます。

**Back**関数を実行すると、既定では逆遷移が使用されます。 たとえば、画面が左に移動したときに画面が表示**された**場合、 **Back** **を使用し**てを返します。  **フェード**と**None**は独自の逆です。 特定の遷移を強制**するに**は、省略可能な引数を渡します。

**Back**は通常は**true**を返しますが、ユーザーがアプリを起動してから別の画面に移動していない場合は**false**を返します。

## <a name="syntax"></a>構文

**戻る**([*遷移*])

* *Transition* -省略可能。 現在の画面と前の画面の間で使用するビジュアルの切り替え効果。 このトピックで既に説明した、この引数の有効な値の一覧を参照してください。 既定では、画面が戻る切り替え効果は、表示された切り替え効果の逆になります。

**Navigate**(*画面*[, *Transition* [, *UpdateContextRecord* ]])

* *Screen* - 必須。 表示する画面。
* *Transition* -省略可能。  現在の画面と次の画面の間で使用するビジュアルの切り替え。 このトピックで既に掲載した、この引数の有効な値の一覧を参照してください。 既定値は**None**です。
* *UpdateContextRecord* - 省略可能。  1 つ以上の列の名前と、その列ごとの値を含むレコード。 このレコードは、 **[UpdateContext](function-updatecontext.md)** 関数に渡されたときのように、新しい画面のコンテキスト変数を更新します。

## <a name="examples"></a>例

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **移動 (詳細)** |切り替えもコンテキスト変数の値の変更もせずに、**Details** 画面を表示します。 |**Details** 画面がすばやく表示されます。 |
| **Navigate( Details, ScreenTransition.Fade )** |**Details** 画面を **Fade** 切り替えで表示します。  コンテキスト変数の値は変更されません。 |現在の画面がフェードアウトし、**Details** 画面が表示されます。 |
| **Navigate( Details, ScreenTransition.Fade, {&nbsp;ID:&nbsp;12&nbsp;} )** |**Details** 画面を **Fade** 切り替えで表示し、コンテキスト変数 **ID** の値を **12** に更新します。 |現在の画面がフェードアウトし、**Details** 画面が表示され、画面上のコンテキスト変数 **ID** の値が **12** に設定されます。 |
| **Navigate( Details, ScreenTransition.Fade, {&nbsp;ID:&nbsp;12&nbsp;,&nbsp;Shade:&nbsp;Color.Red&nbsp;} )** |**Details** 画面を **Fade** 切り替えで表示します。 コンテキスト変数 **ID** の値を **12** に更新し、コンテキスト変数 **Shade** の値を **Color.Red** に更新します。 |現在の画面がフェードアウトし、**Details** 画面が表示されます。 **Details** 画面上のコンテキスト変数 **ID** が **12** に設定され、コンテキスト変数 **Shade** が **Color.Red** に設定されます。 **Details** 画面上のコントロールの **Fill** プロパティを **Shade** に設定した場合、そのコントロールは赤色で表示されます。 |
| **Back()** | 既定の戻り値の切り替えを使用して、前の画面を表示します。 | 現在の画面が表示された切り替え効果の逆の切り替えを通じて、前の画面を表示します。 |
| **戻る (ScreenTransition. カバー)** |  前の画面に**カバー**の切り替えを表示します。 | 現在の画面が表示された切り替え効果に関係なく、前の画面を**カバー**の切り替えによって表示します。 |

### <a name="step-by-step"></a>ステップバイステップ

1. 空のアプリを作成します。

1. 2番目の画面を追加します。

    アプリには、次の2つの空白の画面があります。**Screen1**と**Screen2**。

1. **Screen2**の**Fill**プロパティを `Gray` の値に設定します。

1. **Screen2**で、ボタンを追加し、 **[onselect](../controls/properties-core.md)** プロパティを次の数式に設定します。

    ```powerapps-dot
    Navigate( Screen1, ScreenTransition.Cover )
    ```

1. **Alt**キーを押しながら、ボタンを選択します。

    左側に表示される切り替え効果を使用して、白い背景で**Screen1**が表示されます。

1. **Screen1**で、ボタンを追加し、 **onselect**プロパティを次の数式に設定します。

    ```powerapps-dot
    Back()
    ```

1. **Alt**キーを押しながら、ボタンを選択します。

    2番目の画面には、右側に表示されているトランジション (**カバー**の逆) がグレーで表示されます。

1. 各画面のボタンを繰り返しクリックして、前後にバウンスします。

[その他の例](../add-screen-context-variables.md)

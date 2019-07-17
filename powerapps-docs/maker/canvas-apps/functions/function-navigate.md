---
title: Back および Navigate 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Navigate および Back 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 05/16/2019
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: e57cc541c753ff3f24f66a78c6e30d6e5683b41a
ms.sourcegitcommit: 57dfad065318263e162e949e26b5c2684ba0dccb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2019
ms.locfileid: "65828172"
---
# <a name="back-and-navigate-functions-in-powerapps"></a>PowerApps の Back および Navigate 関数

表示する画面を変更します。

## <a name="overview"></a>概要

ほとんどのアプリには、複数の画面が含まれます。  **Back** および **Navigate** 関数を使用して、表示する画面を変更します。 たとえば、ユーザーがボタンを選択したときに別の画面を表示する場合は、**Navigate** 関数が含まれた数式に、ボタンの **[OnSelect](../controls/properties-core.md)** プロパティを設定します。 その数式では、**Fade** などのビジュアルの切り替えを指定することで、画面の切り替わり方を選択できます。  

**Back** および **Navigate** で変更できるのは、表示する画面のみです。 現在表示されていない画面は、バックグラウンドで引き続き動作します。 その他の画面のコントロールのプロパティを参照する数式を作成できます。 たとえば、ユーザーことができます 1 つの画面上のスライダーの値を変更、数式では、その値を使用する別の画面に移動しますおよび新しい画面での動作の影響を確認します。 ユーザーは、元の画面に戻るし、スライダーがその値を保持することを確認します。

ユーザーが画面間を移動したとき、[コンテキスト変数](../working-with-variables.md#use-a-context-variable)も保持されます。 **Navigate** を使用して、数式で表示される画面に 1 つ以上のコンテキスト変数を設定できます。これは、画面外からコンテキスト変数を設定する唯一の方法です。 このアプローチにより、画面にパラメーターを渡すことができます。 他のプログラミング ツールを使用したことがあれば、このアプローチはプロシージャにパラメーターを渡す処理に似ています。

内でのみ、いずれの関数を使用することができます、[動作の数式](../working-with-formulas-in-depth.md)します。

## <a name="navigate"></a>Navigate

最初の引数で、表示する画面の名前を指定します。  

 2 番目の引数で、前の画面がどのように新しい画面に変化するかを指定します。

| 切り替えの引数 | 説明 | デモ |
| --- | --- | --- |
| **ScreenTransition.Cover** |新しい画面はスライドして表示、現在の画面をカバーする、左から右に移動します。 | ![画面遷移カバーのアニメーション](media/function-navigate/cover.gif) |
| **ScreenTransition.CoverRight** |移行のビューに新しい画面のスライドは左から右、現在の画面をカバーすることです。 | ![画面遷移カバーの適切なアニメーション](media/function-navigate/coverright.gif) |
| **ScreenTransition.Fade** |新しい画面を表示する現在の画面のフェードします。 | ![画面の遷移のフェード アニメーション](media/function-navigate/fade.gif) |
| **ScreenTransition.None** (既定) |迅速に、新しい画面には、現在の画面が置き換えられます。 | ![画面遷移 none アニメーション](media/function-navigate/none.gif) |
| **ScreenTransition.UnCover** | 現在の画面は、新しい画面を明らかにするため、左から右に移動してスライドします。 | ![画面遷移アニメーションを発見します。](media/function-navigate/uncover.gif) |
| **ScreenTransition.UnCoverRight** | 非表示、移動、現在の画面スライドは左から右を新しい画面を明らかにすることです。 | ![画面の切り替えが適切なアニメーションを発見します。](media/function-navigate/uncoverright.gif) |

**Navigate** を使用して、新しい画面のコンテキスト変数を作成または更新できます。 省略可能な 3 番目の引数として、コンテキスト変数の名前 ([列](../working-with-tables.md#columns)名として) とコンテキスト変数の新しい値を含む[レコード](../working-with-tables.md#records)を渡します。  このレコードは、 **[UpdateContext](function-updatecontext.md)** 関数で使用するレコードと同じです。

前の画面の **[OnHidden](../controls/control-screen.md)** プロパティまたは新しい画面の **[OnVisible](../controls/control-screen.md)** プロパティ、あるいはその両方を設定して、切り替え時の追加の変更を実施します。 **App.ActiveScreen** プロパティが更新され、変更が反映されます。

**移動**通常返す**true**が返されますが、 **false**エラーが発生した場合。

## <a name="back"></a>Back

**戻る**関数は、最近表示された画面に戻ります。

各**Navigate**呼び出し、表示された画面と、移行、アプリを追跡します。 連続するを使用する**戻る**呼び出し、ユーザーに表示されていたときに画面をアプリで開始します。

ときに、**戻る**関数が実行される、逆の遷移は、既定で使用されます。 画面に表示されていた場合など、 **CoverRight**遷移、**戻る**を使用して**スライドアウト**(左側には) を返します。  **フェード**と**None**は独自の逆です。 省略可能な引数を渡す**戻る**特定の遷移を強制的にします。

**戻る**通常返す**true**返しますが、 **false**ユーザーがアプリを起動してから別の画面に移動していない場合。

## <a name="syntax"></a>構文

**Back**( [ *Transition* ] )

* *遷移*- 省略可能。 現在の画面と、前の画面間を使用するビジュアルの切り替え。 このトピックの前に、この引数の有効な値の一覧を参照してください。 既定では、画面を返します、遷移は、表示される、切り替え効果の逆数です。

**Navigate**( *Screen* [, *Transition* [, *UpdateContextRecord* ] ] )

* *Screen* - 必須。 表示する画面。
* *遷移*- 省略可能。  現在の画面と次の画面の間で使用するビジュアルの切り替え。 このトピックで既に掲載した、この引数の有効な値の一覧を参照してください。 既定値は**None**します。
* *UpdateContextRecord* - 省略可能。  1 つ以上の列の名前と、その列ごとの値を含むレコード。 このレコードは、 **[UpdateContext](function-updatecontext.md)** 関数に渡されたときのように、新しい画面のコンテキスト変数を更新します。

## <a name="examples"></a>例

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **(詳細) を移動します。** |切り替えもコンテキスト変数の値の変更もせずに、**Details** 画面を表示します。 |**Details** 画面がすばやく表示されます。 |
| **Navigate( Details, ScreenTransition.Fade )** |**Details** 画面を **Fade** 切り替えで表示します。  コンテキスト変数の値は変更されません。 |現在の画面がフェードアウトし、**Details** 画面が表示されます。 |
| **Navigate( Details, ScreenTransition.Fade, {&nbsp;ID:&nbsp;12&nbsp;} )** |**Details** 画面を **Fade** 切り替えで表示し、コンテキスト変数 **ID** の値を **12** に更新します。 |現在の画面がフェードアウトし、**Details** 画面が表示され、画面上のコンテキスト変数 **ID** の値が **12** に設定されます。 |
| **Navigate( Details, ScreenTransition.Fade, {&nbsp;ID:&nbsp;12&nbsp;,&nbsp;Shade:&nbsp;Color.Red&nbsp;} )** |**Details** 画面を **Fade** 切り替えで表示します。 コンテキスト変数 **ID** の値を **12** に更新し、コンテキスト変数 **Shade** の値を **Color.Red** に更新します。 |現在の画面がフェードアウトし、**Details** 画面が表示されます。 **Details** 画面上のコンテキスト変数 **ID** が **12** に設定され、コンテキスト変数 **Shade** が **Color.Red** に設定されます。 **Details** 画面上のコントロールの **Fill** プロパティを **Shade** に設定した場合、そのコントロールは赤色で表示されます。 |
| **Back()** | 既定の戻り値の移行前の画面が表示されます。 | 現在の画面が表示されていた、遷移の逆の遷移を前の画面が表示されます。 |
| **Back( ScreenTransition.Cover )** |  前の画面が表示されます、**カバー**遷移します。 | 前の画面が表示されます、**カバー**により、現在の画面が表示された遷移に関係なく、移行します。 |

### <a name="step-by-step"></a>ステップバイステップ

1. 空のアプリを作成します。

1. 2 番目の画面を追加しています。

    アプリには、2 つの空の画面が含まれています。**Screen1**と**Screen2**します。

1. 設定、**入力**プロパティの**Screen2**値`Gray`します。

1. **Screen2**、ボタンを追加し、設定、その **[OnSelect](../controls/properties-core.md)** に次の式のプロパティ。

    ```powerapps-dot
    Navigate( Screen1, ScreenTransition.Cover )
    ```

1. 押しながら、 **Alt**キーで、ボタンを選択します。

    **Screen1**左側に対応する切り替えを白い背景が表示されます。

1. **Screen1**、ボタンを追加し、設定、その**OnSelect**に次の式のプロパティ。

    ```powerapps-dot
    Back()
    ```

1. 押しながら、 **Alt**キーで、ボタンを選択します。

    グレーの背景を右に明らかにする遷移を 2 番目の画面が表示されます (逆の**カバー**)。

1. あちこちに繰り返し、各画面にボタンを選択します。

[その他の例](../add-screen-context-variables.md)

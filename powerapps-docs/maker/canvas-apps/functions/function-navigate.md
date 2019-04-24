---
title: Back および Navigate 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Navigate および Back 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 11/08/2015
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: f0bd11881dc0999cada58f65d7ed8d7f9df68c5a
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61562786"
---
# <a name="back-and-navigate-functions-in-powerapps"></a>PowerApps の Back および Navigate 関数
表示する画面を変更します。

## <a name="overview"></a>概要
ほとんどのアプリには、複数の画面が含まれます。  **Back** および **Navigate** 関数を使用して、表示する画面を変更します。 たとえば、ユーザーがボタンを選択したときに別の画面を表示する場合は、**Navigate** 関数が含まれた数式に、ボタンの **[OnSelect](../controls/properties-core.md)** プロパティを設定します。 その数式では、**Fade** などのビジュアルの切り替えを指定することで、画面の切り替わり方を選択できます。  

**Back** および **Navigate** で変更できるのは、表示する画面のみです。 現在表示されていない画面は、バックグラウンドで引き続き動作します。 別の画面上のコントロールのプロパティを参照する数式を作成できます。 たとえば、いずれかの画面上のスライダーの値を変更した後、数式内でその値を使用する別の画面に移動し、この値が新しい画面にどのように影響するかを確認することができます。  その後、元の画面に戻り、スライダーの値が保持されていることを確認できます。

ユーザーが画面間を移動したとき、[コンテキスト変数](../working-with-variables.md#use-a-context-variable)も保持されます。 **Navigate** を使用して、数式で表示される画面に 1 つ以上のコンテキスト変数を設定できます。これは、画面外からコンテキスト変数を設定する唯一の方法です。 このアプローチにより、画面にパラメーターを渡すことができます。 他のプログラミング ツールを使用したことがあれば、このアプローチはプロシージャにパラメーターを渡す処理に似ています。

## <a name="description"></a>説明
### <a name="back"></a>Back
**Back** 関数では、最後に表示された画面が表示されます。 この関数では引数は指定しません。

### <a name="navigate"></a>Navigate
最初の引数で、表示する画面の名前を指定します。  

 2 番目の引数で、前の画面がどのように新しい画面に変化するかを指定します。

| 切り替えの引数 | 説明 |
| --- | --- |
| **ScreenTransition.Cover** |新しい画面が、現在の画面を覆うようにスライドしながら表示されます。 |
| **ScreenTransition.Fade** |前の画面がフェードアウトし、新しい画面が表示されます。 |
| **ScreenTransition.None** |前の画面が新しい画面にすばやく置き換わります。 |
| **ScreenTransition.UnCover** |前の画面がスライドしながら画面外に移動し、その下から新しい画面が現れます。 |

**Navigate** を使用して、新しい画面のコンテキスト変数を作成または更新できます。 省略可能な 3 番目の引数として、コンテキスト変数の名前 ([列](../working-with-tables.md#columns)名として) とコンテキスト変数の新しい値を含む[レコード](../working-with-tables.md#records)を渡します。  このレコードは、**[UpdateContext](function-updatecontext.md)** 関数で使用するレコードと同じです。

前の画面の **[OnHidden](../controls/control-screen.md)** プロパティまたは新しい画面の **[OnVisible](../controls/control-screen.md)** プロパティ、あるいはその両方を設定して、切り替え時の追加の変更を実施します。 **App.ActiveScreen** プロパティが更新され、変更が反映されます。

**Back** は通常は **true** を返しますが、ユーザーが最初の画面を表示していて前の画面が存在しない場合は、**false** を返します。  **Navigate** は通常は **true** を返しますが、いずれかの引数に問題がある場合は、**false** を返します。

これらの関数は、[動作の数式](../working-with-formulas-in-depth.md)内でのみ使用できます。

## <a name="syntax"></a>構文
**Back**()

**Navigate**( *Screen*, *Transition* [, *UpdateContextRecord* ] )

* *Screen* - 必須。 表示する画面。
* *Transition* - 必須。  現在の画面と次の画面の間で使用するビジュアルの切り替え。 このトピックで既に掲載した、この引数の有効な値の一覧を参照してください。
* *UpdateContextRecord* - 省略可能。  1 つ以上の列の名前と、その列ごとの値を含むレコード。 このレコードは、**[UpdateContext](function-updatecontext.md)** 関数に渡されたときのように、新しい画面のコンテキスト変数を更新します。

## <a name="examples"></a>例

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Navigate( Details, ScreenTransition.None )** |切り替えもコンテキスト変数の値の変更もせずに、**Details** 画面を表示します。 |**Details** 画面がすばやく表示されます。 |
| **Navigate( Details, ScreenTransition.Fade )** |**Details** 画面を **Fade** 切り替えで表示します。  コンテキスト変数の値は変更されません。 |現在の画面がフェードアウトし、**Details** 画面が表示されます。 |
| **Navigate( Details, ScreenTransition.Fade, {&nbsp;ID:&nbsp;12&nbsp;} )** |**Details** 画面を **Fade** 切り替えで表示し、コンテキスト変数 **ID** の値を **12** に更新します。 |現在の画面がフェードアウトし、**Details** 画面が表示され、画面上のコンテキスト変数 **ID** の値が **12** に設定されます。 |
| **Navigate( Details, ScreenTransition.Fade, {&nbsp;ID:&nbsp;12&nbsp;,&nbsp;Shade:&nbsp;Color.Red&nbsp;} )** |**Details** 画面を **Fade** 切り替えで表示します。 コンテキスト変数 **ID** の値を **12** に更新し、コンテキスト変数 **Shade** の値を **Color.Red** に更新します。 |現在の画面がフェードアウトし、**Details** 画面が表示されます。 **Details** 画面上のコンテキスト変数 **ID** が **12** に設定され、コンテキスト変数 **Shade** が **Color.Red** に設定されます。 **Details** 画面上のコントロールの **Fill** プロパティを **Shade** に設定した場合、そのコントロールは赤色で表示されます。 |

### <a name="step-by-step"></a>ステップバイステップ
1. 既定の画面に **DefaultScreen** という名前を付け、ラベルを追加します。そのラベルの **[Text](../controls/properties-core.md)** プロパティを設定して、**Default** と表示させます。
2. 画面を追加し、**AddlScreen** という名前を付けます。
3. **AddlScreen** にラベルを追加し、ラベルの **[Text](../controls/properties-core.md)** プロパティを設定して、**Addl** と表示させます。
4. **AddlScreen** にボタンを追加し、このボタンの **[OnSelect](../controls/properties-core.md)** プロパティを次の関数に設定します。<br>**Navigate(DefaultScreen, ScreenTransition.Fade)**
5. **AddlScreen** で F5 キーを押し、ボタンを選択します。<br>**DefaultScreen** が表示されます。

[その他の例](../add-screen-context-variables.md)


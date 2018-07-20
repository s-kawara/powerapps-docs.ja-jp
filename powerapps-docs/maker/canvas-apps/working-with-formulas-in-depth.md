---
title: 動作の数式について | Microsoft Docs
description: 動作の数式を操作するための参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 11/10/2015
ms.author: gregli
ms.openlocfilehash: 8ac9cfc2a949cf059d84b5338220e0366094e24b
ms.sourcegitcommit: dfa0e1a7981814e15e6ca4720e2a5f930e859db1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2018
ms.locfileid: "39015595"
---
# <a name="understand-behavior-formulas-in-powerapps"></a>PowerApps の動作の数式について

ほとんどの数式は、値を計算するために使用します。  Excel のスプレッドシートと同様に、値が変わると再計算が自動的に行われます。  たとえば、**[ラベル](controls/control-text-box.md)** コントロールの値が 0 未満の場合は値を赤で表示し、それ以外の場合は値を黒で表示することができます。 そのためには、そのコントロールの **[Color](controls/properties-color-border.md)** プロパティを次の数式に設定します。
<br>**If( Value(TextBox1.Text) >= 0, Color.Black, Color.Red )**

このコンテキストにおいて、ユーザーが**[ボタン](controls/control-button.md)** コントロールを選択したらどうなるでしょうか。  値は変更されていません。したがって、新しく計算するものはありません。 Excel には、**[ボタン](controls/control-button.md)** コントロールに相当するものがありません。  

**[ボタン](controls/control-button.md)** コントロールを選択することによって、ユーザーは、アプリの状態を変更する一連のアクションまたは動作を開始します。

* 表示される画面を変更する: **[Back](functions/function-navigate.md)** 関数と **[Navigate](functions/function-navigate.md)** 関数。
* [シグナル](functions/signals.md)を制御する: **[Enable](functions/function-enable-disable.md)** 関数と **[Disable](functions/function-enable-disable.md)** 関数。
* [データ ソース](working-with-data-sources.md)項目を更新または削除する: **[Refresh](functions/function-refresh.md)**、**[Update](functions/function-update-updateif.md)**、**[UpdateIf](functions/function-update-updateif.md)**、**[Patch](functions/function-patch.md)**、**[Remove](functions/function-remove-removeif.md)**、**[RemoveIf](functions/function-remove-removeif.md)** の各関数。
* [コンテキスト変数](working-with-variables.md#create-a-context-variable)を更新する: **[UpdateContext](functions/function-updatecontext.md)** 関数。
* [コレクション](working-with-data-sources.md#collections)内の項目を作成、更新、または削除する: **[Collect](functions/function-clear-collect-clearcollect.md)** 関数、**[Clear](functions/function-clear-collect-clearcollect.md)** 関数、**[ClearCollect](functions/function-clear-collect-clearcollect.md)** 関数。

これらの関数はアプリの状態を変更するため、自動的に再計算することはできません。 これらは、動作の数式と呼ばれる、**[OnSelect](controls/properties-core.md)**、**[OnVisible](controls/control-screen.md)**、**[OnHidden](controls/control-screen.md)**、およびその他の **On...** プロパティの数式で使用できます。

### <a name="more-than-one-action"></a>複数のアクション
実行するアクションのリストを作成するには、セミコロンを使用します。 たとえば、コンテキスト変数を更新して前の画面に戻るには、次のように指定します。

* **UpdateContext( { x: 1 } ); Back()**

アクションは、数式に出現する順序で実行されます。  現在の関数が完了しないと、その次の関数は開始されません。 エラーが発生した場合、後続の関数が開始されない場合があります。


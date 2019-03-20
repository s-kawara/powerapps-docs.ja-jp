---
title: キャンバス アプリの動作の数式について | Microsoft Docs
description: PowerApps でキャンバス アプリの状態を変更する、動作の数式の使用に関する参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 11/10/2015
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: d48559ee3a54cbb723621a0e36f09cb4a1d0fe3b
ms.sourcegitcommit: 825daacc9a812637815afc1ce6fad28f0cebd479
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/04/2019
ms.locfileid: "57803437"
---
# <a name="understand-behavior-formulas-for-canvas-apps-in-powerapps"></a>PowerApps でのキャンバス アプリの動作の数式について

ほとんどの数式は、値を計算するために使用します。  Excel のスプレッドシートと同様に、値が変わると再計算が自動的に行われます。  たとえば、**[ラベル](controls/control-text-box.md)** コントロールの値が 0 未満の場合は値を赤で表示し、それ以外の場合は値を黒で表示することができます。 そのためには、そのコントロールの **[Color](controls/properties-color-border.md)** プロパティを次の数式に設定します。

**If( Value(TextBox1.Text) >= 0, Color.Black, Color.Red )**

このコンテキストにおいて、ユーザーが**[ボタン](controls/control-button.md)** コントロールを選択したらどうなるでしょうか。  値は変更されていません。したがって、新しく計算するものはありません。 Excel には、**[ボタン](controls/control-button.md)** コントロールに相当するものがありません。  

**[ボタン](controls/control-button.md)** コントロールを選択することによって、ユーザーは、アプリの状態を変更する一連のアクションまたは動作を開始します。

* 表示される画面を変更します。**[戻る](functions/function-navigate.md)** と**[Navigate](functions/function-navigate.md)** 関数。
* コントロール、[信号](functions/signals.md):**[有効にする](functions/function-enable-disable.md)** と**[を無効にする](functions/function-enable-disable.md)** 関数。
* 更新、更新、または内の項目を削除する[データソース](working-with-data-sources.md):**[更新](functions/function-refresh.md)**、  **[Update](functions/function-update-updateif.md)**、  **[UpdateIf](functions/function-update-updateif.md)**、  **[修正プログラム](functions/function-patch.md)**、 **[削除](functions/function-remove-removeif.md)**、 **[RemoveIf](functions/function-remove-removeif.md)** 関数。
* 更新プログラム、[コンテキスト変数](working-with-variables.md#use-a-context-variable):**[UpdateContext](functions/function-updatecontext.md)** 関数。
* 作成、更新、または内の項目を削除する[コレクション](working-with-data-sources.md#collections):**[収集](functions/function-clear-collect-clearcollect.md)**、 **[クリア](functions/function-clear-collect-clearcollect.md)**、 **[ClearCollect](functions/function-clear-collect-clearcollect.md)** 関数。

これらの関数はアプリの状態を変更するため、自動的に再計算することはできません。 これらは、動作の数式と呼ばれる、**[OnSelect](controls/properties-core.md)**、**[OnVisible](controls/control-screen.md)**、**[OnHidden](controls/control-screen.md)**、およびその他の **On...** プロパティの数式で使用できます。

### <a name="more-than-one-action"></a>複数のアクション
実行するアクションのリストを作成するには、セミコロンを使用します。 たとえば、コンテキスト変数を更新して前の画面に戻るには、次のように指定します。

* **UpdateContext( { x:1 } ); Back()**

アクションは、数式に出現する順序で実行されます。  現在の関数が完了しないと、その次の関数は開始されません。 エラーが発生した場合、後続の関数が開始されない場合があります。


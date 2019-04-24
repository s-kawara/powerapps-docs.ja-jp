---
title: キャンバス アプリの変数について | Microsoft Docs
description: キャンバス アプリの状態、コンテキスト変数、およびコレクションを操作するための参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 02/28/2019
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 6f46dcdf300c91be9fbc2f39e6b2a5418a4b82de
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61559314"
---
# <a name="understand-canvas-app-variables-in-powerapps"></a>PowerApps のキャンバス アプリの変数について

Visual Basic や JavaScript などの別のプログラミング ツールを使用するかどうかを抱くこと。**変数の検索** PowerApps は若干異なり、別のアプローチが必要です。 キャンバス アプリをビルドするときに、変数の説明に進む、代わりにしてください。**Excel では何が実行しますか。**

他のツールでは、明示的に計算を実行し、その結果を変数に格納していたことでしょう。 ところが、PowerApps と Excel のどちらも、入力データが変更されると自動的に数式が再計算されます。そのため、通常は変数を作成したり更新したりする必要はありません。 可能な限りこの方法に従うことで、アプリをより簡単に作成、理解、維持することができます。

場合によっては、PowerApps で変数を使用する必要があります。これにより、[動作の数式](working-with-formulas-in-depth.md)を追加して Excel のモデルを拡張します。 これらの数式が実行されるのは、ユーザーがボタンを選択したときなどです。 動作の数式の中では、他の数式で使用する変数を設定すると便利なことがよくあります。

一般的には、変数の使用を避けてください。 ただし、変数を使わないと目的の動作が得られないこともあります。 変数は暗黙的に作成され、その値を設定する関数に表示されるときに型指定します。 

## <a name="translate-excel-into-powerapps"></a>Excel を PowerApps に変換する

### <a name="excel"></a>Excel

それでは、Excel のしくみを確認しましょう。 セルには、数値や文字列などの値、または他のセルの値に基づく数式を含めることができます。 ユーザーがセルに別の値を入力すると、新しい値に応じてすべての数式が自動的に再計算されます。 この動作を実現するためにプログラミングは必要ありません。

次の例では、セル**A3**数式に設定されている**A1 と A2**します。 場合**A1**または**A2**変更、 **A3**変更を反映するように自動的に再計算します。 コーディングには式自体の外部でこの動作は不要です。

![Excel での 2 つの数値の合計を再計算のアニメーション](media/working-with-variables/excel-recalc.gif)

Excel に変数がありません。 数式が含まれるセルの値は入力内容に基づいて変化しますが、数式の結果を記憶してそれをセルや他の場所に格納する方法はありません。 セルの値を変更すると、スプレッドシート全体が変更される可能性があり、それ以前に計算された値はすべて失われます。 Excel のユーザーは、セルをコピーして貼り付けることができますが、それはユーザーが手動で制御するものであり、数式では不可能です。

### <a name="powerapps"></a>PowerApps

PowerApps で作成したアプリの動作は、Excel と非常によく似ています。 セルを更新する代わりに、画面上の任意の場所にコントロールを追加し、数式で使用するために名前を付けることができます。

追加することで、アプリで Excel の動作をレプリケートするなど、 **[ラベル](controls/control-text-box.md)** という名前のコントロール**Label1**、および 2 つ **[テキスト入力](controls/control-text-input.md)** という名前のコントロール**TextInput1**と**TextInput2**します。 設定する場合、 **[テキスト](controls/properties-core.md)** プロパティの**Label1**に**textinput 1 + TextInput2**、任意の数値の合計は常に表示されます**TextInput1**と**TextInput2**自動的にします。

![PowerApps での 2 つの数値の合計を計算します。](media/working-with-variables/recalc1.png)

注意、 **Label1**コントロールを選択すると、表示、 **[テキスト](controls/properties-core.md)** 画面の上部にある数式バーで数式。 ここで、数式が **TextInput1 + TextInput2** となっていることがわかります。 Excel ブック内のセル間に依存関係が作成されるのと同様に、この数式によってこれらのコントロール間に依存関係が作成されます。  値を変更してみましょう**TextInput1**:

![PowerApps での 2 つの数値の合計を計算のアニメーション](media/working-with-variables/recalc2.gif)

数式を**Label1**が自動的に再計算される、新しい値を表示します。

PowerApps では、数式を使用して、コントロールのプライマリ値だけでなく、書式設定などのプロパティも決定できます。 次の例では、ラベルの **[Color](controls/properties-color-border.md)** プロパティに設定された数式により、負の値は自動的に赤で表示されます。 **[If](functions/function-if.md)** 関数は Excel と非常によく似ています。

`If( Value(Label1.Text) < 0, Red, Black )`

![条件付き書式のアニメーション](media/working-with-variables/recalc-color.gif)

数式は、さまざまなシナリオで利用できます。

* デバイスの GPS を使用した場合、**Location.Latitude** と **Location.Longitude** を使用する数式によって、マップ コントロールに現在の位置を表示できます。  移動すると、マップによって位置が自動的に追跡されます。
* 他のユーザーが[データ ソース](working-with-data-sources.md)を更新できます。  たとえば、チームの他のメンバーが SharePoint リスト内の項目を更新する場合があります。  データ ソースを更新すると、依存するすべての数式が自動的に再計算され、更新されたデータが反映されます。 この例をさらに進めて、ギャラリーの **[Items](controls/properties-core.md)** プロパティを数式 **Filter( SharePointList )** に設定すると、新しくフィルター処理された[レコード](working-with-tables.md#records) セットが自動的に表示されます。

### <a name="benefits"></a>利点

数式をしたアプリの作成には多くの利点があります。

* Excel を知っていれば PowerApps もわかります。 モデルと数式の言語は同じです。
* 他のプログラミング ツールを使用したことがある場合は、これらの例を実現するためにどれだけの量のコードが必要になるかを考えてみてください。  Visual Basic では、各テキスト入力コントロールの変更イベント用にイベント ハンドラーを記述する必要があります。  このそれぞれで計算を実行するコードは冗長であり、不一致が生じる可能性があります。また、共通のサブルーチンを記述することが必要になる場合もあります。  PowerApps では、1 行の数式 1 つでこのすべての処理を実現しました。
* 場所を理解する**Label1**のテキストがから、検索場所を正確にわかって: 数式に含まれる、 **[テキスト](controls/properties-core.md)** プロパティ。  ほかに、このコントロールのテキストを変更する方法はありません。  従来のプログラミング ツールでは、プログラムのどこからでも、任意のイベント ハンドラーまたはサブルーチンでラベルの値を変更できました。  これにより、変数がいつどこで変更されたかを追跡するのが難しくなります。
* ユーザーは、スライダー コントロールを変更した後に考えを変えた場合、スライダーを元の値に戻すことができます。  アプリでは以前と変わらず同じコントロールが表示されるため、まるで何も変わっていないかのように見えます。  "what if" を試したり要求したりした場合でも、Excel の場合と同様、派生的な問題は発生しません。  

一般的に、数式を使用して効果を得ることができれば楽になります。 PowerApps の数式エンジンをうまく利用しましょう。  

## <a name="know-when-to-use-variables"></a>変数を使用するタイミングを把握する

単純な加算器に変更を加えて、累計機能を備えた昔ながらの計算機のように動作するようにしましょう。 **[Add]** ボタンを選択すると、数値が累計に加算されます。 **[Clear]** ボタンを選択すると、累計が 0 にリセットされます。

| 表示 | 説明 |
|----|----|
| <style> img {幅の最大値: none} </style> ![テキストを使用してアプリの入力コントロール、ラベル、および 2 つのボタン](media/working-with-variables/button-changes-state-1.png) | アプリの起動時に実行中の合計は 0 です。<br><br>赤色のドットは、ユーザーが入力したテキスト入力ボックスで、ユーザーの指を表す**77**します。 |
| ![テキスト入力コントロールには、77 が含まれているし、[追加] ボタンが押されました。](media/working-with-variables/button-changes-state-2.png) | ユーザーが選択、**追加**ボタンをクリックします。 |
| ![合計は 77、およびそれに追加されるもう 1 つの 77](media/working-with-variables/button-changes-state-3.png) | 実行中の合計に 77 が追加されます。<br><br>ユーザーが選択、**追加**もう一度ボタンをクリックします。 |
| ![合計値は 154 前に、クリアされます。](media/working-with-variables/button-changes-state-4.png) | 77 は 154 でその結果、実行中の合計に再度追加されます。<br><br>ユーザーが選択、**クリア**ボタンをクリックします。 |
| ![合計がクリアされます。](media/working-with-variables/button-changes-state-5.png) | 実行中の合計が 0 にリセットされます。 |

ここで作成する計算機では、Excel に存在しない機能、つまりボタンを使用しています。 このアプリでは、数式だけを使用して累計を計算することはできません。なぜなら、値はユーザーが行う一連の操作によって異なるからです。 代わりに、累計を手動で記録して更新する必要があります。 ほとんどのプログラミング ツールでは、この情報を "*変数*" に格納します。

場合によっては、アプリが目的の動作を行うために変数が必要になります。  ただし、このアプローチには注意が必要です。

* 累計を手動で更新する必要があります。 この処理は自動再計算では実行されません。
* 累計は、他のコントロールの値に基づいて計算できません。 累計は、ユーザーが **[Add]** ボタンを選択した回数と、選択したときにテキスト入力コントロールに格納されていた値に基づきます。 ユーザーが 77 を入力した後で **[Add]** を 2 回選択したのか、加算する値に 24 と 130 を指定したのか、 合計が 154 になった後でその違いを見分けることはできません。
* 合計に対する変更は、異なる経路から生じている可能性があります。 この例では、**[Add]** ボタンでも **[Clear]** ボタンでも合計を更新できます。 アプリが期待どおりに動作しない場合、どちらかのボタンに問題の原因があるのでしょうか。

## <a name="use-a-global-variable"></a>グローバル変数を使用します。

計算機を作成するには、累計を保持する変数が必要です。 PowerApps で使用できる最も単純な変数は、*グローバル変数*です。  

グローバル変数は次のように機能します。

* **[Set](functions/function-set.md)** 関数を使用して、グローバル変数の値を設定します。  **Set( MyVar, 1 )** とすることで、グローバル変数 **MyVar** の値を **1** に設定します。
* **Set** 関数とともに使用した名前を参照すると、グローバル変数を使用できます。  この場合、**MyVar** は **1** を返します。
* グローバル変数は、文字列、数値、レコード、[テーブル](working-with-tables.md)など、すべての値を保持できます。

それでは、グローバル変数を使用して計算機を作り直してみましょう。

1. **TextInput1** という名前のテキスト入力コントロールと、**Button1** および **Button2** という名前の 2 つのボタンを追加します。

2. **Button1** の **[Text](controls/properties-core.md)** プロパティを **"Add"** に設定し、**Button2** の **Text** プロパティを **"Clear"** に設定します。

3. ユーザーが **[Add]** ボタンを選択するたびに累計を更新するために、**[OnSelect](controls/properties-core.md)** プロパティを次の数式に設定します。

    **Set( RunningTotal, RunningTotal + TextInput1 )**

    この数式の単なるが存在する確立**RunningTotal**のための数を保持するグローバル変数として、 **+** 演算子。 参照できる**RunningTotal**アプリで任意の場所。 ユーザーがこのアプリを開くたびに**RunningTotal**の最初の値を持つ*空白*します。

    最初に、ユーザーが選択した、**追加**ボタンと **[設定](functions/function-set.md)** 実行**RunningTotal**値に設定されている**RunningTotal + TextInput1**します。

    ![関数の設定を追加 ボタンの OnSelect プロパティを設定します。](media/working-with-variables/global-variable-1.png)

4. ユーザーが **[Clear]** ボタンを選択するたびに累計を **0** に設定するために、**[OnSelect](controls/properties-core.md)** プロパティを次の数式に設定します。

    **Set( RunningTotal, 0 )**

    ![関数の設定をクリア ボタンの OnSelect プロパティを設定します。](media/working-with-variables/global-variable-2.png)

5. **[ラベル](controls/control-text-box.md)** コントロールを追加し、**[Text](controls/properties-core.md)** プロパティを **RunningTotal** に設定します。

    この数式は自動的に再計算され、ユーザーが選択したボタンに基づいて変更される **RunningTotal** の値が表示されます。

    ![ラベルのテキストのプロパティは、変数の名前に設定します。](media/working-with-variables/global-variable-3.png)

6. アプリをプレビューします。前述のように計算機が完成しました。 テキスト ボックスに数値を入力して **[追加]** ボタンを数回クリックします。 準備ができたら、Esc キーを押して作成環境に戻ります。

    ![テキスト入力コントロールには、値が含まれていて、ラベルには、実行中の合計が含まれています。](media/working-with-variables/global-variable-4.png)

7. グローバル変数の値を表示するには、選択、**ファイル**メニューを選択し、**変数**左側のウィンドウ。

    ![[ファイル] メニュー オプションを変数](media/working-with-variables/global-variable-file-1.png)

8. すべての場所を変数の定義し、使用の場所を表示するを選択します。

    ![変数が使用されている場所の一覧](media/working-with-variables/global-variable-file-2.png)

## <a name="types-of-variables"></a>変数の種類

PowerApps では、3 種類の変数があります。

| 変数の種類 | 適用範囲 | 説明 | 確立関数 |
| --- | --- | --- | --- |
| グローバル変数 |App |使い方が最も単純です。 数値、テキスト文字列、ブール値、レコード、テーブルなどを保持し、アプリ内のどこからでも参照できます。 |[**Set**](functions/function-set.md) |
| コンテキスト変数 |画面 |他の言語のプロシージャにパラメーターを渡す場合など、画面に値を渡すのに最適です。 1 つの画面から参照できます。 |[**UpdateContext**](functions/function-updatecontext.md)<br>[**Navigate**](functions/function-navigate.md) |
| コレクション |App |アプリで任意の場所から参照できるテーブルを保持します。 全体として設定するのではなく、テーブルのコンテンツごとに変更できます。 後で使用するためにローカル デバイスに保存できます。 |[**Collect**](functions/function-clear-collect-clearcollect.md)<br>[**ClearCollect**](functions/function-clear-collect-clearcollect.md) |

## <a name="create-and-remove-variables"></a>作成し、変数の削除

表示されるときに、すべての変数は暗黙的に作成、**設定**、 **UpdateContext**、 **Navigate**、**収集**、または**ClearCollect**関数。 変数とその型を宣言するには、必要がありますのみこれらの関数のいずれかで任意の場所に含めるアプリ。 変数を作成これらの関数の [なし]値を持つ変数を入力するだけです。 決して変数を宣言する明示的に別のプログラミング ツールの可能性があり、使用法から暗黙的にすべてを入力します。

たとえば、ボタン コントロールがある、 **OnSelect**式と等しく**セット (X, 1)** します。 次の数式を確立**X**数の型の変数として。 使用することができます**X**数値、およびその変数の数式での値を持つ*空白*アプリを開いた後、ボタンを選択する前にします。 ボタンを選択するときに付与**X**の値**1**します。

別に追加した場合はボタンをクリックし、設定、 **OnSelect**プロパティを**セット (X,「こんにちは」)**、型 (文字列) は、前の型に一致しないため、エラーが発生**設定**(数)。 型変数のすべての暗黙的な定義が一致する必要があります。 先ほど言われたため、これはすべて発生した、もう一度**X**数式では、これらの数式のいずれかが実際に実行しないためです。

すべてを削除することで、変数を削除する、**設定**、 **UpdateContext**、 **Navigate**、**収集**、または**ClearCollect**変数を暗黙的に確立する関数。 これらの関数はなく、変数が存在しません。 エラーが発生するためにも、変数への参照を削除する必要があります。

## <a name="variable-lifetime-and-initial-value"></a>変数の有効期間と初期値

すべての変数は、アプリの実行中にメモリに保持されます。 アプリを閉じた後、変数が保持されている値は失われます。

使用してデータ ソースで変数の内容を保存することができます、**パッチ**または**収集**関数。 使用して、ローカル デバイス上のコレクションに値を格納することも、 [ **SaveData** ](functions/function-savedata-loaddata.md)関数。

すべての変数に、初期値がある、ユーザーがアプリを開くときに*空白*します。

## <a name="reading-variables"></a>変数を読み取る

値を読み取るには、変数の名前を使用します。 たとえば、次の数式の変数を定義できます。

`Set( Radius, 12 )`

使用すると、 **Radius**任意の場所を数値を使用することができますに置き換えられます**12**:

`Pi() * Power( Radius, 2 )`

コンテキスト変数に、グローバル変数またはコレクションと同じ名前を付ける場合は、コンテキスト変数が優先されます。 ただし、引き続き参照できます、グローバル変数またはコレクションを使用する場合、[曖昧性除去演算子](functions/operators.md#disambiguation-operator) **@[Radius]** します。

## <a name="use-a-context-variable"></a>コンテキスト変数を使用します。

グローバル変数の代わりにコンテキスト変数を使用した計算機の作成方法を説明します。

コンテキスト変数のしくみは次のとおりです。

* 暗黙的に確立し、使用して、コンテキスト変数を設定する、、 **[UpdateContext](functions/function-updatecontext.md)** または **[Navigate](functions/function-navigate.md)** 関数。 すべてのコンテキスト変数の初期値は、アプリの起動時、*空白*します。
* レコードには、コンテキスト変数を更新します。 他のプログラミング ツールでは、一般的に、"x = 1" のように、代入には "=" を使用します。 コンテキストの変数を使用して **{x:1}** 代わりにします。 コンテキスト変数を使用する場合は、レコード構文を使用しないで直接には、その名前を使用します。
* 使用すると、コンテキスト変数を設定することも、 **[Navigate](functions/function-navigate.md)** の画面を表示する関数。 プロシージャまたはサブルーチン、このアプローチの一種として画面の思われる場合は、他のプログラミング ツールに渡すパラメーターに似ています。
* **[Navigate](functions/function-navigate.md)** を除き、コンテキスト変数は、名前を取得する場所である単一の画面のコンテキストに制限されます。 このコンテキスト以外でコンテキスト変数を使用または設定することはできません。
* コンテキスト変数では、文字列、数値、レコード、[テーブル](working-with-tables.md)など、任意の値を保持できます。

それでは、コンテキスト変数を使用して計算機を作り直してみましょう。

1. **TextInput1** という名前のテキスト入力コントロールと、**Button1** および **Button2** という名前の 2 つのボタンを追加します。

2. **Button1** の **[Text](controls/properties-core.md)** プロパティを **"Add"** に設定し、**Button2** の **Text** プロパティを **"Clear"** に設定します。

3. ユーザーが **[Add]** ボタンを選択するたびに累計を更新するために、**[OnSelect](controls/properties-core.md)** プロパティを次の数式に設定します。

    **UpdateContext ({RunningTotal:RunningTotal + TextInput1 } )**

    この数式の単なるが存在する確立**RunningTotal**のための数を保持するコンテキスト変数として、 **+** 演算子。 参照できる**RunningTotal**この画面で任意の場所。 ユーザーがこのアプリを開くたびに**RunningTotal**の最初の値を持つ*空白*します。

    最初に、ユーザーが選択した、**追加**ボタンと **[UpdateContext](functions/function-updatecontext.md)** 実行**RunningTotal** 値に設定されている**RunningTotal + TextInput1**します。

    ![[追加] ボタンの OnSelect プロパティ](media/working-with-variables/context-variable-1.png)

4. ユーザーが **[Clear]** ボタンを選択するたびに累計を **0** に設定するために、**[OnSelect](controls/properties-core.md)** プロパティを次の数式に設定します。

    **UpdateContext ({RunningTotal:0 } )**

    ここでも、 **[UpdateContext](functions/function-updatecontext.md)** 数式で使用**UpdateContext ({RunningTotal:0 } )**.

    ![クリア ボタンの OnSelect プロパティ](media/working-with-variables/context-variable-2.png)

5. **[ラベル](controls/control-text-box.md)** コントロールを追加し、**[Text](controls/properties-core.md)** プロパティを **RunningTotal** に設定します。

    この数式は自動的に再計算され、ユーザーが選択したボタンに基づいて変更される **RunningTotal** の値が表示されます。

    ![ラベルのテキスト プロパティ](media/working-with-variables/context-variable-3.png)

6. アプリをプレビューします。前述のように計算機が完成しました。 テキスト ボックスに数値を入力して **[追加]** ボタンを数回クリックします。 準備ができたら、Esc キーを押して作成環境に戻ります。

    ![テキスト入力コントロールには、値が表示されます、ラベルでは、合計の実行が表示](media/working-with-variables/context-variable-4.png)

7. 画面に移動する際にコンテキスト変数の値を設定できます。 これはある画面から別の画面に "コンテキスト" または "パラメーター" を渡すのに役立ちます。 この手法を示すためには、画面の挿入、ボタンを挿入し、設定、 **OnSelect**に次の式のプロパティ。

    **Navigate( Screen1, None, { RunningTotal: -1000 } )**

    ![ボタンの OnSelect プロパティ](media/working-with-variables/context-variable-5.png)

    Alt キーを押しながら両方表示するには、このボタンを選択**Screen1**コンテキスト変数を設定および**RunningTotal** -1000 にします。

    ![Screen1 が開いて](media/working-with-variables/context-variable-6.png)

8. コンテキスト変数の値を表示するには、選択、**ファイル**] メニューの [クリックして**変数**左側のウィンドウ。

    ![[ファイル] メニュー オプションを変数](media/working-with-variables/context-variable-file-1.png)

9. コンテキスト変数の定義し、使用場所を表示するのには、それを選択します。

    ![変数が使用されているの一覧](media/working-with-variables/context-variable-file-2.png)

## <a name="use-a-collection"></a>コレクションを使用します。

最後に、コレクションを使用した計算機の作成方法を説明します。  コレクションは、変更が容易なテーブルを保持しているため、この計算機に値が入力されたときに、それぞれの値を "紙テープ" に記録するようにします。

コレクションのしくみは次のとおりです。

* コレクションを作成および設定するには、**[ClearCollect](functions/function-clear-collect-clearcollect.md)** 関数を使用します。  代わりに **[Collect](functions/function-clear-collect-clearcollect.md)** 関数を使用できますが、実質的には、古い変数を置き換えるのではなく別の変数が必要になります。  
* コレクションは一種のデータ ソース、すなわちテーブルです。 コレクションの単一の値にアクセスするには、**[First](functions/function-first-last.md)** 関数を使用し、結果のレコードから 1 つのフィールドを抽出します。 **[ClearCollect](functions/function-clear-collect-clearcollect.md)** で単一の値を使用した場合、これは次の例のように **Value** フィールドになります。<br>
**First(** *VariableName* **).Value**

それでは、コレクションを使用して計算機を作り直してみましょう。

1. **TextInput1** という名前の **[テキスト入力](controls/control-text-input.md)** コントロールと、**Button1** および **Button2** という名前の 2 つのボタンを追加します。

2. **Button1** の **[Text](controls/properties-core.md)** プロパティを **"Add"** に設定し、**Button2** の **Text** プロパティを **"Clear"** に設定します。

3. ユーザーが **[Add]** ボタンを選択するたびに累計を更新するために、**[OnSelect](controls/properties-core.md)** プロパティを次の数式に設定します。

    **Collect( PaperTape, TextInput1.Text )**

    この数式の単なるが存在する確立**PaperTape**としてテキスト文字列の単一列テーブルを保持するコレクション。 参照できる**PaperTape**このアプリで任意の場所。 ユーザーがこのアプリを開くたびに**PaperTape**は空のテーブルです。

    次の数式を実行すると、コレクションの末尾に新しい値を追加します。 に 1 つの値を追加している**収集**単一列テーブルに自動的に配置され、列の名前が**値**、後で使用します。

    ![[追加] ボタンの OnSelect プロパティ](media/working-with-variables/papertape-1.png)

4. ユーザーが選択したときに紙テープを消去する、**オフ** ボタンを設定、 **[OnSelect](controls/properties-core.md)** プロパティをこの式に。

    **Clear( PaperTape )**

    ![クリア ボタンの OnSelect プロパティ](media/working-with-variables/papertape-2.png)

5. 累計を表示するために、ラベルを追加し、**[Text](controls/properties-core.md)** プロパティを次の数式に設定します。

    **Sum( PaperTape, Value )**

    ![ラベルのテキスト プロパティ](media/working-with-variables/papertape-3.png)

6. 計算機を実行するために、F5 キーを押してプレビューを開き、テキスト入力コントロールに数値を入力して、ボタンを選択します。

    ![テキスト入力コントロールには、値、およびラベルの表示、実行中の合計が表示されます。](media/working-with-variables/papertape-run-1.png)

7. 既定のワークスペースに戻るには、Esc キーを押します。

8. 紙テープを表示するには、**データ テーブル** コントロールを挿入し、その **[Items](controls/properties-core.md)** プロパティを次の数式に設定します。

    **PaperTape**

    右側のウィンドウで、選択、**値**列を表示します。

    ![データのテーブルに、コレクションに追加された値を表示](media/working-with-variables/papertape-4.png)

9. コレクション内の値を確認するために、**[ファイル]** メニューの **[コレクション]** を選択します。

    ![PaperTape コレクションのプレビュー](media/working-with-variables/papertape-file.png)

10. 格納およびコレクションを取得、2 つの追加のボタン コントロールを追加し、設定、**テキスト**プロパティ**ロード**と**保存**します。 設定、 **OnSelect**のプロパティ、**ロード**に次の式ボタン。

     **Clear( PaperTape ); LoadData( PaperTape, "StoredPaperTape", true )**

     ため、最初にコレクションをクリアする必要がある**LoadData**コレクションの末尾に格納された値が追加されます。

     ![読み込み ボタンの OnSelect プロパティ](media/working-with-variables/papertape-5.png)

11. 設定、 **OnSelect**のプロパティ、**保存**に次の式ボタン。

     **SaveData( PaperTape, "StoredPaperTape" )**

     ![[保存] ボタンの OnSelect * プロパティ](media/working-with-variables/papertape-6.png)

12. F5 キーを押してもう一度プレビューを表示し、テキスト入力コントロールに数値を入力してボタンを選択します。 **[保存]** ボタンを選択します。 閉じると、アプリを再読み込みし、選択、**ロード**コレクションを再読み込みするボタンをクリックします。

> [!NOTE]
> **SaveData**と**LoadData** PowerApps Studio または PowerApps の web player ではありませんが、PowerApps Mobile での関数。
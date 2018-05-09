---
title: 変数について | Microsoft Docs
description: 状態、コンテキスト変数、およびコレクションを操作するための参照情報
documentationcenter: na
author: gregli-msft
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: conceptual
ms.component: canvas
ms.date: 07/06/2017
ms.author: gregli
ms.openlocfilehash: d77bc3c90b16fae60fb0daf78376beaa31d67098
ms.sourcegitcommit: 45fac73f04aa03b5796ae6833d777f4757e67945
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="understand-variables-in-powerapps"></a>PowerApps の変数について
Visual Basic や JavaScript などの別のプログラミング ツールを使ってきた方は、**変数はどこにあるのか**という疑問を抱くことでしょう。 PowerApps は若干異なり、別のアプローチが必要です。 変数の説明に進む代わりに、**Excel で何をしようとしているか**を考えてください。

他のツールでは、明示的に計算を実行し、その結果を変数に格納していたことでしょう。 ところが、PowerApps と Excel のどちらも、入力データが変更されると自動的に数式が再計算されます。そのため、通常は変数を作成したり更新したりする必要はありません。 可能な限りこの方法に従うことで、アプリをより簡単に作成、理解、維持することができます。

場合によっては、PowerApps で変数を使用する必要があります。これにより、[動作の数式](working-with-formulas-in-depth.md)を追加して Excel のモデルを拡張します。 これらの数式が実行されるのは、ユーザーがボタンを選択したときなどです。 動作の数式の中では、他の数式で使用する変数を設定すると便利なことがよくあります。

一般的には、変数の使用を避けてください。 ただし、変数を使わないと目的の動作が得られないこともあります。

## <a name="translate-excel-into-powerapps"></a>Excel を PowerApps に変換する
### <a name="excel"></a>Excel
それでは、Excel のしくみを確認しましょう。 セルには、数値や文字列などの値、または他のセルの値に基づく数式を含めることができます。 ユーザーがセルに別の値を入力すると、新しい値に応じてすべての数式が自動的に再計算されます。 この動作を実現するためにプログラミングは必要ありません。

![](media/working-with-variables/excel-recalc.png)

Excel に変数がありません。 数式が含まれるセルの値は入力内容に基づいて変化しますが、数式の結果を記憶してそれをセルや他の場所に格納する方法はありません。 セルの値を変更すると、スプレッドシート全体が変更される可能性があり、それ以前に計算された値はすべて失われます。  Excel のユーザーは、セルをコピーして貼り付けることができますが、それはユーザーが手動で制御するものであり、数式では不可能です。

### <a name="powerapps"></a>PowerApps
PowerApps で作成したアプリの動作は、Excel と非常によく似ています。 セルを更新する代わりに、画面上の任意の場所にコントロールを追加し、数式で使用するために名前を付けることができます。

たとえば、**TextBox1** という名前の**[ラベル](controls/control-text-box.md)** コントロールのほか、**TextInput1** と **TextInput2** という名前の 2 つの**[テキスト入力](controls/control-text-input.md)** コントロールを追加することで、アプリで Excel の動作を複製できます。 **TextBox1** の **[Text](controls/properties-core.md)** プロパティを **TextInput1 + TextInput2** に設定すると、**TextInput1** と **TextInput2** に格納されている値がどのような数値であってもその合計が自動的に表示されます。

![](media/working-with-variables/recalc1.png)

**TextBox1** コントロールが選択されていて、**[Text](controls/properties-core.md)** の数式が画面上部の数式バーに表示されていることに注目してください。  ここで、数式が **TextInput1 + TextInput2** となっていることがわかります。  Excel ブック内のセル間に依存関係が作成されるのと同様に、この数式によってこれらのコントロール間に依存関係が作成されます。  ここで、**TextInput1** の値を変更してみましょう。

![](media/working-with-variables/recalc2.png)

**TextBox1** の数式が自動的に再計算され、新しい値が表示されます。

PowerApps では、数式を使用して、コントロールのプライマリ値だけでなく、書式設定などのプロパティも決定できます。 次の例では、ラベルの **[Color](controls/properties-color-border.md)** プロパティに設定された数式により、負の値は自動的に赤で表示されます。 **[If](functions/function-if.md)** 関数は Excel と非常によく似ています。
<br>**If( Value(TextBox1.Text) < 0, Red, Black )**

![](media/working-with-variables/recalc-color1.png)

**TextBox1.Text** の計算結果が負の場合、数値が赤で表示されます。

![](media/working-with-variables/recalc-color2.png)

数式は、さまざまなシナリオで利用できます。

* デバイスの GPS を使用した場合、**Location.Latitude** と **Location.Longitude** を使用する数式によって、マップ コントロールに現在の位置を表示できます。  移動すると、マップによって位置が自動的に追跡されます。
* 他のユーザーが[データ ソース](working-with-data-sources.md)を更新できます。  たとえば、チームの他のメンバーが SharePoint リスト内の項目を更新する場合があります。  データ ソースを更新すると、依存するすべての数式が自動的に再計算され、更新されたデータが反映されます。 この例をさらに進めて、ギャラリーの **[Items](controls/properties-core.md)** プロパティを数式 **Filter( SharePointList )** に設定すると、新しくフィルター処理された[レコード](working-with-tables.md#records) セットが自動的に表示されます。

### <a name="benefits"></a>利点
数式をしたアプリの作成には多くの利点があります。

* Excel を知っていれば PowerApps もわかります。 モデルと数式の言語は同じです。
* 他のプログラミング ツールを使用したことがある場合は、これらの例を実現するためにどれだけの量のコードが必要になるかを考えてみてください。  Visual Basic では、各テキスト入力コントロールの変更イベント用にイベント ハンドラーを記述する必要があります。  このそれぞれで計算を実行するコードは冗長であり、不一致が生じる可能性があります。また、共通のサブルーチンを記述することが必要になる場合もあります。  PowerApps では、1 行の数式 1 つでこのすべての処理を実現しました。
* **TextBox1** のテキストがどこから取得されるかを理解するには、**[Text](controls/properties-core.md)** プロパティの数式だけを確認すればいいことがわかります。  ほかに、このコントロールのテキストを変更する方法はありません。  従来のプログラミング ツールでは、プログラムのどこからでも、任意のイベント ハンドラーまたはサブルーチンでラベルの値を変更できました。  これにより、変数がいつどこで変更されたかを追跡するのが難しくなります。
* ユーザーは、スライダー コントロールを変更した後に考えを変えた場合、スライダーを元の値に戻すことができます。  アプリでは以前と変わらず同じコントロールが表示されるため、まるで何も変わっていないかのように見えます。  "what if" を試したり要求したりした場合でも、Excel の場合と同様、派生的な問題は発生しません。  

一般的に、数式を使用して効果を得ることができれば楽になります。 PowerApps の数式エンジンをうまく利用しましょう。  

## <a name="know-when-to-use-variables"></a>変数を使用するタイミングを把握する
単純な加算器に変更を加えて、累計機能を備えた昔ながらの計算機のように動作するようにしましょう。 **[Add]** ボタンを選択すると、数値が累計に加算されます。 **[Clear]** ボタンを選択すると、累計が 0 にリセットされます。

![](media/working-with-variables/button-changes-state.png)

ここで作成する計算機では、Excel に存在しない機能、つまりボタンを使用しています。 このアプリでは、数式だけを使用して累計を計算することはできません。なぜなら、値はユーザーが行う一連の操作によって異なるからです。 代わりに、累計を手動で記録して更新する必要があります。 ほとんどのプログラミング ツールでは、この情報を "*変数*" に格納します。    

場合によっては、アプリが目的の動作を行うために変数が必要になります。  ただし、このアプローチには注意が必要です。

* 累計を手動で更新する必要があります。 この処理は自動再計算では実行されません。
* 累計は、他のコントロールの値に基づいて計算できません。 累計は、ユーザーが **[Add]** ボタンを選択した回数と、選択したときにテキスト入力コントロールに格納されていた値に基づきます。 ユーザーが 77 を入力した後で **[Add]** を 2 回選択したのか、加算する値に 24 と 130 を指定したのか、 合計が 154 になった後でその違いを見分けることはできません。
* 合計に対する変更は、異なる経路から生じている可能性があります。 この例では、**[Add]** ボタンでも **[Clear]** ボタンでも合計を更新できます。 アプリが期待どおりに動作しない場合、どちらかのボタンに問題の原因があるのでしょうか。

## <a name="create-a-global-variable"></a>グローバル変数を作成する
計算機を作成するには、累計を保持する変数が必要です。 PowerApps で使用できる最も単純な変数は、*グローバル変数*です。  

グローバル変数は次のように機能します。

* **[Set](functions/function-set.md)** 関数を使用して、グローバル変数の値を設定します。  **Set( MyVar, 1 )** とすることで、グローバル変数 **MyVar** の値を **1** に設定します。
* **Set** 関数とともに使用した名前を参照すると、グローバル変数を使用できます。  この場合、**MyVar** は **1** を返します。
* グローバル変数は、文字列、数値、レコード、[テーブル](working-with-tables.md)など、すべての値を保持できます。

それでは、グローバル変数を使用して計算機を作り直してみましょう。

1. **TextInput1** という名前のテキスト入力コントロールと、**Button1** および **Button2** という名前の 2 つのボタンを追加します。

2. **Button1** の **[Text](controls/properties-core.md)** プロパティを **"Add"** に設定し、**Button2** の **Text** プロパティを **"Clear"** に設定します。

3. ユーザーが **[Add]** ボタンを選択するたびに累計を更新するために、**[OnSelect](controls/properties-core.md)** プロパティを次の数式に設定します。
   
    **Set( RunningTotal, RunningTotal + Text1 )**
   
    ユーザーが初めて **[追加]** ボタンを選択し、**[Set](functions/function-set.md)** が呼び出されたときに、既定値が*空白*の **RunningTotal** が作成されます。  加算では、この値が 0 として処理されます。
   
    ![](media/working-with-variables/global-variable-1.png)
4. ユーザーが **[Clear]** ボタンを選択するたびに累計を **0** に設定するために、**[OnSelect](controls/properties-core.md)** プロパティを次の数式に設定します。
   
    **Set( RunningTotal, 0 )**
   
    ![](media/working-with-variables/global-variable-2.png)
5. **[ラベル](controls/control-text-box.md)** コントロールを追加し、**[Text](controls/properties-core.md)** プロパティを **RunningTotal** に設定します。
   
    この数式は自動的に再計算され、ユーザーが選択したボタンに基づいて変更される **RunningTotal** の値が表示されます。
   
    ![](media/working-with-variables/global-variable-3.png)
6. アプリをプレビューします。前述のように計算機が完成しました。  テキスト ボックスに数値を入力して **[追加]** ボタンを数回クリックします。  準備ができたら、Esc キーを押して作成環境に戻ります。  
   
    ![](media/working-with-variables/global-variable-4.png)
7. グローバル変数の値を表示するには、**[ファイル]** メニューを選択して、左側のウィンドウにある **[変数]** を選択します。
   
    ![](media/working-with-variables/global-variable-file-1.png)
8. 変数がどこで定義され使用されているかを確認するには、その変数を選択します。
   
    ![](media/working-with-variables/global-variable-file-2.png)

## <a name="types-of-variables"></a>変数の種類
PowerApps には 3 種類の変数があります。

| 変数の種類 | 適用範囲 | 説明 | 関数 |
| --- | --- | --- | --- |
| グローバル変数 |アプリ |使い方が最も単純です。  数値、テキスト文字列、ブール値、レコード、テーブルなどを保持し、アプリ内のどこからでも参照できます。 |[**Set**](functions/function-set.md) |
| コンテキスト変数 |画面 |他の言語のプロシージャにパラメーターを渡す場合など、画面に値を渡すのに最適です。  1 つの画面からのみ参照できます。 |[**UpdateContext**](functions/function-navigate.md) |
| コレクション |アプリ |アプリ内のどこからでも参照できるテーブルを保持します。  全体として設定するのではなく、テーブルのコンテンツごとに変更できます。 後で使用するためにローカル デバイスに保存できます。 |[**Collect**](functions/function-savedata-loaddata.md)<br>など。 |

**Set**、**UpdateContext**、**Navigate**、または **Collect** 関数を使用すると、すべての変数は暗黙的に作成されます。  他のプログラミング ツールで行われるような変数の明示的な宣言はありません。  また、変数の種類は、変数に入る値によって暗黙的に決定します。

アプリの実行中はすべての変数がメモリに保持されます。  アプリを終了すると、変数に保持されている値は失われます。  **Patch** または **Collect** 関数を使用して、変数の値をデータ ソースに保存できます。あるいは、コレクションの場合は、**SaveData** 関数を使用して、ローカル デバイスに保存できます。  アプリが最初に読み込まれるとき、すべての変数の値は*空白*になります。

変数の値を参照するために変数名を使用できます。  たとえば、一度 **Set( MyColor, Red )** で定義しておけば、色の値を使用できるところならどこでも **MyVar** だけで使用でき、値は **Red** に置き換えられます。  コンテキスト変数と同じ名前のグローバル変数、またはコレクションを設定できます。  この場合、コンテキスト変数が優先されます。  [曖昧性除去演算子](functions/operators.md#disambiguation-operator) **@[MyColor]** を使用して、グローバル変数またはコレクションを引き続き参照できます。

## <a name="create-a-context-variable"></a>コンテキスト変数を作成する
グローバル変数の代わりにコンテキスト変数を使用した計算機の作成方法を説明します。    

コンテキスト変数のしくみは次のとおりです。

* コンテキスト変数を作成および設定するには、**[UpdateContext](functions/function-updatecontext.md)** 関数を使用します。  最初の更新時にコンテキスト変数がまだ存在しない場合は、既定値が "*空白*" のコンテキスト変数が作成されます。
* コンテキスト変数は、レコードを使用して作成および更新します。 他のプログラミング ツールでは、一般的に、"x = 1" のように、代入には "=" を使用します。  コンテキスト変数の場合は、代わりに **{ x: 1 }** を使用します。 コンテキスト変数を使用する場合は、その名前を直接使用します。  
* **[Navigate](functions/function-navigate.md)** 関数を使用すると、画面が表示されるときにコンテキスト変数も設定できます。 画面を一種のプロシージャまたはサブルーチンと考えた場合、これは他のプログラミング ツールのパラメーター渡しに似ています。
* **[Navigate](functions/function-navigate.md)** を除き、コンテキスト変数は、名前を取得する場所である単一の画面のコンテキストに制限されます。  このコンテキスト以外でコンテキスト変数を使用または設定することはできません。
* コンテキスト変数では、文字列、数値、レコード、[テーブル](working-with-tables.md)など、任意の値を保持できます。

それでは、コンテキスト変数を使用して計算機を作り直してみましょう。

1. **TextInput1** という名前のテキスト入力コントロールと、**Button1** および **Button2** という名前の 2 つのボタンを追加します。

2. **Button1** の **[Text](controls/properties-core.md)** プロパティを **"Add"** に設定し、**Button2** の **Text** プロパティを **"Clear"** に設定します。

3. ユーザーが **[Add]** ボタンを選択するたびに累計を更新するために、**[OnSelect](controls/properties-core.md)** プロパティを次の数式に設定します。
   
    **UpdateContext( { RunningTotal: RunningTotal + Text1 } )**
   
    ユーザーが初めて **[Add]** ボタンを選択し、**[UpdateContext](functions/function-updatecontext.md)** が呼び出されたときに、既定値が "*空白*" の **RunningTotal** が作成されます。  加算では、この値が 0 として処理されます。
   
    ![](media/working-with-variables/context-variable-1.png)
4. ユーザーが **[Clear]** ボタンを選択するたびに累計を **0** に設定するために、**[OnSelect](controls/properties-core.md)** プロパティを次の数式に設定します。
   
    **UpdateContext( { RunningTotal: 0 } )**
   
    ここでも、**[UpdateContext](functions/function-updatecontext.md)** を数式 **UpdateContext( { RunningTotal: 0 } )** で使用します。
   
    ![](media/working-with-variables/context-variable-2.png)
5. **[ラベル](controls/control-text-box.md)** コントロールを追加し、**[Text](controls/properties-core.md)** プロパティを **RunningTotal** に設定します。
   
    この数式は自動的に再計算され、ユーザーが選択したボタンに基づいて変更される **RunningTotal** の値が表示されます。
   
    ![](media/working-with-variables/context-variable-3.png)
6. アプリをプレビューします。前述のように計算機が完成しました。  テキスト ボックスに数値を入力して **[追加]** ボタンを数回クリックします。  準備ができたら、Esc キーを押して作成環境に戻ります。  
   
    ![](media/working-with-variables/context-variable-4.png)
7. 画面に移動する際にコンテキスト変数の値を設定できます。  これはある画面から別の画面に "コンテキスト" または "パラメーター" を渡すのに役立ちます。  これを確認するには、新しい画面を挿入し、**OnSelect** プロパティを次の数式に設定したボタンを挿入します。
   
    **Navigate( Screen1, None, { RunningTotal: -1000 } )**
   
    ![](media/working-with-variables/context-variable-5.png)
   
    **Screen2** でこのボタンを選択すると (ボタンを最後まで選択したまま作成している場合でも選択できます)、**Screen1** が表示され、コンテキスト変数 **RunningTotal** が -1000 に設定されます。
   
    ![](media/working-with-variables/context-variable-6.png)
8. コンテキスト変数の値を表示するには、**[ファイル]** メニューを選択して、左側のウィンドウにある **[変数]** を選択します。
   
    ![](media/working-with-variables/context-variable-file-1.png)
9. コンテキスト変数が定義され使用される場所を確認するには、そのコンテキスト変数を選択します。
   
    ![](media/working-with-variables/context-variable-file-2.png)

## <a name="create-a-collection"></a>コレクションの作成
最後に、コレクションを使用した計算機の作成方法を説明します。  コレクションは、変更が容易なテーブルを保持しているため、この計算機に値が入力されたときに、それぞれの値を "紙テープ" に記録するようにします。

コレクションのしくみは次のとおりです。

* コレクションを作成および設定するには、**[ClearCollect](functions/function-clear-collect-clearcollect.md)** 関数を使用します。  代わりに **[Collect](functions/function-clear-collect-clearcollect.md)** 関数を使用できますが、実質的には、古い変数を置き換えるのではなく別の変数が必要になります。  
* コレクションは一種のデータ ソース、すなわちテーブルです。 コレクションの単一の値にアクセスするには、**[First](functions/function-first-last.md)** 関数を使用し、結果のレコードから 1 つのフィールドを抽出します。 **[ClearCollect](functions/function-clear-collect-clearcollect.md)** で単一の値を使用した場合、これは次の例のように **Value** フィールドになります。<br>**First(** *VariableName* **).Value**

それでは、コレクションを使用して計算機を作り直してみましょう。

1. **TextInput1** という名前の**[テキスト入力](controls/control-text-input.md)** コントロールと、**Button1** および **Button2** という名前の 2 つのボタンを追加します。

2. **Button1** の **[Text](controls/properties-core.md)** プロパティを **"Add"** に設定し、**Button2** の **Text** プロパティを **"Clear"** に設定します。

3. ユーザーが **[Add]** ボタンを選択するたびに累計を更新するために、**[OnSelect](controls/properties-core.md)** プロパティを次の数式に設定します。
   
    **Collect( PaperTape, TextInput1.Text )**
   
    この数式では、新しい値をコレクションの末尾に追加します。  1 つの値を追加しようとしているため、**Collect** はその値を自動的に **Value** という列名の単一列テーブル (これはあとで使用します) に入力します。
   
    ![](media/working-with-variables/papertape-1.png)
4. ユーザーが **[クリア]** ボタンを選択したときに紙テープがクリアされるようにするには、そのボタンの **[OnSelect](controls/properties-core.md)** プロパティを次の数式に設定します。
   
    **Clear( PaperTape )**
   
    ![](media/working-with-variables/papertape-2.png)
5. 累計を表示するために、ラベルを追加し、**[Text](controls/properties-core.md)** プロパティを次の数式に設定します。
   
    **Sum( PaperTape, Value )**
   
    ![](media/working-with-variables/papertape-3.png)
6. 計算機を実行するために、F5 キーを押してプレビューを開き、テキスト入力コントロールに数値を入力して、ボタンを選択します。
   
    ![](media/working-with-variables/papertape-run-1.png)
7. 既定のワークスペースに戻るには、Esc キーを押します。
8. 紙テープを表示するには、**データ テーブル** コントロールを挿入し、その **[Items](controls/properties-core.md)** プロパティを次の数式に設定します。
   
    **PaperTape**
   
    また、右側のウィンドウに表示するには列を選択する必要があります。ここでは **Value** 列を表示します。
   
    ![](media/working-with-variables/papertape-4.png)
9. コレクション内の値を確認するために、**[ファイル]** メニューの **[コレクション]** を選択します。
   
    ![](media/working-with-variables/papertape-file.png)
10. コレクションを保存したり取得したりするには、さらに 2 つのボタン コントロールを追加し、そのテキストを **Load** と **Save** にします。  **Load** については、次の数式に **OnSelect** プロパティを設定します。
    
     **Clear( PaperTape ); LoadData( PaperTape, "StoredPaperTape", true )**
    
     **LoadData** は保存された値をコレクションの末尾に追加するため、最初にコレクションをクリアする必要があります。
    
     ![](media/working-with-variables/papertape-5.png)
11. **Save** については、次の数式に **OnSelect** プロパティを設定します。
    
     **SaveData( PaperTape, "StoredPaperTape" )**
    
     ![](media/working-with-variables/papertape-6.png)
12. F5 キーを押してもう一度プレビューを表示し、テキスト入力コントロールに数値を入力してボタンを選択します。  **[保存]** ボタンを選択します。  アプリを終了してもう一度読み込み、**[読み込む]** ボタンを選択してコレクションを再読み込みします。  
    
    > [!NOTE]
    > Web ブラウザーで実行されている場合、**SaveData** と **LoadData** は機能しません。 PowerApps Studio for Windows または PowerApps Mobile を使用する必要があります。


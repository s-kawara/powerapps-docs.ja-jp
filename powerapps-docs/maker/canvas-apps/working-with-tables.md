---
title: キャンバス アプリのテーブルについて | Microsoft Docs
description: PowerApps におけるキャンバス アプリのテーブル、列、およびレコードの操作に関する参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 04/26/2016
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 38745810321807e69d5eba8e1f2c281dafa73ae5
ms.sourcegitcommit: 5db6e3ac3a622de313a1102417397e126c3f92f2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/15/2018
ms.locfileid: "45640448"
---
# <a name="understand-canvas-app-tables-and-records-in-powerapps"></a>PowerApps におけるキャンバス アプリのテーブルとレコードについて

PowerApps では、Microsoft Excel、SharePoint、SQL Server など、レコード形式やテーブル形式でデータを格納するソースにアクセスして情報を取得する、キャンバス アプリを作成できます。 このタイプのデータを効率的に操作できるように、その構造の基になる概念を確認しておきましょう。

* レコードには、ある人、場所、または物事について 1 つ以上のカテゴリの情報が格納されます。 たとえば、1 つのレコードに、1 人の顧客の名前、電子メール アドレス、電話番号を格納できます。 他のツールでは、レコードが "行" や "項目" と呼ばれることもあります。
* テーブルには、同じカテゴリ設定で情報が格納されている 1 つ以上のレコードが保持されます。 たとえば、1 つのテーブルに、50 人の顧客の名前、電子メール アドレス、電話番号を格納できます。

作成するアプリでは、[数式](working-with-formulas.md)を使用して、レコードとテーブルの作成、更新、操作を行います。 外部の[データ ソース](working-with-data-sources.md)に対してデータの読み取りと書き込みを行うことがあるでしょう。このデータ ソースを拡張テーブルと呼びます。 内部テーブルを 1 つ以上作成することもできます。これを[コレクション](working-with-data-sources.md#collections)と呼びます。

Excel の数式が 1 つ以上のセル参照を引数として受け取るのと同じように、テーブルの名前を引数として受け取るさまざまな数式を作成できます。 PowerApps の数式には、指定された他の引数を使用して作成したテーブルを返すものもあります。 たとえば、次のような数式を作成できます。

* **[Patch](functions/function-patch.md)** 関数が受け取る複数の引数の 1 つとしてテーブルを指定することで、テーブル内のレコードを更新する。
* **[AddColumns](functions/function-table-shaping.md)** 関数、**[DropColumns](functions/function-table-shaping.md)** 関数、または **[RenameColumns](functions/function-table-shaping.md)** 関数の引数としてテーブルを指定することで、テーブル内の列の追加、削除、名前の変更を行う。 これらの関数によって元のテーブルが変更されることはありません。 指定された他の引数に基づいて別のテーブルが作成されて返されます。

## <a name="elements-of-a-table"></a>テーブルの要素
![](media/working-with-tables/elements-of-a-table.png)

### <a name="records"></a>レコード
各テーブルには、ある人、場所、または物事に関する 1 つ以上のカテゴリの情報が格納されます。 上記の例では、製品 (**Chocolate (チョコレート)**、**Bread (パン)**、**Water (水)**) ごとにレコードがあり、各情報カテゴリ (**Price (価格)**、**Quantity on Hand (在庫数量)**、**Quantity on Order (注文数量)**) に対応した列があります。

数式でレコードを参照する際は、テーブルとは切り離して、中かっこを使用してレコードそのものを記述できます。 たとえば、レコードを **{ Name: "Strawberries", Price: 7.99 }** のように書きますが、これはテーブルとは関連付けられていません。 この例では、**Name** や **Price** などのフィールド名が二重引用符で囲まれていないことに注意してください。

### <a name="fields"></a>フィールド
フィールドは、レコードに含まれる個々の情報です。 フィールドは特定のレコードの列に格納された値として捉えることができます。

コントロールの場合と同様、レコードのフィールドを参照する際は、レコードに **.**  [演算子](functions/operators.md)を付けます。  たとえば、**First(Products).Name** と指定すると、**Products** テーブル内の 1 つ目のレコードの **Name** フィールドが返されます。

フィールドには、**[GroupBy](functions/function-groupby.md)** 関数の例が示すように、別のレコードやテーブルを格納できます。 レコードとテーブルは入れ子構造にすることができ、入れ子レベルの数に制限はありません。

### <a name="columns"></a>列
列は、テーブル内の 1 つ以上のレコードに設定された同じフィールドを指します。 上記の例では、各製品に価格フィールドがあり、すべての製品で同じ列に価格が格納されています。  上のテーブルには 4 つの列があります。一番上には左から順に下記のように示されています。

* **Name**
* **Price**
* **Quantity on Hand**
* **Quantity on Order**

列の名前には、その列のフィールドの内容が反映されています。

列内にあるすべての値はデータ型が同じです。 上記の例では、"Quantity on Hand" 列には常に数値が格納され、いずれかのレコードに "12 units" などの文字列を含めることはできません。  また、どの列も値を *空白* にすることができます。  

他のツールでは、列が "フィールド" と呼ばれることもあります。

> [!NOTE]
> 名前にスペースが使われている列を含む SharePoint および Excel のデータ ソースの場合、PowerApps ではスペースが **"\_x0020\_"** に置き換えられます。 たとえば、SharePoint または Excel の **"Column Name"** は、PowerApps のデータ レイアウトに表示されるときや数式で使用されるときは **"Column_x0020_Name"** と表示されます。

### <a name="table"></a>テーブル
テーブルは 1 つ以上のレコードで構成されます。各レコードは複数のフィールドで構成され、フィールドにはレコード全体で一貫したフィールド名が使用されます。

データ ソースやコレクションに格納されているテーブルにもすべて名前があります。この名前は、テーブルを参照したり、引数として受け取る関数にテーブルを渡したりする際に使用します。  関数や数式の結果をテーブルにすることもできます。

数式でテーブルを表すには、次の例に示すように、**[Table](functions/function-table.md)** 関数を使用してレコードのセットを指定します。各レコードは中かっこで囲みます。

**Table( { Value: "Strawberry" }, { Value: "Vanilla" } )**

角かっこを使って、列が 1 つのテーブルを定義することもできます。  上と同じテーブルを次の方法で記述できます。

**[ "Strawberry", "Vanilla" ]**

## <a name="table-formulas"></a>テーブルの数式
Excel と PowerApps は、似た方法で数式を使用してテキストの数値と文字列を操作します。

* Excel では、セル **A1** に「**42**」などの値を入力し、別のセルに「**A1+2**」などの数式を入力すると **44** という値が表示されます。
* PowerApps では、**Slider1** の **[Default](controls/properties-core.md)** プロパティを **42** に設定し、ラベルの **[Text](controls/properties-core.md)** プロパティを **Slider1.Value + 2** に設定すると、**44** という値が表示されます。

どちらの場合も、引数の値 (上の例では、セル **A1** や **Slider1** の数値) を変更すると、計算された値が自動的に変更されます。

同様に、数式を使用して、テーブルやレコード内のデータにアクセスし、操作することができます。 たとえば、引数としてテーブルの名前を使用できる数式があります。**Min(Catalog, Price)** という数式は **Catalog** テーブルの **Price** 列内の最小値を返します。 また、テーブル全体を戻り値として返す数式もあります。**RenameColumns(Catalog, "Price", "Cost")** という数式では、**Catalog** テーブルのすべてのレコードを返し、**Price** 列の名前を **Cost** に変更します。

数値の場合と同様、テーブルやレコードが含まれた数式でも、基になるテーブルやレコードが変更されると自動的に再計算が行われます。 **Catalog** テーブルに格納されている製品のコストが以前の最小値よりも小さくなった場合、**[Min](functions/function-aggregates.md)** 数式ではそれに合わせて自動的に値が変更されます。

単純な例をいくつか見てみましょう。

1. スマートフォン用の空のアプリを作成し、他のコントロールを含む垂直方向の**[ギャラリー](controls/control-gallery.md)** コントロールを追加します。

    既定では、画面には **CustomGallerySample** という名前のテーブルから取得したプレースホルダー テキストが表示されます。 画面の **[[ギャラリー]](controls/control-gallery.md)** コントロールの **[Items](controls/properties-core.md)** プロパティは自動的にこのテーブルに設定されます。

    ![](media/working-with-tables/gallery-items.png)

    > [!NOTE]
    > 一部のコントロールは、分かりやすいように配置変更され、拡大されています。

2. **[Items](controls/properties-core.md)** プロパティにテーブルの名前を設定する代わりに、次の例のように、テーブルの名前を引数として受け取る数式を設定します。<br>
    **Sort(CustomGallerySample, SampleHeading, Descending)**

    この数式では **[Sort](functions/function-sort.md)** 関数が使用されています。Sort 関数は、1 つ目の引数としてテーブルの名前を受け取り、2 つ目の引数としてそのテーブル内の列の名前を受け取ります。 また、省略可能な 3 つ目の引数も用意されており、データを降順で並べ替えるように指定できます。

    ![](media/working-with-tables/gallery-items-sort.png)

3. 下の例のように、前の手順で作成した数式を引数として受け取ってテーブルを返す数式を **[Items](controls/properties-core.md)** プロパティに設定します。<br>
   **FirstN(Sort(CustomGallerySample, SampleHeading, Descending), 2)**

    この数式では、**[FirstN](functions/function-first-last.md)** 関数を使って、テーブルから特定の数のレコードを取得しています。 **[FirstN](functions/function-first-last.md)** の 1 つ目の引数として **[Sort](functions/function-sort.md)** 関数を使用し、2 つ目の引数として数字 (この例では **2**) を指定しています。この数字は返すレコードの数を表しています。
   
    全体の数式は、**CustomGallerySample** テーブルの最初の 2 つのレコードを格納して **SampleHeading** 列で降順に並べ替えたテーブルを返します。
   
    ![](media/working-with-tables/gallery-items-sort-firstn.png)

### <a name="table-functions-and-control-properties"></a>テーブルの関数とコントロール プロパティ
PowerApps の多くの関数が、テーブル名を引数として受け取り、同じデータを格納した別のテーブルを作成し、他の引数に基づいてそのテーブルを操作したうえで結果として返します。 このような関数では、単にデータ ソースであっても元のテーブルに変更を加えることはありません。

* **[Sort](functions/function-sort.md)**、**[Filter](functions/function-filter-lookup.md)** - レコードの並べ替えとフィルター処理を行います。
* **[FirstN](functions/function-first-last.md)**、**[LastN](functions/function-first-last.md)** - テーブル内の最初の N 個または最後の N 個のレコードを返します。
* **[Abs](functions/function-numericals.md)**、**[Sqrt](functions/function-numericals.md)**、**[Round](functions/function-round.md)**、**[RoundUp](functions/function-round.md)**、**[RoundDown](functions/function-round.md)** - 単一列テーブルの各レコードに対して行う算術演算で、演算結果が含まれた単一列テーブルを返します。
* **[Left](functions/function-left-mid-right.md)**、 **[Mid](functions/function-left-mid-right.md)**、 **[Right](functions/function-left-mid-right.md)**、**[Replace](functions/function-replace-substitute.md)**、 **[Substitute](functions/function-replace-substitute.md)**、 **[Trim](functions/function-trim.md)**、 **[Lower](functions/function-lower-upper-proper.md)**、 **[Upper](functions/function-lower-upper-proper.md)**、 **[Proper](functions/function-lower-upper-proper.md)** - 単一列テーブルの各レコードに対して行う文字列操作で、操作後の文字列が含まれた単一列テーブルを返します。
* **[Len](functions/function-len.md)** - 文字列が格納されている 1 列を調べて、各文字列の長さを格納した単一列テーブルを返します。
* **[Concatenate](functions/function-concatenate.md)** - 文字列が格納されている複数の列を連結して、文字列の単一列テーブルを返します。
* **[AddColumns](functions/function-table-shaping.md)**、**[DropColumns](functions/function-table-shaping.md)**、**[RenameColumns](functions/function-table-shaping.md)**、**[ShowColumns](functions/function-table-shaping.md)** - テーブルの列を操作し、元のテーブルとは異なる列で構成された新しいテーブルを返します。
* **[Distinct](functions/function-distinct.md)** - 重複したレコードを削除します。
* **[Shuffle](functions/function-shuffle.md)** - レコードをランダムな順序でシャッフルします。
* **[HashTags](functions/function-hashtags.md)** - 文字列にハッシュタグがないかを検索します。
* **[Errors](functions/function-errors.md)** - データ ソースを使用している場合にエラー情報を提供します。

引数として 1 つの列を受け取る関数であっても、複数の列で構成されたテーブルに対して実行できます。 複数列テーブルから 1 つの列を抽出するには、次の例のように、使用したい関数の引数として **[ShowColumns](functions/function-table-shaping.md)** 関数を使用します。<br>**Lower( ShowColumns( Products, "Name" ) )**

この数式は、**Products** テーブルの **Name** 列からすべてのデータを取得して単一列テーブルを作成し、大文字を小文字に変換します。 **[AddColumns](functions/function-table-shaping.md)** 関数、**[RenameColumns](functions/function-table-shaping.md)** 関数、**[DropColumns](functions/function-table-shaping.md)** 関数の引数としてテーブルを指定すると、必要な形にテーブルを再構成することができます。

これらの関数の引数としてデータ ソースを指定すると、データ ソースのレコードに変更が加えられ、通常はその新しい値がテーブルとして返されます。

* **[Collect](functions/function-clear-collect-clearcollect.md)**、**[Clear](functions/function-clear-collect-clearcollect.md)**、**[ClearCollect](functions/function-clear-collect-clearcollect.md)** - コレクションの作成、クリア、追加を行います。
* **[Update](functions/function-update-updateif.md)**、**[UpdateIf](functions/function-update-updateif.md)** - 指定した 1 つ以上の条件に一致するレコードを更新します。
* **[Remove](functions/function-remove-removeif.md)**、**[RemoveIf](functions/function-remove-removeif.md)** - 指定した 1 つ以上の条件に一致するレコードを削除します。

これらのプロパティには、テーブルに該当する値が設定されます。

* **Items** - ギャラリーとリスト ボックスに適用します。 ギャラリーに表示するテーブルです。
* **SelectedItems** - リスト ボックスに適用します。 ユーザーが選択した項目で構成されたテーブルです。

## <a name="record-formulas"></a>レコードの数式
レコード単位でデータを計算したり、個々のレコードを引数として受け取ったり、戻り値として返したりする数式を作成できます。 前のセクションで使用したギャラリーの例に戻り、**Gallery1.Selected** プロパティを使用して、ギャラリーでユーザーが選択した任意のレコードから情報を取得しましょう。

1. ボタンを追加し、**[OnSelect](controls/properties-core.md)** プロパティを次の数式に設定します。<br>
    **Collect( SelectedRecord, Gallery1.Selected )**

2. Alt キーを押しながら、ボタンを選択します。

3. **[ファイル]** メニューの **[コレクション]** を選択します。

    ![](media/working-with-tables/selected-collection.png)

この数式で返されるレコードには、ギャラリーで選択されているレコードのデータだけでなく、そのギャラリーにある各コントロールも格納されます。 上の例では、元のテーブルの **SampleText** 列に対応する **SampleText** 列と、その列のデータを表示するラベルに相当する **Subtitle1** 列の両方がレコードに含まれています。 **Subtitle1** 列のテーブル アイコンを選択すると、そのデータの詳細が表示されます。

> [!NOTE]
> このトピックで指定する要素以外の要素を追加した場合、**Subtitle1** 列には **Subtitle2** または類似する名前が付けられる場合があります。

選択したレコードが用意できたので、このレコードから個々のフィールドを抽出しましょう。これには、**.**  。

1. **[ラベル](controls/control-text-box.md)** コントロールを追加し、ギャラリーとボタンの下に移動します。

1. ラベルの **[Text](controls/properties-core.md)** プロパティに次の式を設定します。<br>
    **"Selected: " & Gallery1.Selected.SampleHeading**
   
    ![](media/working-with-tables/gallery-selected.png)

レコードである **Selected** プロパティを受け取り、そこから **SampleHeading** プロパティを抽出しました。

関連する名前付きの値の汎用コンテナーとしてレコードを使用することもできます。

* **[UpdateContext](functions/function-updatecontext.md)** 関数や **[Navigate](functions/function-navigate.md)** 関数を使用した数式を作成する場合は、レコードを使用して、更新する[コンテキスト変数](working-with-variables.md#create-a-context-variable)を収集できます。
* **[編集フォーム](controls/control-form-detail.md)** コントロールで **[Updates](controls/control-form-detail.md)** プロパティを使用して、ユーザーがフォームで加えた変更を収集できます。
* **[Patch](functions/function-patch.md)** 関数を使用し、データ ソースを更新してレコードをマージできます。

このような場合、このレコードはテーブルには含まれません。

### <a name="record-functions-and-control-properties"></a>レコードの関数とコントロール プロパティ
レコードを返す関数:

* **[FirstN](functions/function-first-last.md)**、**[LastN](functions/function-first-last.md)** - テーブルの最初のレコードまたは最後のレコードを返します。
* **[Lookup](functions/function-filter-lookup.md)** - テーブル内で、1 つ以上の条件に一致する最初のレコードを返します。
* **[Patch](functions/function-patch.md)** - データ ソースを更新するか、レコードをマージします。
* **[Defaults](functions/function-defaults.md)** - データ ソースの既定値を返します。

レコードを返すプロパティ:

* **Selected** - ギャラリーとリスト ボックスに適用します。 現在選択されているレコードを返します。
* **Updates** - ギャラリーに適用します。  ユーザーがデータ エントリ フォームで加えたすべての変更が 1 つにまとめられます。
* **[Update](functions/function-update-updateif.md)** - テキスト入力コントロールやスライダーなどの入力コントロールに適用します。 ギャラリーの個々のプロパティを 1 つにまとめて設定します。

## <a name="record-scope"></a>レコード スコープ
関数の中には、テーブル内のすべてのレコードについて個別に数式を評価して演算を行うものがあります。  数式の結果は、さまざまな方法で使用されます。  

* **Filter**、**Lookup** - 該当するレコードを出力に含めるかどうかを指定します。
* **Sort** - レコードを並べ替える基準となる値を指定します。
* **Concat** - 連結する文字列を指定します。
* **ForAll** - 該当するすべての値を返すことができます。副作用が生じる可能性もあります。
* **Distinct** - 値を 1 つ返します。重複したレコードを識別するために使用します。  
* **AddColumns** - 追加されるフィールドの値を指定します。
* **Average**、**Max**、**Min**、**Sum**、**StdevP**、**VarP** - 集計する値を指定します。

これらの数式内では、処理するレコードのフィールドを参照できます。  関数が実行されると、数式を評価するための "レコード スコープ" が作成されます。この範囲にあるレコードのフィールドが最上位の識別子として使用されます。  また、コントロール プロパティやその他の値はアプリのどこからでも参照できます。

例として、次のような **Products** というテーブルがあるとします。

![](media/working-with-tables/requested.png)

これらの製品 (Product) の中に、リクエストされた数量 (Quantity Requested) が在庫数量 (Quantity Available) を超えている製品がないかを調べるには、次の数式を使用します。

**Filter( Products, 'Quantity Requested' > 'Quantity Available' )**

**Filter** の 1 つ目の引数は演算対象のレコードがあるテーブルで、2 つ目の引数は数式です。  **Filter** 関数を実行すると、この数式を評価するためのレコード スコープが作成されます。この範囲にある各レコードのフィールドが評価の対象となります。上の例では、**Product**、**Quantity Requested**、**Quantity Available** です。  数式の評価 (この例では比較) によって、関数の結果に各レコードを含めるかどうかが判断されます。

![](media/working-with-tables/needed.png)

この例に数式を追加して、各製品の注文数量を計算できます。

**AddColumns( Filter( Products, 'Quantity Requested' > 'Quantity Available' ), "Quantity To Order", 'Quantity Requested' - 'Quantity Available' )**

上の数式では、計算された列が結果に追加されます。  **AddColumns** では、リクエストされた数量と在庫数量の差の計算に使用するレコード スコープが作成されます。

![](media/working-with-tables/toorder.png)

最後に、結果のテーブルを必要な列だけに絞ることができます。

**ShowColumns( AddColumns( Filter( Products, 'Quantity Requested' > 'Quantity Available' ), "Quantity To Order", 'Quantity Requested' - 'Quantity Available' ), "Product", "Quantity To Order" )**

![](media/working-with-tables/toorderonly.png)

上の数式では、二重引用符 (") を使用している箇所と一重引用符 (') を使用している箇所があります。  一重引用符は、フィールドやテーブルなどのオブジェクトの値を参照する際に使用します。オブジェクトの名前にはスペースが含まれています。  二重引用符は、オブジェクトの値を参照するのではなく、オブジェクトの値を表す際、特に **AddColumns** のときのように、オブジェクトがまだ存在しない状況で使用します。  

### <a name="disambiguation"></a>曖昧性の除去
レコード スコープによって追加されたフィールド名は、アプリの別の場所にある同じ名前をオーバーライドします。  このような状況が発生した場合でも、[**@** 曖昧性除去](functions/operators.md)演算子を使用すれば、レコード スコープの外部の値にアクセスできます。

* 入れ子になったレコード スコープの値にアクセスするには、次のパターンを使用した操作対象のテーブルの名前の **@** 演算子を使います。<br>_Table_**[@**_フィールド名_**]**
* データ ソース、コレクション、コンテキスト変数などのグローバル値にアクセスするには、**[@**_オブジェクト名_**]** のパターンを使用します (テーブルは指定しません)。

演算対象のテーブルが **Filter(** _テーブル_**,** ... **)** のような式である場合は、曖昧性除去演算子を使用することはできません。  最も内側のレコード スコープのみが、曖昧性除去演算子を使用せずに、このテーブル式のフィールドにアクセスできます。

たとえば、次のようなコレクション **X** があるとします。

![](media/working-with-tables/X.png)

このコレクションは、**ClearCollect( X, \[1, 2\] )** で作成できます。

また、次のようなコレクション **Y** があります。

![](media/working-with-tables/Y.png)

このコレクションは、**ClearCollect( Y, ["A", "B"] )** で作成できます。

さらに、**Value** というコンテキスト変数を、数式 **UpdateContext( {Value: "!"} )** で定義します。

これらを 1 つにまとめましょう。  この状況では、次の数式を使用できます。

* **Ungroup( ForAll( X, ForAll( Y, Y[@Value] & Text( X[@Value] ) & [@Value] ) ), "Value" )**

次のテーブルが生成されます。

![](media/working-with-tables/XY.png)

数式を詳しく見てみましょう。  最も外側の **ForAll** 関数によって **X** のレコード スコープが定義されます。これにより、処理の際に各レコードの **Value** フィールドにアクセスできます。  フィールドには **Value** という語か **X[@Value]** を使用してアクセスできます。

最も内側の **ForAll** 関数では、**Y** のレコード スコープが定義されます。このテーブルにも **Value** フィールドが定義されているため、ここでも **Value** を使用して **Y** のレコード内のフィールドを参照しています。**X** のフィールドは参照されません。ここで **X** 内の **Value** フィールドにアクセスする場合は、曖昧性除去演算子を使用して、もっと長い数式を作成する必要があります。

**Y** は最も内側にあるレコード スコープなので、このテーブルのフィールドにアクセスする際に曖昧性除去は必要ありません。次の数式を使用して同じ結果を返すことができます。

* **Ungroup( ForAll( X, ForAll( Y, Value & Text( X[@Value] ) & [@Value] ) ), "Value" )**

すべての **ForAll** レコード スコープはグローバル スコープをオーバーライドします。  上で定義した **Value** コンテキスト変数は、曖昧性除去演算子がなければ名前で参照することができません。   この値にアクセスするには **[@Value]** を使用する必要があります。

入れ子になった **ForAll** 関数は入れ子になったテーブルを返すため、**Ungroup** で結果をフラット化しています。

## <a name="inline-syntax"></a>インライン構文
### <a name="records"></a>レコード
レコードを表すには、名前付きフィールドの値を中かっこで囲みます。  たとえば、次の数式で、このトピックの冒頭に出てきたテーブル内の 1 つ目のレコードを表すことができます。

**{ Name: "Chocolate", Price: 3.95, 'Quantity on Hand': 12, 'Quantity on Order': 10 }**

次の例に示すように、数式を他の数式に埋め込むこともできます。

**{ Name: First(Products).Name, Price: First(Products).Price * 1.095 }**

次の例に示すように、中かっこを入れ子にすると、レコードを入れ子にすることができます。

**{ 'Quantity': { 'OnHand': ThisItem.QuantOnHand, 'OnOrder': ThisItem.QuantOnOrder } }**

空白やコロンなどの特殊文字が含まれている列名は一重引用符で囲みます。  列名の中で一重引用符を使用するには、一重引用符を二重に使用します。

**Price** 列内の値にドル記号などの通貨記号が含まれていない点に注意してください。 この書式は、値が表示される際に適用されます。  

### <a name="tables"></a>テーブル
テーブルの作成には、**[Table](functions/function-table.md)** 関数とレコードのセットを使用します。 このトピックの冒頭で出てきたテーブルを、次の数式で表すことができます。

**Table( { Name: "Chocolate", Price: 3.95, 'Quantity on Hand': 12, 'Quantity on Order': 10 },<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{ Name: "Bread", Price: 4.95, 'Quantity on Hand': 34, 'Quantity on Order': 0 },<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{ Name: "Water", Price: 4.95, 'Quantity on Hand': 10, 'Quantity on Order': 0 } )**

また、次の数式で、テーブルを入れ子にすることができます。

**Table( { Name: "Chocolate",<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;'Quantity History': Table( { Quarter: "Q1", OnHand: 10, OnOrder: 10 },<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{ Quarter: "Q2", OnHand: 18, OnOrder: 0 } ) } )**

### <a name="value-tables"></a>値のテーブル
単一列テーブルを作成するには、値を角かっこで指定します。 結果として返されるテーブルには、**Value** という名前の列が 1 つだけ含まれています。

たとえば、**[ 1, 2, 3, 4 ]** は、**Table( { Value: 1 }, { Value: 2 }, { Value: 3 }, { Value: 4 } )** と等しく、次のテーブルを返します。

![](media/working-with-tables/inline-table.png)


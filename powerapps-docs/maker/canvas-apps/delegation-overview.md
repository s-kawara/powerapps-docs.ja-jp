---
title: 委任について | Microsoft Docs
description: 委任を使用すると、大規模なデータ セットが効率的に処理されます。
documentationcenter: na
author: gregli-msft
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: conceptual
ms.component: canvas
ms.date: 03/27/2018
ms.author: gregli
ms.openlocfilehash: 0800adf43f5a7d74d0334e9f39216a70b9350d6d
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "31838058"
---
# <a name="understand-delegation"></a>委任について
PowerApps には、データのフィルター処理、並べ替え、およびテーブルの整形を行う強力な一連の関数が用意されています。たとえば、**[Filter](functions/function-filter-lookup.md)**、**[Sort](functions/function-sort.md)**、**[AddColumns](functions/function-table-shaping.md)** 関数があります。  これらの関数を使用すると、ユーザーが必要とする情報に絞り込んでアクセスするようにすることができます。  データベースに関する知識がある方にとっては、これらの関数の使用はデータベース クエリの記述に似ています。  

効率的なアプリを構築する鍵は、デバイスに取り込む必要があるデータの量を最小限に抑えることにあります。  おそらく、何百万件ものレコードがあっても必要なレコードはごく一部です。また、1 つの集計値で何千件ものレコードを表すことができます。  さらに、先頭のレコード セットのみを取得し、残りはユーザーが要求したときに取得することもできます。  レコードを絞り込むことで、アプリに必要な処理能力、メモリ、およびネットワーク帯域幅を大幅に削減できます。その結果、携帯ネットワークで接続している電話でも、ユーザーへの応答時間が短縮されます。  

*委任*では、PowerApps の数式の表現力により、ネットワーク経由で移動するデータを最小限に抑えるというニーズに対応できます。  つまり、委任とは、PowerApps がデータをアプリに移動してローカルで処理せずに、データの処理をデータ ソースに委任することです。  

委任が複雑であり、この記事が存在する理由は、PowerApps の数式で表現できるすべての処理をすべてのデータ ソースに委任できるわけではないからです。  PowerApps 言語は Excel の数式言語によく似ており、さまざまな数値操作関数やテキスト操作関数を使用して、メモリ内のブック全体に完全かつ瞬時にアクセスできるように設計されています。  そのため、SQL Server などの強力なデータベース エンジンを始め、ほとんどのデータ ソースよりも機能が充実しています。

**大規模なデータ セットを操作するには、委任できるデータ ソースと数式を使用する必要があります。**  これが、アプリの高いパフォーマンスを維持し、ユーザーが必要とするすべての情報にアクセスできるようにする唯一の方法です。 委任できない箇所を示す[青い点の修正候補](delegation-overview.md#blue-dot-suggestions)に注意してください。  小規模なデータ セット (500 件未満のレコード) を操作する場合は、数式を委任できなければ処理をローカルで実行できるため、どのデータ ソースと数式でも使用できます。 

## <a name="delegable-data-sources"></a>委任可能なデータ ソース
委任をサポートしているソース データとサポート範囲の完全な一覧については、[委任の一覧](delegation-list.md)を参照してください。

今後も既存のデータ ソースへの委任のサポートを追加するだけでなく、データ ソースも追加していきます。

インポートされた Excel ブック ("静的データをアプリに追加します" データ ソースを使用)、コレクション、およびコンテキスト変数に格納されたテーブルには、委任が不要です。 これらのデータはすべてメモリ内に既にあり、PowerApps 言語をすべて適用できます。

## <a name="delegable-functions"></a>委任可能な関数
次の手順では、委任できる数式のみを使用します。 ここに含まれるのは、委任できる数式の要素です。  ただし、データ ソースはすべて異なっており、すべてのデータ ソースでこれらの要素がすべてサポートされているわけではありません。 数式を作成する際は、青い点の修正候補の有無を確認してください。

この一覧は随時変更されます。 より多くの関数と演算子で委任がサポートされるよう取り組んでいます。

### <a name="filter-functions"></a>フィルター関数
**[Filter](functions/function-filter-lookup.md)****[Search](functions/function-filter-lookup.md)**、および **[LookUp](functions/function-filter-lookup.md)** は委任できます。  

**Filter** 関数と **LookUp** 関数内では、以下をテーブルの列と組み合わせて使用して、適切なレコードを選択できます。

* **[And](functions/function-logicals.md)** (**[&&](functions/operators.md)** を含む)、**[Or](functions/function-logicals.md)** (**[||](functions/operators.md)** を含む)、**[Not](functions/function-logicals.md)** (**[!](functions/operators.md)** を含む)
* **[In](functions/operators.md)**
* **[=](functions/operators.md)**、**[<>](functions/operators.md)**、**[>=](functions/operators.md)**、**[<=](functions/operators.md)**、**[>](functions/operators.md)**、**[<](functions/operators.md)**
* **[+](functions/operators.md)**、**[-](functions/operators.md)**
* **[TrimEnds](functions/function-trim.md)**
* **[IsBlank](functions/function-isblank-isempty.md)**
* **[StartsWith](functions/function-startswith.md)**
* コントロール プロパティや[グローバルとコンテキスト変数](working-with-variables.md)のように、すべてのレコードで定数値となるものです。

すべてのレコードで 1 つの定数値に評価される数式の一部を使用することもできます。  たとえば、**Left( Language(), 2 )** は、レコードのどの列にも依存していないため、すべてのレコードに対して同じ値を返します。  実質的には定数です。  コンテキスト変数、コレクション、および信号を使用した場合は、定数でない可能性があるため、**Filter** および **LookUp** は委任できなくなります。  

上記の一覧に記載されていない重要な項目:

* **[If](functions/function-if.md)**
* **[*](functions/operators.md)**、**[/](functions/operators.md)**、**[Mod](functions/function-mod.md)**
* **[Concatenate](functions/function-concatenate.md)** (**[&](functions/operators.md)** を含む)
* **[ExactIn](functions/operators.md)**
* 文字列操作関数: **[Lower](functions/function-lower-upper-proper.md)**、**[Upper](functions/function-lower-upper-proper.md)**、**[Left](functions/function-left-mid-right.md)**、**[Mid](functions/function-left-mid-right.md)**、**[Len](functions/function-left-mid-right.md)**、...
* 信号: **[Location](functions/signals.md)**、**[Acceleration](functions/signals.md)**、**[Compass](functions/signals.md)**、...
* 可変: **[Now](functions/function-now-today-istoday.md)**、**[Today](functions/function-now-today-istoday.md)**、**[Rand](functions/function-rand.md)**、...
* [コレクション](working-with-variables.md)

### <a name="sorting-functions"></a>並べ替え関数
**[Sort](functions/function-sort.md)** と **[SortByColumns](functions/function-sort.md)** は委任できます。  

**Sort** の数式には、1 つの列の名前のみを指定できます。他の演算子や関数を含めることはできません。

### <a name="aggregate-functions"></a>集計関数
**[Sum](functions/function-aggregates.md)**、**[Average](functions/function-aggregates.md)**、**[Min](functions/function-aggregates.md)**、および **[Max](functions/function-aggregates.md)** を委任できます。  現時点では、限定された数のデータ ソースがこの委任をサポートしています。詳細については、[委任一覧](delegation-list.md)に関するページをご覧ください。

**[CountRows](functions/function-table-counts.md)**、**[CountA](functions/function-table-counts.md)**、および **[Count](functions/function-table-counts.md)** などのカウント関数は委任できません。

**[StdevP](functions/function-aggregates.md)** および **[VarP](functions/function-aggregates.md)** などの他の集計関数についても委任できません。

## <a name="non-delegable-functions"></a>委任できない関数
以下の関数を含むその他すべての関数では、委任がサポートされません。

* テーブルの整形: **[AddColumns](functions/function-table-shaping.md)**、**[DropColumns](functions/function-table-shaping.md)**、**[ShowColumns](functions/function-table-shaping.md)**、...
* **[First](functions/function-first-last.md)**、**[FirstN](functions/function-first-last.md)**、**[Last](functions/function-first-last.md)**、**[LastN](functions/function-first-last.md)**
* **[Concat](functions/function-concatenate.md)**
* **[Collect](functions/function-clear-collect-clearcollect.md)**、**[ClearCollect](functions/function-clear-collect-clearcollect.md)**
* **[CountIf](functions/function-table-counts.md)**、**[RemoveIf](functions/function-remove-removeif.md)**、**[UpdateIf](functions/function-update-updateif.md)**
* **[GroupBy](functions/function-groupby.md)**、**[Ungroup](functions/function-groupby.md)**

一般的なパターンでは、**AddColumns** と **LookUp** を使用して、1 つのテーブルの情報を別のテーブルにマージします。これは、データベース用語では一般に結合と呼ばれます。  例:

**AddColumns( Products, "Supplier Name", LookUp( Suppliers, Suppliers.ID = Product.SupplierID ).Name )**

**LookUp** は委任可能な関数ですが、**Products** と **Suppliers** が委任可能なデータ ソースであっても、**AddColumns** 関数は委任できません。  数式全体の結果は、**Products** データ ソースの先頭部分に制限されます。  

**LookUp** とそのデータ ソースは委任可能なため、大規模でも、データ ソース内のどこかで **Suppliers** の一致が見つかる可能性があります。  潜在的な欠点は、**LookUp** により、**Products** の先頭の各レコードについて個別にデータ ソースへの呼び出しが行われるため、ネットワーク上でのやり取りが大量に発生することです。  **Suppliers** が十分小さく、頻繁に変更されない場合は、代わりに、アプリの起動時に **Collect** 呼び出しを使用してデータ ソースをアプリにキャッシュし (最初の画面で [**OnVisible**](controls/control-screen.md) を使用します)、キャッシュに対して **LookUp** を実行します。  

## <a name="non-delegable-limits"></a>委任できない場合の制限
委任できない数式は、ローカルで処理されます。  これにより、PowerApps の数式言語をすべて使用できます。  ただし、欠点があります。最初にすべてのデータをデバイスに取り込む必要があるため、ネットワーク経由で大量のデータを取得する可能性があります。  その処理には時間がかかり、アプリの動作が遅いとか、ハングしているかもしれないという印象を与える可能性があります。

この問題を回避するために、PowerApps では、ローカルで処理可能なデータの量を既定で 500 件のレコードに制限しています。  この数字を選択したのは、小規模なデータ セットには変わらず完全にアクセスでき、大規模なデータ セットでは部分的な結果を確認して使い方を改善できるためです。

この機能は、ユーザーの混乱を招く可能性があるため、使用する際は当然注意が必要です。  たとえば、100 万件のレコードがあるデータ ソースに対する、委任できない選択数式の **Filter** 関数があるとします。  フィルター処理はローカルで実行されるため、100 万件のレコードのうち先頭の 500 件だけがスキャンされます。  目的のレコードがレコード 501 または 500,001 の場合、**Filter** では考慮されず、返されません。

また、集計関数でも混乱を招く可能性があります。  100 万件のレコードがある同じデータ ソースの 1 つの列の**平均**を計算します。  **Average** はまだ委任できないため、先頭の 500 件のレコードのみの平均が計算されます。  注意が必要です。アプリのユーザーが部分的な回答を完全な回答と誤解する可能性があります。

## <a name="changing-the-limit"></a>制限の変更

既定のレコード数は、500 件です。  この数を変更するには [ファイル] タブに移動し、左側のナビゲーション ウィンドウの [App Settings]\(アプリ設定)\ を選択し、[試験的な機能] の下を確認します。  ここで "Data row limit for non-delegable queries\(委任できないクエリのデータ行の制限\)" 設定の数を 1 から 2000 の間で変更することができます。  この設定はアプリ全体に適用されます。

場合によっては、2000 (または 1000 や 1500) の方がシナリオのニーズに適していることがあるでしょう。  シナリオに合わせて、この数を慎重に増やしてください。  この数を増やすと、特に列の数が多く幅が広いテーブルで、アプリのパフォーマンスが低下する場合があります。  それでも、可能な限り多く委任することが最善の方法です。

アプリが大規模なデータ セットに合わせて拡張できるようにするには、この設定を 1 まで減らしてください。  委任できない場合は、アプリのテストのタイミングが見つけやすくなるように、必ず単一のレコードのみが返されます。  これにより、概念実証アプリを運用するときに予想外の事態が発生することを回避できます。

## <a name="blue-dot-suggestions"></a>青い点の修正候補
委任されるかどうかを簡単に確認できるように、作成時に数式に委任できないものが含まれている場合に青い点の修正候補が表示されます。

青い点は、委任可能なデータ ソースを操作する数式にのみ表示されます。  青い点が表示されないものの、数式が適切に委任されていないと思われる場合は、上記の<a href="#delegable-data-sources">委任可能なデータ ソース</a>の一覧でデータ ソースの種類を確認してください。

## <a name="examples"></a>例
この例では、商品 (具体的には果物) を含む **[dbo].[Products]** という名前の SQL Server テーブルを使用します。  PowerApps では、[新しい画面] でこのデータ ソースに接続する 3 つの画面から成る基本的なアプリを作成できます。

![3 画面アプリ](./media/delegation-overview/products-afd.png)

ギャラリーの **Items** プロパティの数式に注目してください。  **SortByColumns** 関数と **Search** 関数を使用しています。どちらも委任できます。

検索テキスト入力コントロールに「**Apple**」と入力します。  注意して見ると、新しい検索の新しいエントリの処理中に、少しの間、画面の上部で点が動いているのがわかります。  点が動いているのは、SQL Server と通信していることを示しています。

![検索テキスト入力コントロール](./media/delegation-overview/products-apple.png)

これはすべて委任できるため、**[dbo].[Products]** テーブルに何百万件ものレコードが含まれていても、すべてが検索されます。ユーザーが結果をスクロールすると、ギャラリー内のページが移動します。

ご覧のように、"Apple" と "Pineapple" の両方に一致しています。  **Search** 関数では、テキスト列内全体から検索語句を探します。  それでは、代わりに、果物の名前の先頭のみで検索語句を検索してみましょう。  別の委任可能な関数である **Filter** を使用すると、より複雑な検索語句を指定できます (わかりやすくするために、**SortByColumns** 呼び出しを削除します)。

![SortByColumns 呼び出しを削除する](./media/delegation-overview/products-apple-bluedot.png)

これは正常に機能しているようで、**"Apples"** だけ表示され、**"Pineapple"** は表示されていません。  ただし、ギャラリーの横に青い点が表示され、数式の一部分の下に青い波線があります。  画面上のサムネイルにも青い点が表示されています。  ギャラリーの横にある青い点をポイントすると、次のメッセージが表示されます。

![青い点をポイントする](./media/delegation-overview/products-apple-bluepopup.png)

委任可能なデータ ソースである SQL Server と委任可能な **Filter** 関数を使用しているものの、**Filter** 内で使用した数式は委任可能ではありません。  **Mid** と **Len** はどのデータ ソースにも委任できません。

それでも、一応  機能しています。  これが、注意を促す黄色のアイコンや赤色の波線エラーではなく、青い点が表示される理由です。  **[dbo].[Products]** テーブルに含まれているレコードは 500 件未満なので、問題なく機能しました。   すべてのレコードがデバイスに取り込まれ、**Filter** がローカルで適用されました。  

このテーブルに含まれているレコードが 500 件を超える場合は、"*テーブルの 500 件の先頭レコード内の*" **"Apple"** で始まる果物だけがギャラリーに表示されます。  レコード 501 または 500,001 に **"Apple, Fuji"** という名前が含まれていても、見つかりません。

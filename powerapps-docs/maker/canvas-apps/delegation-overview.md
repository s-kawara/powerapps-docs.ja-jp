---
title: キャンバス アプリでの委任について | Microsoft Docs
description: 委任を使用すると、キャンバス アプリで大規模なデータ セットが効率的に処理されます。
author: lancedMicrosoft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 07/05/2018
ms.author: lanced
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 61a7e67b7914e5f844397389833f830244d5af28
ms.sourcegitcommit: 4ed29d83e90a2ecbb2f5e9ec5578e47a293a55ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63318099"
---
# <a name="understand-delegation-in-a-canvas-app"></a>キャンバス アプリでの委任について
PowerApps には、キャンバスアプリでデーターのテーブルをフィルター処理、並べ替え、および整形するための強力な一連の機能があります。数例を挙げると **[フィルター](functions/function-filter-lookup.md)** 、 **[並べ替え](functions/function-sort.md)**、および **[AddColumns](functions/function-table-shaping.md)** などの関数です。これらの関数を使用すると、ユーザーが必要とする情報を絞り込んでアクセスすることができます。 データベースに関する知識がある方にとっては、これらの関数の使用はデータベース クエリの記述に似ています。

効率的なアプリを構築する鍵は、デバイスに取り込む必要があるデータの量を最小限に抑えることにあります。 おそらく、何百万件ものレコードがあっても必要なレコードはごく一部です。また、1 つの集計値で何千件ものレコードを表すことができます。 さらに、先頭のレコード セットのみを取得し、残りはユーザーが要求したときに取得することもできます。 レコードを絞り込むことで、アプリに必要な処理能力、メモリ、ネットワーク帯域幅を大幅に削減できます。その結果、携帯ネットワークで接続している電話でも、ユーザーへの応答時間が短縮されます。 

*委任* では、PowerApps の数式の表現力により、ネットワーク経由で移動するデータを最小限に抑えるというニーズに対応できます。 つまり、PowerApps はデータをアプリに移動してローカルで処理せずに、データの処理をデータ ソースに委任します。

委任が複雑であり、この記事が存在する理由は、PowerApps の数式で表現できるすべての処理をすべてのデータ ソースに委任できるわけではないからです。 PowerApps 言語は メモリ内のブック全体に瞬時にアクセスできるように設計された Excel の数式言語に似ており、さまざまな数値操作関数やテキスト操作関数を備えています。そのため、SQL Server などの強力なデータベース エンジンを始め、ほとんどのデータ ソースよりも機能が充実しています。

**大規模なデータ セットを操作するには、委任できるデータ ソースと数式を使用する必要があります。** これが、アプリの高いパフォーマンスを維持し、ユーザーが必要とするすべての情報にアクセスできるようにする唯一の方法です。 委任が利用できない場所を示す委任の警告に留意してください。 小規模なデータ セット (500 件未満のレコード) を操作する場合は、式を委任できなくてもアプリはデータをローカルに処理できるため、任意のデータ ソースと式を使用できます。 

> [!NOTE]
> 以前の PowerApps では、委任の警告に "青いドット" の修正候補フラグが設定されていましたが、委任の修正候補は警告として再分類されています。 データ ソースのデータが 500 レコードを超えて、関数を委任できない場合、PowerApps はすべてのデータを取得できない可能性があり、結果が正しくなくなることがあります。 委任の警告は、正しい結果が得られるようにアプリを管理するのに役立ちます。

## <a name="delegable-data-sources"></a>委任可能なデータ ソース
委任は、特定の表形式のデータ ソースのみサポートされます。 データ ソースは、委任をサポートしている場合、[コネクタ ドキュメント](https://docs.microsoft.com/connectors/)でサポートするについて説明します。 たとえば、最も人気のあるこれらの表形式のデータ ソースと委任がサポートされています。

- [Common Data Service](https://docs.microsoft.com/connectors/commondataservice/) 
- [SharePoint](https://docs.microsoft.com/connectors/sharepointonline/) 
- [SQL Server](https://docs.microsoft.com/connectors/sql/) 

インポートされたExcel ブック (**静的データをアプリに追加します。** を使用)、コレクション、およびコンテキスト変数に格納されたテーブルには委任は必要ありません。 これらのデータはすべてメモリ内に既にあり、PowerApps 言語をすべて適用できます。

## <a name="delegable-functions"></a>委任可能な関数
次の手順では、委任できる数式のみを使用します。 ここに含まれるのは、委任できる数式の要素です。 ただし、データ ソースはすべて異なっており、すべてのデータ ソースでこれらの要素がすべてサポートされているわけではありません。 特定の式で委任の警告を確認します。

この一覧は随時変更されます。 より多くの関数と演算子で委任がサポートされるよう取り組んでいます。

### <a name="filter-functions"></a>フィルター関数
**[Filter](functions/function-filter-lookup.md)**, **[Search](functions/function-filter-lookup.md)**、および **[LookUp](functions/function-filter-lookup.md)** は委任できます。  

**Filter** 関数と **LookUp** 関数内では、テーブルの列でこれらを使用して、適切なレコードを選択できます。

* **[And](functions/function-logicals.md)** (**[&&](functions/operators.md)** を含む)、**[Or](functions/function-logicals.md)** (**[||](functions/operators.md)** を含む)、**[Not](functions/function-logicals.md)** (**[!](functions/operators.md)** を含む)
* **[In](functions/operators.md)**
* **[=](functions/operators.md)**、**[<>](functions/operators.md)**、**[>=](functions/operators.md)**、**[<=](functions/operators.md)**、**[>](functions/operators.md)**、**[<](functions/operators.md)**
* **[+](functions/operators.md)**、**[-](functions/operators.md)**
* **[TrimEnds](functions/function-trim.md)**
* **[IsBlank](functions/function-isblank-isempty.md)**
* **[StartsWith](functions/function-startswith.md)**、  **[EndsWith](functions/function-startswith.md)**
* コントロール プロパティや[グローバルとコンテキスト変数](working-with-variables.md)のように、すべてのレコードで定数値となるものです。

また、すべてのレコードで 1 つの定数値に評価される式の一部を使用することもできます。 たとえば、 **Left (Language(), 2)**、**日付 (2019、3、31)**、および**Today()** は、レコードのどの列にも依存しないため、すべてのレコードの同じ値を返します。 これらの値は定数としてデータ ソースに送信することができ、委任はブロックされません。 

上のリストには、これらの注目すべき項目は含まれません。

* **[If](functions/function-if.md)**
* **[*](functions/operators.md)**、**[/](functions/operators.md)**、**[Mod](functions/function-mod.md)**
* **[Concatenate](functions/function-concatenate.md)** (**[&](functions/operators.md)** を含む)
* **[ExactIn](functions/operators.md)**
* 文字列操作関数:**[Lower](functions/function-lower-upper-proper.md)**、 **[Upper](functions/function-lower-upper-proper.md)**、 **[Left](functions/function-left-mid-right.md)**、 **[Mid](functions/function-left-mid-right.md)**、  **[Len](functions/function-left-mid-right.md)**、.
* 信号:**[Location](functions/signals.md)**、 **[Acceleration](functions/signals.md)**、  **[Compass](functions/signals.md)**、.
* 可変:**[Rand](functions/function-rand.md)**、.
* [Collections](working-with-variables.md)

### <a name="sorting-functions"></a>並べ替え関数
**[Sort](functions/function-sort.md)** と **[SortByColumns](functions/function-sort.md)** は委任できます。

**Sort** の数式には、1 つの列の名前のみを指定できます。他の演算子や関数を含めることはできません。

### <a name="aggregate-functions"></a>集計関数
**[Sum](functions/function-aggregates.md)**、**[Average](functions/function-aggregates.md)**、**[Min](functions/function-aggregates.md)**、および **[Max](functions/function-aggregates.md)** を委任できます。 現時点では、限定された数のデータ ソースがこの委任をサポートしています。詳細については、[委任一覧](delegation-list.md)に関するページをご覧ください。

**[CountRows](functions/function-table-counts.md)**、**[CountA](functions/function-table-counts.md)**、**[Count](functions/function-table-counts.md)** などのカウント関数は委任できません。

**[StdevP](functions/function-aggregates.md)** および **[VarP](functions/function-aggregates.md)** などの他の集計関数についても委任できません。

### <a name="table-shaping-functions"></a>テーブル整形関数

**[AddColumns](functions/function-table-shaping.md)**、 **[DropColumns](functions/function-table-shaping.md)**、 **[RenameColumns](functions/function-table-shaping.md)**、および **[ShowColumns](functions/function-table-shaping.md)** 委任は部分的にサポートします。  その引数で数式を委任できます。  ただし、これらの関数の出力は、委任レコード以外の制限があります。

この例では、作成者が多くの場合、**AddColumns**と**ルックアップ**を使用して、あるテーブルの情報を別のテーブルにマージします。これは、一般にデータベース用語での結合とも呼ばれます。

```powerapps-dot
AddColumns( Products, 
    "Supplier Name", 
    LookUp( Suppliers, Suppliers.ID = Product.SupplierID ).Name 
)
```

**製品**と**Suppliers**が委任可能なデータ ソースであり、**ルックアップ**委任可能な関数であっても、 **AddColumns**関数の出力は、委任可能なではありません。 全体の数式の結果は、**製品**データ ソースの最初の部分に限定されます。 **LookUp** 関数とそのデータ ソースは委任可能なため、大規模でも、データ ソース内のどこかで **Suppliers** の一致が見つかる可能性があります。 

この方法で**AddColumns**を使用すると、**ルックアップ**は**製品**内の最初のレコードごとにデータソースを個別に呼び出す必要があるため、多くのネットワークのチャネリングが発生します。**Suppliers**が十分に小さくて、頻繁に変更されない場合は、**関数[ **OnStart** ](functions/signals.md)で**Collect関数**を呼び出し、起動時にデーターソースをアプリにキャッシュすることができます。別の方法として、ユーザーが要求したときにのみ関連レコードを取得するようにアプリを再構築することもできます。  
 
## <a name="non-delegable-functions"></a>委任できない関数
以下の関数を含むその他すべての関数では、委任がサポートされません。

* **[First](functions/function-first-last.md)**、**[FirstN](functions/function-first-last.md)**、**[Last](functions/function-first-last.md)**、**[LastN](functions/function-first-last.md)**
* **[Choices](functions/function-choices.md)**
* **[Concat](functions/function-concatenate.md)**
* **[Collect](functions/function-clear-collect-clearcollect.md)**、**[ClearCollect](functions/function-clear-collect-clearcollect.md)**
* **[CountIf](functions/function-table-counts.md)**、**[RemoveIf](functions/function-remove-removeif.md)**、**[UpdateIf](functions/function-update-updateif.md)**
* **[GroupBy](functions/function-groupby.md)**、**[Ungroup](functions/function-groupby.md)**

## <a name="non-delegable-limits"></a>委任できない場合の制限
委任できない数式は、ローカルで処理されます。 これにより、PowerApps の数式言語をすべて使用できます。 ただし、欠点があります。最初にすべてのデータをデバイスに取り込む必要があるため、ネットワーク経由で大量のデータを取得する可能性があります。 その処理には時間がかかり、アプリの動作が遅いとか、クラッシュしているかもしれないという印象を与える可能性があります。

これを回避するには、PowerApps のローカルで処理できるデータ量に制限しています。既定では 500 件のレコード。  この数字を選択したのは、小規模なデータ セットには変わらず完全にアクセスでき、大規模なデータ セットでは部分的な結果を確認して使い方を改善できるためです。

この機能は、ユーザーの混乱を招く可能性があるため、使用する際は当然注意が必要です。 たとえば、100 万件のレコードを含むデータ ソースに対する、委任できない選択数式の **Filter** 関数があるとします。 フィルター処理はローカルに行われるため、最初の 500 レコードのみがスキャンされます。 目的のレコードがレコード 501 や 500,001 の場合、**Filter** では考慮されず、返されません。

集計関数も混乱を招く可能性があります。 100 万件のレコードがある同じデータ ソースの 1 つの列の**平均**を計算します。 **Average** はまだ委任できないため、先頭の 500 件のレコードのみの平均が計算されます。 注意しないと、アプリのユーザーが部分的な回答を完全な回答と誤解する可能性があります。

## <a name="changing-the-limit"></a>制限の変更
500 が既定のレコード数ですが、アプリ全体についてこの値を変更することができます。

1. **[ファイル]** タブの **[アプリの設定]**、**[詳細設定]** を選択します。
2. **[詳細設定]** で、**[委任できないクエリのデータ行の制限]** の設定を 500 から 2,000 に変更します。

場合によっては、2,000 (または 1,000 や 1,500) の方がシナリオのニーズに適していることがあるでしょう。 シナリオに合わせて、この数を慎重に増やしてください。 この数を増やすと、特に列の数が多く幅が広いテーブルで、アプリのパフォーマンスが低下する場合があります。 やはり、最もいいのはできる限り委任することです。

アプリが大規模なデータ セットに合わせて拡張できるようにするには、この設定を 1 まで減らしてください。 委任できないものはすべて、アプリのテストのタイミングが見つけやすくなるように、単一のレコードを返します。 これにより、概念実証アプリを運用するときに予想外の事態が発生することを回避できます。

## <a name="delegation-warnings"></a>委任の警告
委任されるものとされないものを見分けやすいように、PowerApps では、委任できないものを含む式を作成すると、警告 (黄色の三角形) が表示されます。

委任の警告は、委任可能なデータ ソースを操作する式にのみ表示されます。 警告が表示されないものの、式が適切に委任されていないと思われる場合は、前に示した[委任可能なデータ ソース](delegation-overview.md#delegable-data-sources)の一覧で、データ ソースの種類を確認してください。

## <a name="examples"></a>例
この例では、**[dbo].[Fruit]** という名前の SQL Server テーブルを基にして、3 画面のアプリを自動的に生成します。 アプリを生成する方法についてで同様の原則を適用することができます、 [Common Data Service に関するトピック](data-platform-create-app.md)SQL サーバーにします。

![3 画面アプリ](./media/delegation-overview/products-afd.png)

ギャラリーの **Items** プロパティは、**SortByColumns** 関数と **Search** 関数を含む式に設定されています。どちらの関数も委任できます。

検索ボックスに「**Apple**」と入力します。

アプリが SQL Server と通信して検索を処理する間、画面の上部近くに動くドットが一瞬表示されます。 データ ソースに何百万ものレコードが含まれる場合でも、検索条件を満たすすべてのレコードが表示されます。

![検索テキスト入力コントロール](./media/delegation-overview/products-apple.png)

**Search** 関数はテキスト列のすべての場所を探すので、検索結果には **"Apples"**、**"Crab apples"**、**"Pineapple"** が含まれます。 果物の名前の先頭に検索語を含むレコードのみを検索する場合は、別の委任可能な関数 **Filter** でさらに複雑な検索語を使用できます。 (簡単にするため、**SortByColumns** の呼び出しは削除します。)

![SortByColumns 呼び出しを削除する](./media/delegation-overview/products-apple-delegationwarning.png)

新しい結果には、**"Apples"** は含まれますが、**"Crab apples"** や **"Pineapple"** は含まれません。  ただし、ギャラリーの横 (および、左側のナビゲーション バーにサムネイルが表示されている場合は画面のサムネイル) に黄色の三角形が表示され、式の一部分の下に青い波線が表示されます。 これらの各要素は警告を示します。 ギャラリーの横の黄色い三角形をポイントすると、次のメッセージが表示されます。

![委任の警告をポイントする](./media/delegation-overview/products-apple-yellowwarning.png)

SQL Server は委任可能なデータ ソースであり、**Filter** は委任可能な関数ですが、**Mid** と **Len** はどのデータ ソースにも委任できません。

それでも、一応 機能しています。 そしてそれこそが、これが警告であり、赤い波線ではない理由です。

- テーブルのレコードが 500 未満の場合、式は完璧に動作しました。 すべてのレコードがデバイスに取り込まれ、**Filter** がローカルで適用されました。
- テーブルのレコードが 500 を超えると、条件に一致していても、式は 501 番目以降のレコードを返しません。

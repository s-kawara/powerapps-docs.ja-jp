---
title: ForAll 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の ForAll 関数の参照情報
documentationcenter: na
author: gregli-msft
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: reference
ms.component: canvas
ms.date: 04/26/2016
ms.author: gregli
ms.openlocfilehash: 7df5e270e92930fa494ec8a30a59d46d022fd915
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "31838242"
---
# <a name="forall-function-in-powerapps"></a>PowerApps の ForAll 関数
値を計算し、[テーブル](../working-with-tables.md)のすべての[レコード](../working-with-tables.md#records)に対して操作を実行します。

## <a name="description"></a>説明
**ForAll** 関数は、テーブルのすべてのレコードについて数式を評価します。  数式は、値を計算したり、操作 (データの変更や接続の操作など) を実行したりできます。

[!INCLUDE [record-scope](../../../includes/record-scope.md)]

### <a name="return-value"></a>戻り値
各数式の評価結果はテーブルで返され、その順序は入力テーブルと同じです。

数式の結果が単一の値の場合、結果として返されるテーブルは単一列テーブルになります。  数式の結果がレコードの場合、結果として返されるテーブルには、結果のレコードと同じ列を含むレコードが格納されます。  

数式の結果が "*空白*" 値の場合、その入力レコードに対応するレコードが結果テーブルに存在しません。  この場合、結果テーブル内のレコード数は元のテーブルよりも少なくなります。

### <a name="taking-action"></a>操作の実行
この数式には、**[Patch](function-patch.md)** 関数と **[Collect](function-clear-collect-clearcollect.md)** 関数によるデータ ソースのレコードの変更など、操作を実行する関数を含めることができます。  また、この数式は、接続に対してメソッドを呼び出すこともできます。  [**;** 演算子](operators.md)を使用すると、レコードごとに複数の操作を実行できます。 **ForAll** 関数の対象であるテーブルを変更することはできません。

数式を記述する際、レコードはどのような順序でも (可能な場合は並行して) 処理できることに注意してください。  テーブルの最初のレコードが最後のレコードの後に処理される場合があります。  順序に依存しないように注意してください。  このため、**[UpdateContext](function-updatecontext.md)**、**[Clear](function-clear-collect-clearcollect.md)**、**[ClearCollect](function-clear-collect-clearcollect.md)** 関数を **ForAll** 関数内で使用することはできません。これらの関数は、この影響を受けやすい変数を保持するために簡単に使用できる可能性があります。  **[Collect](function-clear-collect-clearcollect.md)** を使用することはできますが、レコードが追加される順序は定義されていません。

**Collect**、**Remove**、**Update** など、データ ソースを変更するいくつかの関数は、戻り値として変更後のデータ ソースを返します。  このような戻り値は大きくなり、**ForAll** テーブルのレコードごとに返される場合に多くのリソースを使用する可能性があります。  また、これらの戻り値が予想したものとは異なることに気付く場合もあります。これは、**ForAll** が並行して動作できることで、これらの関数の副作用が結果の取得から切り離される可能性があるためです。  さいわいにも、**ForAll** からの戻り値が実際には使用されない場合 (データ変更関数の場合によく見られます)、戻り値は作成されないため、リソースまたは順序付けに関する懸念事項はありません。  ただし、**ForAll** の結果やデータ ソースを返す関数のいずれかを使用している場合は、結果の構築方法について慎重に考えて、最初は小さいデータ セットで試してください。  

### <a name="alternatives"></a>代替手段
PowerApps の多くの関数は、単一列テーブルを利用して複数の値を一度に処理することができます。  たとえば、**Len** 関数は、テキスト値のテーブルを処理して、**ForAll** と同じように、長さのテーブルを返すことができます。  これにより、多くの場合は **ForAll** を使用する必要性がなくなり、効率が向上し、読みやすくなります。

もう 1 つの考慮事項は、**ForAll** が委任できないのに対して、**Filter** などの他の関数は委任できることです。  

### <a name="delegation"></a>委任
[!INCLUDE [delegation-no-one](../../../includes/delegation-no-one.md)]

## <a name="syntax"></a>構文
**ForAll**( *Table*, *Formula* )

* *Table* - 必須。 操作対象のテーブル。
* *Formula* - 必須。  *Table* のすべてのレコードについて評価する数式。

## <a name="examples"></a>例
### <a name="calculations"></a>計算
次の例では、**Squares** [データ ソース](../working-with-data-sources.md)を使用します。

![](media/function-forall/squares.png)

このデータ ソースをコレクションとして作成するには、**ボタン** コントロールの **OnSelect** プロパティをこの数式に設定し、プレビュー モードを開始して、ボタンをクリックまたはタップします。

* **ClearCollect( Squares, [ "1", "4", "9" ] )**

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **ForAll(&nbsp;Squares, Sqrt(&nbsp;Value&nbsp;)&nbsp;)**<br><br>**Sqrt(&nbsp;Squares&nbsp;)** |入力テーブルのすべてのレコードについて、**Value** 列の平方根を計算します。  **Sqrt** 関数も単一列テーブルで使用できます。これにより、**ForAll** を使用しなくてもこの例を実行できます。 |<style> img { max-width: none } </style> ![](media/function-forall/sqrt.png) |
| **ForAll(&nbsp;Squares, Power(&nbsp;Value,&nbsp;3&nbsp;)&nbsp;)** |入力テーブルのすべてのレコードについて、**Value** 列の 3 乗を計算します。  **Power** 関数は、単一列テーブルをサポートしていません。 そのため、この場合は、**ForAll** を使用する必要があります。 |<style> img { max-width: none } </style> ![](media/function-forall/power3.png) |

### <a name="using-a-connection"></a>接続の使用
次の例では、**Expressions** [データ ソース](../working-with-data-sources.md)を使用します。

![](media/function-forall/translate.png)

このデータ ソースをコレクションとして作成するには、**ボタン** コントロールの **OnSelect** プロパティをこの数式に設定し、プレビュー モードを開始して、ボタンをクリックまたはタップします。

* **ClearCollect( Expressions, [ "Hello", "Good morning", "Thank you", "Goodbye" ] )**

この例では、[Microsoft Translator](../connections/connection-microsoft-translator.md) 接続も使用します。  アプリにこの接続を追加するには、[接続を管理する](../add-manage-connections.md)方法に関するトピックを参照してください。

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **ForAll( Expressions, MicrosoftTranslator.Translate( Value, "es" ) )** |Expressions テーブルのすべてのレコードについて、**Value** 列の内容をスペイン語 (略語は "es") に翻訳します。 |<style> img { max-width: none } </style> ![](media/function-forall/translate-es.png) |
| **ForAll( Expressions, MicrosoftTranslator.Translate( Value, "fr" ) )** |Expressions テーブルのすべてのレコードについて、**Value** 列の内容をフランス語 (略語は "fr") に翻訳します。 |<style> img { max-width: none } </style> ![](media/function-forall/translate-fr.png) |

### <a name="copying-a-table"></a>テーブルのコピー
場合によっては、データのフィルター処理、形成、並べ替え、操作が必要になります。  PowerApps には、**Filter**、**AddColumns**、**Sort** など、この処理を行うための多数の関数が用意されています。  PowerApps では、各テーブルが値として扱われるため、これは数式にの対象として簡単に使用できるようになります。      

さらに、後で使用できるように、この結果のコピーを作成する場合があります。  また、データ ソース間で情報を移動する場合もあります。  PowerApps には、データをコピーするための **Collect** 関数が用意されています。

ただし、コピーを作成する前に、本当に必要かどうかを十分検討してください。  数式で必要に応じて基のデータ ソースのフィルター処理や形成を行うことで、多くの状況に対処することができます。 コピーの作成の欠点のいくつかを次に示します。

* 同じ情報のコピーが 2 部あるということは、そのうち一方が同期されなくなる可能性があることを意味します。  
* コピーの作成では、多くのコンピューター メモリ、ネットワーク帯域幅、時間が使用される可能性があります。  
* ほとんどのデータ ソースでは、コピーを委任できないため、移動できるデータ量は制限されます。      

次の例では、**Products** [データ ソース](../working-with-data-sources.md)を使用します。

![](media/function-forall/prod.png)

このデータ ソースをコレクションとして作成するには、**ボタン** コントロールの **OnSelect** プロパティをこの数式に設定し、プレビュー モードを開始して、ボタンをクリックまたはタップします。

* **ClearCollect( Products, Table( { Product: "Widget", 'Quantity Requested': 6, 'Quantity Available': 3 }, { Product: "Gadget", 'Quantity Requested': 10, 'Quantity Available': 20 }, { Product: "Gizmo", 'Quantity Requested': 4, 'Quantity Available': 11 }, { Product: "Apparatus", 'Quantity Requested': 7, 'Quantity Available': 6 } ) )**

ここでの目的は、リクエストされた数量が在庫数量を超えているアイテムのみが含まれる派生テーブルを操作することです。そのためには、注文する必要があります。

![](media/function-forall/prod-order.png)  

このタスクはさまざまな方法で実行できます。すべての方法には、さまざまな長所と短所がありますが、結果は同じになります。

#### <a name="table-shaping-on-demand"></a>要求に応じたテーブルの整形
そのコピーを作成しないでください。  必要であればどこでも次の数式を使用できます。

* **ShowColumns( AddColumns( Filter( Products, 'Quantity Requested' > 'Quantity Available' ), "Quantity To Order", 'Quantity Requested' - 'Quantity Available' ), "Product", "Quantity To Order" )**

[レコード スコープ](../working-with-tables.md#record-scope)は、それぞれ各レコードの **'Quantity Requested'** フィールドと **'Quantity Available'** フィールドを使用して比較操作と減算操作を実行する **Filter** 関数と **AddColumns** 関数によって作成されます。

この例では、**Filter** 関数を委任できます。  これは、条件を満たすすべての製品を検出できるため、テーブルの多数のレコードのうちほんのわずかであっても、重要です。  この時点では、**ShowColumns** と **AddColumns** を委任できません。そのため、注文する必要がある製品の実際の数は制限されます。  この結果のサイズが常に比較的小さくなることがわかれば、この方法で十分です。

また、コピーを作成しなかったため、ほかに管理したり古くなったりする情報のコピーはありません。  

#### <a name="forall-on-demand"></a>要求に応じた ForAll
別の方法として、テーブル整形関数の代わりに **ForAll** 関数を使用します。

* **ForAll( Products, If( 'Quantity Requested' > 'Quantity Available', { Product: Product, 'Quantity To Order': 'Quantity Requested' - 'Quantity Available' } ) )**

この数式は、一部の人にとって読み書きしやすくなっている場合があります。

**ForAll** のどの部分も委任できません。  **Products** テーブルの最初の部分のみが評価されますが、このテーブルが非常に大きい場合は問題になることがあります。  **Filter** は、前の例では委任できたので、大きなデータ セットではより有効に動作する可能性があります。

#### <a name="collect-the-result"></a>結果の収集
場合によっては、データのコピーが必要になることがあります。  データ ソース間で情報を移動することが必要になる場合もあります。  この例では、ベンダーのシステム上の **NewOrder** テーブルから注文が行われます。  ユーザー操作の速度を上げるために、サーバーの待ち時間が発生しないようにテーブルのローカル コピーをキャッシュすることもできます。

ここでは、前の 2 つの例と同じテーブル整形を使用しますが、結果をコレクションにキャプチャします。

* **ClearCollect( NewOrder, ShowColumns( AddColumns( Filter( Products, 'Quantity Requested' > 'Quantity Available' ), "Quantity To Order", 'Quantity Requested' - 'Quantity Available' ), "Product", "Quantity To Order" ) )**
* **ClearCollect( NewOrder, ForAll( Products, If( 'Quantity Requested' > 'Quantity Available', { Product: Product, 'Quantity To Order': 'Quantity Requested' - 'Quantity Available' } ) ) )**

**ClearCollect** と **Collect** は委任できません。  その結果、この方法で移動できるデータの量は制限されます。

#### <a name="collect-within-forall"></a>ForAll 内での収集
最後に、**ForAll** 内で直接 **Collect** を実行できます。

* **Clear( ProductsToOrder ); ForAll( Products, If( 'Quantity Requested' > 'Quantity Available', Collect( NewOrder, { Product: Product, 'Quantity To Order': 'Quantity Requested' - 'Quantity Available' } ) ) )**

繰り返しますが、この時点で **ForAll** 関数を委任することはできません。  **Products** テーブルが大きい場合、**ForAll** は先頭のレコード セットのみを参照するため、注文する必要がある製品をいくつか見落とす可能性があります。  ただし、小さいままであることがわかっているテーブルの場合は、この方法が適しています。

**ForAll** の結果をキャプチャしていないことに注意してください。  その関数の中から行われた **Collect** 関数の呼び出しにより、すべてのレコードに対して **NewOrder** データ ソースが返されるため、キャプチャした場合は最終的に大量のデータが生じることになります。  


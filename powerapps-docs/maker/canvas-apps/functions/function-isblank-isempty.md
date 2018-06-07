---
title: Blank、Coalesce、IsBlank、および IsEmpty 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Blank、Coalesce、IsBlank、および IsEmpty 関数の参考情報
documentationcenter: na
author: gregli-msft
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: reference
ms.component: canvas
ms.date: 07/24/2017
ms.author: gregli
ms.openlocfilehash: 80d06a30dbe334f7fa9691d2a56805d53876693c
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "31838558"
---
# <a name="blank-coalesce-isblank-and-isempty-functions-in-powerapps"></a>PowerApps の Blank、Coalesce、IsBlank、および IsEmpty 関数
値が空白であるかどうか、または、[テーブル](../working-with-tables.md)に[レコード](../working-with-tables.md#records)が含まれていないかどうかをテストし、*空白*の値を作成する方法を提供します。

## <a name="overview"></a>概要
"*空白*" は、"値がない" または "不明な値" の場合のプレースホルダーです。 ユーザーが**[テキスト入力](../controls/control-text-input.md)** コントロールに文字を入力しなかった場合、テキスト入力コントロールは "*空白*" になります。 ユーザーが文字を入力するとすぐに、そのコントロールは "*空白*" ではなくなります。  一部のデータ ソースは、NULL 値を格納し、返します。これは、PowerApps では "*空白*" として表されます。

> [!NOTE]
> 現時点で、"*空白*" の値の保存は、ローカル コレクションでのみサポートされています。 多くのデータ ソースで "*空白*" (NULL) 値がサポートされていることがわかっており、マイクロソフトでは、この制限の解消に取り組んでいます。

プロパティまたは計算された値はどれも、"*空白*" になる可能性があります。  たとえばブール値は通常、**true** と **false** のいずれかの値になります。  しかし、これら 2 つの値のほかに、"*空白*" になることがあります。  これは特に Microsoft Excel に似ています。Excel では、最初は空白であるワークシートのセルに **true** または **false** の値を設定できます。 このセルの内容はいつでも削除でき、削除したらセルの内容は "*空白*" の状態に戻ります。

"*空*" は、レコードがないテーブルに固有です。 テーブル構造は完全で、[列](../working-with-tables.md#columns)の名前は付いているものの、テーブル内にデータがありません。 最初は空だったテーブルにレコードを追加して空でない状態にした後で、レコードを削除してもう一度空にすることができます。

## <a name="description"></a>説明
**空白**関数は、"*空白*" の値を返します。 この関数を使用して、これらの値をサポートするデータ ソースに NULL 値を格納して、フィールドから値を効率的に削除します。

**IsBlank** 関数は "*空白*" の値の有無をテストします。 "*空白*" の値は、次のような場合に見つかります。

* **空白**関数からの戻り値。
* コントロール プロパティに数式が設定されていない。
* テキスト入力コントロールに値が入力されていない。または、リスト ボックスで選択が行われていない。 **IsBlank** を使用して、フィールドが必須であることをフィードバックで示すことができます。
* 文字が含まれていない文字列に、0 の **[Len](function-len.md)** がある。
* 関数でエラーが発生した。 多くの場合、関数に渡された引数のいずれかが無効です。 引数の値が "*空白*" の場合、多くの関数は "*空白*" の値を返します。
* (SQL Server などの) 接続された[データ ソース](../working-with-data-sources.md)で "null" 値が使用されている。 PowerApps では、これらの値は "*空白*" になります。
* **[If](function-if.md)** 関数の *else* 部分が指定されておらず、すべての条件が **false** である。
* **[Update](function-update-updateif.md)** 関数を使用したものの、すべての列の値を指定していなかったため、 指定した列に値が入力されなかった。

**Coalesce** 関数は、引数を順番に評価し、*空*でない最初の値を返します。  この関数を使用すると*空*の値を別の値で置き換えますが、*空*以外の値は変更されません。  すべての引数が*空*である場合、関数は*空*を返します。  **Coalesce** のすべての引数は同じ型である必要があります。たとえば、数値とテキスト文字列を混在させることはできません。  **Coalesce(value1, value2)** は、**If(IsBlank(value1) value1, value2)** と等しく、より簡潔ですが、**value1** を 2 度評価せずにすみます。  

**IsEmpty** 関数は、テーブル内にレコードがあるかどうかをテストします。 これは、**[CountRows](function-table-counts.md)** 関数を使用してゼロの有無をチェックするのと同じことです。 **IsEmpty** は、**[Errors](function-errors.md)** 関数と組み合わせることで、データソース エラーのチェックに使用できます。

**IsBlank** と **IsEmpty** のどちらの関数の戻り値も、ブール値の **true** または **false** です。

## <a name="syntax"></a>構文
**空白**()

**Coalesce**(*Value1* [, *Value2*, ... ])

* *Value(s)* – 必須。 テストする値。  それぞれの値が、*空*の値が見つかるまで順番に評価されます。  最初の*空*以外の値の後にくる値は評価されません。  

**IsBlank**( *Value* )

* *Value* – 必須。 テストする値。

**IsEmpty**( *Table* )

* *Table* - 必須。 レコードの有無をテストするテーブル。

## <a name="examples"></a>例
### <a name="blank"></a>空白
> [!NOTE]
> 現時点で、次の例はローカル コレクションでのみ機能します。  多くのデータ ソースで "*空白*" (NULL) 値がサポートされていることがわかっており、マイクロソフトでは、この制限の解消に取り組んでいます。

1. アプリを最初から作成し、**ボタン** コントロールを追加します。
2. ボタンの **[OnSelect](../controls/properties-core.md)** プロパティを次の数式に設定します。
   
    **ClearCollect( Cities, { Name: "Seattle", Weather: "Rainy" } )**
3. アプリをプレビューし、追加したボタンをクリックまたはタップして、プレビューを終了します。  
4. **[ファイル]** メニューの **[コレクション]** をクリックまたはタップします。
   
     **[Cities]** (都市) コレクションが表示され、"Seattle" および "Rainy" の 1 つのレコードが表示されます。
   
    ![天気が Rainy (雨) の Seattle (シアトル) を示すコレクション](./media/function-isblank-isempty/seattle-rainy.png)
5. 戻る矢印をクリックまたはタップして、既定のワークスペースに戻ります。
6. **ラベル** コントロールを追加し、その **Text** プロパティを次の数式に設定します。
   
    **IsBlank( First( Cities ).Weather )**
   
    **[Weather]** (天気) フィールドに値 ("Rainy" (雨)) が含まれているため、ラベルには **false** と表示されます。
7. 2 つ目のボタンを追加し、その **OnSelect** プロパティを次の数式に設定します。
   
    **Patch( Cities, First( Cities ), { Weather: Blank() } )**
8. アプリをプレビューし、追加したボタンをクリックまたはタップして、プレビューを終了します。  
   
    **Cities (都市)** の最初のレコードの **[Weather]** (天気) フィールドは、"*空白*" に置き換えられ、そこに設定されていた "Rainy" は削除されます。
   
    ![[Weather] (天気) フィールドが空白の、Seattle を示すコレクション](./media/function-isblank-isempty/seattle-blank.png)
   
    **[Weather]** (天気) フィールドに値が含まれていないため、ラベルには **true** と表示されます。

### <a name="coalesce"></a>Coalesce
| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Coalesce(Blank(), 1)** |**空白**関数からの戻り値をテストします。常に "*空白*" の値が返されます。 最初の引数が*空*であるため、*空*以外の値が見つかるまで、次の引数の評価を続けます。 |**1** |
| **Coalesce(Blank(), Blank(), Blank(), Blank(), 2, 3)** |**Coalesce** は、引数リストの先頭から開始し、*空*以外の値が見つかるまで、各引数を順番に評価します。  この場合は、最初の 4 つの引数はすべて*空*を返すため、評価は 5 番目の引数まで続きます。 5 番目の引数は*空*ではないため、評価はここで停止します。 5 番目の引数の値が返され、6 番目の引数は評価されません。 |**2** |

### <a name="isblank"></a>IsBlank
1. アプリを最初から作成し、テキスト入力コントロールを追加して **FirstName** という名前を付けます。
2. ラベルを追加し、その **[Text](../controls/properties-core.md)** プロパティを次の数式に設定します。
   
    **If( IsBlank( FirstName.Text ), "First Name is a required field." )**
   
    既定では、テキスト入力コントロールの **[Text](../controls/properties-core.md)** プロパティは **"Text input"** に設定されています。 このプロパティには値が含まれており、空白ではないため、ラベルにはメッセージが表示されません。
3. テキスト入力コントロールから、スペースを含めたすべての文字を削除します。
   
    **[Text](../controls/properties-core.md)** プロパティ内の文字がなくなったため、これは "*空白*" になり、**IsBlank( FirstName.Text )** は **true** になります。 必須フィールドのメッセージが表示されます。

他のツールを使用して検証を実行する方法については、**[Validate](function-validate.md)** 関数と[データ ソースの操作方法](../working-with-data-sources.md)をご確認ください。  

他には次のような例があります。

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **IsBlank( Blank() )** |**空白**関数からの戻り値をテストします。常に "*空白*" の値が返されます。 |**true** |
| **IsBlank( "" )** |文字が含まれていない文字列。 |**true** |
| **IsBlank( "Hello" )** |1 つ以上の文字が含まれている文字列。 |**false** |
| **IsBlank( *AnyCollection* )** |[コレクション](../working-with-data-sources.md#collections)が存在するため、レコードがなくとも空白ではありません。 空のコレクションの有無をチェックするには、代わりに **IsEmpty** を使用します。 |**false** |
| **IsBlank( Mid( "Hello", 17, 2 ) )** |**[Mid](function-left-mid-right.md)** の開始文字が文字列の範囲外になっています。  そのため、空の文字列が返されます。 |**true** |
| **IsBlank( If( false, false ) )** |*ElseResult* がない **[If](function-if.md)** 関数。  条件が常に **false** になるため、この **[If](function-if.md)** は常に "*空白*" を返します。 |**true** |

### <a name="isempty"></a>IsEmpty
1. アプリを最初から作成し、**ボタン** コントロールを追加します。
2. ボタンの **[OnSelect](../controls/properties-core.md)** プロパティを次の数式に設定します。
   
    **Collect( IceCream, { Flavor: "Strawberry", Quantity: 300 }, { Flavor: "Chocolate", Quantity: 100 } )**
3. アプリをプレビューし、追加したボタンをクリックまたはタップして、プレビューを終了します。  
   
    **IceCream** という名前のコレクションが作成されます。このデータには、次のデータが含まれます。
   
    ![](media/function-isblank-isempty/icecream-strawberry-chocolate.png)
   
    このコレクションには 2 つのレコードがあり、空ではありません。 **IsEmpty( IceCream )** は **false** を返し、**CountRows( IceCream )** は **2** を返します。
4. 2 つ目のボタンを追加し、その **[OnSelect](../controls/properties-core.md)** プロパティを次の数式に設定します。
   
    **Clear( IceCream )**
5. アプリをプレビューし、2 つ目のボタンをクリックまたはタップして、プレビューを終了します。  
   
    これでコレクションは空になりました。
   
    ![](media/function-isblank-isempty/icecream-clear.png)
   
    **[Clear](function-clear-collect-clearcollect.md)** 関数でコレクションからすべてのレコードが削除され、コレクションは空になっています。 **IsEmpty( IceCream )** は **true** を返し、**CountRows( IceCream )** は **0** を返します。

以下の例のように、**IsEmpty** を使用して、計算されたテーブルが空かどうかをテストすることもできます。

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **IsEmpty( [&nbsp;1,&nbsp;2,&nbsp;3 ] )** |単一列テーブルに 3 つのレコードが含まれており、テーブルは空ではありません。 |**false** |
| **IsEmpty( [&nbsp;] )** |単一列テーブルにレコードが含まれておらず、テーブルは空です。 |**true** |
| **IsEmpty( Filter( [&nbsp;1,&nbsp;2,&nbsp;3&nbsp;], Value > 5 ) )** |単一列テーブルに 5 より大きい値が含まれていません。  フィルター処理後のテーブルにはレコードが含まれておらず、テーブルは空です。 |**true** |


---
title: Sort および SortByColumns 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Sort および SortByColumns 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 04/26/2016
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: d3a83f5ae96b8d9146163ed7d5ff4c4529f8d562
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "42830773"
---
# <a name="sort-and-sortbycolumns-functions-in-powerapps"></a>PowerApps の Sort および SortByColumns 関数
[テーブル](../working-with-tables.md)を並べ替えます。

## <a name="description"></a>説明
**Sort** 関数は、数式に基づいてテーブルを並べ替えます。  

数式は、それぞれのテーブルの[レコード](../working-with-tables.md#records)に対して評価され、結果はテーブルの並べ替えに使用されます。  数式の結果は、数値、文字列、またはブール値になる必要があります。結果がテーブルまたはレコードになることはできません。

[!INCLUDE [record-scope](../../../includes/record-scope.md)]

まず 1 つの列で並べ替えてから、別の列で並べ替えるには、**Sort** 式を別の Sort 式に埋め込みます。 たとえば、次の数式を使用して最初に **Contacts** テーブルを **LastName** 列で並べ替えてから、**FirstName** 列で並べ替えることができます: **Sort( Sort( Contacts, LastName ), FirstName )**

**SortByColumns** 関数は、1 つまたは複数の列に基づいてテーブルを並べ替える場合にも使用できます。

**SortByColumns** のパラメーター リストでは、並べ替える列の名前と、各列の並べ替えの方向を指定します。  並べ替えは、パラメーターの順序で実行されます (最初の列が最初に並べ替えられ、次に 2 番目の列が並べ替えられるという順序です)。  列名は、文字列として指定し、パラメーター リストに直接指定する場合は、二重引用符で囲む必要があります。  たとえば、**SortByColumns( CustomerTable, "LastName" )** となります。

**SortByColumns** と**[ドロップ ダウン](../controls/control-drop-down.md)** コントロールまたは**[リスト ボックス](../controls/control-list-box.md)** コントロールを組み合わせると、並べ替える列を選択できます。

**SortByColumns** では、昇順または降順で並べ替えるだけでなく、値を含んだ単一列テーブルに基づいて並べ替えることができます。  たとえば、**["Monday","Tuesday"、"Wednesday"、"Thursday"、"Friday"、"Saturday"、"Sunday"]** を並べ替え順序として指定すると、曜日の名前に基づいてレコードを並べ替えることができます。  **Monday"** が含まれるレコードが先頭に表示され、続いて **Tuesday** の順序で表示されます。  並べ替えテーブルに表示されないレコードは、リストの末尾に表示されます。

文字列または数値と同じように、[テーブル](../working-with-tables.md)は PowerApps 内の値です。  関数に渡して、関数から返すことができます。  **Sort** と **SortByColumn** はテーブルを変更しません。代わりに、テーブルを引数として受け取り、並べ替えた新しいテーブルを返します。  詳細については、[テーブルの使用](../working-with-tables.md)に関するページを参照してください。

[!INCLUDE [delegation](../../../includes/delegation.md)]

## <a name="syntax"></a>構文
**Sort**( *Table*, *Formula* [, *SortOrder* ] )

* *Table* - 必須。 並べ替えるテーブル。
* *Formula* - 必須。 この数式は、それぞれのテーブルのレコードに対して評価され、結果はテーブルの並べ替えに使用されます。  テーブル内の列を参照することができます。
* *SortOrder* - 省略可能。 **SortOrder.Descending** を指定すると、降順でテーブルを並べ替えます。 **SortOrder.Ascending** が既定値です。

**SortByColumns**( *Table*, *ColumnName1* [, *SortOrder1*, *ColumnName2*, *SortOrder2*, ... ] )

* *Table* - 必須。 並べ替えるテーブル。
* *ColumnName(s)* - 必須。 文字列として、並べ替える列名。
* *SortOrder(s)* - 省略可能。  **SortOrder.Ascending** または **SortOrder.Descending**。  **SortOrder.Ascending** が既定です。  複数の *ColumnNames* が指定されている場合は、最後の列以外に、*SortOrder* を含める必要があります。
  
    > [!NOTE]
  > 名前にスペースが使われている列を含む SharePoint および Excel のデータ ソースの場合、各スペースを **"\_x0020\_"** として指定します。 たとえば、**"Column Name"** として **"Column_x0020_Name"** を指定します。

**SortByColumns**( *Table*, *ColumnName*, *SortOrderTable* )

* *Table* - 必須。 並べ替えるテーブル。
* *ColumnName(s)* - 必須。 文字列として、並べ替える列名。
* *SortOrderTable* - 必須。  並べ替えの対象となる、値を含んだ単一列テーブル。
  
    > [!NOTE]
  > 名前にスペースが使われている列を含む SharePoint および Excel のデータ ソースの場合、各スペースを **"\_x0020\_"** として指定します。 たとえば、**"Column Name"** として **"Column_x0020_Name"** を指定します。

## <a name="examples"></a>例
以下の例では、次のテーブルにデータが含まれている **IceCream** [データ ソース](../working-with-data-sources.md)を使用します。

![](media/function-sort/icecream.png)

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Sort( IceCream, Flavor )**<br><br>**SortByColumns( IceCream, "Flavor" )** |**IceCream** を **Flavor** 列で並べ替えます。 **Flavor** 列に文字列が含まれているため、テーブルはアルファベット順に並べ替えられます。 既定では、並べ替え順序は昇順です。 |<style> img { max-width: none; } </style> ![](media/function-sort/icecream-flavor.png) |
| **Sort( IceCream, Quantity )**<br><br>**SortByColumns( IceCream, "Flavor" )** |**IceCream** を **Quantity** 列で並べ替えます。  **Quantity** 列に数値が含まれているため、テーブルは数値の順で並べ替えられます。  既定では、並べ替え順序は昇順です。 |![](media/function-sort/icecream-quantity-asc.png) |
| **Sort( IceCream, Quantity, SortOrder.Descending )**<br><br>**SortByColumns( IceCream, "Quantity", SortOrder.Descending )** |**IceCream** を **Quantity** 列で並べ替えます。  **Quantity** 列に数値が含まれているため、数値の順で並べ替えられます。  並べ替え順序は、降順に指定されています。 |![](media/function-sort/icecream-quantity-desc.png) |
| **Sort( IceCream, Quantity + OnOrder )** |**IceCream** を、各レコードの **Quantity** 列と **OnOrder** 列の合計で並べ替えます。 合計が数値であるため、テーブルは数値の順に並べ替えられます。  既定では、並べ替え順序は昇順です。  列のそのままの値ではなく、数式によって並べ替えるため、**SortByColumns** を使って同じことはできません。 |![](media/function-sort/icecream-total.png) |
| **Sort( Sort( IceCream, OnOrder ), Quantity )**<br><br>**SortByColumns( IceCream, "OnOrder", Ascending, "Quantity", Ascending )** |**IceCream** を最初に  **OnOrder** 列で並べ替えてから、次に **Quantity** 列で並べ替えます。  最初の並べ替えで **OnOrder** に基づいて "Pistachio" が "Vanilla" の上に移動し、次に **Quantity** に基づいて、共に適切な位置に移動します。 |![](media/function-sort/icecream-onorder-quantity.png) |
| **SortByColumns( IceCream, "Flavor", [&nbsp;"Pistachio",&nbsp;"Strawberry"&nbsp;] )** |"Pistachio" と "Strawberry" を含んだ単一列テーブルに基づいて **IceCream** を **Flavor** 列で並べ替えます。  **Flavor** 列に "Pistachio" があるレコードが結果の先頭に表示され、次に "Strawberry" を含むレコードが表示されます。  "Vanilla" のように **Flavor** 列の値が一致しない場合は、その値は一致した項目の後に表示されます。 |![](media/function-sort/icecream-onflavor-sorttable.png) |

### <a name="step-by-step"></a>ステップ バイ ステップ
これらの例を実行するには、次のように **IceCream** データ ソースを[コレクション](../working-with-data-sources.md#collections)として作成します。

1. ボタンを追加し、**[OnSelect](../controls/properties-core.md)** プロパティを次の数式に設定します。<br>**ClearCollect( IceCream, { Flavor: "Chocolate", Quantity: 100, OnOrder: 150 }, { Flavor:  "Vanilla", Quantity: 200, OnOrder: 20 }, { Flavor: "Strawberry", Quantity: 300, OnOrder: 0 }, { Flavor: "Mint Chocolate", Quantity: 60, OnOrder: 100 }, { Flavor: "Pistachio", Quantity: 200, OnOrder: 10 } )**
2. アプリをプレビューし、ボタンを選択してから、Esc キーを押して既定のワークスペースに戻ります。
3. **[ファイル]** メニューの **[コレクション]** を選択して、作成したコレクションを表示し、Esc キーを押して既定のワークスペースに戻ります。

#### <a name="sort"></a>Sort
1. もう 1 つボタンを追加し、**[OnSelect](../controls/properties-core.md)** プロパティを次の数式に設定します。<br>
   **ClearCollect( SortByFlavor, Sort( IceCream, Flavor ) )**
   
     上の数式では、**IceCream** と同じデータを含む、**SortByFlavor** という名前の 2 つ目のコレクションを作成します。 ただし、新しいコレクションに含まれるデータは、**Flavor** 列でアルファベットの昇順に並べ替えられます。
2. F5 キーを押して、新しいボタンを選択し、Esc キーを押します。
3. **[ファイル]** メニューの **[コレクション]** を選択して両方のコレクションを表示し、Esc キーを押して既定のワークスペースに戻ります。
4. 最後の 3 つの手順を繰り返しますが、作成するコレクションの名前を変更し、**Sort** 式を、前にこのセクションで示した **Sort** の使用例の表にある別の式で置き換えます。

#### <a name="sortbycolumns"></a>SortByColumns
1. もう 1 つボタンを追加し、**[OnSelect](../controls/properties-core.md)** プロパティを次の数式に設定します。<br>
   **ClearCollect( SortByQuantity, SortByColumns( IceCream, "Quantity", Ascending, "Flavor", Descending ) )**
   
     上の数式では、**IceCream** と同じデータを含む、**SortByQuantity** という名前の 3 つ目のコレクションを作成します。 ただし、新しいコレクションに含まれるデータは、**Quanity** 列で数値の昇順で並べ替えられてから、**Flavor** 列で降順に並べ替えられます。
2. F5 キーを押して、新しいボタンを選択し、Esc キーを押します。
3. **[ファイル]** メニューの **[コレクション]** を選択して 3 つのコレクションをすべて表示し、Esc キーを押して既定のワークスペースに戻ります。
4. 最後の 3 つの手順を繰り返しますが、作成するコレクションの名前を変更し、**SortByColumns** 式を、前にこのセクションで示した **SortByColumns** の使用例の表にある別の式で置き換えます。


---
title: AddColumns、DropColumns、RenameColumns、および ShowColumns 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の AddColumns、DropColumns、RenameColumns、および ShowColumns 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 04/04/2019
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: fc682694bb22ecc63ecc762a735df07950ce29d3
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61543774"
---
# <a name="addcolumns-dropcolumns-renamecolumns-and-showcolumns-functions-in-powerapps"></a>PowerApps の AddColumns、DropColumns、RenameColumns、および ShowColumns 関数
[列](../working-with-tables.md#columns)の追加、削除、名前の変更、選択により、[テーブル](../working-with-tables.md)の表示を調整します。

## <a name="overview"></a>概要
これらの関数は、列を調整することでテーブルの表示を調整します。

* 複数の列を持つテーブルを単一列にし、**[Lower](function-lower-upper-proper.md)** や **[Abs](function-numericals.md)** といった単一列関数で使用できるようにします。  
* 計算列をテーブルに追加します (たとえば、**Quantity** を **Unit Price** で乗算した結果を示す **Total Price** 列)。
* ユーザーに表示するため、または数式で使用するために、列の名前をよりわかりやすく変更します。

テーブルは、文字列や数値と同様、PowerApps 内での値です。  テーブルは数式内で引数として指定できるほか、関数から結果として返すことができます。

> [!NOTE]
> このトピックで説明する関数は、元のテーブルを変更しないでください。 代わりに、そのテーブルを引数としてと適用される変換を使用して、新しいテーブルを返します。 詳細については、[テーブルの使用](../working-with-tables.md)に関するページを参照してください。  

これらの関数を使用しても、[データ ソース](../working-with-data-sources.md)の列は変更できません。 そのデータは、ソースで変更する必要があります。 **[Collect](function-clear-collect-clearcollect.md)** 関数を使用して、[コレクション](../working-with-data-sources.md#collections)に列を追加できます。 詳細については、[データ ソースの使用](../working-with-data-sources.md)に関するページを参照してください。  

## <a name="description"></a>説明
**AddColumns** 関数は、テーブルに列を追加し、数式でその列内の値を定義します。 既存の列は変更されません。

数式はテーブルの各レコードについて評価されます。
[!INCLUDE [record-scope](../../../includes/record-scope.md)]

**DropColumns** 関数は、テーブルから列を除外します。  その他すべての列は変更されません。 **DropColumns** は列を除外し、**ShowColumns** は列を表示します。

**RenameColumns** 関数を使用して、テーブルの 1 つ以上の列の名前を変更します。この操作は、テーブルに含まれる列の名前 (置換対象の古い名前) と、テーブルに含まれない列の名前 (使用する新しい名前) を指定する、引数のペアを少なくとも 1 つ指定することで実行します。 以前の名前はテーブルに既に存在している必要があり、新しい名前は存在していてはなりません。 各列名は、古い列名または新しい列名のいずれかとして、引数リストに一度だけ表示できます。 列の名前を既存の列名に変更するには、まず **DropColumns** を使用して既存の列を削除するか、または 1 つの **RenameColumns** 関数を別の関数内に入れ子にすることで既存の列名を変更します。

**ShowColumns** 関数は、テーブルの列を表示し、その他すべての列を削除します。 **ShowColumns** を使用して、複数列テーブルから単一列テーブルを作成できます。  **ShowColumns** は列を表示し、**DropColumns** は列を除外します。  

これらすべての関数の結果は、変換が適用された新しいテーブルになります。 元のテーブルは変更されません。 数式で既存のテーブルを変更することはできません。 SharePoint、Common Data Service、SQL Server、および他のデータ ソースは、リスト、エンティティ、および多くの場合、スキーマと呼ばれる、テーブルの列を変更するためのツールを提供します。 このトピック内の関数は、のみ元を使用するための出力テーブルに変更することがなく、入力テーブルを変換します。

これらの関数の引数は、委任をサポートします。 など、**フィルター**関数関連レコードを検索するすべての一覧を取得する引数として使用する場合でも、 **' [dbo]. [AllListings]'** データ ソースに 100万行が含まれています。

```powerapps-dot
AddColumns( RealEstateAgents, 
    "Listings",  
    Filter(  '[dbo].[AllListings]', ListingAgentName = AgentName ) 
)
```

ただし、これらの関数の出力が対象には、[制限のない委任レコード](../delegation-overview.md#non-delegable-limits)します。  この例では 500 個のみのレコードが返される場合でも、 **RealEstateAgents**データ ソースは、501 または複数のレコード。

使用する場合**AddColumns** 、この方法で**フィルター**でそれらの最初のレコードの各データ ソースに個別の呼び出しを行う必要があります**RealEstateAgents**、それが原因で、多くのネットワークの chatter します。 場合 **[dbo]. [AllListings]** が十分に小さくて、なおかつ変わらない多くの場合、呼び出すことができます、**収集**関数[ **OnStart** ](signals.md#app)アプリでデータ ソースをキャッシュするにはときに開始します。 別の方法としては、要求したときに、ユーザーの場合にのみ、関連するレコードにプルするように、アプリが再構築できます。  

## <a name="syntax"></a>構文
**AddColumns**( *Table*, *ColumnName1*, *Formula1* [, *ColumnName2*, *Formula2*, ... ] )

* *Table* - 必須。  操作の対象となるテーブル。
* *ColumnName(s)* - 必須。 追加する列の名前。  この引数には、文字列を指定する必要があります (たとえば、二重引用符を含む **"Name"** など)。
* *Formula(s)* - 必須。  各レコードについて評価する数式。 結果は、対応する新しい列の値として追加されます。 この数式では、テーブルの他の列を参照できます。

**DropColumns**( *Table*, *ColumnName1* [, *ColumnName2*, ... ] )

* *Table* - 必須。  操作の対象となるテーブル。
* *ColumnName(s)* - 必須。 削除する列の名前。 この引数には、文字列を指定する必要があります (たとえば、二重引用符を含む **"Name"** など)。

**RenameColumns**( *Table*, *OldColumnName1*, *NewColumnName1* [, *OldColumnName2*, *NewColumnName2*, ... ] )

* *Table* - 必須。  操作の対象となるテーブル。
* *OldColumnName* - 必須。 元のテーブルから名前を変更する列の名前。 この要素は、引数のペアの先頭に (または、数式に複数のペアが含まれている場合は、各引数の先頭に) 表示されます。 この名前は、文字列である必要があります (たとえば、二重引用符を含む **"Name"** など)。
* *NewColumnName* - 必須。 置換後の名前。 この要素は、引数のペアの末尾に (または、数式に複数のペアが含まれている場合は、各引数のペアの末尾に) 表示されます。 この引数には、文字列を指定する必要があります (たとえば、二重引用符を含む **"Customer Name"** など)。

**ShowColumns**( *Table*, *ColumnName1* [, *ColumnName2*, ... ] )

* *Table* - 必須。  操作の対象となるテーブル。
* *ColumnName(s)* - 必須。 表示する列の名前。 この引数には、文字列を指定する必要があります (たとえば、二重引用符を含む **"Name"** など)。

## <a name="examples"></a>例
このセクションの例では、次のテーブルにデータが含まれている **IceCreamSales** データ ソースを使用します。

![](media/function-table-shaping/icecream.png)

これらの例ではいずれも、**IceCreamSales** データ ソースは変更されません。 各関数は、データ ソースの値をテーブルに変換し、その値を結果として返します。

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **AddColumns( IceCreamSales, "Revenue", UnitPrice * QuantitySold )** |結果に **Revenue** 列を追加します。  各レコードで **UnitPrice * QuantitySold** が評価され、その結果が新しい列に配置されます。 |<style> img { max-width: none; } </style> ![](media/function-table-shaping/icecream-add-revenue.png) |
| **DropColumns( IceCreamSales, "UnitPrice" )** |結果から **UnitPrice** 列を除外します。 この関数は列の除外に使用し、**ShowColumns** は列の表示に使用します。 |![](media/function-table-shaping/icecream-drop-price.png) |
| **ShowColumns( IceCreamSales, "Flavor" )** |結果に **Flavor** 列のみを表示します。 この関数は列の表示に使用し、**DropColumns** は列の除外に使用します。 |![](media/function-table-shaping/icecream-select-flavor.png) |
| **RenameColumns( IceCreamSales, "UnitPrice", "Price")** |名前を変更、 **UnitPrice**結果の列。 |![](media/function-table-shaping/icecream-rename-price.png) |
| **RenameColumns( IceCreamSales, "UnitPrice", "Price", "QuantitySold", "Number")** |結果内の **UnitPrice** 列と **QuantitySold** 列の名前を変更します。 |![](media/function-table-shaping/icecream-rename-price-quant.png) |
| **DropColumns(<br>RenameColumns(<br>AddColumns( IceCreamSales, "Revenue",<br>UnitPrice * QuantitySold ),<br>"UnitPrice", "Price" ),<br>"Quantity" )** |次のテーブル変換を、数式の内側から順に実行します。 <ol><li>**UnitPrice * Quantity** のレコードごとの計算に基づいて、**Revenue** 列を追加します。<li>**UnitPrice** という名前を **Price** に変更します。<li>**Quantity** 列を除外します。</ol>  この順番は重要なので、注意してください。 たとえば、名前を変更した後は、**UnitPrice** を使用した計算ができません。 |![](media/function-table-shaping/icecream-all-transforms.png) |

### <a name="step-by-step"></a>ステップ バイ ステップ

このトピックの前の例の一部を試してみましょう。  

1. 追加することでコレクションを作成、 **[ボタン](../controls/control-button.md)** コントロールと設定、 **OnSelect**プロパティをこの式に。

    ```powerapps-dot
    ClearCollect( IceCreamSales, 
        Table(
            { Flavor: "Strawberry", UnitPrice: 1.99, QuantitySold: 20 }, 
            { Flavor: "Chocolate", UnitPrice: 2.99, QuantitySold: 45 },
            { Flavor: "Vanilla", UnitPrice: 1.50, QuantitySold: 35 }
        )
    )
    ```

1. Alt キーを押しながら、ボタンを選択して数式を実行します。

1. 1 秒あたりの追加**ボタン**コントロール、 **OnSelect**プロパティをこの数式にし、実行。

    ```powerapps-dot
    ClearCollect( FirstExample, 
        AddColumns( IceCreamSales, "Revenue", UnitPrice * QuantitySold )
    ) 
    ```
1. **ファイル**メニューの **コレクション**、し、 **IceCreamSales**をそのコレクションを表示します。
 
    次の図に示すよう、2 番目の数式は、このコレクションを変更しませんでした。 **AddColumns**使用される関数**IceCreamSales**は読み取り専用の引数として、関数がその引数が参照するテーブルを変更していません。
    
    ![収入列が含まれていないアイスクリームの売上のコレクションの 3 つのレコードが表示されたコレクションの表示](media/function-table-shaping/ice-cream-sales-collection.png)

1. 選択**FirstExample**します。

    次の図に示す 2 番目の数式に追加された列を含む新しいテーブルが返されます。 **ClearCollect**関数で新しいテーブルのキャプチャ、 **FirstExample**コレクション、ソースを変更することがなく関数を介して送信されることに、元のテーブルに追加するもの。

    ![新しい収益の列を含む最初の例のコレクションの 3 つのレコードが表示されたコレクションの表示](media/function-table-shaping/first-example-collection.png)

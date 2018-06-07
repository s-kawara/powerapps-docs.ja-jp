---
title: Filter、Search、および LookUp 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Filter 関数および LookUp 関数の参照情報
documentationcenter: na
author: gregli-msft
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: reference
ms.component: canvas
ms.date: 02/05/2017
ms.author: gregli
ms.openlocfilehash: 35dec320b52dd934d616ba067932228b0e15ee3d
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "31838811"
---
# <a name="filter-search-and-lookup-functions-in-powerapps"></a>PowerApps の Filter、Search、および LookUp 関数
[テーブル](../working-with-tables.md)内の 1 つ以上の[レコード](../working-with-tables.md#records)を検索します。

## <a name="description"></a>説明
**Filter** 関数は、数式を満たすレコードをテーブル内で検索します。  1 つ以上の条件に一致する一連のレコードを検索したり、そのような条件に一致しないレコードを除外したりするには、**Filter** を使用します。

**LookUp** 関数は、テーブル内で数式を満たす最初のレコードを検索します。  1 つ以上の条件に一致する 1 つのレコードを検索するには、**LookUp** を使用します。

どちらの場合も、数式はテーブルの各レコードについて評価されます。  *true* となるレコードが結果に含まれます。  標準的な数式の[演算子](operators.md)に加えて、部分文字列の照合には **[in](operators.md#in-and-exactin-operators)** 演算子と **[exactin](operators.md#in-and-exactin-operators)** 演算子を使用できます。

[!INCLUDE [record-scope](../../../includes/record-scope.md)]

**Search** 関数は、テーブル内でそのいずれかの列にある文字列が含まれているレコードを検索します。 この文字列は、列内のどこに現れてもかまいません。たとえば、"rob" または "bert" を検索すると、"Robert" を含む列で一致が検出されます。 検索では大文字小文字が区別されません。 **Filter** および **LookUp** とは異なり、**Search** 関数は、照合に数式ではなく 1 つの文字列を使用します。

**Filter** と **Search** は、元のテーブルと同じ列および条件と一致するレコードを含むテーブルを返します。 **LookUp** は、レコードを 1 つの値まで減らす数式を適用した後に、最初に見つかったレコードのみを返します。 レコードが見つからなかった場合、**Filter** と **Search** は[空](function-isblank-isempty.md)のテーブルを返し、**LookUp** は "*空白*" を返します。  

文字列または数値と同じように、[テーブル](../working-with-tables.md)は PowerApps 内の値です。 関数に渡して、関数から返すことができます。  **Filter**、**Search**、**LookUp** は、テーブルを変更しません。 代わりに、引数としてテーブルを受け取り、そこからテーブル、レコード、または 1 つの値を返します。 詳細については、[テーブルの使用](../working-with-tables.md)に関するページを参照してください。

[!INCLUDE [delegation](../../../includes/delegation.md)]

## <a name="syntax"></a>構文
**Filter**( *Table*, *Formula1* [, *Formula2*, ... ] )

* *Table* - 必須。 検索するテーブル。
* *Formula(s)* - 必須。 テーブルの各レコードの評価に使用する数式。 関数は、結果が **true** になるすべてのレコードを返します。 テーブル内の列を参照することができます。 複数の数式を指定した場合、すべての数式の結果は **[And](function-logicals.md)** 関数を使用して結合されます。

**Search**( *Table*, *SearchString*, *Column1* [, *Column2*, ... ] )

* *Table* - 必須。 検索するテーブル。
* *SearchString* - 必須。 検索対象文字列。 "*空白*" または空の文字列の場合は、すべてのレコードが返されます。
* *Column(s)* - 必須。 *Table* 内で検索する列の名前。 検索する列には、テキストが含まれている必要があります。 列名は、文字列であり、二重引用符で囲む必要があります。 ただし、列名は静的である必要があるため、数式を使用して計算することはできません。 *SearchString* が、これらの列のいずれかのデータ内で部分一致として見つかった場合は、レコード全体が返されます。

> [!NOTE]
> 名前にスペースが使われている列を含む SharePoint および Excel のデータ ソースの場合、各スペースを **"\_x0020\_"** として指定します。 たとえば、**"Column Name"** として **"Column_x0020_Name"** を指定します。

**LookUp**( *Table*, *Formula* [, *ReductionFormula* ] )

* *Table* - 必須。 検索するテーブル。 UI で、構文が関数ボックスの上に*ソース*として表示されます。
* *Formula* - 必須。
  テーブルの各レコードの評価に使用する数式。 関数は、結果が **true** になる最初のレコードを返します。 テーブル内の列を参照することができます。 UI で、構文が関数ボックスの上に*条件*として表示されます。
* *ReductionFormula* - 省略可能。 この数式は、検出されたレコードについて評価されるため、レコードが 1 つの値まで減ります。 テーブル内の列を参照することができます。 このパラメーターを使用しない場合、この関数はテーブルからレコード全体を返します。 UI で、構文が関数ボックスの上に*結果*として表示されます。

## <a name="examples"></a>例
次の例では、**IceCream** [データ ソース](../working-with-data-sources.md)を使用します。

![](media/function-filter-lookup/icecream.png)

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Filter( IceCream, OnOrder > 0 )** |**OnOrder** が 0 より大きいレコードを返します。 |<style> img { max-width: none; } </style> ![](media/function-filter-lookup/icecream-onorder.png) |
| **Filter( IceCream, Quantity + OnOrder > 225 )** |**Quantity** 列と **OnOrder** 列の合計が 225 より大きいレコードを返します。 |![](media/function-filter-lookup/icecream-overstock.png) |
| **Filter( IceCream, "chocolate" in Lower( Flavor ) )** |大文字か小文字かに関係なく、**Flavor** の名前に "chocolate" という単語が含まれるレコードを返します。 |![](media/function-filter-lookup/icecream-chocolate.png) |
| **Filter( IceCream, Quantity < 10  && OnOrder < 20 )** |**Quantity** が 10 未満かつ **OnOrder** が 20 未満のレコードを返します。  これらの条件に一致するレコードがないため、空のテーブルが返されます。 |![](media/function-filter-lookup/icecream-empty.png) |
| **Search( IceCream, "choc", "Flavor" )** |大文字か小文字かに関係なく、**Flavor** の名前に "choc" という文字列が含まれるレコードを返します。 |![](media/function-filter-lookup/icecream-chocolate.png) |
| **Search( IceCream, "", "Flavor" )** |検索語句が空であるため、すべてのレコードが返されます。 |![](media/function-filter-lookup/icecream.png) |
| **LookUp( IceCream, Flavor = "Chocolate", Quantity )** |**Flavor** が "Chocolate" に等しいレコードを検索します (その中で 1 つあります)。  見つかった最初のレコードについて、そのレコードの **Quantity** を返します。 |100 |
| **LookUp( IceCream, Quantity > 150, Quantity + OnOrder )** |**Quantity**が 100 を超えるレコードを検索します (その中で複数あります)。  見つかった最初のレコード (**Flavor** が "Vanilla") について、**Quantity** 列と **OnOrder** 列の合計を返します。 |250 |
| **LookUp( IceCream, Flavor = "Pistachio", OnOrder )** |**Flavor** が "Pistachio" に等しいレコードを検索します (その中には存在しません)。  見つからなかったため、**Lookup** は "*空白*" を返します。 |"*空白*" |
| **LookUp( IceCream, Flavor = "Vanilla" )** |**Flavor** が "Vanilla" に等しいレコードを検索します (その中で 1 つあります)。  換算公式が指定されていなかったため、レコード全体が返されます。 |{ Flavor: "Vanilla", Quantity: 200, OnOrder: 75 } |

### <a name="search-user-experience"></a>検索のユーザー エクスペリエンス
多くのアプリでは、検索ボックスに 1 つ以上の文字を入力して、大きなデータ セット内のレコードの一覧をフィルター処理することができます。 入力すると、一覧には、検索条件に一致するレコードのみが表示されます。

このトピックの残りの部分にある例では、**Customers** という一覧を検索した場合の結果を示しています。この一覧には、次のデータが含まれています。

![](media/function-filter-lookup/customers.png)

このデータ ソースをコレクションとして作成するには、**[ボタン](../controls/control-button.md)** コントロールを作成し、その **OnSelect** プロパティを次の数式に設定します。

**ClearCollect( Customers, Table( { Name: "Fred Garcia", Company: "Northwind Traders" }, { Name: "Cole Miller", Company: "Contoso" }, { Name: "Glenda Johnson", Company: "Contoso" }, { Name: "Mike Collins", Company: "Adventure Works" }, { Name: "Colleen Jones", Company: "Adventure Works" } ) )**

この例に示すように、画面下部にある[**ギャラリー コントロール**](../controls/control-gallery.md)にレコードの一覧を表示できます。 画面の上部には、ユーザーが関心のあるレコードを指定できるように、**SearchInput** という名前の[**テキスト入力**](../controls/control-text-input.md)コントロールを追加できます。

![](media/function-filter-lookup/customers-ux-unfiltered.png)

ユーザーが **SearchInput** に文字を入力すると、ギャラリーの結果は自動的にフィルター処理されます。 この場合、ギャラリーは、(会社の名前ではなく) 顧客の名前が **SearchInput** の文字シーケンスで始まるレコードを表示するように構成されています。 ユーザーが検索ボックスに「**co**」と入力した場合、ギャラリーには次の結果が表示されます。

![](media/function-filter-lookup/customers-ux-startswith-co.png)

**Name** 列に基づいてフィルター処理するには、ギャラリー コントロールの **Items** プロパティを次の数式のいずれかに設定します。

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Filter( Customers, StartsWith( Name, SearchInput.Text ) )** |**Customers** データ ソースで、検索文字列が **Name** 列の先頭に出現するレコードをフィルター処理します。 このテストでは、大文字と小文字が区別されません。 ユーザーが検索ボックスに「**co**」と入力した場合、ギャラリーには、**Colleen Jones** と **Cole Miller** が表示されます。 ギャラリーに **Mike Collins** が表示されないのは、そのレコードの **Name** 列の先頭に検索文字列がないためです。 |<style> img { max-width: none } </style> ![](media/function-filter-lookup/customers-name-co-startswith.png) |
| **Filter( Customers, SearchInput.Text in Name )** |**Customers** データ ソースで、検索文字列が **Name** 列のどこかに出現するレコードをフィルター処理します。 このテストでは、大文字と小文字が区別されません。 ユーザーが検索ボックスに「**co**」と入力した場合、ギャラリーには、**Colleen Jones**、**Cole Miller**、および **Mike Collins** が表示されます。これは、検索文字列が、これらすべてのレコードの **Name** 列のどこかに出現しているためです。 |<style> img { max-width: none } </style> ![](media/function-filter-lookup/customers-name-co-contains.png) |
| **Search( Customers, SearchInput.Text, "Name" )** |**in** 演算子を使用した場合と同様、**Search** 関数は、各レコードの **Name** 列内で一致を検索します。 列名を二重引用符で囲む必要があることに注意してください。 |<style> img { max-width: none } </style> ![](media/function-filter-lookup/customers-name-co-contains.png) |

**Name** 列だけでなく **Company** 列を含めるように検索範囲を広げることができます。

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Filter( Customers, StartsWith( Name, SearchInput.Text ) &#124;&#124; StartsWith( Company, SearchInput.Text ) )** |**Customers** データ ソースで、**Name** 列または **Company** 列の先頭に検索文字列 (たとえば、**co**) があるレコードをフィルター処理します。  どちらか一方の **StartsWith** 関数が *true* の場合、[**&#124;&#124;** 演算子](operators.md)は *true* になります。 |<style> img { max-width: none } </style> ![](media/function-filter-lookup/customers-all-co-startswith.png) |
| **Filter( Customers, SearchInput.Text in Name &#124;&#124; SearchInput.Text in Company )** |**Customers** データ ソースで、**Name** 列または **Company** 列の中に検索文字列 (たとえば、**co**) が含まれているレコードをフィルター処理します。 |<style> img { max-width: none } </style> ![](media/function-filter-lookup/customers-all-co-contains.png) |
| **Search( Customers, SearchInput.Text, "Name", "Company" )** |**in** 演算子を使用した場合と同様、**Search** 関数は、**Customers** データ ソースで、**Name** 列または **Company** 列の中に検索文字列 (たとえば、**co**) が含まれているレコードを検索します。 複数の列と複数の **in** 演算子を指定する場合は、**Filter** よりも **Search**関数の方が読み書きが簡単です。 列の名前を二重引用符で囲む必要があることに注意してください。 |<style> img { max-width: none } </style> ![](media/function-filter-lookup/customers-all-co-contains.png) |


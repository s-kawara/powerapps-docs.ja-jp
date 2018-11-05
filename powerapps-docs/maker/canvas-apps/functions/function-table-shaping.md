---
title: AddColumns、DropColumns、RenameColumns、および ShowColumns 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の AddColumns、DropColumns、RenameColumns、および ShowColumns 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 08/24/2018
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 056c5e1142b3a34776e72f788f5b2cef9e3b2a27
ms.sourcegitcommit: 3dc330d635aaf5bc689efa6bd39826d6e396c832
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/09/2018
ms.locfileid: "48875901"
---
# <a name="addcolumns-dropcolumns-renamecolumns-and-showcolumns-functions-in-powerapps"></a>PowerApps の AddColumns、DropColumns、RenameColumns、および ShowColumns 関数
[列](../working-with-tables.md#columns)の追加、削除、名前の変更、選択により、[テーブル](../working-with-tables.md)の表示を調整します。

## <a name="overview"></a>概要
これらの関数は、列を調整することでテーブルの表示を調整します。

* 複数の列を持つテーブルを単一列にし、**[Lower](function-lower-upper-proper.md)** や **[Abs](function-numericals.md)** といった単一列関数で使用できるようにします。  
* 計算列をテーブルに追加します (たとえば、**Quantity** を **Unit Price** で乗算した結果を示す **Total Price** 列)。
* ユーザーに表示するため、または数式で使用するために、列の名前をよりわかりやすく変更します。

テーブルは、文字列や数値と同様、PowerApps 内での値です。  テーブルは数式内で引数として指定できるほか、関数から結果として返すことができます。 このトピックで説明する関数は、テーブルを変更しません。 その代わりに、引数としてテーブルを受け取り、変換を適用した新しいテーブルを返します。  詳細については、[テーブルの使用](../working-with-tables.md)に関するページを参照してください。  

これらの関数を使用しても、[データ ソース](../working-with-data-sources.md)の列は変更できません。 そのデータは、ソースで変更する必要があります。 **[Collect](function-clear-collect-clearcollect.md)** 関数を使用して、[コレクション](../working-with-data-sources.md#collections)に列を追加できます。  詳細については、[データ ソースの使用](../working-with-data-sources.md)に関するページを参照してください。  

## <a name="description"></a>説明
**AddColumns** 関数は、テーブルに列を追加し、数式でその列内の値を定義します。 既存の列は変更されません。

数式はテーブルの各レコードについて評価されます。
[!INCLUDE [record-scope](../../../includes/record-scope.md)]

**DropColumns** 関数は、テーブルから列を除外します。  その他すべての列は変更されません。 **DropColumns** は列を除外し、**ShowColumns** は列を表示します。

**RenameColumns** 関数を使用して、テーブルの 1 つ以上の列の名前を変更します。この操作は、テーブルに含まれる列の名前 (置換対象の古い名前) と、テーブルに含まれない列の名前 (使用する新しい名前) を指定する、引数のペアを少なくとも 1 つ指定することで実行します。 以前の名前はテーブルに既に存在している必要があり、新しい名前は存在していてはなりません。 各列名は、古い列名または新しい列名のいずれかとして、引数リストに一度だけ表示できます。 列の名前を既存の列名に変更するには、まず **DropColumns** を使用して既存の列を削除するか、または 1 つの **RenameColumns** 関数を別の関数内に入れ子にすることで既存の列名を変更します。

**ShowColumns** 関数は、テーブルの列を表示し、その他すべての列を削除します。 **ShowColumns** を使用して、複数列テーブルから単一列テーブルを作成できます。  **ShowColumns** は列を表示し、**DropColumns** は列を除外します。  

これらすべての関数の結果は、変換が適用された新しいテーブルになります。  元のテーブルは変更されません。

[!INCLUDE [delegation-no](../../../includes/delegation-no.md)]

## <a name="syntax"></a>構文
**AddColumns**( *Table*, *ColumnName1*, *Formula1* [, *ColumnName2*, *Formula2*, ... ] )

* *Table* - 必須。  操作の対象となるテーブル。
* *ColumnName(s)* - 必須。 追加する列の名前。  この引数には、文字列を指定する必要があります (たとえば、二重引用符を含む **"Name"** など)。
* *Formula(s)* - 必須。  各レコードについて評価する数式。 結果は、対応する新しい列の値として追加されます。 この数式では、テーブルの他の列を参照できます。

**DropColumns**( *Table*, *ColumnName1* [, *ColumnName2*, ... ] )

* *Table* - 必須。  操作の対象となるテーブル。
* *ColumnName(s)* - 必須。 削除する列の名前。 この引数には、文字列を指定する必要があります (たとえば、二重引用符を含む **"Name"** など)。

**RenameColumns**( *Table*, *OldColumneName1*, *NewColumnName1* [, *OldColumnName2*, *NewColumnName2*, ... ] )

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
| **RenameColumns( IceCreamSales, "UnitPrice", "Price")** |結果で **UnitPrice** 列の名前を変更します。 |![](media/function-table-shaping/icecream-rename-price.png) |
| **RenameColumns( IceCreamSales, "UnitPrice", "Price", "QuantitySold", "Number")** |結果内の **UnitPrice** 列と **QuantitySold** 列の名前を変更します。 |![](media/function-table-shaping/icecream-rename-price-quant.png) |
| **DropColumns(<br>RenameColumns(<br>AddColumns( IceCreamSales, "Revenue",<br>UnitPrice * QuantitySold ),<br>"UnitPrice", "Price" ),<br>"Quantity" )** |次のテーブル変換を、数式の内側から順に実行します。 <ol><li>**UnitPrice * Quantity** のレコードごとの計算に基づいて、**Revenue** 列を追加します。<li>**UnitPrice** という名前を **Price** に変更します。<li>**Quantity** 列を除外します。</ol>  この順番は重要なので、注意してください。 たとえば、名前を変更した後は、**UnitPrice** を使用した計算ができません。 |![](media/function-table-shaping/icecream-all-transforms.png) |

### <a name="step-by-step"></a>ステップ バイ ステップ
1. [ギャラリーにテキストとイメージを表示する](../show-images-text-gallery-sort-filter.md)方法に関するページの最初の手順に従って、**Inventory** という名前のコレクションをインポートするか作成します。
2. ボタンを追加し、**[OnSelect](../controls/properties-core.md)** プロパティを次の数式に設定します。
   
    **ClearCollect(Inventory2, RenameColumns(Inventory, "ProductName", "JacketID"))**
3. F5 キーを押し、作成したボタンを選択してから、Esc キーを押して、デザイン ワークスペースに戻ります。
4. **[ファイル]** メニューの **[コレクション]** を選択します。
5. **Inventory2** という名前のコレクションを作成できたことを確認します。 新しいコレクションには **Inventory** と同じ情報が含まれていますが、**Inventory** の **ProductName** という列は、**Inventory2** では **JacketID** という名前になっています。


---
title: EndsWith 関数と StartsWith 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の EndsWith 関数と StartsWith 関数の参考情報
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
ms.openlocfilehash: c01a69f311378e8e818036c866b96a78f223baf9
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "31837127"
---
# <a name="endswith-and-startswith-functions-in-powerapps"></a>PowerApps の EndsWith 関数と StartsWith 関数
あるテキスト文字列が、別のテキスト文字列で始まっているか、または終わっているかをテストします。

## <a name="description"></a>説明
**EndsWith** 関数は、あるテキスト文字列が別のテキスト文字列で終わるかどうかをテストします。

**StartsWith** 関数は、あるテキスト文字列が別のテキスト文字列で始まるかどうかをテストします。    

どちらの関数も、大文字と小文字を区別してテストします。  どちらの戻り値も、ブール値の **true** または **false** です。  

アプリ内でデータを検索するには、**[Filter](function-filter-lookup.md)** 関数と共に **EndsWith** および **StartsWith** を使用します。 また、**[in](operators.md#in-and-exactin-operators)** 演算子または **[Search](function-filter-lookup.md)** 関数を使用すると、先頭や末尾だけでなく、テキスト文字列の中も検索できます。  アプリのニーズや、特定のデータ ソースで[委任](../delegation-overview.md)できる関数に応じて、関数を選ぶことができます。  これらの関数のいずれかを委任できない場合は、作成時に青い点が表示され、この制限に関する警告が表示されます。

## <a name="syntax"></a>構文
**EndsWith**(*Text*, *EndText*)

* *Text* - 必須。  テストするテキスト。
* *EndText* - 必須です。  *Text* の末尾の検索に使用するテキスト。  *EndText* が空の文字列の場合、**EndsWith** は *true* を返します。

**StartsWith**( *Text*, *StartText* )

* *Text* - 必須。  テストするテキスト。
* *StartText* - 必須。  *Text* の先頭で検索するテキスト。  *StartText* が空の文字列の場合、**StartsWith** は *true* を返します。

## <a name="examples"></a>例
| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **EndsWith("Hello World", "world")** |**"Hello World"** が **"world"** で終わるかどうかを調べます。  このテストでは、大文字と小文字が区別されません。 |**true** |
| **EndsWith("Good bye", "good")** |**"Good bye"** が **"good"** で終わるかどうかを調べます。  *EndText* の引数 (**"good"**) は、テキストの中に表れますが、末尾にはありません。 |**false** |
| **EndsWith("Always say hello", "hello")** |**"Always say hello"** が **"hello"** で終わるかどうかをテストします。 |**true** |
| **Endswith("Bye bye", "")** |**"Bye bye"** が、空のテキスト文字列 (**Len** は 0 を返します) で終わるかどうかをテストします。  **フィルター**式を使用して条件を緩和している場合、**EndsWith** は、ここでは **true** を返すように定義されます。 |**true** |

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **StartsWith( "Hello World", "hello" )** |**"Hello World"** が **"hello"** で始まるかどうかをテストします。  このテストでは、大文字と小文字が区別されません。 |**true** |
| **StartsWith( "Good bye", "hello" )** |**"Good bye"** が **"hello"** で始まるかどうかをテストします。 |**false** |
| **StartsWith( "Always say hello", "hello" )** |**"Always say hello"** が **"hello"** で始まるかどうかをテストします。  **"hello"** はテキスト内に出現しますが、先頭にはありません。 |**false** |
| **StartsWith("Bye bye", "")** |**"Bye bye"** が、空のテキスト文字列 (**Len** は 0 を返します) で始まるかどうかをテストします。  **フィルター**式を使用して条件を緩和している場合、**StartsWith** は、ここでは **true** を返すように定義されます。 |**true** |

### <a name="search-user-experience"></a>検索のユーザー エクスペリエンス
多くのアプリでは、検索ボックスに 1 つ以上の文字を入力して、大きなデータ セット内のレコードの一覧をフィルター処理することができます。 入力すると、一覧には、検索条件に一致するレコードのみが表示されます。

このトピックの残りの部分にある例では、次のデータを含む **Customers** という一覧を検索した場合の結果を示しています。

![](media/function-startswith/customers.png)

このデータ ソースをコレクションとして作成するには、**[ボタン](../controls/control-button.md)** コントロールを作成し、その **OnSelect** プロパティを次の数式に設定します。

**ClearCollect( Customers, Table( { Name: "Fred Garcia", Company: "Northwind Traders" }, { Name: "Cole Miller", Company: "Contoso" }, { Name: "Glenda Johnson", Company: "Contoso" }, { Name: "Mike Collins", Company: "Adventure Works" }, { Name: "Colleen Jones", Company: "Adventure Works" } ) )**

この例に示すように、画面下部にある[**ギャラリー コントロール**](../controls/control-gallery.md)にレコードの一覧を表示できます。 画面の上部には、ユーザーが関心のあるレコードを指定できるように、**SearchInput** という名前の[**テキスト入力**](../controls/control-text-input.md)コントロールを追加できます。

![](media/function-startswith/customers-ux-unfiltered.png)

ユーザーが **SearchInput** に文字を入力すると、ギャラリーの結果は自動的にフィルター処理されます。 この場合、ギャラリーは、(会社の名前ではなく) 顧客の名前が **SearchInput** の文字シーケンスで始まるレコードを表示するように構成されています。ユーザーが検索ボックスに「**co**」と入力した場合、ギャラリーには次の結果が表示されます。

![](media/function-startswith/customers-ux-startswith-co.png)

**Name** 列に基づいてフィルター処理するには、ギャラリー コントロールの **Items** プロパティを次の数式のいずれかに設定します。

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Filter( Customers, StartsWith( Name, SearchInput.Text ) )** |**Customers** データ ソースで、検索文字列が **Name** 列の先頭に出現するレコードをフィルター処理します。 このテストでは、大文字と小文字が区別されません。 ユーザーが検索ボックスに「**co**」と入力した場合、ギャラリーには、**Colleen Jones** と **Cole Miller** が表示されます。 ギャラリーに **Mike Collins** が表示されないのは、そのレコードの **Name** 列の先頭に検索文字列がないためです。 |<style> img { max-width: none } </style> ![](media/function-startswith/customers-name-co-startswith.png) |
| **Filter( Customers, SearchInput.Text in Name )** |**Customers** データ ソースで、検索文字列が **Name** 列のどこかに出現するレコードをフィルター処理します。 このテストでは、大文字と小文字が区別されません。 ユーザーが検索ボックスに「**co**」と入力した場合、ギャラリーには、**Colleen Jones**、**Cole Miller**、および **Mike Collins** が表示されます。これは、検索文字列が、これらすべてのレコードの **Name** 列のどこかに出現しているためです。 |<style> img { max-width: none } </style> ![](media/function-startswith/customers-name-co-contains.png) |
| **Search( Customers, SearchInput.Text, "Name" )** |**in** 演算子を使用した場合と同様、**Search** 関数は、各レコードの **Name** 列内で一致を検索します。 列名を二重引用符で囲む必要があることに注意してください。 |<style> img { max-width: none } </style> ![](media/function-startswith/customers-name-co-contains.png) |

**Name** 列だけでなく **Company** 列を含めるように検索範囲を広げることができます。

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Filter( Customers, StartsWith( Name, SearchInput.Text ) &#124;&#124; StartsWith( Company, SearchInput.Text ) )** |**Customers** データ ソースで、**Name** 列または **Company** 列の先頭に検索文字列 (たとえば、**co**) があるレコードをフィルター処理します。  どちらか一方の **StartsWith** 関数が *true* の場合、[**&#124;&#124;** 演算子](operators.md)は *true* になります。 |<style> img { max-width: none } </style> ![](media/function-startswith/customers-all-co-startswith.png) |
| **Filter( Customers, SearchInput.Text in Name &#124;&#124; SearchInput.Text in Company )** |**Customers** データ ソースで、**Name** 列または **Company** 列の中に検索文字列 (たとえば、**co**) が含まれているレコードをフィルター処理します。 |<style> img { max-width: none } </style> ![](media/function-startswith/customers-all-co-contains.png) |
| **Search( Customers, SearchInput.Text, "Name", "Company" )** |**in** 演算子を使用した場合と同様、**Search** 関数は、**Customers** データ ソースで、**Name** 列または **Company** 列の中に検索文字列 (たとえば、**co**) が含まれているレコードを検索します。 複数の列と複数の **in** 演算子を指定する場合は、**Filter** よりも **Search**関数の方が読み書きが簡単です。 列の名前を二重引用符で囲む必要があることに注意してください。 |<style> img { max-width: none } </style> ![](media/function-startswith/customers-all-co-contains.png) |


---
title: Patch 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Patch 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 10/21/2015
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 3adb036a1619263d2b8cef1f649c2d2f97925ceb
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61543908"
---
# <a name="patch-function-in-powerapps"></a>PowerApps の Patch 関数
[データ ソース](../working-with-data-sources.md)内で 1 つ以上の[レコード](../working-with-tables.md#records)を変更または作成するか、データ ソースの外部でレコードをマージします。

**Patch** 関数は、複雑な状況でレコードを変更するために使用します (ユーザーの操作を必要としない更新を実行する場合や、複数の画面にまたがったフォームを使用するなど)。

それほど複雑でない状況の場合は、**編集フォーム** コントロールを使用して、データ ソース内のレコードをより簡単に更新することができます。 **編集フォーム** コントロールを追加する場合には、データ ソースへの変更を入力し、その後保存するためのフォームをユーザーに提供します。 詳しくは、「[データ フォームの概要](../working-with-forms.md)」をご覧ください。

## <a name="overview"></a>概要
**Patch** 関数を使用して、データ ソースの 1 つ以上のレコードを変更します。  特定の[フィールド](../working-with-tables.md#elements-of-a-table)の値が、その他のプロパティに影響を与えることなく変更されます。 たとえば、次の式では、Contoso という名前の顧客の電話番号が変更されます。

`Patch( Customers, First( Filter( Customers, Name = "Contoso" ) ), { Phone: “1-212-555-1234” } )`

**Patch** は、レコードを作成するために **[Defaults](function-defaults.md)** 関数と併せて使用します。 この動作は、レコードの作成と編集に使用する[単一の画面](../working-with-data-sources.md)を構築するのに使用できます。 たとえば、次の式では、Contoso という名前の顧客のレコードが作成されます。

`Patch( Customers, Defaults( Customer ), { Name: “Contoso” } )`

データ ソースを使用していない場合でも、**Patch** を使用して 2 つ以上のレコードをマージすることができます。 たとえば、次の式では、2 つのレコードがマージされ、Contoso の電話番号と所在地の両方を識別するレコードが作成されます。

`Patch( { Name: "Contoso", Phone: “1-212-555-1234” }, { Name: "Contoso", Location: “Midtown”  } )`

## <a name="description"></a>説明
### <a name="modify-or-create-a-record-in-a-data-source"></a>データ ソースのレコードを変更または作成する
データ ソースに対してこの関数を使用するには、データ ソースを指定し、基本レコードを指定します。

* レコードを変更する場合、基本レコードはデータ ソースからのものである必要があります。  基本レコードは、ギャラリーの **[Items](../controls/properties-core.md)** プロパティから取得されて[コンテキスト変数](../working-with-variables.md#use-a-context-variable)内に配置されることも、他のパスを通じて取得されることもあります。 しかし、基本レコードは、データ ソースまで追跡可能である必要があります。  レコードには、変更する際にそのレコードを再度特定するのに役立つ情報を追加するため、これは重要です。  
* レコードを作成する際は、**[Defaults](function-defaults.md)** 関数を使用して既定値で基本レコードを作成します。  

次に、1 つ以上の変更レコードを指定します。各レコードには、基本レコード内のプロパティ値をオーバーライドする新しいプロパティ値が含まれます。 変更レコードは、引数リストの先頭から末尾まで順に処理されます。その際、前のプロパティ値は後のプロパティ値によってオーバーライドされます。

**Patch** の戻り値は、変更または作成したレコードです。  レコードを作成した場合、戻り値にはデータ ソースによって自動的に生成されたプロパティが含まれる場合があります。

データ ソースを更新するとき、1 つまたは複数の問題が発生する場合があります。 [データ ソースの利用](../working-with-data-sources.md)に関する記事で説明されているとおり、問題の特定と調査には **[Errors](function-errors.md)** 関数を使用します。

関連する関数として、レコード全体の置き換えに使用できる **[Update](function-update-updateif.md)** 関数や、レコードの作成に使用できる **[Collect](function-clear-collect-clearcollect.md)** 関数などがあります。  **[UpdateIf](function-update-updateif.md)** 関数を使用すると、条件に基づいて複数のレコードの特定のプロパティを変更できます。

### <a name="modify-or-create-a-set-of-records-in-a-data-source"></a>データ ソースのレコード セットを変更または作成する
**Patch** は、1 回の呼び出しで複数のレコードを作成または変更するときにも使用できます。

基本レコードを 1 つ渡す代わりに、2 番目の引数で基本レコードのテーブルを渡せます。  変更レコードもテーブルで渡され、基本レコードに一対一で対応します。  各変更テーブル内のレコードの数は、基本テーブル内のレコードの数と同じである必要があります。

この方法で **Patch** を使用した場合、戻り値もテーブルになり、その各レコードは基本レコードと変更レコードに一対一で対応します。

### <a name="merge-records-outside-of-a-data-source"></a>データ ソースの外部でレコードをマージする
マージする 2 つ以上のレコードを指定します。 レコードは、引数リストの先頭から末尾まで順に処理されます。その際、前のプロパティ値は後のプロパティ値によってオーバーライドされます。

**Patch** はマージされたレコードを返します。引数またはデータ ソース内のレコードは変更されません。

## <a name="syntax"></a>構文
#### <a name="modify-or-create-a-record-in-a-data-source"></a>データ ソースのレコードを変更または作成する
**Patch**( *DataSource*, *BaseRecord*, *ChangeRecord1* [, *ChangeRecord2*, … ])

* *DataSource* – 必須。 変更するレコードを含むデータ ソースまたはこれから作成するレコードを含むデータ ソース。
* *BaseRecord* – 必須。 変更または作成するレコード。  レコードがデータ ソースからのものだった場合、レコードが検出され、変更されます。 **[Defaults](function-defaults.md)** の結果を使用した場合は、レコードが作成されます。
* *ChangeRecord(s)* – 必須。  *BaseRecord* 内で変更するプロパティを含む、1 つまたは複数のレコード。  変更レコードは、引数リストの先頭から末尾まで順に処理されます。その際、前のプロパティ値は後のプロパティ値によってオーバーライドされます。

#### <a name="modify-or-create-a-set-of-records-in-a-data-source"></a>データ ソースのレコード セットを変更または作成する
**Patch**( *DataSource*, *BaseRecordsTable*, *ChangeRecordTable1* [, *ChangeRecordTable2*, … ] )

* *DataSource* – 必須。 変更するレコードを含むデータ ソースまたはこれから作成するレコードを含むデータ ソース。
* *BaseRecordTable* – 必須。 変更または作成するレコードのテーブル。  レコードがデータ ソースからのものだった場合、レコードが検出され、変更されます。 **[Defaults](function-defaults.md)** の結果を使用した場合は、レコードが作成されます。
* *ChangeRecordTable(s)* – 必須。  *BaseRecordTable* の各レコードで変更するプロパティを含む、1 つまたは複数のレコード テーブル。  変更レコードは、引数リストの先頭から末尾まで順に処理されます。その際、前のプロパティ値は後のプロパティ値によってオーバーライドされます。

#### <a name="merge-records"></a>レコードをマージする
**Patch**( *Record1*, *Record2* [, …] )

* *Record(s)* - 必須。  少なくとも 2 つ以上の、マージするレコード。 レコードは、引数リストの先頭から末尾まで順に処理されます。その際、前のプロパティ値は後のプロパティ値によってオーバーライドされます。

## <a name="examples"></a>例
#### <a name="modify-or-create-a-record-in-a-data-source"></a>(データ ソースの) レコードを変更または作成する
これらの例では、**IceCream** というデータ ソースのレコードを変更または作成します。このデータ ソースは次の[テーブル](../working-with-tables.md)のデータを含み、**ID** [列](../working-with-tables.md#columns)内の値を自動的に生成します。

![](media/function-patch/icecream.png)

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Patch(&nbsp;IceCream,<br>First( Filter( IceCream, Flavor = "Chocolate" ) ), {&nbsp;Quantity:&nbsp;400&nbsp;} )** |**IceCream** データ ソース内のレコードを変更します。<ul><li> 変更するレコードの **ID** 列には値 **1** が含まれます  (**Chocolate** レコードの ID がこれです)。</li><li>**Quantity** 列の値が **400** に変更されます。 |{&nbsp;ID:&nbsp;1, Flavor:&nbsp;"Chocolate", Quantity:&nbsp;400 }<br><br>**IceCream** データ ソースの **Chocolate** エントリが変更されています。 |
| **Patch( IceCream, Defaults(&nbsp;IceCream ), {&nbsp;Flavor:&nbsp;"Strawberry"&nbsp;}&nbsp;)** |**IceCream** データ ソース内のレコードを作成します。<ul><li>**ID** 列には値 **3** が含まれます。これはデータ ソースが自動的に生成するものです。</li><li>**Quantity** 列には **0** が含まれます。これは **[Defaults](function-defaults.md)** 関数で指定するとおり、**IceCream** データ ソースにおけるこの列の既定値です。<li>**Flavor** 列には **Strawberry** という値が含まれます。</li> |{ ID:&nbsp;3, Flavor:&nbsp;"Strawberry", Quantity:&nbsp;0&nbsp;}<br><br>**IceCream** データ ソースの **Strawberry** エントリが作成されています。 |

前の数式が評価された後、データ ソースはこれらの値で終了します。

![](media/function-patch/icecream-after.png)

#### <a name="merge-records-outside-of-a-data-source"></a>(データ ソースの外部で) レコードをマージする

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Patch(&nbsp;{&nbsp;Name:&nbsp;"James",&nbsp;Score:&nbsp;90&nbsp;}, {&nbsp;Name:&nbsp;"Jim",&nbsp;Passed:&nbsp;true&nbsp;} )** |データ ソースの外部で 2 つのレコードをマージします。<br><ul><li>各レコードの **Name** 列の値は一致しません。 結果には、引数リストの先頭に近いレコードの値 (**James**) ではなく、末尾に近いレコードの値 (**Jim**) が含まれます。</li><li>最初のレコードには、2 番目のレコードには存在しない列 (**Score**) が含まれます。 結果には、その列とその値 (**90**) が含まれます。</li><li>2 番目のレコードには、最初のレコードには存在しない列 (**Passed**) が含まれます。 結果には、その列とその値 (**true**) が含まれます。 |{&nbsp;Name:&nbsp;"Jim", Score:&nbsp;90, Passed:&nbsp;true&nbsp;} |


---
title: Remove および RemoveIf 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Remove および RemoveIf 関数の参照情報
documentationcenter: na
author: gregli-msft
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: reference
ms.component: canvas
ms.date: 10/21/2015
ms.author: gregli
ms.openlocfilehash: 1f4df70ce3274c4d83c39955df58ebc344038de3
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "31832715"
---
# <a name="remove-and-removeif-functions-in-powerapps"></a>PowerApps の Remove および RemoveIf 関数
[データ ソース](../working-with-tables.md#records)から[レコード](../working-with-data-sources.md)を削除します。

## <a name="description"></a>説明
### <a name="remove-function"></a>Remove 関数
**Remove** 関数を使用して、1 つまたは複数の特定のレコードをデータ ソースから削除します。  

[コレクション](../working-with-data-sources.md#collections)の場合には、レコード全体が一致している必要があります。 レコードのコピー全部を削除する場合には、**All** 引数を使用します。この引数を使用しなかった場合には、レコードのコピーが 1 つだけ削除されます。

### <a name="removeif-function"></a>RemoveIf 関数
**RemoveIf** 関数を使用して、1 つの条件または一連の条件に基づき、1 つまたは複数のレコードを削除します。 各条件には、結果が **true** または **false** になるものであれば、どのような数式でも指定できます。また、データ ソースの[列](../working-with-tables.md#columns)を、名前を使って参照することもできます。 各条件はレコードごとに個別に評価され、すべての条件が **true** と評価された場合にそのレコードが削除されます。

**Remove** と **RemoveIf** は、変更後のデータ ソースを[テーブル](../working-with-tables.md)として返します。 これらの関数は、いずれも[動作の数式](../working-with-formulas-in-depth.md)内でのみ使用できます。

また、**[Clear](function-clear-collect-clearcollect.md)** 関数を使用して、データ ソースのすべてのレコードを削除することもできます。

### <a name="delegation"></a>委任
[!INCLUDE [delegation-no](../../../includes/delegation-no.md)]

## <a name="syntax"></a>構文
**Remove**( *DataSource*, *Record1* [, *Record2*, ... ] [, **All** ] )

* *DataSource* – 必須。 削除の対象となるレコードが含まれるデータ ソース。
* *Record(s)* – 必須。 削除する 1 つまたは複数のレコード。
* **All** – 省略可能。 コレクションでは、同じレコードが複数存在することがあります。  レコードのコピーをすべて削除するために、**All** 引数を追加できます。

**Remove**( *DataSource*, *Table* [, **All** ] )

* *DataSource* – 必須。 削除の対象となるレコードが含まれるデータ ソース。
* *Table* – 必須。 削除するレコードのテーブル。
* **All** – 省略可能。 コレクションでは、同じレコードが複数存在することがあります。  レコードのコピーをすべて削除するために、**All** 引数を追加できます。

**RemoveIf**( *DataSource*, *Condition* [, ... ] )

* *DataSource* – 必須。 削除の対象となるレコードが含まれるデータ ソース。
* *Condition(s)* – 必須。 削除の対象とするレコードについて評価結果が **true** となる数式。  数式では、*DataSource* の列名を使用できます。  複数の *Condition* を指定する場合、削除の対象とするレコードについて、評価結果がすべて **true** となる必要があります。

## <a name="examples"></a>例
ここで紹介する例では、**IceCream** という名前のデータ ソースの 1 つまたは複数のレコードを削除します。このデータ ソースは次のテーブルのデータから始まります。

![](media/function-remove-removeif/icecream.png)

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Remove(&nbsp;IceCream,<br>First(&nbsp;Filter(&nbsp;IceCream,&nbsp;Flavor="Chocolate"&nbsp;)&nbsp;) )** |データ ソースの **Chocolate** レコードを削除します。 |<style> img { max-width: none } </style> ![](media/function-remove-removeif/icecream-no-chocolate.png)<br><br>**IceCream** データ ソースの内容が変更されました。 |
| **Remove(&nbsp;IceCream,<br>First(&nbsp;Filter(&nbsp;IceCream,&nbsp;Flavor="Chocolate"&nbsp;)&nbsp;) First(&nbsp;Filter(&nbsp;IceCream,&nbsp;Flavor="Strawberry"&nbsp;)&nbsp;) )** |データ ソースから 2 つのレコードを削除します。 |![](media/function-remove-removeif/icecream-only-vanilla.png)<br><br>**IceCream** データ ソースの内容が変更されました。 |
| **RemoveIf(&nbsp;IceCream, Quantity&nbsp;>&nbsp;150 )** |**Quantity** の値が **150** よりも大きいレコードを対象として削除を実行します。 |![](media/function-remove-removeif/icecream-only-chocolate.png)<br><br>**IceCream** データ ソースの内容が変更されました。 |
| **RemoveIf(&nbsp;IceCream, Quantity&nbsp;>&nbsp;150, Left(&nbsp;Flavor,&nbsp;1&nbsp;) = "S" )** |**Quantity** の値が 150 よりも大きく、**Flavor** が **S** で始まるレコードを対象として削除を実行します。 |![](media/function-remove-removeif/icecream-no-strawberry.png)<br><br><br>**IceCream** データ ソースの内容が変更されました。 |
| **RemoveIf(&nbsp;IceCream, true )** |データ ソースからすべてのレコードを削除します。 |![](media/function-remove-removeif/icecream-empty.png)<br><br>**IceCream** データ ソースの内容が変更されました。 |

### <a name="step-by-step"></a>ステップ バイ ステップ
1. **Inventory** という名前のコレクションをインポートまたは作成し、[ギャラリーにデータを表示する](../show-images-text-gallery-sort-filter.md)方法に関するページの手順に従って、コレクションをギャラリーに表示します。
2. ギャラリーで、イメージの **[OnSelect](../controls/properties-core.md)** プロパティを次の式に設定します。<br>**Remove(Inventory, ThisItem)**
3. F5 キーを押し、ギャラリーのイメージを選択します。<br>ギャラリーとコレクションから項目が削除されます。


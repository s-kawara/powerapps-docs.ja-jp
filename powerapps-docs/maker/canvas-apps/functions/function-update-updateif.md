---
title: Update および UpdateIf 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Update および UpdateIf 関数の参照情報
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
ms.openlocfilehash: d74f05c87cd5b9a3e7aed7891c6d2aaa54adfd1a
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61548575"
---
# <a name="update-and-updateif-functions-in-powerapps"></a>PowerApps の Update および UpdateIf 関数
[データ ソース](../working-with-data-sources.md)内の[レコード](../working-with-tables.md#records)を更新します。

## <a name="description"></a>説明
### <a name="update-function"></a>Update 関数
データ ソースのレコード全体を置換するときには、**Update** 関数を使用します。 これに対して、**UpdateIf** 関数と **[Patch](function-patch.md)** 関数は、レコード内の一定の値だけを変更し、残りの値をそのまま維持するものです。

[コレクション](../working-with-data-sources.md#collections)の場合には、レコード全体が一致している必要があります。 コレクションではレコードの重複が許可されているため、複数のレコードが一致することがあります。 レコードのコピー全部を更新する場合には、**All** 引数を使用します。この引数を使用しなかった場合には、レコードのコピーが 1 つだけ更新されます。

データ ソースによって列の値が自動で生成されている場合には、その[列](../working-with-tables.md#columns)の値を再確認する必要があります。

### <a name="updateif-function"></a>UpdateIf 関数
一定の条件に合致するレコードの値を変更するときには、**UpdateIf** 関数を使用します。 条件には、結果が **true** または **false** になるものであれば、どのような数式でも指定できます。また、データ ソースの列を名前で参照することもできます。 この関数では、各レコードについて条件が評価され、評価結果が **true** のレコードがあれば変更されます。  

変更内容の指定には変更レコードを使用して、そこにプロパティの新しい値を指定します。 この変更レコードを中かっこを使ってインラインで指定した場合には、プロパティの数式が変更対象のレコードのプロパティを参照できるようになります。 数式に基づいてレコードを変更する場合には、この動作を使用します。

特定の列だけを変更し、他の列はそのまま維持する場合には、**UpdateIf** のほかに **[Patch](function-patch.md)** 関数も使用できます。

**Update** と **UpdateIf** のどちらも、変更後のデータ ソースを[テーブル](../working-with-tables.md)として返します。 [動作の数式](../working-with-formulas-in-depth.md)では、どちらかの関数を使用する必要があります。

### <a name="delegation"></a>委任
[!INCLUDE [delegation-no](../../../includes/delegation-no.md)]

## <a name="syntax"></a>構文
**Update**( *DataSource*, *OldRecord*, *NewRecord* [, **All** ] )

* *DataSource* – 必須。 置換の対象となるレコードが含まれるデータ ソース。
* *OldRecord* – 必須。 置換の対象となるレコード。
* *NewRecord* – 必須。 置換後のレコード。 これは、変更レコードとは異なるものです。 この NewRecord で置換されるのはレコード全体であり、不足しているプロパティがある場合には、その値が "*空白*" になります。
* **All** – 省略可能。 コレクションでは、同じレコードが複数存在することがあります。 レコードのコピーをすべて削除する場合には、**All** 引数を指定します。

**UpdateIf**( *DataSource*, *Condition1*, *ChangeRecord1* [, *Condition2*, *ChangeRecord2*, ... ] )

* *DataSource* – 必須。 変更の対象となるレコードが含まれるデータ ソース。
* *Condition(s)* – 必須。 変更の対象となるレコードについて評価結果が **true** となる数式。  数式では、*DataSource* の列名を使用できます。  
* *ChangeRecord(s)* - 必須。  条件別にプロパティの新しい値を指定した変更レコード。この変更レコードで指定された値が、条件を満たした *DataSource* のレコードに適用されます。 中かっこを使ってレコードをインラインで指定した場合には、そのプロパティの数式で既存のレコードのプロパティの値を使用できます。

## <a name="examples"></a>例
ここで紹介する例では、**IceCream** という名前のデータ ソースのレコードを置換したり、変更したりしていきます。このデータ ソースには以下のテーブルが存在し、初期データが次のようになっています。

![](media/function-update-updateif/icecream.png)

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Update(&nbsp;IceCream,<br>First(&nbsp;Filter(&nbsp;IceCream,&nbsp;Flavor="Chocolate"&nbsp;)&nbsp;), {&nbsp;ID:&nbsp;1,&nbsp;Flavor:&nbsp;"Mint&nbsp;Chocolate",&nbsp;Quantity:150&nbsp;} )** |データ ソースのレコードを 1 つ置換します。 |<style> img { max-width: none } </style> ![](media/function-update-updateif/icecream-mint.png)<br><br>**IceCream** データ ソースの内容が変更されました。 |
| **UpdateIf(&nbsp;IceCream, Quantity > 175, {&nbsp;Quantity:&nbsp;Quantity&nbsp;+&nbsp;10&nbsp;} )** |**Quantity** の値が **150** よりも大きなレコードを対象として変更を実施します。  **Quantity** フィールドの値を 10 増やします。他のフィールドは変更しません。 |![](media/function-update-updateif/icecream-mint-plus10.png)<br><br>**IceCream** データ ソースの内容が変更されました。 |
| **Update(&nbsp;IceCream,<br>First(&nbsp;Filter(&nbsp;IceCream, Flavor="Strawberry"&nbsp;)&nbsp;),<br>{&nbsp;ID:&nbsp;3, Flavor:&nbsp;"Strawberry Swirl"} )** |データ ソースのレコードを 1 つ置換します。 置換レコードで **Quantity** プロパティが指定されていないため、結果ではこのプロパティが "*空白*" になります。 |![](media/function-update-updateif/icecream-mint-swirl.png)<br><br>**IceCream** データ ソースの内容が変更されました。 |
| **UpdateIf(&nbsp;IceCream, true, {&nbsp;Quantity:&nbsp;0&nbsp;} )** |データ ソース内の全レコードについて、**Quantity** プロパティの値を 0 に設定します。 |![ ](./media/function-update-updateif/icecream-mint-zero.png)<br> <br>**IceCream** データ ソースの内容が変更されました。 |

### <a name="step-by-step"></a>ステップ バイ ステップ
1. **Inventory** という名前のコレクションをインポートまたは作成し、[ギャラリーにデータを表示する](../show-images-text-gallery-sort-filter.md)方法に関するページの手順に従って、コレクションをギャラリーに表示します。
2. ギャラリーの名前として **ProductGallery** を指定します。
3. **UnitsSold** という名前のスライダーを追加し、**Max** プロパティを次の数式に設定します。<br>**ProductGallery.Selected.UnitsInStock**
4. ボタンを追加し、**[OnSelect](../controls/properties-core.md)** プロパティを次の数式に設定します。<br>**UpdateIf(Inventory, ProductName = ProductGallery.Selected.ProductName, {UnitsInStock:UnitsInStock-UnitsSold.Value})**
5. F5 キーを押し、ギャラリーで製品を選択して、スライダーで目的の値を指定したら、ボタンを推します。
   
    指定した製品の在庫数が、指定した量だけ減少します。


---
title: Collect、Clear、および ClearCollect 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Collect、Clear、および ClearCollect 関数の参照情報
documentationcenter: na
author: gregli-msft
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: reference
ms.component: canvas
ms.date: 11/01/2015
ms.author: gregli
ms.openlocfilehash: 9d67db7829361565072362b6ac37125dc0dc673a
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "31834106"
---
# <a name="collect-clear-and-clearcollect-functions-in-powerapps"></a>PowerApps の Collect、Clear、および ClearCollect 関数
[コレクション](../working-with-data-sources.md#collections)の作成とクリアおよび任意の[データ ソース](../working-with-data-sources.md)への[レコード](../working-with-tables.md#records)の追加を行います。

## <a name="description"></a>説明
### <a name="collect"></a>Collect
**Collect** 関数は、データ ソースにレコードを追加します。 次の項目を追加できます。

* 1 つの値: 値は新しいレコードの **[Value](function-value.md)** フィールドに配置されます。  その他のプロパティはすべて[空白](function-isblank-isempty.md)のままになります。
* レコード: 指定した各プロパティは、新しいレコードの対応するプロパティに配置されます。  その他のプロパティはすべて空白のままになります。
* [テーブル](../working-with-tables.md): テーブルの各レコードは、前述のように、データ ソースの個別のレコードとして追加されます。 テーブルが入れ子になったテーブルとしてはレコードに追加されることはありません。 これを行うには、先にレコードでテーブルをラップします。

コレクションに対して使用した場合は、必要に応じて追加の[列](../working-with-tables.md#columns)が作成されます。 その他のデータ ソースの列はデータ ソースによって固定されており、新しい列を追加することはできません。  

データ ソースがまだ存在しない場合は、コレクションが作成されます。

コレクションは、グローバル変数を保持するためや、データ ソースの一時的なコピーを作成するために、使用されることがあります。 PowerApps では基本的に、ユーザーがアプリを操作すると、数式が自動的に再計算されます。 コレクションでは再計算されません。そのため、コレクションを使うと、アプリの作成が難しく、わかりにくくなる場合があります。 この方法でコレクションを使用する場合は、先に[変数の使用方法](../working-with-variables.md)を確認してください。

また、**[Patch](function-patch.md)** 関数を使用して、データ ソースのレコードを作成することもできます。

**Collect** は、変更されたデータ ソースをテーブルとして返します。  **Collect** は、[動作の数式](../working-with-formulas-in-depth.md)内でのみ使用できます。

### <a name="clear"></a>Clear
**Clear** 関数は、コレクションのすべてのレコードを削除します。  コレクションの列は残ります。

**Clear** は、コレクションに対してのみ動作し、その他のデータ ソースでは動作しません。  その他のデータ ソースには、**[RemoveIf](function-remove-removeif.md)( *DataSource*, true )** を使用できます。  ただし、データ ソースのストレージからすべてのレコードが削除され、他のユーザーに影響する可能性があるため、注意してください。

**[Remove](function-remove-removeif.md)** 関数を使用すると、レコードを選択して削除できます。

**Clear** には、戻り値がありません。  Clear は、動作の数式内でのみ使用できます。

### <a name="clearcollect"></a>ClearCollect
**ClearCollect** 関数は、コレクションからすべてのレコードを削除し、同じコレクションに異なるレコード セットを追加します。  **ClearCollect** は、1 つの関数で、**Clear** の後に **Collect** を実行します。

**ClearCollect** は、変更されたコレクションをテーブルとして返します。  **ClearCollect** は、動作の数式内でのみ使用できます。

## <a name="syntax"></a>構文
**Collect**( *DataSource*, *Item*, ... )

* *DataSource* – 必須。 データを追加するデータ ソース。  存在しない場合は、新しいコレクションが作成されます。
* *Item(s)* - 必須。  データ ソースに追加する 1 つ以上のレコードまたはテーブル。  

**Clear**( *Collection* )

* *Collection* - 必須。 クリアするコレクション。

**ClearCollect**( *Collection*, *Item*, ... )

* *Collection* - 必須。 クリアした後にデータを追加するコレクション。
* *Item(s)* - 必須。  データ ソースに追加する 1 つ以上のレコードまたはテーブル。  

## <a name="examples"></a>例
### <a name="clearing-and-adding-records-to-a-data-source"></a>データ ソースのクリアとレコードの追加
次の例では、**IceCream** という名前のコレクションに対して消去および追加を行います。  このデータ ソースの先頭には、次の内容が含まれています。

![](media/function-clear-collect-clearcollect/icecream.png)

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **ClearCollect( IceCream, {&nbsp;Flavor:&nbsp;"Strawberry",&nbsp;Quantity:&nbsp;300&nbsp;} )** |**IceCream** コレクションのすべてのデータをクリアし、その後、ストロベリー アイスクリームの数量を含むレコードを追加します。 |<style> img { max-width: none } </style> ![](media/function-clear-collect-clearcollect/icecream-clearcollect.png)<br><br>**IceCream** データ ソースも変更されています。 |
| **Collect( IceCream, {&nbsp;Flavor:&nbsp;"Pistachio",&nbsp;Quantity:&nbsp;40&nbsp;}, {&nbsp;Flavor:&nbsp;"Orange",&nbsp;Quantity:&nbsp;200&nbsp;}  )** |ピスタチオとオレンジ アイスクリームの数量を含む 2 つのレコードを **IceCream** コレクションに追加します。 |![](media/function-clear-collect-clearcollect/icecream-collect.png)<br><br>**IceCream** データ ソースも変更されています。 |
| **Clear( IceCream )** |**IceCream** コレクションからすべてのレコードを削除します。 |![](media/function-clear-collect-clearcollect/icecream-clear.png)<br><br>**IceCream** データ ソースも変更されています。 |

### <a name="step-by-step"></a>ステップ バイ ステップ
1. ボタンを追加し、その **[OnSelect](../controls/properties-core.md)** プロパティを次の関数に設定します。<br>**Collect(Products, &quot;Europa&quot;, &quot;Ganymede&quot;, &quot;Callisto&quot;)**
   
    この関数では、3 つの各製品名の行を含む **Products** という名前のコレクションを作成します。
2. F5 キーを押し、ボタンをクリックしてから、Esc キーを押して、デザイン ワークスペースに戻ります。
3. (省略可能) 作成したコレクションのプレビューを表示するには、**[コンテンツ]** タブで **[コレクション]** をクリックします。


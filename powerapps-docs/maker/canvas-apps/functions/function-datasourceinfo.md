---
title: DataSourceInfo 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の DataSourceInfo 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 11/11/2015
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: d856ccd086a919e206175c25eee19f435325fb8c
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61551312"
---
# <a name="datasourceinfo-function-in-powerapps"></a>PowerApps の DataSourceInfo 関数
[データ ソース](../working-with-data-sources.md)に関する情報を返します。

## <a name="overview"></a>概要
データ ソースは、ユーザー エクスペリエンスの最適化に役立つさまざまな情報を提供できます。

**[Patch](function-patch.md)** 関数を使用する前に、[列](../working-with-tables.md#columns)レベルの情報を使用して、ユーザー入力を検証し、ユーザーにすぐにフィードバックを返すことができます。 **[Validate](function-validate.md)** 関数では、これと同じ情報を使用します。

データ ソース レベルの情報を使用して、たとえば、[レコード](../working-with-tables.md#records)を編集および作成するためのアクセス許可を持たないユーザーに対して、**編集**および**新規作成**用のボタンを無効または非表示にすることができます。

データ ソースが提供する情報の量は、データ ソースによって異なります。まったく情報を提供しないデータ ソースもあります。  [コレクション](../working-with-data-sources.md#collections)は情報を提供しません。 情報が提供されない場合は、既定値が使用されるか、"*空白*" が返されます。

## <a name="description"></a>説明
### <a name="column-information"></a>列の情報
**DataSourceInfo** を使用すると、データ ソースの特定の列に関する次の情報を取得できます。  

| 情報の引数 | 結果の型 | 説明 |
| --- | --- | --- |
| **DataSourceInfo.DisplayName** |String |列の表示名。 表示名が定義されていない場合は、列名を返します。 |
| **DataSourceInfo.MaxLength** |Number |列が保持できる最大文字数。 文字列が含まれている列にのみ適用されます。 最大数が設定されていない場合は、"*空白*" を返します。 |
| **DataSourceInfo.MaxValue** |Number |列が保持できる最大値。 数値が含まれている列にのみ適用されます。 最大値が設定されていない場合は、"*空白*" を返します。 |
| **DataSourceInfo.MinValue** |Number |列が保持できる最小値。 数値が含まれている列にのみ適用されます。 最小値が設定されていない場合は、"*空白*" を返します。 |
| **DataSourceInfo.Required** |Boolean |この列の値が必須かどうか。 データ ソースで設定されていない場合は、**false** を返します。 |

3 番目の引数は、列の名前 (文字列) です。  たとえば、**People** コレクションの **Phone** は、**"Phone"** として渡されます (二重引用符が含まれます)。

### <a name="data-source-information"></a>データ ソースの情報
**DataSourceInfo** を使用すると、データ ソース全体に関する次の情報を取得することもできます。  

| 情報の引数 | 結果の型 | 説明 |
| --- | --- | --- |
| **DataSourceInfo.AllowedValues** |Boolean |このデータ ソースに対してユーザーに付与できるアクセス許可の種類。 データ ソースで設定されていない場合は、"*空白*" を返します。 |
| **DataSourceInfo.CreatePermission** |Boolean |現在のユーザーに対象データ ソースのレコードを作成するためのアクセス許可があるかどうか。 データ ソースで設定されていない場合は、**true** を返します。 |
| **DataSourceInfo.DeletePermission** |Boolean |現在のユーザーに対象データ ソースのレコードを削除するためのアクセス許可があるかどうか。 データ ソースで設定されていない場合は、**true** を返します。 |
| **DataSourceInfo.EditPermission** |Boolean |現在のユーザーに対象データ ソースのレコードを編集するためのアクセス許可があるかどうか。 データ ソースで設定されていない場合は、**true** を返します。 |
| **DataSourceInfo.ReadPermission** |Boolean |現在のユーザーに対象データ ソースのレコードを読み取るためのアクセス許可があるかどうか。 データ ソースで設定されていない場合は、**true** を返します。 |

## <a name="syntax"></a>構文
**DataSourceInfo**( *DataSource*, *Information*, *ColumnName* )

* *DataSource* – 必須。 使用するデータ ソース。
* *Information* – 必須。 取得する情報の種類。
* *ColumnName* – 省略可能。 列レベルの情報の場合は、列名 (文字列)。 **Phone** は、**"Phone"** として渡されます (二重引用符が含まれます)。 データ ソース レベルの情報の場合は、*ColumnName* 引数を使用することはできません。
  
    > [!NOTE]
  > 名前にスペースが使われている列を含む SharePoint および Excel のデータ ソースの場合、各スペースを **"\_x0020\_"** として指定します。 たとえば、**"Column Name"** として **"Column_x0020_Name"** を指定します。

## <a name="examples"></a>例
このセクションの例では、**IceCream** という名前のデータ ソースを使用します。

![](media/function-datasourceinfo/icecream.png)

このデータ ソースは、次の情報も提供します。

* **Quantity** の表示名は "Quantity on Hand" です。
* **Flavor** の最大長は 30 文字です。
* **Flavor** 列には値を含める必要があります。 **Quantity** 列は必須ではありません。
* **Quantity** の最小値は 0 です。
* **Quantity** の最大値は 100 です。
* 現在のユーザーは、**IceCream** データ ソースのレコードの読み取りと編集を行うことができますが、レコードを作成および削除することはできません。

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **DataSourceInfo(&nbsp;IceCream, DataSourceInfo.DisplayName,&nbsp;"Quantity"&nbsp;)** |**IceCream** データ ソースの **Quantity** 列の表示名を返します。 |"Quantity on Hand" |
| **DataSourceInfo(&nbsp;IceCream, DataSourceInfo.MaxLength,&nbsp;"Flavor"&nbsp;)** |**IceCream** データ ソースの **Flavor** 列の文字列の最大長を返します。 |30 |
| **DataSourceInfo(&nbsp;IceCream, DataSourceInfo.Required,&nbsp;"Flavor"&nbsp;)** |**IceCream** データ ソースの **Flavor** 列が必須かどうか。 |**true** |
| **DataSourceInfo(&nbsp;IceCream, DataSourceInfo.Required,&nbsp;"Quantity"&nbsp;)** |**IceCream** データ ソースの **Quantity** 列が必須かどうか。 |**false** |
| **DataSourceInfo(&nbsp;IceCream, DataSourceInfo.MaxValue,&nbsp;"Quantity"&nbsp;)** |**IceCream** データ ソースの **Quantity** 列の最大値を返します。 |100 |
| **DataSourceInfo(&nbsp;IceCream, DataSourceInfo.MinValue,&nbsp;"Quantity"&nbsp;)** |**IceCream** データ ソースの **Quantity** 列の最小値を返します。 |0 |
| **DataSourceInfo(&nbsp;IceCream, DataSourceInfo.ReadPermission)** |現在のユーザーが **IceCream** データ ソースのレコードを読み取ることができるかどうか。 |**true** |
| **DataSourceInfo(&nbsp;IceCream, DataSourceInfo.EditPermission)** |現在のユーザーが **IceCream** データ ソースのレコードを編集できるかどうか。 |**true** |
| **DataSourceInfo(&nbsp;IceCream, DataSourceInfo.CreatePermission)** |現在のユーザーが **IceCream** データ ソースのレコードを作成できるかどうか。 |**false** |
| **DataSourceInfo(&nbsp;IceCream, DataSourceInfo.DeletePermission)** |現在のユーザーが **IceCream** データ ソースのレコードを削除できるかどうか。 |**false** |


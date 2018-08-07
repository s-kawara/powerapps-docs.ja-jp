---
title: GroupBy 関数と Ungroup 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の GroupBy 関数と Ungroup 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 04/26/2016
ms.author: gregli
ms.openlocfilehash: 1c54b905c4942ab824d10acbb32dbc5d7a4a98a7
ms.sourcegitcommit: 0f6d7bb9e524202c065b9a7ef92a7f54bdc4bc7c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2018
ms.locfileid: "39021414"
---
# <a name="groupby-and-ungroup-functions-in-powerapps"></a>PowerApps の GroupBy 関数と Ungroup 関数
[テーブル](../working-with-tables.md)の[レコード](../working-with-tables.md#records)のグループ化とグループ化解除を行います。

## <a name="description"></a>説明
**GroupBy** 関数は、1 つ以上の[列](../working-with-tables.md#columns)の値に基づいてレコードをグループ化したテーブルを返します。 同じグループのレコードは単一のレコードにまとめられ、列が追加されます。この列には、残りの列が入れ子になったテーブルが保持されます。   

**Ungroup** 関数では、**GroupBy** と逆の処理が行われます。 この関数は、グループ化されていたレコードを個別のレコードに分割してテーブルを返します。

**GroupBy** でレコードをグループ化し、返されたテーブルに変更を加え、それから **Ungroup** を使ってその変更したテーブルのレコードのグループ化を解除することができます。 たとえば、次の方法でレコードのグループを削除できます。

* **GroupBy** 関数を使用します。
* **[Filter](function-filter-lookup.md)** 関数を使用して、レコードのグループ全体を削除します。
* **Ungroup** 関数を使用します。  

グループ化に基づいて結果を集計することもできます。

* **GroupBy** 関数を使用します。
* **[Sum](function-aggregates.md)**、**[Average](function-aggregates.md)**、その他の集計関数と共に **[AddColumns](function-table-shaping.md)** 関数を使用して、グループ テーブルの集計結果である新しい列を追加します。
* **[DropColumns](function-table-shaping.md)** 関数を使用して、グループ テーブルを削除します。

**Ungroup** は、**GroupBy** に渡されたレコードの順番を元のまま保持しようとしますが、  必ずしも可能ではありません (元のテーブルに "*空白*" のレコードが含まれている場合など)。

テーブルは、文字列や数値と同様、PowerApps 内での値です。 テーブルは関数の引数として指定できるほか、関数で返すことができます。 **GroupBy** と **Ungroup** では、テーブルは変更されません。代わりに、これらの関数はテーブルを引数として受け取り、別のテーブルを返します。 詳細については、[テーブルの使用](../working-with-tables.md)に関するページを参照してください。

## <a name="syntax"></a>構文
**GroupBy**( *Table*, *ColumnName1* [, *ColumnName2*, ... ], *GroupColumnName* )

* *Table* - 必須。 グループ化するテーブル。
* *ColumnName(s)* - 必須。  レコードをグループ化する基準となる、*Table* 内の列名。  これらの列は、返されるテーブルで列になります。
* *GroupColumnName* - 必須。  *ColumnName(s)* 内にないレコード データが格納される列の名前。
  
    > [!NOTE]
  > 名前にスペースが使われている列を含む SharePoint および Excel のデータ ソースの場合、各スペースを **"\_x0020\_"** として指定します。 たとえば、**"Column Name"** として **"Column_x0020_Name"** を指定します。

**Ungroup**( *Table*, *GroupColumnName* )

* *Table* - 必須。 グループ化を解除するテーブル。
* *GroupColumnName* - 必須。 **GroupBy** 関数によって設定されたレコード データを含む列。
  
    > [!NOTE]
  > 名前にスペースが使われている列を含む SharePoint および Excel のデータ ソースの場合、各スペースを **"\_x0020\_"** として指定します。 たとえば、**"Column Name"** として **"Column_x0020_Name"** を指定します。

## <a name="examples"></a>例
### <a name="create-a-collection"></a>コレクションの作成
1. ボタンを追加し、**Original** と表示されるように **[Text](../controls/properties-core.md)** プロパティを設定します。
2. **Original** ボタンの **[OnSelect](../controls/properties-core.md)** プロパティを次の式に設定します。
   
    **ClearCollect(CityPopulations, {City:"London", Country:"United Kingdom", Population:8615000}, {City:"Berlin", Country:"Germany", Population:3562000}, {City:"Madrid", Country:"Spain", Population:3165000}, {City:"Rome", Country:"Italy", Population:2874000}, {City:"Paris", Country:"France", Population:2273000}, {City:"Hamburg", Country:"Germany", Population:1760000}, {City:"Barcelona", Country:"Spain", Population:1602000}, {City:"Munich", Country:"Germany", Population:1494000}, {City:"Milan", Country:"Italy", Population:1344000})**
3. F5 キーを押して **Original** ボタンを選択し、Esc キーを押します。
   
    次のデータが含まれた **CityPopulations** という名前の[コレクション](../working-with-data-sources.md#collections)が作成されました。
   
    ![](media/function-groupby/cities.png)
4. このコレクションを表示するには、**[ファイル]** メニューの **[コレクション]** を選択してから、**CityPopulations** コレクションを選択します。  コレクションに含まれているレコードのうち最初の 5 つが表示されます。
   
    ![](media/function-groupby/citypopulations-collection.png)

### <a name="group-records"></a>レコードのグループ化
1. もう 1 つボタンを追加し、**[Text](../controls/properties-core.md)** プロパティを **"Group"** に設定します。
2. このボタンの **[OnSelect](../controls/properties-core.md)** プロパティを次の式に設定します。
   
    **ClearCollect( CitiesByCountry, GroupBy( CityPopulations, "Country", "Cities" ) )**
3. F5 キーを押して **Group** ボタンを選択し、Esc キーを押します。
   
    **CitiesByCountry** という名前のコレクションが作成されました。このコレクションでは、前のコレクションのレコードが **Country** 列に基づいてグループ化されています。
   
    ![](media/function-groupby/cities-grouped.png)
4. このコレクションに含まれているレコードの最初の 5 つを表示するには、**[ファイル]** メニューの **[コレクション]** を選択します。
   
    ![](media/function-groupby/citiesbycountry-collection.png)
5. ある国の各市の人口を表示するには、その国 (例: Germany) の **Cities** 列内のテーブル アイコンを選択します。
   
    ![](media/function-groupby/population-germany.png)

### <a name="filter-and-ungroup-records"></a>レコードのフィルターとグループ化解除
1. もう 1 つボタンを追加し、**"Filter"** と表示されるように **[Text](../controls/properties-core.md)** プロパティを設定します。
2. このボタンの **[OnSelect](../controls/properties-core.md)** プロパティを次の式に設定します。
   
    **ClearCollect( CitiesByCountryFiltered, Filter( CitiesByCountry, "e" in Country ) )**
3. F5 キーを押して追加したボタンを選択し、Esc キーを押します。
   
    **CitiesByCountryFiltered** という名前の 3 つ目のコレクションが作成されました。このコレクションには、名前に "e" が付いた国だけが含まれています (つまり、Spain や Italy は除外)。
   
    ![](media/function-groupby/cities-grouped-hase.png)
4. さらに 1 つボタンを追加し、**"Ungroup"** と表示されるように **[Text](../controls/properties-core.md)** プロパティを設定します。
5. このボタンの **[OnSelect](../controls/properties-core.md)** プロパティを次の式に設定します。
   
    **ClearCollect( CityPopulationsUngrouped, Ungroup( CitiesByCountryFiltered, "Cities" ) )**
   
    結果は次のようになります。
   
    ![](media/function-groupby/cities-hase.png)

### <a name="aggregate-results"></a>結果の集計
このほか、グループ化したテーブルでは結果の集計が行えます。  この例では、各国の主な都市の人口を合計します。

1. もう 1 つボタンを追加し、**"Sum"** と表示されるように **[Text](../controls/properties-core.md)** プロパティを設定します。
2. **"Sum"** ボタンの **[OnSelect](../controls/properties-core.md)** プロパティを次の式に設定します。
   
    **ClearCollect( CityPopulationsSum, AddColumns( CitiesByCountry, "Sum of City Populations", Sum( Cities, Population ) ) )**
   
    結果は次のようになります。
   
    ![](media/function-groupby/cities-sum.png)
   
    **[AddColumns](function-table-shaping.md)** では **CitiesByCountry** コレクションがベースとなり、新しい列 **Sum of City Populations** がそこに追加されます。  この列の値は、数式 **Sum( Cities, Population )** に基づいて行ごとに計算されます。  **AddColumns** によって **Cities** 列 (テーブル) の値が行ごとに入力され、**[Sum](function-aggregates.md)** によってこのサブ テーブルの各行の **Population** が合計されます。
3. 目的の合計値が得られたところで、**[DropColumns](function-table-shaping.md)** を使用してサブ テーブルを削除できます。  次の数式が使用されるように **[OnSelect](../controls/properties-core.md)** プロパティを変更します。
   
    **ClearCollect( CityPopulationsSumOnly, DropColumns( CityPopulationsSum, "Cities" ) )**
   
    結果は次のようになります。
   
    ![](media/function-groupby/cities-sum-drop-cities.png)
   
    このテーブルではグループ化解除が不要だったことに注意してください。


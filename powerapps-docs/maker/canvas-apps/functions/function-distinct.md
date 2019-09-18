---
title: Distinct 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Distinct 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 09/14/2019
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 98fd1b67d4835969ac01b1ce63155bc81ed36630
ms.sourcegitcommit: 5899d37e38ed7111d5a9d9f3561449782702a5e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71038121"
---
# <a name="distinct-function-in-powerapps"></a>PowerApps の Distinct 関数
重複を削除して、[テーブル](../working-with-tables.md)の[レコード](../working-with-tables.md#records)を要約します。

## <a name="description"></a>説明
**Distinct**関数は、テーブルの各レコードに対して数式を評価し、重複する値が削除された結果の1列のテーブルを返します。  列の名前は**Result**です。  

[!INCLUDE [record-scope](../../../includes/record-scope.md)]

[!INCLUDE [delegation-no-one](../../../includes/delegation-no-one.md)]

## <a name="syntax"></a>構文
**Distinct**( *Table*, *Formula* )

* *Table* - 必須。  全体を評価するテーブル。
* *Formula* - 必須。  各レコードについて評価する数式。

## <a name="example"></a>例

1. [**ボタン**](../controls/control-button.md)コントロールを挿入し、その**onselect**プロパティを次の数式に設定します。

    ```powerapps-dot
    ClearCollect( CityPopulations,
        { City: "London",    Country: "United Kingdom", Population: 8615000 },
        { City: "Berlin",    Country: "Germany",        Population: 3562000 },
        { City: "Madrid",    Country: "Spain",          Population: 3165000 },
        { City: "Hamburg",   Country: "Germany",        Population: 1760000 },
        { City: "Barcelona", Country: "Spain",          Population: 1602000 },
        { City: "Munich",    Country: "Germany",        Population: 1494000 }
    );
    ```

1. Alt キーを押しながらボタンを選択します。

    数式は evaluatd であり、数式バーで**CityPopulations**を選択することによって表示できる**CityPopulations** collection が作成されます。

    > [!div class="mx-imgBorder"]
    > ![結果ビューに表示される CityPopulations collection](media/function-distinct/citypopulations-create.png)

1. [**データテーブル**](../controls/control-data-table.md)コントロールを挿入し、その**Items**プロパティを次の数式に設定します。

    ```powerapps-dot
    Distinct( CityPopulations, Country )
    ```

    数式バーで数式全体を選択することで、この数式の結果を表示できます。

    > [!div class="mx-imgBorder"]
    > ![結果ビューに表示される Distinct 関数からの出力](media/function-distinct/citypopulations-distinct.png)

1. データテーブルのプロパティペインの **[フィールドの編集]** リンクを使用すると、**結果**列を追加できます。

    > [!div class="mx-imgBorder"]
    > ![データテーブルに表示される Distinct 関数からの出力](media/function-distinct/citypopulations-datatable.png)

1. [**ラベル**](../controls/control-text-box.md)コントロールを挿入し、その**Text**プロパティを数式に設定します。

    ```powerapps-dot
    First( Sort( Distinct( CityPopulations, Country ), Result ) ).Result
    ```

    この数式では、 [**Sort**](function-sort.md)関数を使用して**Distinct**の結果を並べ替え、結果のテーブルの最初のレコードを[**最初**](function-first-last.md)の関数と共に取得し、**結果**フィールドを抽出して、国名だけを取得します。

    > [!div class="mx-imgBorder"]
    > ![名前で最初の国を示す Distinct 関数からの出力](media/function-distinct/citypopulations-first.png)

     

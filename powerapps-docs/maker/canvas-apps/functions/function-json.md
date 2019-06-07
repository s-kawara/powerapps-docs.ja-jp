---
title: JSON 関数 |Microsoft Docs
description: 構文を含む PowerApps の JSON 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 05/02/2019
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 74e10a5b073e16ba9f35139441c94e9911446a0f
ms.sourcegitcommit: 2084789802fc5134dbeb888e759cced46019a017
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2019
ms.locfileid: "66736401"
---
# <a name="json-function-in-powerapps"></a>PowerApps の JSON 関数

テーブル、レコード、または値の JSON テキスト文字列を生成します。

## <a name="description"></a>説明

**JSON**関数は、格納するか、ネットワーク経由で送信に適したされるようにテキストとしてデータ構造の JavaScript Object Notation (JSON) 表現を返します。 [ECMA 404](http://www.ecma-international.org/publications/files/ECMA-ST/ECMA-404.pdf)と[IETF RFC 8259](https://tools.ietf.org/html/rfc8259) JavaScript と他のプログラミング言語で広く使用される形式について説明します。

キャンバス アプリのサポート、[データ型](data-types.md)テキスト形式の詳細を次の表を一覧表示します。

| データ型 | 説明 | 結果の例 |
|-----------|-------------|---------|
| **ブール値** | *true*または*false*します。 | `true` |
| **色** | 色の 8 桁の 16 進数表現を含む文字列。 この表現形式は、#*rrggbbaa*ここで、 *rr*は赤のコンポーネントの*gg*は緑色で、 *bb*は青、および*aa*はアルファ チャネルです。 アルファ チャネルの**00**が完全に透明と**ff**は完全に不透明です。 文字列を渡すことができます、 [ **ColorValue** ](function-colors.md)関数。  | `"#102030ff"` |
| **通貨** | ユーザーの言語の適切な小数点区切り文字を使用する番号。 必要な場合は、科学的表記法が使用されます。 | `1.345` |
| **日付** | ISO 8601 の日付を含む文字列 **- yyyy-mm-dd**形式。 | `"2019-03-31"` |
| **DateTime** | ISO 8601 の日付/時刻を表す文字列です。 日付/時刻値は utc 形式、終了の"Z"が示すとおりです。  | `"2019-03-31T22:32:06.822Z"`  |
| **GUID** | GUID 値を含む文字列。 文字は小文字です。 | `"751b58ac-380e-4a04-a925-9f375995cc40"`
| **イメージ、メディア** | 場合**IncludeBinaryData**を指定すると、メディア ファイルは、文字列でエンコードされます。 Web 参照、http を使用する: または https:URL スキームは変更されません。 メモリ内バイナリ データへの参照は、エンコード、 ["データ:*mimetype*; base64..."](https://en.wikipedia.org/wiki/Data_URI_scheme)形式。 メモリ内のデータには使用してユーザーをキャプチャするイメージが含まれています、 [**カメラ**](../controls/control-camera.md)コントロールと、appres とその他のすべての参照: と blob:URL スキームです。| `"data:image/jpeg;base64,/9j/4AA..."` |
| **数** | ユーザーの言語の適切な小数点区切り文字を使用する番号。 必要な場合は、科学的表記法が使用されます。 | `1.345` |
| **オプション&nbsp;設定** | オプションの値を数値に設定の表示に使用するラベルではなく。 数値の値は、言語に依存しないために使用されます。  | `1001` |
| **時間** | ISO 8601 を含む文字列*hh:mm:ss.fff*形式。  | `"23:12:49.000"` |
| **レコード** | コンマ区切りリスト、間 **{** と **}** フィールドとその値。 指定する、キャンバス アプリ内のレコードのこの表記法に似ていますが、名前は二重引用符の間に常に。 この形式は、多対一のリレーションシップに基づくレコードをサポートしていません。  | `{ "First Name": "Fred", "Age": 21 }` |
| **テーブル** | コンマ区切りリスト、間 **[** と **]** レコードの。 この形式は、一対多のリレーションシップに基づくテーブルでサポートされていません。  | `[ { "First Name": "Fred", "Age": 21 }, { "First Name": "Jean", "Age": 20 } ]` |
| **2 つ&nbsp;オプション** | 2 つのオプションのブール値*true*または*false*ラベルの表示に使用するではなく。 ブール型の値は、言語に依存しないために使用されます。 | `false` |
| **ハイパーリンクのテキスト** | 二重引用符の間で文字列を指定します。 関数は、円記号で埋め込みの二重引用符記号をエスケープし、"\n"、改行文字を置き換えます他の標準の JavaScript の置換を行います。 | `"This is a string."` |

省略可能な指定*形式*結果の読み取り可能な方法を制御する引数とどのようにサポートされていないと、バイナリ データ型を処理します。 既定では、出力、なし、不要な空白または改行文字、できるだけコンパクトにし、サポートされていないデータ型とバイナリ データが許可されていません。 指定した場合は、複数の形式を組み合わせることができます、 **&** 演算子。

| JSONFormat 列挙型 | 説明 |
|-----------------|-------------|
| **Compact** | 既定値。  出力は、追加のスペースや改行文字がない限り、コンパクトです。 |
| **IndentFour** | 読みやすさを向上させるのには、出力は、列および入れ子レベルごとに改行文字が含まれていて、各インデント レベル 4 つのスペースを使用します。 |
| **IncludeBinaryData** | 結果には、イメージ、ビデオ、およびオーディオ クリップの列が含まれています。 この形式は大幅に結果のサイズを大きくし、アプリのパフォーマンスが低下します。 |
| **IgnoreBinaryData** | 結果には、イメージ、ビデオ、またはオーディオ クリップの列が含まれていません。 どちらも指定する場合**IncludeBinaryData**も**IgnoreBinaryData**、バイナリ データが発生した場合、関数がエラーを生成します。 |
| **IgnoreUnsupportedTypes** | サポートされていないデータ型は許可されているが、結果には含まれません。 既定では、サポートされていないデータ型は、エラーを生成します。 |

使用して、 [ **ShowColumns**と**DropColumns** ](function-table-shaping.md)関数の結果には、データを制御して、サポートされていないデータの種類を削除します。

**JSON**できるメモリとコンピューティング集中型で、これを使用する関数でのみ[動作関数を](../working-with-formulas-in-depth.md)します。 結果をキャプチャする**JSON**に、[変数](../working-with-variables.md)、データ フローで使用することができます。

列に表示名と論理名の両方がある場合、結果には、論理名が含まれています。 表示名は、アプリのユーザーとが、そのため、一般的なサービスへのデータ転送の不適切なの言語を反映します。

## <a name="syntax"></a>構文

**JSON**( *DataStructure* [, *Format* ] )

* *データ構造体*– 必須。 JSON に変換するデータ構造体。  テーブル、レコード、およびプリミティブ型の値はサポートされている、任意に入れ子になった。
* *形式*- 省略可能。  **JSONFormat**列挙値。 既定値は**Compact**、改行文字またはスペースが追加されないし、バイナリ データ、およびサポートされていない列をブロックします。

## <a name="examples"></a>例

### <a name="hierarchical-data"></a>階層データ

1. 挿入、 [**ボタン**](../controls/control-button.md)を制御して、設定、 **OnSelect**プロパティをこの式にします。

    ```powerapps-dot
    ClearCollect( CityPopulations,
        { City: "London",    Country: "United Kingdom", Population: 8615000 },
        { City: "Berlin",    Country: "Germany",        Population: 3562000 },
        { City: "Madrid",    Country: "Spain",          Population: 3165000 },
        { City: "Hamburg",   Country: "Germany",        Population: 1760000 },
        { City: "Barcelona", Country: "Spain",          Population: 1602000 },
        { City: "Munich",    Country: "Germany",        Population: 1494000 }
    );
    ClearCollect( CitiesByCountry, GroupBy( CityPopulations, "Country", "Cities" ) )
    ```

1. Alt キーを押しながら、ボタンを選択します。

    **CitiesByCountry**を選択して表示することでこのデータ構造でコレクションが作成された**コレクション**上、**ファイル**の名前を選択し、メニューのコレクションです。

    > [!div class="mx-imgBorder"]
    > ![CitiesByCountry コレクション](media/function-json/cities-grouped.png)

    選択して、このコレクションを表示することもできます**ファイル** > **アプリ設定** > **詳細設定** >   **。数式バー結果ビューを有効にする**、数式バーで、コレクションの名前を選択して、数式バーの下には、コレクションの名前の横にある下向き矢印を選択します。

    > [!div class="mx-imgBorder"]
    > ![数式バーの結果ビュー内のコレクション](media/function-json/cities-grouped-resultview.png)

1. もう 1 つのボタンを挿入し、設定、 **OnSelect**に次の式のプロパティ。

    ```powerapps-dot
    Set( CitiesByCountryJSON, JSON( CitiesByCountry ) )
    ```

    この数式は、グローバル変数を設定**CitiesByCountryJSON**の JSON 表現に**CitiesByCountry**します。

1. Alt キーを押しながら、ボタンを選択します。

1. 挿入、 [**ラベル**](../controls/control-text-box.md)を制御して、設定、**テキスト**プロパティをこの変数にします。

    ```powerapps-dot
    CitiesByCountryJSON
    ```

    ラベルに表示されますこの結果、スペースなしで、1 つの行で、ネットワーク経由での送信に適した。

    ```json
    [{"Cities":[{"City":"London","Population":8615000}],"Country":"United Kingdom"},{"Cities":[{"City":"Berlin","Population":3562000},{"City":"Hamburg","Population":1760000},{"City":"Munich","Population":1494000}],"Country":"Germany"},{"Cities":[{"City":"Madrid","Population":3165000},{"City":"Barcelona","Population":1602000}],"Country":"Spain"}]
    ```

1. 出力を読みやすくする 2 番目のボタンの数式を変更します。

    ```powerapps-dot
    Set( CitiesByCountryJSON, JSON(CitiesByCountry, JSONFormat.IndentFour ))
    ```

1. Alt キーを押しながら 2 番目のボタンを選択します。

    ラベルより読みやすい結果が表示されます。

    ```json
    [
        {
            "Cities": [
                {
                    "City": "London",
                    "Population": 8615000
                }
            ],
            "Country": "United Kingdom"
        },
        {
            "Cities": [
                {
                    "City": "Berlin",
                    "Population": 3562000
                },
                {
                    "City": "Hamburg",
                    "Population": 1760000
                },
                {
                    "City": "Munich",
                    "Population": 1494000
                }
            ],
            "Country": "Germany"
        },
        {
            "Cities": [
                {
                    "City": "Madrid",
                    "Population": 3165000
                },
                {
                    "City": "Barcelona",
                    "Population": 1602000
                }
            ],
            "Country": "Spain"
        }
    ]
    ```

### <a name="images-and-media-in-base64"></a>イメージとメディアの base64

1. 追加、 [**イメージ**](../controls/control-image.md)コントロール。

    このコントロールは**SampleImage**とします。

1. 追加、 [**ボタン**](../controls/control-button.md)を制御して、設定、 **OnSelect**プロパティをこの式にします。

    ```powerapps-dot
    Set( ImageJSON, JSON( SampleImage, JSONFormat.IncludeBinaryData ) )
    ```

1. Alt キーを押しながら、ボタンを選択します。

1. ラベルを追加し、設定、**テキスト**プロパティをこの変数にします。

    ```powerapps-dot
    ImageJSON
    ```

1. コントロールのサイズを変更し、ほとんどの結果を表示する、必要に応じて、フォント サイズを小さきます。

    ラベルの表示テキスト文字列、 **JSON**関数をキャプチャします。

    ```json
    "data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz4NCjxzdmcgdmVyc2lvbj0iMS4xIg0KCSB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHhtbG5zOnhsaW5rPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5L3hsaW5rIiB4bWxuczphPSJodHRwOi8vbnMuYWRvYmUuY29tL0Fkb2JlU1ZHVmlld2VyRXh0ZW5zaW9ucy8zLjAvIg0KCSB4PSIwcHgiIHk9IjBweCIgd2lkdGg9IjI3MHB4IiBoZWlnaHQ9IjI3MHB4IiBlbmFibGUtYmFja2dyb3VuZD0ibmV3IDAgMCAyNzAgMjcwIiB4bWw6c3BhY2U9InByZXNlcnZlIj4NCgk8ZyBjbGFzcz0ic3QwIj4NCgkJPHJlY3QgeT0iMC43IiBmaWxsPSIjRTlFOUU5IiB3aWR0aD0iMjY5IiBoZWlnaHQ9IjI2OS4zIi8+DQoJCTxwb2x5Z29uIGZpbGw9IiNDQkNCQ0EiIHBvaW50cz0iMjc3LjksMTg3LjEgMjQ1LDE0My40IDE4OC42LDIwMi44IDc1LDgwLjUgLTQuMSwxNjUuMyAtNC4xLDI3MiAyNzcuOSwyNzIiLz4NCgkJPGVsbGlwc2UgZmlsbD0iI0NCQ0JDQSIgY3g9IjIwMi40IiBjeT0iODQuMSIgcng9IjI0LjQiIHJ5PSIyNC4zIi8+DQoJPC9nPg0KPC9zdmc+"
    ```

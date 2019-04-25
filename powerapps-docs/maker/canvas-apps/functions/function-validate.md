---
title: Validate 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Validate 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 11/01/2015
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: d92236d630005b4608719efaadef4537984bc3d6
ms.sourcegitcommit: 4ed29d83e90a2ecbb2f5e9ec5578e47a293a55ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63317683"
---
# <a name="validate-function-in-powerapps"></a>PowerApps の Validate 関数
**Validate** 関数は、特定の[データ ソース](../working-with-data-sources.md)について、単一の[列](../working-with-tables.md#columns)または[レコード](../working-with-tables.md#records)全体の値が有効であるかどうかを確認するものです。  

## <a name="description"></a>説明
ユーザーがデータの変更を送信する前に、送信内容の有効性についてその場でフィードバックを返し、ユーザー エクスペリエンスを向上させることができます。

データ ソースでは、レコード内で値が有効になるための要素に関する情報を指定できます。 この情報として指定できる制約には、次に挙げたものをはじめ、さまざまなものがあります。

* 列に値が必要かどうか
* テキストの文字列の長さ
* 数値の範囲
* 日付の範囲

**Validate** 関数は、この情報に基づいて値が有効であるかどうかを判定し、有効でなかった場合にはその内容に合わせたエラー メッセージを返します。 **[DataSourceInfo](function-datasourceinfo.md)** 関数でも、**Validate** が使用する情報を表示できます。

有効性に関して提供される情報の量は、データ ソースによって異なります。まったく情報を提供しないデータ ソースもあります。 **Validate** では、この情報に基づいて値を検証するのみにとどまります。 **Validate** で問題が発見されなかった場合でも、データの変更の適用に失敗する可能性は依然として残っています。 変更の失敗に関する情報を取得するには、**[Errors](function-errors.md)** 関数を使用します。

**Validate** で問題が見つかった場合には、アプリのユーザーに対して表示させることができるエラー メッセージが返されます。 値がすべて有効な場合には、**Validate** の戻り値が[空白](function-isblank-isempty.md)になります。 有効性に関する情報のない[コレクション](../working-with-data-sources.md#collections)の場合には、値が常に有効になります。

## <a name="syntax"></a>構文
**Validate**( *DataSource*, *Column*, *Value* )

* *DataSource* – 必須。 検証に使用するデータ ソース。
* *Column* – 必須。 検証する列。
* *Value* – 必須。 検証対象として選択した列の値。

**Validate**( *DataSource*, *OriginalRecord*, *Updates* )

* *DataSource* – 必須。 検証に使用するデータ ソース。
* *OriginalRecord* - 必須。  更新内容が検証されるレコード。
* *Updates* - 必須。  元のレコードに適用される変更。

## <a name="examples"></a>例
ここに挙げた例では、データ ソース **Scores** の **Percentage** 列の値が 0 以上 100 以下に収まっている必要があります。 データが有効性の検証に合格すると、関数の戻り値が "*空白*" になります。 これに対して、検証に合格しなかった場合には、エラー メッセージが返されます。

### <a name="validate-with-a-single-column"></a>単一の列の検証

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Validate( Scores, Percentage, 10 )** |**10** がデータ ソース **Scores** の **Percentage** 列の値として有効であるかどうかを確認します。 |"*空白*" |
| **Validate( Scores, Percentage, 120 )** |**120** がデータ ソース **Scores** の **Percentage** 列の値として有効であるかどうかを確認します。 |"Values must be between 0 and 100." |

### <a name="validate-with-a-complete-record"></a>レコード全体の検証

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Validate( Scores, EditRecord, Gallery.Updates )** |**Score** データ ソースのすべての列の値が有効かどうかを確認します。 この例では、**Percentage** 列の値は **10** です。 |"*空白*" |
| **Validate( Scores, EditRecord, Gallery.Updates )** | **Score** データ ソースのすべての列の値が有効かどうかを確認します。 この例では、**Percentage** 列の値は **120** です。 |"Values must be between 0 and 100." |


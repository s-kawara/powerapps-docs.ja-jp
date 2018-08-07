---
title: Concat および Concatenate 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Concat および Concatenate 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 08/28/2017
ms.author: gregli
ms.openlocfilehash: 2ead46b4b34e2013205a412eacd86197a3c3b552
ms.sourcegitcommit: 0f6d7bb9e524202c065b9a7ef92a7f54bdc4bc7c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2018
ms.locfileid: "39015825"
---
# <a name="concat-and-concatenate-functions-in-powerapps"></a>PowerApps の Concat および Concatenate 関数
テキストの個々の文字列および[テーブル](../working-with-tables.md)内の文字列を連結します。

## <a name="description"></a>説明
**Concat** 関数は、テーブルのすべての[レコード](../working-with-tables.md#records)に適用される数式の結果を連結して、単一の文字列を生成します。 この関数は、**[Sum](function-aggregates.md)** 関数が数値をまとめるように、テーブルの文字列をまとめます。

[!INCLUDE [record-scope](../../../includes/record-scope.md)]

文字列を部分文字列のテーブルに分割するには、**[Split](function-split.md)** 関数を使用します。

**Concatenate** 関数は、個々の文字列の組み合わせおよび文字列の単一列テーブルを連結します。 個々の文字列に対して使用した場合、この関数は **&** [演算子](operators.md)と同等です。 **[ShowColumns](function-table-shaping.md)** 関数を含む数式を使用して、複数の列があるテーブルから単一列テーブルを作成できます。

## <a name="syntax"></a>構文
**Concat**( *Table*, *Formula* )

* *Table* - 必須。  操作の対象となるテーブル。
* *Formula* - 必須。  テーブルのレコードに適用する数式。

**Concatenate**( *String1* [, *String2*, ...] )

* *String(s)* - 必須。  個々の文字列の組み合わせまたは文字列の単一列テーブル。

## <a name="examples"></a>例
#### <a name="concat"></a>Concat
1. **[[ボタン]](../controls/control-button.md)** コントロールを追加し、**[OnSelect](../controls/properties-core.md)** プロパティに次の式を設定します。
   
    **Collect(Products, {String:"Violin", Wind:"Trombone", Percussion:"Bongos"}, {String:"Cello", Wind:"Trumpet", Percussion:"Tambourine"})**
2. F5 キーを押し、ボタンをクリックしてから、Esc キーを押して、デザイン ワークスペースに戻ります。
3. **[ラベル](../controls/control-text-box.md)** コントロールを追加し、その **[Text](../controls/properties-core.md)** プロパティを次の数式に設定します。
   
    **Concat(Products, String & " ")**
   
    ラベルには、"**Violin Cello**" と表示されます。

#### <a name="concatenate"></a>Concatenate
1. **[テキスト入力](../controls/control-text-input.md)** コントロールを追加し、**AuthorName** という名前を付けます。
2. **[ラベル](../controls/control-text-box.md)** コントロールを追加し、その **[Text](../controls/properties-core.md)** プロパティを次の数式に設定します。<br>
   **Concatenate("By ", AuthorName.Text)**
3. **[AuthorName]** に自分の名前を入力します。
   
    ラベルには、"**By**" の後に自分の名前が表示されます。

**FirstName** 列と **LastName** 列を含む **Employees** テーブルがある場合、次の数式ではそれらの列の各行のデータが連結されます。
<br>**Concatenate(Employees.FirstName, " ", Employees.LastName)**


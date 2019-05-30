---
title: Concat および Concatenate 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Concat および Concatenate 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 05/23/2019
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 889f612f3da208d4edfccc43a579ced07933b40d
ms.sourcegitcommit: aa9f78c304fe46922aecfe3b3fadb6bda72dfb23
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/24/2019
ms.locfileid: "66216137"
---
# <a name="concat-and-concatenate-functions-in-powerapps"></a>PowerApps の Concat および Concatenate 関数

テキストの個々の文字列および[テーブル](../working-with-tables.md)内の文字列を連結します。

## <a name="description"></a>説明

**Concatenate** 関数は、個々の文字列の組み合わせおよび文字列の単一列テーブルを連結します。 個々 の文字列をこの関数を使用する場合を使用すると、 **&** [演算子](operators.md)します。

**Concat** 関数は、テーブルのすべての[レコード](../working-with-tables.md#records)に適用される数式の結果を連結して、単一の文字列を生成します。 この関数は、 **[Sum](function-aggregates.md)** 関数が数値をまとめるように、テーブルの文字列をまとめます。

[!INCLUDE [record-scope](../../../includes/record-scope.md)]

使用して、 [**分割**](function-split.md)または[ **MatchAll** ](function-ismatch.md)関数に文字列を部分文字列のテーブルに分割します。

## <a name="syntax"></a>構文

**Concat**( *Table*, *Formula* )

- *Table* - 必須。  操作の対象となるテーブル。
- *Formula* - 必須。  テーブルのレコードに適用する数式。

**Concatenate**( *String1* [, *String2*, ...] )

- *String(s)* - 必須。  個々の文字列の組み合わせまたは文字列の単一列テーブル。

## <a name="examples"></a>例

このセクションの例では、これらのグローバル変数を使用します。

- **FirstName** "Jane"を =
- **LastName** "Doe"を =
- **製品** = ![2 つの列と 4 つの行を持つテーブル](media/function-concatenate/products.png)

アプリでこれらのグローバル変数を作成するには、挿入、 [**ボタン**](../controls/control-button.md)を制御して、設定、 **OnSelect**プロパティをこの式に。

```powerapps-dot
Set( FirstName, "Jane" ); Set( LastName, "Doe" );
Set( Products,
    Table(
        { Name: "Violin", Type: "String" },
        { Name: "Cello", Type: "String" },
        { Name: "Trumpet", Type: "Wind" }
    )
)
```

(Alt キーを押しながらクリック) して、ボタンを選択します。

### <a name="concatenate-function-and-the--operator"></a>関数を連結し、& 演算子

これらの例については、次のように設定します。、**テキスト**のプロパティを[**ラベル**](../controls/control-text-box.md)から次の表の最初の列の数式に制御します。

| 数式 | 説明 | 結果 |
|---------|-------------|--------|
| **Concatenate(&nbsp;LastName,&nbsp;",&nbsp;",&nbsp;FirstName&nbsp;)** | 値を連結**LastName**、文字列 **「,」** (コンマは、スペースで後に)、および値**FirstName**。 | "Doe,&nbsp;Jane" |
| **LastName&nbsp;&&nbsp;"、&nbsp;"&nbsp;&&nbsp;FirstName** | 使用を除き、前の例と同じ、 **&** 演算子関数の代わりにします。 | "Doe,&nbsp;Jane" |
| **Concatenate(&nbsp;FirstName,&nbsp;"&nbsp;",&nbsp;LastName&nbsp;)** | 値を連結**FirstName**、文字列 **""** (単一スペース) の値と**LastName**します。 | "Jane&nbsp;Doe" |
| **FirstName&nbsp;&&nbsp;"&nbsp;"&nbsp;&&nbsp;LastName** | 前の例と同じを使用して、 **&** 演算子関数の代わりにします。 | "Jane&nbsp;Doe" |

### <a name="concatenate-with-a-single-column-table"></a>単一列テーブルと連結します。

この例では、垂直方向で空白を追加[**ギャラリー** ](../controls/control-gallery.md)コントロールを設定、**項目**プロパティを次の表に数式にし、ギャラリー テンプレートにラベルを追加します。

| 数式 | 説明 | 結果 |
|---------|-------------|--------|
| **Concatenate( "Name:&nbsp;",&nbsp;Products.Name, ",&nbsp;Type:&nbsp;",&nbsp;Products.Type )** | 内の各レコード、**製品**テーブルで、文字列の連結 **"名前:"** 、製品、文字列の名前 **"、型:"** と製品の種類。  | ![製品のテーブル](media/function-concatenate/single-column.png) |

### <a name="concat-function"></a>Concat 関数

これらの例については、設定、**テキスト**次の表の最初の列からの数式にラベルのプロパティ。

| 数式 | 説明 | 結果 |
|---------|-------------|--------|
| **Concat( Products, Name & ", " )** | 式を評価**名 &「,」** の各レコードについて**製品**し、結果を 1 つのテキスト文字列に連結します。  | "Violin、&nbsp;Cello、&nbsp;トランペット、&nbsp;" |
| **Concat( Filter(&nbsp;Products,&nbsp;Type&nbsp;=&nbsp;"String"&nbsp;), Name & ", " )** | 数式が評価される**名 &「,」** の各レコードについて**製品**フィルターを満たす**型 ="String"** 、し、結果を 1 つのテキスト文字列に連結します。   | "Violin、&nbsp;Cello、&nbsp;" |

### <a name="trimming-the-end"></a>最後のトリミング

最後の 2 つの例では、余分な結果の末尾に「,」です。 関数は、コンマとスペースを追加します、**名前**を最後のレコードを含むテーブルのすべてのレコードの値。

場合によっては、これらの余分な文字は関係ありません。 たとえばを残して、ラベルに、結果を表示する場合は、区切り記号は表示されません。 これらの余分な文字を削除する場合を使用して、 [**左**](function-left-mid-right.md)または[**一致**](function-ismatch.md)関数。

これらの例については、設定、**テキスト**次の表の最初の列からの数式にラベルのプロパティ。

| 数式 | 説明 | 結果 |
|---------|-------------|--------|
| **Left( Concat(&nbsp;Products,&nbsp;Name&nbsp;&&nbsp;",&nbsp;"&nbsp;), Len(&nbsp;Concat(&nbsp;Products,&nbsp;Name&nbsp;&&nbsp;",&nbsp;"&nbsp;)&nbsp;)&nbsp;-&nbsp;2 )** | 結果を返します**Concat**が余分な区切り記号を形成する最後の 2 つの文字を削除します。 | "Violin、&nbsp;Cello、&nbsp;トランペット" |
| **Match( Concat(&nbsp;Products,&nbsp;Name&nbsp;&&nbsp;",&nbsp;"&nbsp;), "^(?&lt;trim&gt;.*),&nbsp;$" ).trim** | 文字を返します**Concat** ($) の末尾にテキスト文字列 (^) の先頭から、不要なコンマと末尾にスペースが含まれていませんが。 | "Violin、&nbsp;Cello、&nbsp;トランペット" |

### <a name="split-and-matchall"></a>分割と MatchAll

使用した場合**Concat** 、区切り記号で結合して、操作を取り消すことができます、**分割**と**MatchAll**関数。

これらの例については、空白、垂直方向のギャラリーを追加設定その**項目**プロパティを次の表に、数式にし、ギャラリー テンプレートにラベルを追加します。

| 数式 | 説明 | 結果 |
|---------|-------------|--------|
| **Split( Concat(&nbsp;Products,&nbsp;Name&nbsp;&&nbsp;",&nbsp;"&nbsp;), ", " )** | テキスト文字列を区切り記号で分割 **「,」** します。 文字列は、結果の最後の行が空の文字列であるために、コンマとスペースで終わります。  | ![Table](media/function-concatenate/split.png) |
| **MatchAll( Concat(&nbsp;Products,&nbsp;Name&nbsp;&&nbsp;",&nbsp;"&nbsp;), "[^\s,]+" ).FullMatch** | スペースまたはコンマではない文字に基づいて文字列を分割します。 この数式では、余分なコンマと文字列の末尾にスペースを削除します。 | ![Table](media/function-concatenate/matchall.png)
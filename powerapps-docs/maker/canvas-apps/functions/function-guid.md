---
title: GUID 関数 | Microsoft Docs
description: 構文を含む PowerApps の GUID 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 11/14/2018
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 9415ab67b93ef64f5caa025af5ac685ca2363305
ms.sourcegitcommit: 5b2b70c3fc7bcba5647d505a79276bbaad31c610
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2019
ms.locfileid: "58357071"
---
# <a name="guid-function-in-powerapps"></a>PowerApps の GUID 関数
GUID ([Globally Unique Identifier](https://en.wikipedia.org/wiki/Universally_unique_identifier)/グローバル一意識別子) 文字列を GUID 値に変換するか、新しい GUID 値を作成します。

## <a name="description"></a>説明
**GUID** 関数を使用し、GUID の 16 進数表現が含まれる文字列をデータベースに渡せる GUID 値に変換します。 GUID 値は、Common Data Service と SQL Server などのデータベース システムでキーとして使用されます。

渡される文字列には大文字または小文字を含めることができますが、32 桁の 16 進数にする必要があります。形式は次のいずれかにします。

- **"123e4567-e89b-12d3-a456-426655440000"** (標準的な位置にハイフンあり)
- **"123e4567e89b12d3a456426655440000"** (ハイフンなし)

引数を指定しない場合、この関数によって新しい GUID が作成されます。

コンテキストが文字列であれば、GUID 値は文字列に変換されます。 GUID 値は、ハイフンと小文字からなる 16 進数表現の文字列に変換されます。 

この関数で擬似乱数を使用して、バージョン 4 を作成する新しい GUID を生成するときに[IETF RFC 4122](https://www.ietf.org/rfc/rfc4122.txt) GUID。 Guid 文字列を変換するときに、この関数は、32 の 16 進数字の任意の文字列をそのまま使用して任意のバージョンの GUID をサポートします。

## <a name="volatile-functions"></a>揮発性関数
**GUID** は引数なしで使用される揮発性の関数です。 揮発性関数は、評価されるたびに異なる値を返します。  

データ フロー式で使うと、揮発性関数は、それが出現する数式が再評価された場合にのみ、異なる値を返します。 数式で何も変更されていない場合、アプリの実行全体を通じて同じ値を返します。

たとえば、**Text** プロパティが **GUID()** に設定されているラベル コントロールは、アプリがアクティブになっている間は変更されません。 アプリをいったん閉じて再び開いた場合にのみ、異なる値が返されます。

関数は、何かが変更された数式の一部である場合に再評価されます。 たとえば、**Label** コントロールの **Text** プロパティをこの数式に設定すると、ユーザーが **Text input** コントロールの値を変更するたびに、GUID が生成されます。

**TextInput1.Text & " " & GUID()**

[動作の数式](../working-with-formulas-in-depth.md)で使うと、数式が評価されるたびに **GUID** が評価されます。 詳細については、このトピックの後半の例を参照してください。

## <a name="syntax"></a>構文
**GUID**( [ *GUIDString* ] )

* *GUIDString* – 任意。  GUID の 16 進数表現を含むテキスト文字列。 文字列が指定されていない場合、新しい GUID が作成されます。

## <a name="examples"></a>例

#### <a name="basic-usage"></a>基本的な使用方法

16 進数表現に基づいて GUID 値を返すには:

* **GUID( "0f8fad5b-d9cb-469f-a165-70867728950e" )**

ハイフンなしの GUID 文字列を指定することもできます。 この数式では、同じ GUID 値が返されます。

* **GUID( "0f8fad5bd9cb469fa16570867728950e" )**

コンテキストで使用され、新しいデータベース レコードの **Status** フィールドを確立された値に設定します。

* **Patch( Products, Default( Products ), { Status:GUID( "F9168C5E-CEB2-4faa-B6BF-329BF39FA1E4" ) } )**

ユーザーに GIUD を見せることは好ましくないが、GUID がアプリのデバッグに役立つことがあります。 前の例で作成したレコードで **Status** フィールドの値を表示するには、**Label** コントロールの **Text** プロパティを次の数式に設定します。

* **First( Products ).Status**

**Label** コントロールにより **f9168c5e-ceb2-4faa-b6bf-329bf39fa1e4** が表示されます。

#### <a name="create-a-table-of-guids"></a>GUID のテーブルの作成

1. **[ボタン](../controls/control-button.md)** コントロールの **[OnSelect](../controls/properties-core.md)** プロパティを次の数式に設定します。

    **ClearCollect( NewGUIDs, ForAll( [ 1, 2, 3, 4, 5 ], GUID() ) )**

    この式は、5 回反復して 5 つの GUID を生成するために使用される単一列のテーブルを作成します。

1. **[データ テーブル](../controls/control-data-table.md)** コントロールを追加し、その **Items** プロパティを **NewGUIDs** に設定し、**Value** フィールドを表示します。

1. Alt キーを押しながら、クリックまたはタップしてボタンを選択します。

    データ テーブルには、GUID の一覧が表示されます。

    ![5 つの異なる GUID 値を含むデータ テーブルが表示されている画面](media/function-guid/guid-collection-1.png)

1. もう一度ボタンを選択すると、別の GUID リストが表示されます。

    ![同じ画面ですが、データ テーブルに含まれる 5 つの異なる GUID が新しいセットになっています](media/function-guid/guid-collection-2.png)

テーブルではなく単一の GUID を生成するには、次の数式を使用します。

**Set( NewGUID, GUID() )**

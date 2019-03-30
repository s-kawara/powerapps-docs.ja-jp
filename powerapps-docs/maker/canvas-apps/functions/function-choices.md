---
title: Choices 関数 | Microsoft Docs
description: 構文を含む PowerApps の Choices 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 06/15/2018
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: ed555f5de4abc1e29b7d2a637413c440bd882f13
ms.sourcegitcommit: 6b116a4079eb56ebd598d317a12df8856ff3e52a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/30/2019
ms.locfileid: "58671957"
---
# <a name="choices-function-in-powerapps"></a>PowerApps の Choices 関数
ルックアップ列で使用可能な値のテーブルを返します。

## <a name="description"></a>説明
**Choices** 関数は、ルックアップ列で使用可能な値のテーブルを返します。  

**Choices** 関数を使用して、ユーザーが選択する選択肢の一覧を提供します。 この関数は、編集フォームで[**コンボ ボックス**](../controls/control-combo-box.md) コントロールと共によく使用されます。

ルックアップの場合、**Choices** が返すテーブルは、ルックアップに関連付けられている外部テーブルと一致します。 **Choices** を使用することにより、追加データ ソースとして外部テーブルを追加する必要がなくなります。 **Choices** は、外部テーブルのすべての列を返します。

**Choices** はテーブルを返すので、[**Filter**](function-filter-lookup.md)、[**Sort**](function-sort.md)、[**AddColumns**](function-table-shaping.md)、その他すべてのテーブル操作関数を使って、テーブルをフィルター、並べ替え、整形できます。 

現時点で、**Choices** を[委任](../delegation-overview.md)することはできません。 この制限によりアプリで問題がある場合は、データ ソースとして外部エンティティを追加し、それを直接使用してください。 

[**ShowColumns**](function-table-shaping.md)、[**Search**](function-filter-lookup.md)、その他のテーブル関数とは異なり、**Choices** では列名を文字列にして二重引用符で囲む必要はありません。 列を直接参照するのと同じように、式を指定します。

列参照は、データ ソースに対して直接行う必要があります。 たとえば、データ ソースが **Accounts** でルックアップが **SLA** の場合、列参照は **Accounts.SLA** になります。 参照は、関数、変数、またはコントロールを経由することはできません。 この例を拡張し、**Accounts** が **Gallery** コントロールにフィードされる場合は、式 **Gallery.Selected.SLA** を使って選択されたアカウントの SLA を参照します。 ただし、この参照はコントロールを経由したので、**Columns** 関数に渡されることはできません。やはり **Accounts.SLA** を使う必要があります。

この時点では、SharePoint と Common Data Service でのみ参照列を使用できます。

## <a name="syntax"></a>構文
**Choices**( *column-reference* )

* *column-reference* – 必須。  データ ソースのルックアップ列です。 列名を二重引用符で囲まないでください。 参照は、データ ソースの列に対して直接行う必要があり、関数またはコントロールを経由してはなりません。

## <a name="examples"></a>例

#### <a name="choices-for-a-lookup"></a>ルックアップの選択肢

1. [データベースを作成する](../../../administrator/create-database.md)Common Data Service、および選択で、**サンプル アプリとデータを含める**ボックス。

    **Accounts** などの多数のエンティティが作成されます。

    **注**:エンティティの名前は、web.powerapps.com に単数形と PowerApps Studio での複数形です。

    ![Common Data Service for Apps の Account エンティティのフィールドのリストの一部、"Primary Contact" がルックアップ フィールドであることの強調表示](media/function-choices/entity-account.png)

    **Accounts** エンティティには **Primary Contact** 列があり、これは **連絡先** エンティティに対するルックアップです。  

    ![Common Data Service の Contact エンティティのフィールドのリストの一部](media/function-choices/entity-contact.png)

    各アカウントについて、連絡先が主連絡先として指定されているか、または主連絡先が "*ブランク*" になっています。

1. **Accounts** エンティティから[アプリを生成](../data-platform-create-app.md)します。

1. 左端近くにある画面とコントロールの一覧で、**EditScreen1** が表示されるまで下にスクロールし、そのすぐ下にある **EditForm1** を選択します。

    ![左側のナビゲーション バーで、EditScreen1 の EditForm1 を選択する](media/function-choices/select-editform.png)

1. **プロパティ**選択の右側のウィンドウのタブ**フィールドを編集**します。

    ![データ ペインを開く](media/function-choices/open-data-pane.png)

1. **フィールド**ペインで、**フィールドの追加**します。

1. 検索、**主要連絡先**フィールドで、そのチェック ボックスを選択しを選択し、**追加**します。

    ![Accounts を選択して [データ] ウィンドウを開く](media/function-choices/field-list.png)

    **主要連絡先**フィールドは、フォームの下部に表示されます。 フィールドには、エラーが表示される場合は、選択**データ ソース**で、**ビュー**タブの省略記号 (...) を選択、**アカウント**データ ソース、および選択し**更新**.

1. (省略可能) **Primary Contact** フィールドをフィールド一覧の下部から先頭にドラッグします。

1. **Primary Contact** のカードで、**コンボ ボックス** コントロールを選択します。

    **項目**そのコントロールのプロパティは、最初の例では、その表示名、または 2 つ目の例のようにその論理名のいずれかによって、列を識別する数式に設定されています。

   - **Choices( Accounts.'Primary Contact' )**
   - **Choices( Accounts.primarycontactid )**

     ![フォーム コントロールを含むキャンバス画面。 コンボ ボックス コントロール内での主要な連絡先カードを選択すると、および Items プロパティの数式を選択 (アカウントです ' プライマリ連絡先 ') が表示されます。](media/function-choices/accounts-primary-contact.png)

1. **[ホーム]** タブの **[新しい画面]** を選択し、**[空白]** を選択します。

1. **[挿入]** タブの **[データ テーブル]** を選択します。

1. 設定、**項目**のプロパティ、**データ テーブル**コントロールに次の式。

     **Choices( Accounts.'Primary Contact' )**

1. 途中で、**データ テーブル**コントロールを開始するリンクを選択して**フィールドを選択しています.**、し表示するフィールドのチェック ボックスを選択します (たとえば、 **firstname**と**lastname**)。

     ![データ テーブル コントロールを含むキャンバス画面。 Items プロパティは式 Choices( Accounts.'Primary Contact' ) に設定され、テーブルには Contacts エンティティの最初のレコード セットの firstname 列と lastname 列が表示されている](media/function-choices/full-accounts-pc.png)
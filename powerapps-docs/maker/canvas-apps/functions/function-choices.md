---
title: Choices 関数 | Microsoft Docs
description: 構文を含む PowerApps の Choices 関数の参照情報
author: gregli-msft
ms.service: powerapps
ms.topic: reference
ms.component: canvas
ms.date: 06/15/2018
ms.author: gregli
ms.openlocfilehash: ec39a9970c2135e9cf4633f8266d9b2980d8cd9b
ms.sourcegitcommit: 79b8842fb0f766a0476dae9a537a342c8d81d3b3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2018
ms.locfileid: "37895962"
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

現在、ルックアップ列は SharePoint と Common Data Service for Apps でのみ使うことができます。

## <a name="syntax"></a>構文
**Choices**( *column-reference* )

* *column-reference* – 必須。  データ ソースのルックアップ列です。 列名を二重引用符で囲まないでください。 参照は、データ ソースの列に対して直接行う必要があり、関数またはコントロールを経由してはなりません。

## <a name="examples"></a>例

#### <a name="choices-for-a-lookup"></a>ルックアップの選択肢

1. Common Data Service for Apps で[データベースを作成](../../../administrator/create-database.md)し、**[サンプル アプリとデータを含める]** ボックスをオンにします。

    **Accounts** などの多数のエンティティが作成されます。

    **注**: エンティティの名前は、web.powerapps.com では単数形、PowerApps Studio では複数形です。

    ![Common Data Service for Apps の Account エンティティのフィールドのリストの一部、"Primary Contact" がルックアップ フィールドであることの強調表示](media/function-choices/entity-account.png)

    **Accounts** エンティティには **Primary Contact** 列があり、これは **連絡先** エンティティに対するルックアップです。  

    ![Common Data Service の Contact エンティティのフィールドのリストの一部](media/function-choices/entity-contact.png)

    各アカウントについて、連絡先が主連絡先として指定されているか、または主連絡先が "*ブランク*" になっています。

2. **Accounts** エンティティから[アプリを生成](../data-platform-create-app.md)します。

3. 左端近くにある画面とコントロールの一覧で、**EditScreen1** が表示されるまで下にスクロールし、そのすぐ下にある **EditForm1** を選択します。

    ![左側のナビゲーション バーで、EditScreen1 の EditForm1 を選択する](media/function-choices/select-editform.png)

4. 右側のウィンドウの **[プロパティ]** タブで、**Accounts** を選択します。

    ![Accounts を選択して [データ] ウィンドウを開く](media/function-choices/open-data-pane.png)

5. **[データ]** ウィンドウで、フィールドの一覧を下にスクロールします。

    ![Accounts を選択して [データ] ウィンドウを開く](media/function-choices/field-list.png)

6. **Primary Contact** チェック ボックスを探し、オフになっている場合はオンにします。

7. (省略可能) **Primary Contact** フィールドをフィールド一覧の下部から先頭にドラッグします。

8. **Primary Contact** のカードで、**コンボ ボックス** コントロールを選択します。

    そのコントロールの **Items** プロパティは、詳細設定の **[列の表示名を使用]** チェック ボックスの状態に基づいて、2 つの式のいずれかに設定されます。

   - チェック ボックスがオンになっている場合、プロパティは次の式に設定されます。<br>**Choices( Accounts.'Primary Contact' )**
   - チェック ボックスがオフになっている場合、プロパティは次の式に設定されます。<br>**Choices( Accounts.primarycontactid )**

     ![フォーム コントロールを含むキャンバス画面。 **Primary Contact** カードの**コンボ ボックス** コントロールが選択されており、Items プロパティは式 Choices( Accounts.'Primary Contact' ) に設定されている](media/function-choices/accounts-primary-contact.png)

9. **[ホーム]** タブの **[新しい画面]** を選択し、**[空白]** を選択します。

10. **[挿入]** タブの **[データ テーブル]** を選択します。

11. **[データ テーブル]** コントロールの **Items** プロパティを、次の式のいずれかに設定します。

     - 詳細設定の **[列の表示名を使用]** チェック ボックスがオンの場合は、この式を使います。<br>**Choices( Accounts.'Primary Contact' )**
     - それ以外の場合は、この式を使います。<br>**Choices( Accounts.primarycontactid )**

12. **[データ]** ウィンドウを開き、**firstname**、**lastname**、または他の表示するフィールドのチェック ボックスをオンにします。

     ![データ テーブル コントロールを含むキャンバス画面。 Items プロパティは式 Choices( Accounts.'Primary Contact' ) に設定され、テーブルには Contacts エンティティの最初のレコード セットの firstname 列と lastname 列が表示されている](media/function-choices/full-accounts-pc.png)
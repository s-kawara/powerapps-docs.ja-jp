---
title: キャンバス アプリの電子メール画面テンプレートのリファレンス |Microsoft Docs
description: PowerApps でキャンバス アプリの電子メール画面テンプレートのしくみの詳細を理解します。
author: emcoope-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 12/31/2018
ms.author: emcoope
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 8f77fe1194ace2f8cb5abeb3f9657cc76aab263a
ms.sourcegitcommit: 5e15a1033a68289781f8092fb65c57432501f911
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54459484"
---
# <a name="reference-information-about-the-email-screen-template-for-canvas-apps"></a>キャンバス アプリの電子メール画面テンプレートに関する参照情報

PowerApps でキャンバス アプリの場合は、電子メール画面テンプレートの重要な各コントロールは、画面の全体的な既定の機能に貢献する方法について説明します。 この詳細情報は、動作の数式とその他のコントロールがユーザー入力に応答する方法を決定するプロパティの値を表示します。 この画面の既定の機能の概要については、、[電子メール画面概要](email-screen-overview.md)を参照してください。

このトピックでは、いくつかの重要なコントロールを強調表示し、さまざまなプロパティに式または数式をについて説明します (など**項目**と**OnSelect**) は、これらのコントロールの設定。

* [テキスト検索ボックス](#text-search-box)
* [[追加] アイコン](#add-icon)
* [ユーザーがギャラリーを参照します。](#people-browse-gallery)
* [電子メール ユーザー ギャラリー](#email-people-gallery) (+ 子コントロール)
* [メール アイコン](#mail-icon)

## <a name="prerequisite"></a>前提条件

追加しても画面とその他のコントロールを構成する方法に関する知識[PowerApps でアプリを作成](../data-platform-create-app-scratch.md)です。

## <a name="text-search-box"></a>テキスト検索ボックス

   ![TextSearchBox コントロール](media/email-screen/email-search-box.png)

画面の他のいくつかのコントロール依存している、**テキスト検索ボックス**コントロール。

* ユーザーが任意のテキストの入力を始める場合**PeopleBrowseGallery**が表示されます。
* 有効な電子メール アドレスでは、入力された場合**AddIcon**が表示されます。
* ユーザーが内のユーザーを選択すると**PeopleBrowseGallery**、検索内容がリセットされます。

## <a name="add-icon"></a>[追加] アイコン

   ![AddIcon コントロール](media/email-screen/email-add-icon.png)

**追加アイコン**コントロールで構成される電子メールの受信者の一覧に、組織内に存在しないユーザーを追加するアプリのユーザーを使用できます。

* プロパティ:**表示されます。**<br>
    値:ユーザーが検索ボックスに有効な電子メール アドレスを入力する場合にのみ、コントロールを表示するロジック。

    ```powerapps-dot
    !IsBlank( TextSearchBox.Text ) &&
        IsMatch( TextSearchBox.Text, Match.Email ) &&
        Not( Trim( TextSearchBox.Text ) in MyPeople.UserPrincipalName )
    ```
  行ごと、上記のコード ブロックでは、ことを示す、**追加アイコン**コントロールを表示する場合にのみ。

    * **TextSearchBox**テキストが含まれています。
    * 内のテキスト**TextSearchBox**は有効な電子メール アドレスです。
    * 内のテキスト**TextSearchBox**に既に存在しない、 **MyPeople**コレクション。

* プロパティ:**OnSelect**<br>
    値:有効な電子メール アドレスを追加選択すると、 **MyPeople**コレクション。 このコレクションは、受信者の一覧として画面によって使用されます。

    ```powerapps-dot
    Collect( MyPeople,
        { 
            DisplayName: TextSearchBox.Text, 
            UserPrincipalName: TextSearchBox.Text, 
            Mail: TextSearchBox.Text
        }
    );
    Reset( TextSearchBox )
    ```
  
  このコード ブロックに行が追加、 **MyPeople**コレクションし、テキストに 3 つのフィールドを設定します。 **TextSearchBox**します。 これら 3 つのフィールドは**DisplayName**、 **UserPrincipalName**、および**メール**します。 内容をリセットし、 **TextSearchBox**します。

## <a name="people-browse-gallery"></a>ユーザーがギャラリーを参照します。

   ![PeopleBrowseGallery コントロール](media/email-screen/email-browse-gall.png)

* プロパティ:**項目**<br>
    値:上位 15 の検索結果に入力された検索テキストの**TextSearchBox**コントロール。
    
    ```powerapps-dot
    If( !IsBlank( Trim(TextSearchBox.Text ) ), 
        'Office365Users'.SearchUser( {searchTerm: Trim( TextSearchBox.Text ), top: 15} )
    )
    ```

  このギャラリーの項目が検索結果からによって設定された、 [Office365.SearchUser](https://docs.microsoft.com/connectors/office365users/#searchuser)操作。 操作は、テキスト`Trim(TextSearchBox)`用語と上位 15 の結果を返しますで検索結果に基づいてその検索として。
  
  **TextSearchBox**にラップされて、`Trim()`スペース上のユーザーの検索が有効でないため、機能します。 `Office365Users.SearchUser`で操作をラップする`If(!IsBlank(Trim(TextSearchBox.Text)) ... )`関数は、検索ボックスには、ユーザーが入力したテキストが含まれている場合にのみ、操作が実行されます。 これにより、パフォーマンスが向上します。 

### <a name="people-browse-gallery-title-control"></a>ユーザーがギャラリーのタイトルのコントロールを参照します。

   ![PeopleBrowseGallery タイトル コントロール](media/email-screen/email-browse-gall-title.png)

* プロパティ:**[Text (テキスト)]**<br>
    値: `ThisItem.DisplayName`

  Office 365 プロファイルから個人の表示名が表示されます。

* プロパティ:**OnSelect**<br>
    値:アプリ レベルのコレクションにユーザーを追加するコードし、ユーザーを選択します。

    ```powerapps-dot
    Concurrent(
        Set( _selectedUser, ThisItem ),
        Reset( TextSearchBox ),
        If( Not( ThisItem.UserPrincipalName in MyPeople.UserPrincipalName ), 
            Collect( MyPeople, ThisItem )
        )
    )
    ```
このコントロールを選択すると、次の 3 つが同時には。

   * セット、 **_selectedUser**変数を選択した項目にします。
   * 検索用語をリセット**TextSearchBox**します。
   * 選択した項目を追加、 **MyPeople**コレクション、電子メールの画面を一連の受信者として使用するすべての選択したユーザーのコレクション。

## <a name="email-people-gallery"></a>電子メール ユーザー ギャラリー

   ![EmailPeopleGallery コントロール](media/email-screen/email-people-gall.png)

* プロパティ:**項目**<br>
    値: `MyPeople`

  これは、ユーザーを追加または初期化のコレクション、 **PeopleBrowseGallery タイトル**コントロール。

* プロパティ:**高さ**<br>
    値:現在、ギャラリー内の項目の数に基づいて、高さを設定するロジック。

    ```powerapps-dot
    Min( 
        ( EmailPeopleGallery.TemplateHeight + EmailPeopleGallery.TemplatePadding * 2) *
            RoundUp(CountRows(EmailPeopleGallery.AllItems) / 2, 0 ),
        304
    )
    ```

  このギャラリーの高さを 304 の最大の高さをギャラリー内の項目の数を調整します。
  
  かかる`TemplateHeight + TemplatePadding * 2`全体の 1 つの行の高さとして**EmailPeopleGallery**行の数を掛けたします。 `WrapCount = 2`、True の行の数が`RoundUp(CountRows(EmailPeopleGallery.AllItems) / 2, 0)`します。

* プロパティ:**ShowScrollbar**<br>
    値: `EmailPeopleGallery.Height >= 304`
  
  ギャラリーの高さには、304 に達すると、スクロール バーは表示されます。

### <a name="email-people-gallery-title-control"></a>電子メール ユーザー ギャラリー コントロールのタイトル

   ![EmailPeopleGallery タイトル コントロール](media/email-screen/email-people-gall-text.png)

* プロパティ:**OnSelect**<br>
    値: `Set(_selectedUser, ThisItem)`

  セット、 **_selectedUser**変数で選択した項目を**EmailPeopleGallery**します。

### <a name="email-people-gallery-iconremove-control"></a>電子メール ユーザー ギャラリー iconRemove コントロール

   ![MonthDayGallery タイトル コントロール](media/email-screen/email-people-gall-delete.png)

* プロパティ:**OnSelect**<br>
    値: `Remove( MyPeople, LookUp( MyPeople, UserPrincipalName = ThisItem.UserPrincipalName ) )`

  内のレコードを調べ、 **MyPeople**コレクション、場所**UserPrincipalName**と一致する、 **UserPrincipalName**の選択したアイテムとそのからレコードを削除します、コレクションです。

## <a name="mail-icon"></a>メール アイコン

* プロパティ:**OnSelect**<br>
    値:ユーザーの電子メール メッセージを送信するロジック。

    ```powerapps-dot
    Set( _emailRecipientString, Concat( MyPeople, Mail & ";" ) );
    'Office365'.SendEmail( _emailRecipientString, 
        TextEmailSubject.Text,  
        TextEmailMessage.Text, 
        { Importance:"Normal" }
    );
    Reset( TextEmailSubject );
    Reset( TextEmailMessage );
    Clear( MyPeople )
    ```

  電子メール メッセージを送信するには、電子メール アドレスのセミコロン区切りの文字列が必要です。 上記のコード。
  1. コードの最初の行は、**メール**フィールド内のすべての行を**MyPeople**コレクションをセミコロンで区切って電子メール アドレスの 1 つの文字列に連結し、設定、 **_emailRecipientString**変数にその文字列値。

  1. 次を使用して、 [Office365.SendEmail](https://docs.microsoft.com/connectors/office365/#sendemail)受信者に電子メールを送信する操作。
    操作は、次の 3 つの必要なパラメーター**に**、**サブジェクト**、および**本文**と 1 つのオプション パラメーター -**重要度**します。 これらは、上記のコードで **_emailRecipientString**、 **TextEmailSubject**します。テキスト、 **TextEmailMessage**します。テキスト、および**標準**、それぞれします。
  1. 最後に、リセット、 **TextEmailSubject**と**TextEmailMessage**を制御し、クリア、 **MyPeople**コレクション。

* プロパティ:**DisplayMode**<br>
    値:`If( Len( Trim( TextEmailSubject.Text ) ) > 0 && !IsEmpty( MyPeople ), DisplayMode.Edit, DisplayMode.Disabled )` テキスト、および受信者の電子メールを送信する、電子メールの件名行があります (**MyPeople**) コレクションを空にすることはできません。

## <a name="next-steps"></a>次の手順

* [この画面を詳細します。](./email-screen-overview.md)
* [PowerApps での Office 365 Outlook コネクタの詳細します。](../connections/connection-office365-outlook.md)
* [PowerApps での Office 365 Users コネクタの詳細します。](../connections/connection-office365-users.md)

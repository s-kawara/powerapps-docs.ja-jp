---
title: ユーザー画面テンプレートの参照 |Microsoft Docs
description: PowerApps でキャンバス アプリのユーザー画面テンプレートのしくみの詳細を理解します。
author: emcoope-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 1/2/2019
ms.author: emcoope
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 09b92a1e2bc87ac6f4e2ec651aa67a845e0f07b1
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61540785"
---
# <a name="reference-information-about-the-people-screen-template-for-canvas-apps"></a>キャンバス アプリのユーザー画面テンプレートに関する参照情報

PowerApps のキャンバス アプリの場合、ユーザー画面テンプレートの重要な各コントロール画面が全体的な既定の機能にどのように貢献するかついて説明します。 この詳細情報は、動作の数式とその他のコントロールがユーザー入力に応答する方法を決定するプロパティの値を表示します。 この画面の既定の機能の概要については、 [ユーザー画面の概要](people-screen-overview.md) をご覧ください。

このトピックでは、いくつかの重要なコントロールに焦点を当て、これらのコントロールのさまざまなプロパティ( **Item** と **OnSelect** など) に設定される式または数式について説明します。

* [テキスト検索ボックス](#text-search-box)
* [ユーザー参照ギャラリー](#user-browse-gallery) (+ 子コントロール)
* [ユーザーがギャラリーを追加](#people-added-gallery)(+ 子コントロール)

## <a name="prerequisite"></a>前提条件

[PowerApps でアプリを作成](../data-platform-create-app-scratch.md) するときに画面やその他コントロールを追加および構成する方法を理解している方。

## <a name="text-search-box"></a>テキスト検索ボックス

![TextSearchBox コントロール](media/people-screen/people-search-box.png)

他のいくつかのコントロールは、テキストの検索ボックスと対話し、テキスト検索ボックスと依存関係にあります。

* ユーザーが任意のテキストの入力を始めると **UserBrowseGallery** が表示されます。
* ユーザーが、 **UserBrowseGallery** 内でユーザーを選択すると、検索内容がリセットされます。

## <a name="user-browse-gallery"></a>ユーザー参照ギャラリー

![UserBrowseGallery コントロール](media/people-screen/people-browse-gall.png)

* プロパティ:**Items**<br>
    値: ユーザーが入力を開始するときにユーザーを検索するためのロジック:
    
    ```powerapps-dot
    If( !IsBlank( Trim( TextSearchBox.Text ) ), 
        'Office365Users'.SearchUser(
            {
                searchTerm: Trim( TextSearchBox.Text ), 
                top: 15
            }
        )
    )
    ```
    
このギャラリーの項目には、 [Office365.SearchUser](https://docs.microsoft.com/connectors/office365users/#searchuser) 操作の検索結果が表示されます。この操作では、 `Trim(TextSearchBox)` のテキストを検索語として使用し、その検索に基づいて上位 15 件の結果を返します。  **TextSearchBox** は、スペースでのユーザー検索が無効であるため、 `Trim()` 関数でラップされます。

検索ボックスにユーザーが入力したテキストが含まれている場合にのみ操作を呼び出す必要があるため、 `Office365Users.SearchUser` 操作は、 `If(!IsBlank(Trim(TextSearchBox.Text)) ... )` 関数でラップされます。これによりパフォーマンスが向上します。

### <a name="userbrowsegallery-title-control"></a>UserBrowseGallery Title コントロール

![UserBrowseGallery Title コントロール](media/people-screen/people-browse-gall-title.png)

* プロパティ:**[Text (テキスト)]**<br>値: `ThisItem.DisplayName`

  Office 365 プロファイルから個人の表示名が表示されます。

* プロパティ:**OnSelect**<br>
    値: ユーザーをアプリ レベルのコレクションに追加するコードを作成し、ユーザーを選択します。

    ```powerapps-dot
    Concurrent(
        Set( _selectedUser, ThisItem ),
        Reset( TextSearchBox ),
        If( Not( ThisItem.UserPrincipalName in MyPeople.UserPrincipalName ), 
            Collect( MyPeople, ThisItem )
        )
    )
    ```
このコントロールを選択すると、次の 3 つが同時に行われます。

   **\_selectedUser** 変数を選択された項目に設定します。
   **TextSearchBox** の検索語をリセットします。
   * 選択した項目を **MyPeople** コレクションに追加します。コレクションは、アプリユーザーが選択したすべてのユーザーのコレクションです。

### <a name="userbrowsegallery-profileimage-control"></a>UserBrowseGallery ProfileImage コントロール

![UserBrowseGallery ProfileImage コントロール](media/people-screen/people-browse-gall-image.png)

* プロパティ: **Image**<br>
    値:ユーザーのプロファイル写真を取得するロジック。

    ```powerapps-dot
    If( !IsBlank( ThisItem.Id ) && 
            'Office365Users'.UserPhotoMetadata( ThisItem.Id ).HasPhoto,
        'Office365Users'.UserPhoto( ThisItem.Id )
    )
    ```

**Image** コントロールは、 [Office365Users.UserPhoto](https://docs.microsoft.com/connectors/office365users/#get-user-photo--v1-) 操作でユーザーの画像を取得します。 ただし、その前に、次の、2 つのことを確認します。
  
   * ID フィールドが空または空でないかどうか。 これにより、ギャラリーに検索結果が入力される前に、 **Image** コントロールがユーザーの写真を取得しようとするのを防ぎます。
   * ユーザーが写真を持っているかどうか ( [Office365Users.UserPhotoMetadata](https://docs.microsoft.com/connectors/office365users/#get-user-photo-metadata) 操作を使用)。 これにより、ユーザーがプロフィール画像を持っていない場合に `Office365Users.UserPhoto` ルックアップが例外を返すのを防ぎます。

イメージが取得されていない場合、 **Image** コントロールは、空白になり、代わりに **iconUser** コントロールが表示されます。

## <a name="people-added-gallery"></a>ユーザーが追加したギャラリー

![PeopleAddedGallery コントロール](media/people-screen/people-people-gall.png)

* プロパティ: **Items**<br>
    値: `MyPeople`

これは、 **UserBrowseGallery Title** コントロールを選択して初期化または追加されたユーザーのコレクションです。

### <a name="peopleaddedgallery-title-control"></a>PeopleAddedGallery Title コントロール

![PeopleAddedGallery タイトル コントロール](media/people-screen/people-people-gall-title.png)

* プロパティ:**OnSelect**<br>
    値: `Set( _selectedUser, ThisItem )`

**_selectedUser** 変数を **EmailPeopleGallery** で選択された項目に設定します。

### <a name="peopleaddedgallery-iconremove-control"></a>PeopleAddedGallery iconRemove コントロール

![PeopleAddedGallery iconRemove コントロール](media/people-screen/people-people-gall-delete.png)

* プロパティ:**OnSelect**<br>
    値: `Remove( MyPeople, LookUp( MyPeople, UserPrincipalName = ThisItem.UserPrincipalName ) )`

**MyPeople** コレクションのレコードを検索します。 **UserPrincipalName** は、選択した項目の **UserPrincipalName** と一致し、コレクションからそのレコードを削除します。

## <a name="next-steps"></a>次の手順

* [詳細については、この画面は](./people-screen-overview.md)します。
* [詳細については、Office 365 Outlook コネクタは](../connections/connection-office365-outlook.md)します。
* [詳細については、Office 365 ユーザー コネクタは](../connections/connection-office365-users.md)します。

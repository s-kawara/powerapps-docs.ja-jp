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

PowerApps でキャンバス アプリの場合は、ユーザー画面テンプレートの重要な各コントロールは、画面の全体的な既定の機能に貢献する方法について説明します。 この詳細情報は、動作の数式とその他のコントロールがユーザー入力に応答する方法を決定するプロパティの値を表示します。 この画面の既定の機能の概要については、次を参照してください。、[ユーザー画面の概要](people-screen-overview.md)します。

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

* プロパティ:**項目**<br>
    値:ユーザー、ユーザーが入力を開始するときに検索するためのロジック:
    
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
    
このギャラリーの項目には、 [Office365.SearchUser](https://docs.microsoft.com/connectors/office365users/#searchuser) 操作の検索結果が表示されます。 この操作では、 `Trim(TextSearchBox)` のテキストを検索語として使用し、その検索に基づいて上位 15 件の結果を返します。 **TextSearchBox** は、スペースでのユーザー検索が無効であるため、 `Trim()` 関数でラップされます。

検索ボックスにユーザーが入力したテキストが含まれている場合にのみ操作を呼び出す必要があるため、 `Office365Users.SearchUser` 操作は、 `If(!IsBlank(Trim(TextSearchBox.Text)) ... )` 関数でラップされます。 これによりパフォーマンスが向上します。

### <a name="userbrowsegallery-title-control"></a>UserBrowseGallery Title コントロール

![UserBrowseGallery Title コントロール](media/people-screen/people-browse-gall-title.png)

* プロパティ: **[Text (テキスト)]**<br>値: `ThisItem.DisplayName`

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
このコントロールを選択すると、次の 3 つが同時に行われます。

   * セット、  **\_selectedUser**変数を選択した項目にします。
   * **TextSearchBox** の検索語をリセットします。
   * 選択した項目を追加、 **MyPeople**アプリのユーザーが選択されているコレクション、すべてのユーザーのコレクション。

### <a name="userbrowsegallery-profileimage-control"></a>UserBrowseGallery ProfileImage コントロール

![UserBrowseGallery ProfileImage コントロール](media/people-screen/people-browse-gall-image.png)

* プロパティ:**イメージ**<br>
    値:ユーザーのプロファイル写真を取得するロジック。

    ```powerapps-dot
    If( !IsBlank( ThisItem.Id ) && 
            'Office365Users'.UserPhotoMetadata( ThisItem.Id ).HasPhoto,
        'Office365Users'.UserPhoto( ThisItem.Id )
    )
    ```

**Image** コントロールは、 [Office365Users.UserPhoto](https://docs.microsoft.com/connectors/office365users/#get-user-photo--v1-) 操作でユーザーの画像を取得します。 ただし、その前に、次の、2 つのことを確認します。
  
   * ID フィールドが空または空でないかどうか。 これにより、**イメージ**コントロールから、ギャラリーが設定されている検索結果する前に、ユーザーの写真を取得しようとしています。
   * ユーザーが写真を持っているかどうか (で、 [Office365Users.UserPhotoMetadata](https://docs.microsoft.com/connectors/office365users/#get-user-photo-metadata)操作)。 これにより、`Office365Users.UserPhoto`ユーザーがプロファイル画像を持っていない場合に例外を返すから参照します。

イメージが取得されていない場合、**イメージ**コントロールは、空白、 **iconUser**コントロールが表示される代わりにします。

## <a name="people-added-gallery"></a>ユーザーが追加したギャラリー

![PeopleAddedGallery コントロール](media/people-screen/people-people-gall.png)

* プロパティ:**項目**<br>
    値: `MyPeople`

これは、ユーザーを追加または初期化のコレクション、 **UserBrowseGallery タイトル**コントロール。

### <a name="peopleaddedgallery-title-control"></a>PeopleAddedGallery タイトル コントロール

![PeopleAddedGallery タイトル コントロール](media/people-screen/people-people-gall-title.png)

* プロパティ:**OnSelect**<br>
    値: `Set( _selectedUser, ThisItem )`

セット、 **_selectedUser**変数で選択した項目を**EmailPeopleGallery**します。

### <a name="peopleaddedgallery-iconremove-control"></a>PeopleAddedGallery iconRemove コントロール

![PeopleAddedGallery iconRemove コントロール](media/people-screen/people-people-gall-delete.png)

* プロパティ:**OnSelect**<br>
    値: `Remove( MyPeople, LookUp( MyPeople, UserPrincipalName = ThisItem.UserPrincipalName ) )`

内のレコードを検索、 **MyPeople** 、コレクション、 **UserPrincipalName**と一致する、 **UserPrincipalName**のアイテムの選択し、そのからレコードを削除します、コレクションです。

## <a name="next-steps"></a>次の手順

* [詳細については、この画面は](./people-screen-overview.md)します。
* [詳細については、Office 365 Outlook コネクタは](../connections/connection-office365-outlook.md)します。
* [詳細については、Office 365 ユーザー コネクタは](../connections/connection-office365-users.md)します。

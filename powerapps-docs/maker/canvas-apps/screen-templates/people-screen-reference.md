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
ms.sourcegitcommit: 5e15a1033a68289781f8092fb65c57432501f911
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54459461"
---
# <a name="reference-information-about-the-people-screen-template-for-canvas-apps"></a>キャンバス アプリのユーザー画面テンプレートに関する参照情報

PowerApps でキャンバス アプリの場合は、ユーザー画面テンプレートの重要な各コントロールは、画面の全体的な既定の機能に貢献する方法について説明します。 この詳細情報は、動作の数式とその他のコントロールがユーザー入力に応答する方法を決定するプロパティの値を表示します。 この画面の既定の機能の概要については、、[ユーザー画面の概要](people-screen-overview.md)を参照してください。

このトピックでは、いくつかの重要なコントロールを強調表示し、さまざまなプロパティに式または数式をについて説明します (など**項目**と**OnSelect**) は、これらのコントロールの設定。

* [テキスト検索ボックス](#text-search-box)
* [ユーザー参照ギャラリー](#user-browse-gallery) (+ 子コントロール)
* [ユーザーがギャラリーを追加](#people-added-gallery)(+ 子コントロール)

## <a name="prerequisite"></a>前提条件

追加しても画面とその他のコントロールを構成する方法に関する知識[PowerApps でアプリを作成](../data-platform-create-app-scratch.md)です。

## <a name="text-search-box"></a>テキスト検索ボックス

![TextSearchBox コントロール](media/people-screen/people-search-box.png)

他のいくつかのコントロールまたは対話、テキストの検索ボックスに、依存関係にあります。

* ユーザーが任意のテキストの入力を始める場合**UserBrowseGallery**が表示されます。
* ユーザーが内のユーザーを選択すると**UserBrowseGallery**、検索内容がリセットされます。

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
    
このギャラリーの項目が検索結果からによって設定された、 [Office365.SearchUser](https://docs.microsoft.com/connectors/office365users/#searchuser)操作。 操作は、テキスト`Trim(TextSearchBox)`用語と上位 15 の結果を返しますで検索結果に基づいてその検索として。 **TextSearchBox**にラップされて、`Trim()`スペース上のユーザーの検索が有効でないため、機能します。

`Office365Users.SearchUser`に操作がラップされて、`If(!IsBlank(Trim(TextSearchBox.Text)) ... )`関数のみを検索ボックスには、ユーザーが入力したテキストが含まれている場合、操作を呼び出す必要があるためです。 これにより、パフォーマンスが向上します。

### <a name="userbrowsegallery-title-control"></a>UserBrowseGallery タイトル コントロール

![UserBrowseGallery タイトル コントロール](media/people-screen/people-browse-gall-title.png)

* プロパティ:**[Text (テキスト)]**<br>値: `ThisItem.DisplayName`

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

   * セット、  **\_selectedUser**変数を選択した項目にします。
   * 検索用語をリセット**TextSearchBox**します。
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

**イメージ**コントロールを使用して、ユーザーのイメージを取得、 [Office365Users.UserPhoto](https://docs.microsoft.com/connectors/office365users/#get-user-photo--v1-)操作。 ただし、その前に、これは、2 つのことを確認します。
  
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

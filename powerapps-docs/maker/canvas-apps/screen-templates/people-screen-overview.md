---
title: ユーザー画面テンプレート |Microsoft Docs
description: キャンバス アプリのユーザー画面テンプレートの動作とユース ケースの画面を拡張する方法を理解します。
author: emcoope-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 12/30/2018
ms.author: emcoope
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 85da6f5414cc25d1145f0fa8910e8c78bfb74533
ms.sourcegitcommit: 5e15a1033a68289781f8092fb65c57432501f911
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54459438"
---
# <a name="overview-of-the-people-screen-template-for-canvas-apps"></a>キャンバス アプリのユーザー画面テンプレートの概要

キャンバス アプリでは、ユーザーが組織内のユーザーを検索できるようにするユーザーの画面を追加します。 ユーザーは、検索、選択、およびコレクションにユーザーを追加できます。 ギャラリーの検索結果に表示されます、電子メールを送信する、ユーザーの選択内容を使用して、および他のカスタマイズを行うデータの種類を変更することができます。

など、Office 365 から別のデータを表示する他のテンプレートに基づく画面を追加することもできます[電子メール](email-screen-overview.md)、ユーザーの[カレンダー](calendar-screen-overview.md)、および[可用性](meeting-screen-overview.md)人のユーザー可能性があります。会議に招待するとしてください。

この概要を説明します。
> [!div class="checklist"]
> * 既定のユーザーの画面を使用する方法。
> * 画面を変更する方法。
> * 画面をアプリに統合する方法。

この画面の既定の機能について詳しくを参照してください、[ユーザー画面参照](people-screen-reference.md)します。

## <a name="prerequisite"></a>前提条件

追加しても画面とその他のコントロールを構成する方法に関する知識[PowerApps でアプリを作成](../data-platform-create-app-scratch.md)です。

## <a name="default-functionality"></a>既定の機能

テンプレートからのユーザー画面を追加します。

1. [サインイン](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)PowerApps にアプリを作成するか、PowerApps Studio で既存のアプリを開きます。

    このトピックでは、phone アプリが、タブレット アプリを同じ概念が適用されます。

1. **ホーム**、リボンのタブ**新しい画面** > **人**します。

    既定では、次の画面のように。

    ![初期のユーザーの画面の状態](media/people-screen/people-screen-empty.png)

1. ユーザーの検索を開始するには、上部にあるテキスト入力ボックスを選択し、同僚の名前を入力します。 テキスト入力ボックスの下に検索結果が表示されます。

    ![ユーザー画面の検索の状態](media/people-screen/people-browse-gall-full.png)

1. 追加、検索結果から個人を選択すると、 **MyPeople**コレクション。 選択したユーザーのコレクションを公開、検索バーは、入力値がリセットされます。

    ![ユーザーがコレクションの結果を画面します。](media/people-screen/people-people-gall-full.png)

## <a name="modify-the-screen"></a>画面を変更します。

この画面での既定の機能を変更する[人の別のデータを示す](people-screen-overview.md#show-different-data-for-people)します。

さらに画面を変更する場合を使用して、[ユーザー画面参照](./people-screen-reference.md)をガイドとして。

### <a name="show-different-data-for-people"></a>ユーザーのさまざまなデータを表示します。

この画面を使用して、 [Office365Users.SearchUser](https://docs.microsoft.com/connectors/office365users/#searchuser)組織内のユーザーを検索する操作機能の各イベントの追加のフィールドを提供します、 **UserBrowseGallery**コントロール。 追加またはギャラリー内のフィールドを変更する、単純なプロセスです。

1. **UserBrowseGallery**、変更 (または追加してから、選択されているように) するためのラベルを選択します。

1. その**テキスト**数式バーで、選択したプロパティと内容の置換 `ThisItem.`

    IntelliSense では、選択可能なフィールドの一覧が表示されます。

1. 使用するフィールドを選択します。

    **テキスト**プロパティを更新する必要があります`ThisItem.{FieldSelection}`します。

## <a name="integrate-the-screen-into-an-app"></a>画面をアプリに統合します。

ユーザーの画面は、独自の右にあるコントロールの強力なバンドルが通常最適な大規模でより汎用的なアプリの一部として実行します。 この画面は、さまざまな方法で大規模なアプリケーションに統合できます[キャッシュされたユーザーの一覧を使用して](people-screen-overview.md#use-your-cached-list-of-people)します。

### <a name="use-your-cached-list-of-people"></a>キャッシュされたユーザーの一覧を使用して、

ユーザーの画面でユーザーの選択のキャッシュ、 **MyPeople**コレクション。 ビジネス シナリオは、担当者の参照を呼び出す必要があります、このコレクションを使用する方法を理解する必要があります。 電子メールの初歩的な画面にこの画面を接続し、内のユーザーに電子メールを送信する方法をここでは、追って、 **MyPeople**コレクション。 方法に洞察を得ることでしょうも[電子メール画面](./email-screen-overview.md)動作します。

1. 選択して、アプリに Office 365 Outlook のデータ ソースを追加、**ビュー** ] タブの [選択**データソース** > **データ ソースの追加**オフィスを探して365 outlook コネクタです。 選択する必要があります**新しい接続**を検索します。
1. ユーザーの画面を挿入した後、新しい空の画面を挿入します。 、その画面内では、左向き矢印アイコン、2 つのテキスト入力ボックス、および送信 アイコンを追加します。
1. 画面の名前を変更**EmailScreen**、戻る矢印アイコンを**BackIcon**、1 つのテキスト入力ボックスに**SubjectLine**に他の**MessageBody**に送信 アイコンと**SendIcon**します。
1. 設定、 **OnSelect**プロパティの**BackIcon**に`Back()`します。
1. 設定、 **OnSelect**プロパティの**SendIcon**に次の式。

    ```powerapps-dot
    Office365.SendEmail( 
        Concat( MyPeople, UserPrincipalName & ";" ), 
        SubjectLine.Text, 
        MessageBody.Text 
    )
    ```
    
    ここでは、電子メールを送信する Outlook connector を使用しています。 値を渡す`Concat(MyPeople, UserPrincipalName & ";")`として受信者の一覧。 次の式を連結しますすべての電子メール アドレスで、 **MyPeople**コレクションを 1 つの文字列をセミコロンで区切ることにします。 これは、お気に入りのメール クライアントの"To"の行にセミコロンで区切って電子メール アドレスの文字列の書き込みと変わりありません。
    * 渡す`SubjectLine.Text`として、メッセージの件名と`MessageBody.Text`メッセージの本文として。
1. ユーザーの画面で、右上隅にある、挿入、**メール**アイコン。
   アイコンの色を変更するには、お客様に適したものに。
1. 設定、 **OnSelect**のプロパティ、 **SendIcon**に`Navigate( EmailScreen, None )`します。

    2 つの画面のアプリをユーザーの選択には、電子メール メッセージを作成して、送信があるようになりました。 追加を自由に試してみるがアプリ送信のすべてのユーザーに電子メールを送信するために、注意が必要ですが、 **MyPeople**コレクション。

## <a name="next-steps"></a>次の手順

* [この画面のリファレンス ドキュメントを表示](./people-screen-reference.md)します。
* [詳細については、Office 365 Outlook コネクタは](../connections/connection-office365-outlook.md)します。
* [詳細については、Office 365 ユーザー コネクタは](../connections/connection-office365-users.md)します。

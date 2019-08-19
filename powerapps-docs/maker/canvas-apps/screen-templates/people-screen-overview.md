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
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61536160"
---
# <a name="overview-of-the-people-screen-template-for-canvas-apps"></a>キャンバス アプリのユーザー画面テンプレートの概要

キャンバス アプリでは、ユーザーが組織内のユーザーを検索できるようにするユーザーの画面を追加します。 ユーザーは、検索、選択、およびコレクションにユーザーを追加できます。 ギャラリーの検索結果に表示されたデータの種類を変更したり、選択したユーザーを使用して電子メールを送信したり、その他のカスタマイズを行うことができます。

など、Office 365 から別のデータを表示する他のテンプレートに基づく画面を追加することもできます[電子メール](email-screen-overview.md)、ユーザーの[カレンダー](calendar-screen-overview.md)、および[可用性](meeting-screen-overview.md)人のユーザー可能性があります。会議に招待するとしてください。

この概要では、次のことを説明します。
> [!div class="checklist"]
> * 既定のユーザーの画面を使用する方法。
> * 画面を変更する方法。
> * 画面をアプリに統合する方法。

この画面の既定の機能の詳細については、[ユーザー画面の参照](people-screen-reference.md)をご覧ください。

## <a name="prerequisite"></a>前提条件

[PowerApps でアプリを作成](../data-platform-create-app-scratch.md)するときに画面やその他のコントロールを追加および構成する方法を理解している方。

## <a name="default-functionality"></a>既定の機能

テンプレートからのユーザー画面を追加します。

1. PowerApps に[サインイン](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)してから、アプリを作成するか、PowerApps Studio で既存のアプリを開きます。

    このトピックでは、携帯電話のアプリを示しますが、同じ概念がタブレットのアプリにも適用されます。

1. リボンの**ホーム**タブで、**新しい画面** > **人々**を選択します。

    既定では、次の画面のように。

    ![初期のユーザーの画面の状態](media/people-screen/people-screen-empty.png)

1. ユーザーの検索を開始するには、上部にあるテキスト入力ボックスを選択し、同僚の名前を入力します。 テキスト入力ボックスの下に検索結果が表示されます。

    ![ユーザー画面の検索の状態](media/people-screen/people-browse-gall-full.png)

1. 検索結果から個人を選択すると、**MyPeople** コレクションに追加されます。 検索バーの入力値がリセットされ、選択したユーザーのコレクションが表示されます。

    ![ユーザーがコレクションの結果を画面します。](media/people-screen/people-people-gall-full.png)

## <a name="modify-the-screen"></a>画面を変更します。

[ユーザーのさまざまなデータを表示](people-screen-overview.md#show-different-data-for-people)することで、この画面の既定の機能を変更します。

さらに画面を変更する場合は、[ユーザー画面参照](./people-screen-reference.md)をガイドとして使用してください。

### <a name="show-different-data-for-people"></a>ユーザーのさまざまなデータを表示します。

この画面を使用して、 [Office365Users.SearchUser](https://docs.microsoft.com/connectors/office365users/#searchuser)組織内のユーザーを検索する操作機能の各イベントの追加のフィールドを提供します、 **UserBrowseGallery**コントロール。 追加またはギャラリー内のフィールドを変更する、単純なプロセスです。

1. **UserBrowseGallery** で変更するラベルを選択します (またはラベルを追加して選択したままにします)。

1. **Text** プロパティを選択した状態で、数式バーの内容を `ThisItem.` に置き換えます。

    IntelliSense では、選択可能なフィールドの一覧が表示されます。

1. 使用するフィールドを選択します。

    **Text** プロパティを `ThisItem.{FieldSelection}` に更新します。

## <a name="integrate-the-screen-into-an-app"></a>画面をアプリに統合します。

ユーザーの画面は、それ自体が強力なコントロールのバンドルですが、通常は、より大規模でより汎用的なアプリの一部とすることでパフォーマンスを発揮します。 [キャッシュされたユーザーの一覧を使用する](people-screen-overview.md#use-your-cached-list-of-people)ことに加えて、さまざまな方法でこの画面をより大きなアプリに統合します。

### <a name="use-your-cached-list-of-people"></a>キャッシュされたユーザーの一覧を使用して、

ユーザーの画面は、**MyPeople** コレクションのユーザー選択をキャッシュします。 ビジネス シナリオでユーザーの検索が必要な場合は、このコレクションの使用方法を知る必要があります。 ここでは、この画面を基本的なメール画面に接続し、**MyPeople** コレクションのユーザーにメールを送信する方法を説明します。 また、[電子メール画面](./email-screen-overview.md)がどのように機能するかについての洞察も得られます。

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

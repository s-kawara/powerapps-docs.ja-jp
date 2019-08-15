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

[電子メール](email-screen-overview.md)、ユーザーの[カレンダー](calendar-screen-overview.md)、およびユーザーが会議に招待する [可用性](meeting-screen-overview.md) のある人の空き時間など、Office 365 からさまざまなデータを表示する他のテンプレートベースの画面を追加することもできます。

この概要では、次のことを説明します。
> [!div class="checklist"]
> * 既定のユーザーの画面を使用する方法。
> * 画面を変更する方法。
> * 画面をアプリに統合する方法。

この画面の既定の機能について詳細については、 [ユーザー画面参照](people-screen-reference.md) をご覧ください。

## <a name="prerequisite"></a>前提条件

[PowerApps でアプリを作成](../data-platform-create-app-scratch.md) するときに画面やその他のコントロールを追加および構成する方法を理解している方。

## <a name="default-functionality"></a>既定の機能

テンプレートからのユーザー画面を追加します。

1. PowerApps に [サインイン](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) してから、アプリを作成するか、 PowerApps Studio で既存のアプリを開きます。

    このトピックでは、携帯電話 アプリを示しますが、タブレット アプリを同じ概念が適用されます。

1. リボンの **ホーム** タブで、 **新しい画面** > **人々** を選択します。

    既定では、次の画面のように。

    ![初期のユーザーの画面の状態](media/people-screen/people-screen-empty.png)

1. ユーザーの検索を開始するには、上部にあるテキスト入力ボックスを選択し、同僚の名前を入力します。 テキスト入力ボックスの下に検索結果が表示されます。

    ![ユーザー画面の検索の状態](media/people-screen/people-browse-gall-full.png)

1. 検索結果から個人を選択すると、 **MyPeople** コレクションに追加されます。検索バーの入力値がリセットされ、選択したユーザーのコレクションが表示されます。

    ![ユーザーがコレクションの結果を画面します。](media/people-screen/people-people-gall-full.png)

## <a name="modify-the-screen"></a>画面を変更します。

[ユーザーのさまざまなデータを表示](people-screen-overview.md#show-different-data-for-people) することで、この画面の既定の機能を変更します。

さらに画面を変更する場合は、 [ユーザー画面参照](./people-screen-reference.md) をガイドとして使用してください。

### <a name="show-different-data-for-people"></a>ユーザーのさまざまなデータを表示します。

この画面では、 [Office365Users.SearchUser](https://docs.microsoft.com/connectors/office365users/#searchuser) 操作を使用して組織内のユーザーを検索します。 **UserBrowseGallery** コントロールに表示されるもの以外の各イベントの追加フィールドを提供します。 ギャラリー でのフィールとの追加または変更は簡単なプロセスです。

1. **UserBrowseGallery** で変更するラベルを選択します。 (またはラベルを追加して選択したままにします。）

1. **Text** プロパティを選択した状態で、数式バーの内容を `ThisItem.` に置き換えます。

    IntelliSense では、選択可能なフィールドの一覧が表示されます。

1. 使用するフィールドを選択します。

    **Text** プロパティが `ThisItem.{FieldSelection}` に更新します。

## <a name="integrate-the-screen-into-an-app"></a>画面をアプリに統合します。

ユーザーの画面は、それ自体が強力なコントロールのバンドルですが、通常は、大規模でより汎用的なアプリの一部として実行します。 [キャッシュされたユーザーの一覧を使用して](people-screen-overview.md#use-your-cached-list-of-people) さまざまな方法でこの画面をより大きなアプリに統合します。

### <a name="use-your-cached-list-of-people"></a>キャッシュされたユーザーの一覧を使用して、

ユーザーの画面は、 **MyPeople** コレクションのユーザー選択をキャッシュします。 ビジネス シナリオ でユーザーの検索が必要な場合は、このコレクションの使用方法を知る必要があります。ここでは、この画面を基本的なメール画面に接続し、 **MyPeople** コレクションのユーザーにメールを送信する方法を説明します。また、 [電子メール画面](./email-screen-overview.md) がどのように機能するかについての洞察も得られます。

1. **ビュー** タブを選択し、 **データソース** > **データ ソースの追加** を選択して、Office 365 Outlook データソースをアプリに追加します。見つけるために、 **新しい接続** を選択する必要がある場合があります。
1. ユーザー画面を挿入した後、新しい空の画面を挿入します。その画面内に、左向き矢印アイコン、2 つのテキスト入力ボックス、および送信 アイコンを追加します。
1. 画面の名前を **EmailScreen** に、戻る矢印アイコンを **BackIcon** に、1 つのテキスト入力ボックスを **SubjectLine** にもう１つを  **MessageBody** 、送信 アイコンを **SendIcon** に変更します。
1. **BackIcon** の **OnSelect** プロパティを `Back()` に設定します。
1. **SendIcon** の **OnSelect** プロパティを次の式に設定します。

    ```powerapps-dot
    Office365.SendEmail( 
        Concat( MyPeople, UserPrincipalName & ";" ), 
        SubjectLine.Text, 
        MessageBody.Text 
    )
    ```
    
    ここでは、Outlook connector を使用してメールを送信しています。 `Concat(MyPeople, UserPrincipalName & ";")` を受信者のリストとして渡します。この式は、 **MyPeople** コレクション内のすべての電子メールアドレスをセミコロンで区切った単一の文字列に連結します。これは、お気に入りの電子メールクライアントの "To" の行をセミコロンで区切られた電子メールアドレスの文字列を書き出すことと同じです。
    * メッセージの件名として `SubjectLine.Text` を、メッセージの本文として `MessageBody.Text` を渡します。
1. ユーザーの画面で、右上隅にある、 **メール** アイコンを挿入します。アイコンの色を自分にあったものに変更します。
1. **SendIcon** の **OnSelect** のプロパティを `Navigate( EmailScreen, None )` に設定します。

    これで、ユーザーを選択し、そのユーザーへおメールメッセージを作成して送信できる 2 つの画面アプリができました。試してみてください。ただし、**MyPeople** コレクションに追加した全員にアプリが送信するため、注意してください。

## <a name="next-steps"></a>次の手順

* [この画面のリファレンス ドキュメントを表示](./people-screen-reference.md)します。
* [詳細については、Office 365 Outlook コネクタは](../connections/connection-office365-outlook.md)します。
* [詳細については、Office 365 ユーザー コネクタは](../connections/connection-office365-users.md)します。

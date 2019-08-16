---
title: 電子メール画面テンプレート |Microsoft Docs
description: キャンバス アプリの電子メール画面テンプレートのしくみを理解し、ユース ケースの画面の拡張
author: emcoope-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 12/29/2018
ms.author: emcoope
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: a1aad5ca9e8c7f8b55b1645b04d6c8dc0b9c707b
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61539237"
---
# <a name="overview-of-the-email-screen-template-for-canvas-apps"></a>キャンバス アプリの電子メール画面テンプレートの概要

キャンバス アプリでは、ユーザーが Office 365 Outlook アカウントからメールを送信できる電子メール画面を追加します。 ユーザーは、組織内の受信者を検索し、外部の電子メール アドレスを追加できます。 添付ファイルのイメージのサポートを追加、ギャラリーの検索に表示されるユーザー データの変更、およびその他のカスタマイズを行うことができます。

ユーザーの[カレンダー](calendar-screen-overview.md)、組織内の[人](people-screen-overview.md)、会議に招待する[可能性](meeting-screen-overview.md)がある人の空き時間など、Office 365 からさまざまなデータを表示する他のテンプレートに基づく画面を追加することができます。

この概要を説明します。
> [!div class="checklist"]
> * 既定の電子メールの画面を使用する方法。
> * これを変更する方法。
> * アプリに統合する方法。

この画面の既定の機能については、[電子メール画面参照](email-screen-reference.md) をご覧ください。

## <a name="prerequisite"></a>前提条件

[PowerApps でアプリを作成](../data-platform-create-app-scratch.md) するときに画面やその他コントロールを追加および構成する方法を理解している方。

## <a name="default-functionality"></a>既定の機能

テンプレートから、電子メールの画面を追加します。

1. PowerApps に [サインイン](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) してから、アプリを作成するか、PowerApps Studio で既存のアプリを開きます。

    このトピックでは、携帯電話 アプリを示しますが、タブレット アプリでも同じ概念が適用されます。

2. リボンの **ホーム** タブから **新しい画面** > **電子メール** を選択します。

    既定では、画面は次のようになります。

    ![電子メールの画面](media/email-screen/email-screen-full.png)

いくつかの役に立つ注記:

* 組織内のユーザーを検索するには、チーム名を"To"の下のテキスト入力ボックスに入力を開始します。
* ユーザーを検索するとき、上位 15 の結果のみが返されます。
* 組織外の電子メール受信者の電子メール アドレスを追加するには、完全な有効な電子メール アドレスを入力し、右側に表示される '+' アイコンを選択します。
* 受信者として少なくとも 1 人のユーザーを追加して、電子メールを送信する件名を指定する必要があります。
* 電子メールを送信した後、件名とメッセージの本文に加えて、受信者の一覧の内容はすべて消去されます。

## <a name="modify-the-screen"></a>画面を変更します。

この画面の既定の機能は、いくつかの一般的な方法で変更できます。

* [添付ファイルのイメージのサポートを追加します。](email-screen-overview.md#add-image-attachment-support)
* [ユーザーのさまざまなデータを表示します。](email-screen-overview.md#show-different-data-for-people)

さらに画面を変更する場合は、 [電子メール画面参照](./email-screen-reference.md) をガイドとして使用してください。

> [!IMPORTANT]
> 次の手順では、1 つだけの電子メールの画面をアプリに追加したことを前提としています。 1 つ以上、コントロール名を追加した場合 ( **iconMail1** など) は、別の数値で終了するため、数式を適宜調整する必要があります。

### <a name="add-image-attachment-support"></a>添付ファイルのイメージのサポートを追加します。

これにより、添付ファイルとして 1 つのイメージを電子メールでユーザーに送信できます。

1. **挿入** タブで **メディア** を選択し、**画像の追加** を選択します。
1. 新しいコントロールの **Y** プロパティを次の式に設定します。

    `TextEmailMessage1.Y + TextEmailMessage1.Height + 20`
    
1. **AddMediaWithImage** コントロールを挿入して、その高さを 210 未満に設定します。
1. コントロールのツリー ビューで **AddMediaWithImage** > **...**  > **再配列** > **背面へ移動** を選択します。
   これにより、コントロールが **PeopleBrowseGallery** コントロールの前に配置されなくなります。
1. **EmailPeopleGallery** の **Height** プロパティを次の式に変更します。

    ```powerapps-dot
    Min( 
        ( EmailPeopleGallery1.TemplateHeight + EmailPeopleGallery1.TemplatePadding * 2 ) *
            RoundUp( CountRows( EmailPeopleGallery1.AllItems ) / 2, 0 ), 
        304
    )
    ```

1. **EmailPeopleGallery** の **ShowScrollbar** プロパティを次の式に変更します。

    ```EmailPeopleGallery1.Height >= 304```
    
    これにより、最大の高さが、 **AddMediaWithImage** コントロールをページから押し出さないようにします。
    
1. **iconMail** コントロールの **OnSelect** プロパティを次の式に変更します。

    ```powerapps-dot
    Set( _emailRecipientString, Concat(MyPeople, Mail & ";") );
    If( IsBlank( UploadedImage1 ),
        'Office365'.SendEmail( _emailRecipientString, 
            TextEmailSubject1.Text, 
            TextEmailMessage1.Text, 
            { Importance: "Normal" }
        ),
        'Office365'.SendEmail( _emailRecipientString, 
            TextEmailSubject1.Text, 
            TextEmailMessage1.Text, 
            {
                Importance: "Normal",
                Attachments: Table(
                    {
                        Name: "Image.jpg", 
                        ContentBytes: UploadedImage1.Image
                    }
                )
            }
        )
    );
    Reset( TextEmailSubject1 );
    Reset( TextEmailMessage1 );
    Reset( AddMediaButton1 );
    Clear( MyPeople )
    ```
    
    この数式は、アップロードされたイメージをチェックします。 まったくが存在しない場合は、次を使用して同じ`Office365.SendEmail`以前と同様に操作します。 イメージがある場合は、添付ファイル テーブル内の添付ファイルとして追加されます。
    電子メール送信後、 **リセット** 操作が実行され **AddMediaButton** でアップロードされたイメージを削除します。
> [!NOTE]
> 電子メールを 1 つ以上の添付ファイルを追加するには、添付ファイル テーブルにレコードを追加します。

### <a name="show-different-data-for-people"></a>ユーザーのさまざまなデータを表示します。

この画面では、 [Office365Users.SearchUser](https://docs.microsoft.com/connectors/office365users/#searchuser) 操作を利用して組織内のユーザーを検索します。 **PeopleBrowseGallery** コントロールに表示されるもの以外に、各イベントに追加のフィールドを提供します。ギャラリーにフィールドを追加または変更するのは簡単です。

1. **PeopleBrowseGallery** コントロールで、変更するラベルを選択します。(またはラベルを追加して選択したままにします。)

1. **Text** プロパティを選択した状態で、数式バーの内容を `ThisItem.` に置き換えます。

    IntelliSense では、選択可能なフィールドの一覧が表示されます。

1. 使用するフィールドを選択します。

    **Text** プロパティが `ThisItem.{FieldSelection}` に更新されます。

## <a name="integrate-the-screen-into-an-app"></a>画面をアプリに統合します。

電子メールの画面は、それ自体が強力なバンドルですが、通常最適な大規模でより汎用的なアプリの一部として実行します。 この画面は、 [カレンダー画面へのリンク](email-screen-overview.md#linking-to-the-calendar-screen) など、さまざまな方法でより大きなアプリに統合できます。

### <a name="linking-to-the-calendar-screen"></a>予定表の画面へのリンク

「イベントの参加者を表示する」セクションに記載されている手順に従います
[カレンダー画面概要](./calendar-screen-overview.md#show-event-attendees) の「イベントの参加者を表示」セクションで説明されている手順に従いますが、最後の手順では、 **Navigate** 関数を利用して電子メール画面を開きます。 これらの手順が完了したら、 **MyPeople** コレクションを設定すると、ユーザーは、選択したイベントに参加している人に電子メールを送信できます。

> [!NOTE]
> この電子メールを送信すると、Outlook の実際のイベントとは別の電子メールが送信されます。

## <a name="next-steps"></a>次の手順

* [この画面のリファレンス ドキュメントを表示](./email-screen-reference.md)します。
* [詳細については、PowerApps での Office 365 ユーザー コネクタは](../connections/connection-office365-users.md)します。
* [PowerApps で利用可能なすべての接続を参照してください。](../connections-list.md)

---
title: 予定表画面テンプレート |Microsoft Docs
description: キャンバス アプリの予定表画面テンプレートのしくみを理解、画面を変更および拡張アプリの一部として
author: emcoope-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 12/28/2018
ms.author: emcoope
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 745b4232a43a06c46866e83ca2452f8a55afeddf
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61536203"
---
# <a name="overview-of-the-calendar-screen-template-for-canvas-apps"></a>キャンバス アプリの予定表画面テンプレートの概要

キャンバス アプリでは、自分の Office 365 Outlook アカウントからの今後のイベントをユーザーに表示されるカレンダー画面を追加します。 ユーザーは、予定表とその日のイベントの一覧をスクロールしてから日付を選択することができます。 詳細情報が一覧に表示、各イベントに関する詳細を表示する 2 つ目の画面を追加、各イベントの出席者の一覧を表示およびその他のカスタマイズを行うを変更することができます。

[電子メール](email-screen-overview.md)、組織内[ユーザー](people-screen-overview.md)、および会議に招待する[可能性](meeting-screen-overview.md)のあるユーザーの空き状況など、Office 365からさまざまなデータを表示するテンプレートベースの画面を追加することができます。

この概要を説明します。
> [!div class="checklist"]
> * 既定のカレンダーの画面を使用する方法。
> * これを変更する方法。
> * アプリに統合する方法。

この画面の既定の機能について詳しくを参照してください、[カレンダー画面参照](calendar-screen-reference.md)します。

## <a name="prerequisite"></a>前提条件

[PowerApps でアプリを作成](../data-platform-create-app-scratch.md) する時に画面・その他のコントロールを追加及び構成する方法に精通していること。

## <a name="default-functionality"></a>既定の機能

テンプレートからカレンダー画面を追加します。

1. [サインイン](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)PowerApps にアプリを作成するか、PowerApps Studio で既存のアプリを開きます。

    このトピックでは、電話 アプリを示しますが、同じ概念がタブレット アプリにも適用されます。

1. リボンの **ホーム** タブで、**新しい画面** > **カレンダー** を選択します。

    既定では、次の画面のように。

    ![予定表の画面](media/calendar-screen/calendar-initial.png)

1. データを表示するには、画面の上部にあるドロップダウン リストでオプションを選択します。

    ![読み込みが完了した後、予定表画面](./media/calendar-screen/calendar-screen.png)

いくつかの役に立つ注記:

* 既定では、今日の日付を選択して、簡単に、右上隅にある予定表アイコンを選択して、返すことができます。
* 別の日付を選択した場合は、円で囲まれて、明るい色の四角形 (青、既定のテーマが適用されている場合) は、今日の日付を囲みます。
* 特定の日付の少なくとも 1 つのイベントがスケジュールされた場合、予定表では、その日付色付きの小さな円が表示されます。
* 1 つまたは複数のイベントがスケジュールされている日付を選択した場合は、予定表の下でイベントが表示されます。

## <a name="modify-the-screen"></a>画面を変更します。

この画面の既定の機能は、いくつかの一般的な方法で変更できます。

* [カレンダーの指定](calendar-screen-overview.md#specify-the-calendar)します。
* [イベントに関するさまざまな詳細の表示](calendar-screen-overview.md#show-different-details-about-an-event)します。
* [非ブロッキングのイベントを非表示に](calendar-screen-overview.md#hide-nonblocking-events)します。

画面を更に変更する場合は、[カレンダー画面リファレンス](./calendar-screen-reference.md)をガイドとして使用してください。

### <a name="specify-the-calendar"></a>カレンダーを指定します。

ユーザーがどのカレンダーを表示する必要があるか知っている場合、アプリを公開する前に、そのカレンダーを指定することで、画面を簡略化できます。 この変更は、カレンダーのドロップダウン リストが不要になるため削除できます。

1. アプリの規定画面プロパティ、 **[OnStart](../controls/control-screen.md)** を次の式に設定します。

    ```powerapps-dot
    Set( _userDomain, Right( User().Email, Len( User().Email ) - Find( "@", User().Email ) ) );
    Set( _dateSelected, Today() );
    Set( _firstDayOfMonth, DateAdd( Today(), 1 - Day( Today() ), Days ) );
    Set( _firstDayInView, 
        DateAdd( _firstDayOfMonth, -( Weekday( _firstDayOfMonth) - 2 + 1 ), Days )
    );
    Set( _lastDayOfMonth, DateAdd( DateAdd( _firstDayOfMonth, 1, Months ), -1, Days ) );
    Set( _calendarVisible, false );
    Set( _myCalendar, 
        LookUp( Office365.CalendarGetTables().value, DisplayName = "{YourCalendarNameHere}" )
    );
    Set( _minDate, 
        DateAdd( _firstDayOfMonth, -( Weekday(_firstDayOfMonth) - 2 + 1 ), Days )
    );
    Set( _maxDate, 
        DateAdd(
            DateAdd( _firstDayOfMonth, -( Weekday(_firstDayOfMonth) - 2 + 1 ), Days ),
            40, 
            Days 
        )
    );
    ClearCollect( MyCalendarEvents, 
        Office365.GetEventsCalendarViewV2( _myCalendar.Name, 
            Text( _minDate, UTC ), 
            Text( _maxDate, UTC ) 
        ).value
    );
    Set( _calendarVisible, true )
    ```

    > [!NOTE]
    > この式は、カレンダーを選択するためのドロップダウンリストの **OnSelect** プロパティのデフォルト値からわずかに編集されています。 そのコントロールの詳細については、[カレンダー画面レファレンス](./calendar-screen-reference.md#calendar-drop-down)のセクションを参照してください。

1. 中括弧を含む`{YourCalendarNameHere}`を、表示する **カレンダー** の名前を使用して置換します。

    > [!IMPORTANT]
    > 次の手順では、予定表の 1 つだけの画面をアプリに追加したことを前提としています。 1 つ以上、コントロール名を追加した場合 、コントロール名 **iconCalendar1** は、別の数値で終了するため、それに応じて数式を調整する必要があります。

1. **iconCalendar1** コントロールの **Y** プロパティに次の式を設定します。

    `RectQuickActionBar1.Height + 20`

1. **LblMonthSelected1** コントロールの **Y** プロパティに次の式を設定します。

    `iconCalendar1.Y + iconCalendar1.Height + 20`

1. **LblNoEvents1** コントロールの **Text** プロパティに次の式を設定します。

    `"No events scheduled"`

1. **LblNoEvents1** コントロールの **Visible** プロパティに次の式を設定します。

    `CountRows(CalendarEventsGallery1.AllItems) = 0 && _calendarVisible`

1. これらのコントロールを削除します。

    - **dropdownCalendarSelection1**
    - **LblEmptyState1**
    - **iconEmptyState1**

1. 予定表の画面が既定の画面でない場合は、アプリをテストできるように、既定の画面から予定表の画面に移動するボタンを追加します。

    たとえば、ボタンを追加で**Screen1**にナビゲートする**Screen2**カレンダー画面を一から作成されたアプリに追加した場合。

1. アプリを保存し、ブラウザーまたはモバイル デバイスで、テストします。

### <a name="show-different-details-about-an-event"></a>イベントに関するさまざまな詳細を表示します。

既定では、[カレンダー] 下の **CalendarEventsGallery** という名前のギャラリーには、各イベントの開始時刻、期間、件名、場所が表示されます。 [Office 365 コネクタ](https://docs.microsoft.com/connectors/office365/#calendareventclientreceive) がサポートするフィールド (オーガナイザーなど) を表示するようにギャラリーを構成できます。

1. **CalendarEventsGallery** で、新規または既存ラベルの **テキスト** プロパティを `ThisItem` に続けてピリオドを設定します。

    IntelliSense には、選択可能なフィールドが一覧表示されます。

1. 使用するフィールドを選択します。

    ラベルには、指定した情報の種類が表示されます。

### <a name="hide-nonblocking-events"></a>非ブロッキングのイベントを非表示にします。

多くのオフィスでは、チームメンバーが会議出席依頼を送信して、オフィスから離れる時に互いに通知します。 要求の送信先のユーザー設定の可用性をすべてのユーザーのスケジュールがブロックされないように、 **Free**に設定します。 2 つのプロパティを更新することで、これらのイベントを予定表とギャラリーから非表示にできます。

1. 設定、**項目**プロパティの**CalendarEventsGallery**に次の式。

    ```powerapps-dot
    SortByColumns(
        Filter(
            MyCalendarEvents,
            Text( Start, DateTimeFormat.ShortDate ) = 
                Text( _dateSelected, DateTimeFormat.ShortDate ),
            ShowAs <> "Free"
        ),
        "Start"
    )
    ```

    この数式で、**フィルター** 関数は、これら以外に選択した日付のようにスケジュールされたイベントだけでなく、可用性が **Free** に設定されているイベントも非表示にします。

1. カレンダーで、**Circle** コントロールの **Visible** プロパティ を次の式に設定します。

    ```powerapps-dot
    CountRows(
        Filter(
            MyCalendarEvents,
            DateValue( Text(Start) ) = DateAdd( _firstDayInView, ThisItem.Value, Days ),
            ShowAs <> "Free"
        )
    ) > 0 && !Subcircle1.Visible && Title2.Visible
    ```
    この数式には、前の式と同じフィルターが含まれています。 そのため、イベント インジケーターサークルは、選択された日付に１つ以上のイベントがあり、可用性が **Free** に設定されていない場合には、日付の下に表示されません。

## <a name="integrate-the-screen-into-an-app"></a>画面をアプリに統合します。

予定表の画面は、それ自体が強力にバンドルされたコントロールですが、通常、大規模でより汎用的なアプリの一部として実行します。 これらのオプションを追加するなど、さまざまな方法でこの画面を大規模なアプリケーションに統合できます。

* [イベントの詳細表示](calendar-screen-overview.md#view-event-details)します。
* [イベントの参加者を表示する](calendar-screen-overview.md#show-event-attendees)します。

### <a name="view-event-details"></a>イベントの詳細の表示

ユーザーが **CalendarEventsGallery** でイベントを選択した場合、そのイベントに関する詳細を表示する別の画面を開くことができます。

> [!NOTE]
> この手順は、動的コンテンツを持つギャラリーのイベントの詳細を示していますが、他のアプローチを実行して、同様の結果を実現できます。 たとえば、代わりに、一連のラベルを使用してデザイン制御を取得できます。

1. **EventDetailsScreen** という名前の空白の画面を追加します。この画面には、空の伸縮可能なギャラリーとカレンダー画面に移動するボタンを格納しています。

1. 高さ可変ギャラリーに **ラベル** コントロールと **HTMLテキスト** を追加し、**AutoHeight** プロパティの両方を **true** に設定します。

    > [!NOTE]
    > PowerApps は、各イベントのメッセージ本文を **HTMLテキスト** として取得するため、そのコンテンツを HTML テキストコントロールで表示する必要があります。

1. **HTML テキスト** コントロールの **Y**  プロパティに次の式を設定します。

    `Label1.Y + Label1.Height + 20`

1. スタイルのニーズに合わせて必要に応じて、追加のプロパティを調整します。

    たとえば、**HTML テキスト** コントロールの下に区切り線を追加することができます。

1. 伸縮可能高さコントロールの **Items** プロパティに次の式を設定します。

    ```powerapps-dot
    Table(
        { Title: "Subject", Value: _selectedCalendarEvent.Subject },
        { 
            Title: "Time", 
            Value: _selectedCalendarEvent.Start & " - " & _selectedCalendarEvent.End 
        },
        { Title: "Body", Value: _selectedCalendarEvent.Body }
    )
    ```

    この式は、 **_selectedCalendarEvent** フィールド値に設定される動的データのギャラリーを作成します。ユーザーが、**CalendarEventsGallery** コントロールでイベントを選択するたびに設定されます。 複数のラベルを追加することでより多くのフィールドを含めるには、このギャラリーを拡張できますが、このセットは、適切な開始点を提供します。

1. ギャラリーアイテムを配置した後、**Label** コントロールの **Text** プロパティを `ThisItem.Title` に設定し、**Htmlテキスト** コントロールの **HtmlText** プロパティに、`ThisItem.Value`を設定します。

1. **CalendarEventsGallery** の **Title** コントロールの **OnSelect** プロパティに以下の式を設定します。

    ```powerapps-dot
    Set( _selectedCalendarEvent, ThisItem );
    Navigate( EventDetailsScreen, None )
    ```

    > [!Note]
    > **_selectedCalendarEvent**変数を使用する代わりに、**CalendarEventsGallery** を使用できます。

### <a name="show-event-attendees"></a>イベントの参加者を表示します。

`Office365.GetEventsCalendarViewV2`操作は、さまざまな必須およびオプションの出席者のセミコロンで区切られたセットを含む、各イベントのフィールドを取得します。 この手順では出席者の各セットを解析し、組織内の参加者を決定し、ユーザーの Office 365 のプロファイルを取得します。

1. アプリには、Office 365 ユーザー コネクタが含まれていない場合[追加](../add-data-connection.md)します。

1. 会議出席者の Office 365 のプロファイルを取得するには、**CalendarEventsGallery** の **Title** プロパティの **OnSelect** プロパティに次の式を設定します。

    ```powerapps-dot
    Set( _selectedCalendarEvent, ThisItem );
    ClearCollect( AttendeeEmailsTemp,
        Filter(
            Split( ThisItem.RequiredAttendees & ThisItem.OptionalAttendees, ";" ),
            !IsBlank( Result )
        )
    );
    ClearCollect( AttendeeEmails,
        AddColumns( AttendeeEmailsTemp, 
            "InOrg",
            Upper( _userDomain ) = Upper( Right( Result, Len( Result ) - Find( "@", Result ) ) )
        )
    );
    ClearCollect( MyPeople,
        ForAll( AttendeeEmails, If( InOrg, Office365Users.UserProfile( Result ) ) ) 
    );
    Collect( MyPeople,
        ForAll( AttendeeEmails,
            If( !InOrg, 
                { DisplayName: Result, Id: "", JobTitle: "", UserPrincipalName: Result }
            )
        )
    )
    ```

この一覧は、**ClearCollect** 操作が行うことについて説明します。

- ClearCollect(AttendeeEmailsTemp)
    ```powerapps-dot
    ClearCollect( AttendeeEmailsTemp,
        Filter(
            Split( ThisItem.RequiredAttendees & ThisItem.OptionalAttendees, ";" ), 
            !IsBlank( Result)
        )
    );
    ```

    この数式は、1 つの文字列に必須およびオプションの参加者を連結し、その文字列をセミコロンで個々のアドレスに分割します。 数式がそのセットから空の値を除去し、その他の値を **AttendeeEmailsTemp** というコレクションに追加します。

- ClearCollect(AttendeeEmails)
    ```powerapps-dot
    ClearCollect( AttendeeEmails,
        AddColumns( AttendeeEmailsTemp, 
            "InOrg",
            Upper( _userDomain ) = Upper( Right( Result, Len(Result) - Find("@", Result) ) )
        )
    );
    ```
    この数式はほぼ、参加者が組織かどうかを判断します。 定義 **_userDomain**は、アプリを実行するユーザーの電子メール アドレスのドメイン URL だけです。 この行は、という名前の追加の true または false 列を作成します。 **InOrg**の、 **AttendeeEmailsTemp**コレクション。 この列に含まれる**true**場合**userDomain**はその特定の行で、電子メール アドレスのドメインの URL に相当**AttendeeEmailsTemp**します。

    このアプローチが常に、正確ではありませんが、かなりの精度で取得します。 たとえば、組織内の特定の出席者には、Jane@OnContoso.comのような電子メールアドレスがあり、 **_userDomain** は、Contoso.com です。 アプリのユーザーと Jane は同じ会社で作業しますが、電子メール アドレスに若干のバリエーションがある可能性があります。 このような場合、以下の式を使用できます。

    `Upper(_userDomain) in Upper(Right(Result, Len(Result) - Find("@", Result)))`

    ただし、この式は、Jane@NotTheContosoCompany.com と Contoso.com のような **_userDomain** を照合し、同じ会社として判断しないようにします。

- ClearCollect(MyPeople)

    ```powerapps-dot
    ClearCollect( MyPeople,
        ForAll( AttendeeEmails, 
            If( InOrg, 
                Office365Users.UserProfile( Result )
            )
        )
    );
    Collect( MyPeople,
        ForAll( AttendeeEmails,
            If( !InOrg, 
                { 
                    DisplayName: Result, 
                    Id: "", 
                    JobTitle: "", 
                    UserPrincipalName: Result
                }
            )
        )
    );
    ```
    Office 365 のプロファイルを取得するに使用する必要があります、 [Office365Users.UserProfile](https://docs.microsoft.com/connectors/office365users/#userprofile)または[Office365Users.UserProfileV2](https://docs.microsoft.com/connectors/office365users/#userprofile)操作。 まず、これらの操作は、ユーザーの組織では参加者の Office 365 のすべてのプロファイルを収集します。操作は、組織の外部からの参加者のいくつかのフィールドを追加します。 個別の操作にこれら 2 つの項目が区切られた、 **ForAll**ループの順序を保証していません。 そのため、 **ForAll**最初に、組織の外部からの参加者を収集する可能性があります。 この場合、スキーマを**MyPeople**のみを含む**DisplayName**、 **Id**、 **JobTitle**、および**UserPrincipalName**. ただし、ユーザー プロファイルの操作より多くの高度なデータが取得されます。 強制するように、 **MyPeople**他のプロファイルの前に Office 365 のプロファイルを追加するコレクション。

    > [!NOTE]
    > 1 つだけで同じ結果を実現する**ClearCollect**関数。

    ```powerapps-dot
    ClearCollect( MyPeople, 
        ForAll(
            AddColumns(
                Filter(
                    Split(
                        ThisItem.RequiredAttendees & ThisItem.OptionalAttendees, 
                        ";"
                    ), 
                    !IsBlank( Result )
                ), 
                "InOrg", _userDomain = Right( Result, Len( Result ) - Find( "@", Result ) )
            ), 
            If( InOrg, 
                Office365Users.UserProfile( Result ), 
                { 
                    DisplayName: Result, 
                    Id: "", 
                    JobTitle: "", 
                    UserPrincipalName: Result, 
                    Department: "", 
                    OfficeLocation: "", 
                    TelephoneNumber: ""
                }
            )
        )
    )
    ```

この演習を完了します。

1. 対象のギャラリーを含む画面を追加、**項目**プロパティに設定されて**MyPeople**します。

1. **OnSelect**のプロパティ、**タイトル**を制御、 **CalendarEventsGallery**、追加、 **Navigate**画面に関数前の手順で作成します。

## <a name="next-steps"></a>次の手順

* [この画面のリファレンス ドキュメントを表示](calendar-screen-reference.md)します。
* [詳細については、Office 365 Outlook コネクタは](../connections/connection-office365-outlook.md)します。
* [詳細については、Office 365 ユーザー コネクタは](../connections/connection-office365-users.md)します。

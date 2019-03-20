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
ms.sourcegitcommit: 5e15a1033a68289781f8092fb65c57432501f911
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2019
ms.locfileid: "54459507"
---
# <a name="overview-of-the-calendar-screen-template-for-canvas-apps"></a>キャンバス アプリの予定表画面テンプレートの概要

キャンバス アプリでは、自分の Office 365 Outlook アカウントからの今後のイベントをユーザーに表示されるカレンダー画面を追加します。 ユーザーは、予定表とその日のイベントの一覧をスクロールしてから日付を選択することができます。 詳細情報が一覧に表示、各イベントに関する詳細を表示する 2 つ目の画面を追加、各イベントの出席者の一覧を表示およびその他のカスタマイズを行うを変更することができます。

など、Office 365 から別のデータを表示する他のテンプレートに基づく画面を追加することもできます[電子メール](email-screen-overview.md)、[人](people-screen-overview.md)、組織内および[可用性](meeting-screen-overview.md)人のユーザーの。会議に招待する必要あります。

この概要を説明します。
> [!div class="checklist"]
> * 既定のカレンダーの画面を使用する方法。
> * これを変更する方法。
> * アプリに統合する方法。

この画面の既定の機能について詳しくを参照してください、[カレンダー画面参照](calendar-screen-reference.md)します。

## <a name="prerequisite"></a>前提条件

追加しても画面とその他のコントロールを構成する方法に関する知識[PowerApps でアプリを作成](../data-platform-create-app-scratch.md)です。

## <a name="default-functionality"></a>既定の機能

テンプレートからカレンダー画面を追加します。

1. [サインイン](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)PowerApps にアプリを作成するか、PowerApps Studio で既存のアプリを開きます。

    このトピックでは、phone アプリが、タブレット アプリを同じ概念が適用されます。

1. **ホーム**、リボンのタブ**新しい画面** > **カレンダー**します。

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

さらに画面を変更する場合を使用して、[カレンダー画面参照](./calendar-screen-reference.md)をガイドとして。

### <a name="specify-the-calendar"></a>カレンダーを指定します。

ユーザーを表示するカレンダーを既に知っている場合、アプリを発行する前に、その暦を指定することで、画面を簡略化できます。 この変更は、それを削除するために、カレンダーのドロップダウン リストの必要性を削除します。

1. 設定、 **[OnStart](../controls/control-screen.md)** 式をアプリで既定の画面のプロパティ。

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
    > 既定値から次の数式を編集して少し、 **OnSelect**カレンダーを選択するためのドロップダウン リストのプロパティ。 そのコントロールの詳細については、そのセクションを参照して、[カレンダー画面参照](./calendar-screen-reference.md#calendar-drop-down)します。

1. 置換`{YourCalendarNameHere}`など、表示するカレンダーの名前を使用して、中かっこ (たとえば、**カレンダー**)。

    > [!IMPORTANT]
    > 次の手順では、予定表の 1 つだけの画面をアプリに追加したことを前提としています。 1 つ以上、コントロール名を追加した場合 (など**iconCalendar1**) を別の数値で終了して、数式を適宜調整する必要があります。

1. 設定、 **Y**のプロパティ、 **iconCalendar1**コントロールに次の式。

    `RectQuickActionBar1.Height + 20`

1. 設定、 **Y**のプロパティ、 **LblMonthSelected1**コントロールに次の式。

    `iconCalendar1.Y + iconCalendar1.Height + 20`

1. 設定、**テキスト**のプロパティ、 **LblNoEvents1**コントロールをこの値にします。

    `"No events scheduled"`

1. 設定、 **Visible**プロパティの**LblNoEvents1**に次の式。

    `CountRows(CalendarEventsGallery1.AllItems) = 0 && _calendarVisible`

1. これらのコントロールを削除します。

    - **dropdownCalendarSelection1**
    - **LblEmptyState1**
    - **iconEmptyState1**

1. 予定表の画面が既定の画面でない場合は、アプリをテストできるように、既定の画面から予定表の画面に移動するボタンを追加します。

    たとえば、ボタンを追加で**Screen1**にナビゲートする**Screen2**カレンダー画面を一から作成されたアプリに追加した場合。

1. アプリを保存し、ブラウザーまたはモバイル デバイスで、テストします。

### <a name="show-different-details-about-an-event"></a>イベントに関するさまざまな詳細を表示します。

既定では、[予定表] ギャラリーでという名前の**CalendarEventsGallery**、開始時刻、期間、件名、および各イベントの場所を示しています。 開催者) などの任意のフィールドを表示するギャラリーを構成することができますが、 [Office 365 コネクタ](https://docs.microsoft.com/connectors/office365/#calendareventclientreceive)をサポートしています。

1. **CalendarEventsGallery**、設定、**テキスト**プロパティの新しいまたは既存のラベルを`ThisItem`ピリオドが続きます。

    IntelliSense には、選択可能なフィールドが一覧表示されます。

1. 使用するフィールドを選択します。

    ラベルには、指定した情報の種類が表示されます。

### <a name="hide-nonblocking-events"></a>非ブロッキングのイベントを非表示にします。

多くのオフィスでは、チーム メンバーは、これらは、オフィスのときに互いに通知する会議出席依頼を送信します。 要求の送信先のユーザー設定の可用性をすべてのユーザーのスケジュールがブロックされないように、 **Free**します。 2 つのプロパティを更新することで、予定表と、ギャラリーからこれらのイベントを非表示にできます。

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

    この数式で、**フィルター**関数は、これら以外に選択した日付のようにスケジュールされたイベントだけでなく、可用性に設定されているイベントを非表示に**Free**します。

1. 予定表、設定、 **Visible**のプロパティ、**円**コントロールをこの式に。

    ```powerapps-dot
    CountRows(
        Filter(
            MyCalendarEvents,
            DateValue( Text(Start) ) = DateAdd( _firstDayInView, ThisItem.Value, Days ),
            ShowAs <> "Free"
        )
    ) > 0 && !Subcircle1.Visible && Title2.Visible
    ```
    次の数式には、前の公式として同じフィルターが含まれています。 そのため、イベント インジケーター円下に表示されます、日付が 1 つかは、可用性がされていないと、選択した日付でより多くのイベントを設定場合にのみ**Free**します。

## <a name="integrate-the-screen-into-an-app"></a>画面をアプリに統合します。

予定表の画面は、独自の右にあるコントロールの強力なバンドルが通常最適な大規模でより汎用的なアプリの一部として実行します。 この画面は、さまざまな方法は、これらのオプションの追加などの大規模なアプリケーションに統合できます。

* [イベントの詳細表示](calendar-screen-overview.md#view-event-details)します。
* [イベントの参加者を表示する](calendar-screen-overview.md#show-event-attendees)します。

### <a name="view-event-details"></a>イベントの詳細の表示

ユーザーが内のイベントを選択した場合**CalendarEventsGallery**、そのイベントの詳細を表示する別の画面を開くことができます。

> [!NOTE]
> この手順は、動的コンテンツを持つギャラリーのイベントの詳細を示していますが、他のアプローチを実行して、同様の結果を実現できます。 たとえば、代わりに、一連のラベルを使用してデザイン制御を取得できます。

1. という名前の空の画面を追加**EventDetailsScreen**、空白の柔軟な高さギャラリーとカレンダー画面に移動するボタンを格納しています。

1. 高さ可変ギャラリーで追加、**ラベル**コントロールと**HTML テキスト**を制御して、設定、 **AutoHeight**プロパティの両方を**true**.

    > [!NOTE]
    > そのコンテンツを表示する必要があるため HTML 文字列として取得しますの各イベントのメッセージ本文を PowerApps を**HTML テキスト**コントロール。

1. 設定、 **Y**のプロパティ、 **HTML テキスト**コントロールに次の式。

    `Label1.Y + Label1.Height + 20`

1. スタイルのニーズに合わせて必要に応じて、追加のプロパティを調整します。

    次の区切り線を追加するなど、 **HTML テキスト**コントロール。

1. 設定、**項目**次の数式に柔軟な高さギャラリーのプロパティ。

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

    次の数式作成の動的なデータのフィールドの値に設定されているギャラリー **_selectedCalendarEvent**、ユーザーが内のイベントを選択するたびに設定されています、 **CalendarEventsGallery**コントロール。 複数のラベルを追加することでより多くのフィールドを含めるには、このギャラリーを拡張できますが、このセットは、適切な開始点を提供します。

1. ギャラリー項目を場所で、設定、**テキスト**のプロパティ、**ラベル**に制御を`ThisItem.Title`と**HtmlText**のプロパティ、 **HTML テキスト**に制御を`ThisItem.Value`します。

1. **CalendarEventsGallery**、設定、 **OnSelect**のプロパティ、**タイトル**コントロールに次の式。

    ```powerapps-dot
    Set( _selectedCalendarEvent, ThisItem );
    Navigate( EventDetailsScreen, None )
    ```

    > [!Note]
    > 使用する代わりに、 **_selectedCalendarEvent**変数、代わりに使用できます**CalendarEventsGallery**します。選択されています。

### <a name="show-event-attendees"></a>イベントの参加者を表示します。

`Office365.GetEventsCalendarViewV2`操作は、さまざまな必須およびオプションの出席者のセミコロンで区切られたセットを含む、各イベントのフィールドを取得します。 この手順ではします出席者の各セットを解析、および、組織内のどの参加者を決定は、ユーザーの Office 365 のプロファイルを取得します。

1. アプリには、Office 365 ユーザー コネクタが含まれていない場合[追加](../add-data-connection.md)します。

1. 会議の出席者の Office 365 のプロファイルを取得するには、設定、 **OnSelect**のプロパティ、**タイトル**を制御、 **CalendarEventsGallery**に次の式。

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

この一覧は、それぞれについて説明します**ClearCollect**操作では。

- ClearCollect(AttendeeEmailsTemp)
    ```powerapps-dot
    ClearCollect( AttendeeEmailsTemp,
        Filter(
            Split( ThisItem.RequiredAttendees & ThisItem.OptionalAttendees, ";" ), 
            !IsBlank( Result)
        )
    );
    ```

    この数式は、1 つの文字列に必須およびオプションの参加者を連結し、し、その文字列をセミコロンで個々 のアドレスに分割します。 数式がそのセットから空の値を除去し、その他の値をという名前のコレクションに追加**AttendeeEmailsTemp**します。

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

    このアプローチが常に、精度ですが言葉を取得します。 たとえば、組織内の特定の出席者のような電子メール アドレスがあるJane@OnContoso.comであるのに対し **_userDomain**は Contoso.com です。 アプリのユーザーと Jane が同じ会社に作業しますが、電子メール アドレスに若干のバリエーションがある可能性があります。 ような場合、この数式を使用する場合があります。

    `Upper(_userDomain) in Upper(Right(Result, Len(Result) - Find("@", Result)))`

    ただし、次の数式がなど、電子メール アドレスと一致するJane@NotTheContosoCompany.comで、 **_userDomain** Contoso.com の場合と持っているユーザーは、同じ会社に機能しないようにします。

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

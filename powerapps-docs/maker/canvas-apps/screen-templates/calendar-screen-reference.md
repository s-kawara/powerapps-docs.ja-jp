---
title: キャンバス アプリの予定表画面テンプレートのリファレンス |Microsoft Docs
description: PowerApps でキャンバス アプリの予定表画面テンプレートのしくみの詳細を理解します。
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
ms.openlocfilehash: e3d5f40a604d2cbfa074ed5973d599c40a6c5c05
ms.sourcegitcommit: 647e183c070c2159b790c7813a7be1d60b2551bd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/01/2019
ms.locfileid: "58765585"
---
# <a name="reference-information-about-the-calendar-screen-template-for-canvas-apps"></a>キャンバス アプリの予定表画面テンプレートに関する参照情報

PowerApps でキャンバス アプリの場合は、カレンダー画面テンプレートの重要な各コントロールは、画面の全体的な既定の機能に貢献する方法について説明します。 この詳細情報は、動作の数式とその他のコントロールがユーザー入力に応答する方法を決定するプロパティの値を表示します。 この画面の既定の機能の概要については、、[カレンダー画面概要](calendar-screen-overview.md)を参照してください。

このトピックでは、いくつかの重要なコントロールを強調表示し、さまざまなプロパティに式または数式をについて説明します (など**項目**と**OnSelect**) は、これらのコントロールの設定。

- [予定表のドロップダウン (dropdownCalendarSelection)](#calendar-drop-down)
- [予定表アイコン (iconCalendar)](#calendar-icon)
- [前の月のシェブロン (iconPrevMonth)](#previous-month-chevron)
- [翌月のシェブロン (iconNextMonth)](#next-month-chevron)
- [予定表のギャラリー (MonthDayGallery) (+ 子コントロール)](#calendar-gallery)
- [イベントのギャラリー (CalendarEventsGallery)](#events-gallery)

## <a name="prerequisite"></a>前提条件

追加しても画面とその他のコントロールを構成する方法に関する知識[PowerApps でアプリを作成](../data-platform-create-app-scratch.md)です。

## <a name="calendar-drop-down"></a>ドロップダウンの予定表

![dropdownCalendarSelection コントロール](media/calendar-screen/calendar-dropdown.png)

- プロパティ:**項目**<br>
    値: `Office365.CalendarGetTables().value`

    この値は、アプリ ユーザーの Outlook の予定表を取得するコネクタの操作です。 わかります[値](https://docs.microsoft.com/connectors/office365/#entitylistresponse[table])この操作を取得します。

- プロパティ:**OnChange**<br>値: `Select(dropdownCalendarSelection)`

    ユーザーが、コントロールの関数の一覧でオプションを選択すると**OnSelect**プロパティを実行します。

- プロパティ:**OnSelect**<br>
    値:**場合**関数で、次のコード ブロックが表示されたら、およびその後のコード ブロックに表示されるいくつかの追加の関数。

   今回の最初に、アプリを開いた後に、ユーザーがドロップダウン リストで、オプションを選択するときにのみ、式が実行されます。

    ```powerapps-dot
    If( IsBlank( _userDomain ),
        UpdateContext( {_showLoading: true} );
        Set( _userDomain, Right( User().Email, Len( User().Email ) - Find( "@", User().Email ) ) );
        Set( _dateSelected, Today() );
        Set( _firstDayOfMonth, DateAdd( Today(), 1 - Day( Today() ), Days ) );  
        Set( _firstDayInView, DateAdd( _firstDayOfMonth, -(Weekday(_firstDayOfMonth) - 1), Days ) );
        Set( _lastDayOfMonth, DateAdd( DateAdd( _firstDayOfMonth, 1, Months ), -1, Days ) )  
    );
    ```

    上記のコードでは、次の変数を定義します。
    
  - **\_userDomain**:アプリ ユーザーの会社のドメイン、ユーザーの電子メール アドレスに反映します。
  - **\_dateSelected**:今日の日付 (既定)。 カレンダー ギャラリーが、この日付を強調表示し、イベント ギャラリーには、その日付のようにスケジュールされたイベントが表示されます。
  - **\_firstDayOfMonth**:現在の月の最初の日。 `(Today + (1 - Today)) = Today - Today + 1 = 1`、この**DateAdd**関数は、常に、1 か月の最初の曜日を返します。
  - **\_firstDayInView**:予定表のギャラリーを表示する最初の日。 この値はありません、1 か月の開始、日曜日の場合を除き、1 か月の最初の日と同じです。 前の月の値の全体の週を表示しないようにする **\_firstDayInView**は`_firstDayOfMonth - Weekday(_firstDayOfMonth) + 1`します。
  - **\_lastDayOfMonth**:来月は、マイナス 1 日の最初の日と同じである現在の月の最終日。

   後に、関数、**場合**関数の実行、ユーザーは、予定表のドロップダウン リスト (だけでなく、ユーザーがアプリを開く最初時間) でオプションを選択するたびに。

    ```powerapps-dot
    Set( _calendarVisible, false );
    UpdateContext( {_showLoading: true} );
    Set( _myCalendar, dropdownCalendarSelection2.Selected );
    Set( _minDate, 
        DateAdd( _firstDayOfMonth, -(Weekday( _firstDayOfMonth ) - 2 + 1), Days )
    );
    Set(_maxDate, 
        DateAdd(
            DateAdd( _firstDayOfMonth, -(Weekday( _firstDayOfMonth ) - 2 + 1), Days ), 
            40, 
            Days
        )
    );
    ClearCollect( MyCalendarEvents, 
        'Office365'.GetEventsCalendarViewV2( _myCalendar.Name, 
            Text( _minDate, UTC ), 
            Text( _maxDate, UTC )
        ).value
    );
    UpdateContext( {_showLoading: false} );
    Set( _calendarVisible, true )
    ```

    上記のコードでは、これらの変数と 1 つのコレクションを定義します。

    - **\_calendarVisible**:設定**false**新しい選択範囲の読み込み中に、カレンダーが表示されないようにします。
    - **\_showLoading**:設定**true**読み込みインジケーターは、新しい選択範囲の読み込み中に表示されるようにします。
    - **\_myCalendar**:現在の値に設定、**カレンダー ドロップダウン**コントロールを適切なカレンダーからイベントを取得します。
    - **\_minDate**:同じ値に設定 **\_firstDayInView**します。 この変数は、どのようなイベントが既に Outlook から取得して、アプリでキャッシュを決定します。
    - **\_maxDate**:カレンダーの表示可能な最後の日に設定します。 数式は`_firstDayInView + 40`します。 予定表 41 日、最大を表示するため、  **\_maxDate**変数は常に最後の表示可能な日を反映し、どのようなイベントが既に Outlook から取得して、アプリでキャッシュを決定します。
    - **MyCalendarEvents**:ユーザーのイベントのコレクションから、選択したカレンダーから設定 **\_minDate**に **\_maxDate**します。
    - **\_showLoading**:設定**false**; **\_calendarVisible**に設定されている**true**他のすべてが読み込まれた後です。

## <a name="calendar-icon"></a>カレンダーのアイコン

![iconCalendar コントロール](media/calendar-screen/calendar-today-icon.png)

- プロパティ:**OnSelect**<br>
    値:次の 4 つ**設定**今日の日付をカレンダー ギャラリーをリセットする関数。

    ```powerapps-dot
    Set( _dateSelected, Today() );
    Set( _firstDayOfMonth, DateAdd( Today(), 1 - Day( Today() ), Days) );
    Set( _firstDayInView, DateAdd(_firstDayOfMonth, -(Weekday( _firstDayOfMonth ) - 2 + 1), Days));
    Set( _lastDayOfMonth, DateAdd( DateAdd( _firstDayOfMonth, 1, Months ), -1, Days ) )
    ```

    上記のコードでは、適切なカレンダー ビューを表示するために必要なすべての日付変数をリセットします。

    - **\_dateSelected**今日にリセットされます。
    - **\_firstDayOfMonth**は現在の月の最初の日にリセットされます。
    - **\_firstDayInView**が現在の月を選択すると、表示可能なから 1 日にリセットします。
    - **\_lastDayOfMonth**は現在の月の最終日にリセットされます。

    [**カレンダー ドロップダウン**](#calendar-drop-down)このトピックのセクションには、これらの変数について詳しくがについて説明します。

## <a name="previous-month-chevron"></a>前の月のシェブロン

![iconPrevMonth コントロール](media/calendar-screen/calendar-back.png)

- プロパティ:**OnSelect**<br>値:次の 4 つ**設定**関数と**場合**カレンダー ギャラリーで、前の月を表示する関数。

    ```powerapps-dot
    Set( _firstDayOfMonth, DateAdd( _firstDayOfMonth, -1, Months ) );
    Set( _firstDayInView, 
        DateAdd( _firstDayOfMonth, -(Weekday( _firstDayOfMonth ) - 2 + 1), Days )
    );
    Set( _lastDayOfMonth, DateAdd(DateAdd( _firstDayOfMonth, 1, Months ), -1, Days ) );
    If( _minDate > _firstDayOfMonth,
        Collect( MyCalendarEvents,
            'Office365'.GetEventsCalendarViewV2( _myCalendar.Name,
                Text( _firstDayInView, UTC ), 
                Text( DateAdd( _minDate, -1, Days ), UTC )
            ).value
        );
        Set( _minDate, _firstDayInView )
    )
    ```

    > [!NOTE]
    > 定義 **\_firstDayOfMonth**、  **\_firstDayInView**、および **\_lastDayOfMonth**とほぼ同じですが[カレンダー ドロップダウン](#calendar-drop-down)このトピックの「します。

    上記のコードの最初の 3 つの行は、ユーザーは、前の月のシェブロンを選択するたびに実行します。 コードでは、適切なカレンダー ビューを表示するために必要な変数を設定します。 残りのコードは、ユーザー、選択したカレンダーの月を選択していない場合のみ実行されます。

    この場合は、  **\_minDate**は、前の月を表示するときに表示される最初の日になります。 ユーザーが、アイコンを選択する前に **\_minDate**が現在の月の 23 の最小有効値。 (3 月 1 日が土曜日、ときに **\_firstDayInView**年 3 月は年 2 月 23日です)。つまり、ユーザーがまだ、この月を選択していない場合 **\_minDate**が、新しいより大きい **\_firstDayOfMonth**、および**場合**関数が返される**true**します。 コードを実行し、コレクションと変数を更新します。

    - **MyCalendarEvents**で選択したカレンダーからイベントを取得、 [Office365.GetEventsCalendarViewV2](https://docs.microsoft.com/connectors/office365/#get-calendar-view-of-events--v2-)操作。 日付範囲は、  **\_firstDayInView**日付と **\_minDate** - 1。 **MyCalendarEvents**でイベントが既に含まれています、  **\_minDate**日付、1 は、この新しい日付の範囲の最大値の日付から減算されます。

    - **\_minDate**現在に設定されている **\_firstDayInView**イベントが取得された最初の日付です。 前の月のシェブロンを選択して、ユーザーがこの日付に戻った場合、**場合**関数が返される**false**; で、このビューのイベントが既にキャッシュされているため、コードを実行しない**MyCalendarEvents**します。

## <a name="next-month-chevron"></a>翌月のシェブロン

![iconNextMonth コントロール](media/calendar-screen/calendar-forward.png)

- プロパティ:**OnSelect**<br>
    値:次の 4 つ**設定**関数と**場合**カレンダー ギャラリーで次の月を表示する関数。

    ```powerapps-dot
    Set( _firstDayOfMonth, DateAdd( _firstDayOfMonth, 1, Months ) );
    Set( _firstDayInView, 
        DateAdd( _firstDayOfMonth, -(Weekday( _firstDayOfMonth ) - 2 + 1), Days ) );
    Set( _lastDayOfMonth, DateAdd( DateAdd( _firstDayOfMonth, 1, Months ), -1, Days ) );
    If( _maxDate < _lastDayOfMonth,
        Collect( MyCalendarEvents, 
            'Office365'.GetEventsCalendarViewV2( _myCalendar.Name, 
                Text( DateAdd( _maxDate, 1, Days ), UTC ), 
                DateAdd( _firstDayInView, 40, Days )
            ).value
        );
        Set( _maxDate, DateAdd( _firstDayInView, 40, Days) )    
    )
    ```

    > [!NOTE]
    > 定義 **\_firstDayOfMonth**、  **\_firstDayInView**、および **\_lastDayOfMonth**とほぼ同じですが[カレンダー ドロップダウン](#calendar-drop-down)このトピックの「します。

    ユーザーが、翌月のシェブロンを選択を実行するには、上記のコードの最初の 3 行では、適切なカレンダー ビューを表示するために必要な変数を設定します。 残りのコードは、ユーザー、選択したカレンダーの月を選択していない場合のみ実行されます。

    その場合は、  **\_maxDate**は、前の月を表示するときに表示される最後の日になります。 ユーザーが、翌月のシェブロンを選択する前に **\_maxDate**が次の月の 13 の場合は、最大有効値。 (2 月 1 日になった場合に非 leap 年で、日曜日 **\_maxDate**年 3 月 13 日に、これは、  **\_firstDayInView** + 40 日間です)。つまり、ユーザーがまだ、この月を選択していない場合 **\_maxDate**が、新しいより大きい **\_lastDayOfMonth**、および**場合**関数返します**true**します。 コードを実行し、コレクションと変数を更新します。

    - **MyCalendarEvents**で選択したカレンダーからイベントを取得、 [Office365.GetEventsCalendarViewV2](https://docs.microsoft.com/connectors/office365/#get-calendar-view-of-events--v2-)操作。 日付範囲は **\_maxDate** + 1 日と **\_firstDayInView** + 40 日。 **MyCalendarEvents**でイベントが既に含まれています、  **\_minDate**日付、1 は、この新しい日付の範囲の最小値の日付に追加されます。 **\_firstDayInView** + 40 は式の **\_maxDate**ので、範囲内の 2 つ目の日付はだけ新しい **\_maxDate**します。

    - **\_maxDate**に設定されている **\_firstDayInView** + 40 日ため、これは、最後の日のイベントが取得されます。 ユーザーが、翌月のシェブロンを選択してこの日付を返す場合、**場合**関数が返される**false**; で、このビューのイベントが既にキャッシュされているため、コードを実行しない**MyCalendarEvents**します。

## <a name="calendar-gallery"></a>予定表のギャラリー

![MonthDayGallery コントロール](media/calendar-screen/calendar-month-gall.png)

- プロパティ:**項目**<br>
    値: `[0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,
    20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41]`
  
  最悪のシナリオでは、カレンダー ビューが 42 の完全な日を表示する必要があるために、予定表のギャラリー内の項目の 0 ~ 41 のセットが使用されます。 これには、月の最初の土曜日に発生し、日曜日に、1 か月の最後に発生しますが発生します。 この場合は、格納している、月の最初の行では、前の月から 6 日と月の最後のタスクを含む行の次の月から 6 日間、カレンダーが表示されます。 これは、30 が選択された月の 42 の一意な値です。

- プロパティ:**WrapCount**<br>
    値: `7`

  この値は、7 日間の週を反映します。

### <a name="title-control-in-the-calendar-gallery"></a>カレンダー ギャラリー内のコントロールのタイトル

![MonthDayGallery タイトル コントロール](media/calendar-screen/calendar-month-text.png)

- プロパティ:**[Text (テキスト)]**<br>
    値: `Day( DateAdd( _firstDayInView, ThisItem.Value, Days ) )`

    いることを思い出してください **\_firstDayInView**として定義されます (**\_firstDayOfMonth** -曜日の値) + 1 です。 これを **\_firstDayInView**は常に日曜日と **\_firstDayOfMonth**の最初の行では常に**MonthDayGallery**します。 これら 2 つの事実により **\_firstDayInView**の最初のセルは、常に**MonthDayGallery**します。 **ThisItem.Value**のセルの数が、 **MonthDayGallery**アイテム プロパティ。 そのため、取得 **\_firstDayInView** 、開始点として、各セルがの増分値を表示します **\_firstDayInView** + の各セルの値。

- プロパティ:**塗りつぶし**<br>
    値:1 つ**場合**関数。

    ```powerapps-dot
    If( DateAdd( _firstDayInView, ThisItem.Value ) = Today() && 
                DateAdd( _firstDayInView, ThisItem.Value ) = _dateSelected, 
            RGBA( 0, 0, 0, 0 ),
        DateAdd( _firstDayInView, ThisItem.Value) = Today(), 
            ColorFade( Subcircle.Fill, 0.67 ),
        Abs( Title.Text - ThisItem.Value) > 10,
            RGBA( 200, 200, 200, 0.3 ),
        RGBA( 0, 0, 0, 0 )
    )
    ```

  説明で説明したように、**テキスト**プロパティ、`DateAdd(_firstDayInView, ThisItem.Value)`表示のセルで、1 日を表します。 これを考慮して、上記のコードは、これらの比較を実行します。
  1. セルの値は、今日の日付と、このセルが等価場合 **\_dateSelected**fill 値を指定しません。
  1. セルの値が今日の日付である場合に相当しないが、  **\_dateSelected**、提供、 **ColorFade**塗りつぶし。
  1. 最後の比較は、クリアはありません。 セルの実際のテキスト値とセルの項目 (ディスプレイの番号) と項目の数の値を比較することをお勧めします。<br>

      より理解を 2018 年 9 月の日を検討してください開始日は土曜日、日曜日に終了する月。 ここでは、予定表は最初の行でから 31 日までの 9 月 1 日、年 8 月の 26 日が表示されますおよび`Abs(Title.Text - ThisItem.Value) = 26`年 9 月 1 日までです。 `Abs(Title.Text - ThisItem.Value) = 5`します。 6 日から 9 月 30 日と年 10 月 1 日を表示します。 予定表の最後の行まで 5 でそのまま残ります。 その`Abs(Title.Text - ThisItem.Value)`年 9 月 30 日の 5 はできますが、年 10 月の日付の 35 になります。<br>

      これは、パターンです。前の月から表示されている日付の`Abs(Title.Text - ThisItem.Value)`が常に等しく、`Title.Text`ディスプレイ上の最初の日の値。 次の月に表示されている日の`Abs(Title.Text - ThisItem.Value)`が常に等しく、 **MonthDayGallery**項目から 1 を引いた (この例では 10 月 1 日) では、その月の最初のセルの値。 現在選択されている 1 か月間に表示されている日付の最も重要なは、`Abs(Title.Text - ThisItem.Value)`から 1 を引いた、その月の最初の項目の値が常に等しくなるし、前の例のように、5 を超えることはありません。 できるようになりますが、数式を記述する完全に有効な`Abs(Title.Text - ThisItem.Value) > 5`します。

      このステートメントでは、日付の値は、現在選択されている月の外部にかどうかを確認します。 場合は、**入力**部分的に非透過的な灰色します。

    > [!NOTE]
    > 自分用のこの最後の比較の有効性を確認するには挿入することで、**ラベル**コントロール ギャラリーと設定をその**テキスト**プロパティをこの値に。<br>`Abs(Title.Text - ThisItem.Value)`.

- プロパティ:**表示されます。**<br>
    値:

    ```powerapps-dot
    !(
        DateAdd( _firstDayInView, ThisItem.Value, Days ) - 
            Weekday( DateAdd( _firstDayInView, ThisItem.Value,Days ) ) + 1 
        > _lastDayOfMonth
    )
    ```

    前のステートメントは、現在選択されている月の日付が発生しない行に、セルがあるかどうかを確認します。 在住されたことを思い出してください日付値からの日の曜日の値を減算して、常に 1 を追加するその日の行の最初の項目を返します。 このため、このステートメントは、行の最初の日が表示可能な月の最終日の後かどうかを確認します。 場合は、行全体には、次の月の日が含まれているために表示されません。

- プロパティ:**OnSelect**<br>
    値:A**設定**を設定する関数、  **\_dateSelected**変数を選択したセルの日付。

    ```powerapps-dot
    Set( _dateSelected, DateAdd( _firstDayInView, ThisItem.Value, Days ) )
    ```

### <a name="circle-control-in-the-calendar-gallery"></a>カレンダー ギャラリー内のコントロールの円

![MonthDayGallery 円コントロール](media/calendar-screen/calendar-month-event.png)

- プロパティ:**表示されます。**<br>
    値:かどうかと、選択した日付のすべてのイベントがスケジュールされているかどうかを決定する式、 **Subcircle**と**タイトル**コントロールを表示します。

    ```powerapps-dot
    CountRows(
        Filter( MyCalendarEvents, 
            DateValue( Text( Start ) ) = DateAdd( _firstDayInView, ThisItem.Value, Days )
        )
    ) > 0 && !Subcircle.Visible && Title.Visible
    ```

    **円**コントロールが表示される場合、**開始**フィールドは、任意のイベントは、そのセルの日付と等しい場合、**タイトル**コントロールが表示される場合は、場合に、 **Subcircle**コントロールは表示されません。 つまり、この日に少なくとも 1 つのイベントが発生し、この日が選択されていない場合は、このコントロールが表示されます。 その日のイベントが表示されますが選択されている場合、 **CalendarEventsGallery**コントロール。

### <a name="subcircle-control-in-the-calendar-gallery"></a>予定表のギャラリーで subcircle コントロール

![MonthDayGallery Subcircle コントロール](media/calendar-screen/calendar-month-selected.png)

- プロパティ:**表示されます。**<br>
    値:

    ```powerapps-dot
    DateAdd( _firstDayInView, ThisItem.Value ) = _dateSelected && Title.Visible
    ```

  **Subcircle**コントロールが表示されるときに **\_dateSelected**は、セルの日付に相当し、**タイトル**コントロールが表示されます。 つまり、このコントロールには、セルが現在選択されている日付が表示されます。

## <a name="events-gallery"></a>イベントのギャラリー

![CalendarEventsGallery コントロール](media/calendar-screen/calendar-events-gall.png)

- プロパティ:**項目**<br>
    値:並べ替えし、イベントのギャラリーをフィルター処理する式。

    ```powerapps-dot
    SortByColumns(
        Filter( MyCalendarEvents,
            Text( Start, DateTimeFormat.ShortDate ) = Text( _dateSelected, DateTimeFormat.ShortDate )
        ),
        "Start"
    )
    ```

   **MyCalendarEvents**コレクション間のすべてのイベントに含まれる **\_minDate**と **\_maxDate**します。 選択されている日付のみをイベントを表示するためにフィルターが適用されて**MyCalendarEvents**と等価の開始日を持つイベントを表示する**\ _dateSelected**します。 項目は順番に挿入するには、開始日で並べ替えられます。

## <a name="next-steps"></a>次の手順

- [この画面を詳細します。](./calendar-screen-overview.md)
- [PowerApps での Office 365 Outlook コネクタの詳細します。](../connections/connection-office365-outlook.md)
- [PowerApps での Office 365 Users コネクタの詳細します。](../connections/connection-office365-users.md)

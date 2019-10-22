---
title: Canvas apps のカレンダー画面テンプレートのリファレンス |Microsoft Docs
description: PowerApps でキャンバスアプリのカレンダー画面テンプレートがどのように機能するかについて詳しく説明します。
author: emcoope-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 12/31/2018
ms.author: emcoope
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: b9e5425244d819816fa05c4b780a6be092b0d22c
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "71995726"
---
# <a name="reference-information-about-the-calendar-screen-template-for-canvas-apps"></a>キャンバスアプリのカレンダー画面テンプレートに関する参照情報

PowerApps のキャンバスアプリの場合、カレンダー画面テンプレートの各重要なコントロールが画面全体の既定の機能にどのように影響するかを理解します。 この詳細では、動作の数式と、コントロールがユーザー入力にどのように応答するかを決定するその他のプロパティの値を示します。 この画面の既定の機能の概要については、「[カレンダー画面の概要](calendar-screen-overview.md)」を参照してください。

ここでは、いくつかの重要なコントロールについて説明し、これらのコントロールのさまざまなプロパティ ( **Items**や**onselect**など) が設定される式または数式について説明します。

- [カレンダーのドロップダウン (dropdownCalendarSelection)](#calendar-drop-down)
- [予定表アイコン (iconCalendar)](#calendar-icon)
- [前の月のシェブロン (iconPrevMonth)](#previous-month-chevron)
- [翌月のシェブロン (iconNextMonth)](#next-month-chevron)
- [Calendar gallery (MonthDayGallery) (+ 子コントロール)](#calendar-gallery)
- [イベントギャラリー (CalendarEventsGallery)](#events-gallery)

## <a name="prerequisite"></a>前提条件

[PowerApps でアプリを作成](../data-platform-create-app-scratch.md)するときに、画面やその他のコントロールを追加および構成する方法について理解します。

## <a name="calendar-drop-down"></a>予定表のドロップダウン

![dropdownCalendarSelection コントロール](media/calendar-screen/calendar-dropdown.png)

- "**品目**<br>
    値: `Office365.CalendarGetTables().value`

    この値は、アプリユーザーの Outlook カレンダーを取得するコネクタ操作です。 この操作によって取得された[値](https://docs.microsoft.com/connectors/office365/#entitylistresponse[table])を確認できます。

- "**OnChange**<br>値: `Select(dropdownCalendarSelection)`

    ユーザーが一覧のオプションを選択すると、コントロールの**Onselect**プロパティ内の関数が実行されます。

- "**OnSelect**<br>
    数値**If**関数。次のコードブロックに表示されます。また、その後のコードブロックに表示されるいくつかの追加の関数もあります。

   数式のこの部分は、ユーザーがアプリを開いた後にドロップダウンリストでオプションを初めて選択したときにのみ実行されます。

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

    上記のコードでは、次の変数を定義しています。
    
  - **\_userDomain**:ユーザーの電子メールアドレスに反映される、アプリユーザーの会社のドメイン。
  - **\_ Dateselected**:今日の日付 (既定)。 カレンダーギャラリーにこの日付が強調表示され、イベントギャラリーには、その日付に対してスケジュールされているイベントが表示されます。
  - **\_firstDayOfMonth**:現在の月の最初の日。 @No__t-0 であるため、この**DateAdd**関数は常に月の最初の日を返します。
  - **\_ Firstdayinview**:カレンダーギャラリーで表示できる最初の日。 月が日曜日で始まる場合を除き、この値は月の最初の日と同じではありません。 前月の週全体が表示されないようにするには、 **\_ Firstdayinview**の値が `_firstDayOfMonth - Weekday(_firstDayOfMonth) + 1` です。
  - **\_lastDayOfMonth**:現在の月の最終日 (翌月の最初の日から1日を引いた日付)。

   **If**関数の後の関数は、ユーザーが初めてアプリを開いたときだけでなく、[カレンダー] ドロップダウンリストでオプションを選択したときに実行されます。

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

    上記のコードでは、これらの変数と1つのコレクションを定義しています。

    - **\_ Calendarvisible**:新しい選択項目が読み込まれるときにカレンダーが表示されないようにするには、 **false**に設定します。
    - **\_showLoading**:新しい選択の読み込み中に読み込みインジケーターが表示されるようにするには、 **true**に設定します。
    - **\_myCalendar**:正しい暦からのイベントが取得されるように、**カレンダーのドロップダウン**コントロールの現在の値に設定します。
    - **\_minDate**: **@No__t-1firstDayInView**と同じ値に設定します。 この変数は、Outlook から既に取得され、アプリにキャッシュされているイベントを判別します。
    - **\_maxDate**:カレンダーの最後の表示可能日に設定します。 数式は @no__t 0 です。 カレンダーには最大41日が表示されるため、 **@no__t 1maxDate**変数には常に最後の表示可能な日が反映され、Outlook から既に取得され、アプリにキャッシュされているイベントが決まります。
    - **MyCalendarEvents**:選択したカレンダーからのユーザーのイベントのコレクションを **\_minDate**から **\_maxDate**に設定します。
    - **\_showLoading**:を**false**に設定します。 **\_calendarVisible は、** 他のすべてのものが読み込まれた後に**true**に設定されます。

## <a name="calendar-icon"></a>予定表アイコン

![iconCalendar コントロール](media/calendar-screen/calendar-today-icon.png)

- "**OnSelect**<br>
    数値カレンダーギャラリーを今日の日付にリセットする4つの**セット**関数:

    ```powerapps-dot
    Set( _dateSelected, Today() );
    Set( _firstDayOfMonth, DateAdd( Today(), 1 - Day( Today() ), Days) );
    Set( _firstDayInView, DateAdd(_firstDayOfMonth, -(Weekday( _firstDayOfMonth ) - 2 + 1), Days));
    Set( _lastDayOfMonth, DateAdd( DateAdd( _firstDayOfMonth, 1, Months ), -1, Days ) )
    ```

    上記のコードでは、適切なカレンダービューを表示するために必要なすべての日付変数がリセットされます。

    - **\_ Dateselected**が現在の状態にリセットされます。
    - **\_firstDayOfMonth**は、今日の月の最初の日にリセットされます。
    - **\_firstDayInView**は、今日の月を選択したときに表示される最初の日にリセットされます。
    - **\_lastDayOfMonth**は、今日の月の最終日にリセットされます。

    このトピックの「[**カレンダー」ドロップダウン**](#calendar-drop-down)セクションでは、これらの変数についてさらに詳しく説明します。

## <a name="previous-month-chevron"></a>前の月のシェブロン

![iconPrevMonth コントロール](media/calendar-screen/calendar-back.png)

- "**OnSelect**<br>数値カレンダーギャラリーで前月を示す4つの**セット**関数と**If**関数。

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
    > 1firstDayOfMonth、 **\_firstDayInView**、および **@no__t** **@no__t**の定義は、このトピックの「 [Calendar (予定表](#calendar-drop-down))」セクションに記載されているものとほぼ同じです。

    前のコードの最初の3行は、ユーザーが前の月のシェブロンを選択するたびに実行されます。 このコードは、適切なカレンダービューを表示するために必要な変数を設定します。 残りのコードは、ユーザーが選択した予定表の今月を選択していない場合にのみ実行されます。

    この場合 **@no__t、1minDate**は前月に表示される最初の日になります。 ユーザーがアイコン @no__t を選択する前に、 **1minDate**には当月の23日の最小値が設定されています。 (3 月1日が土曜日になると、3月の **\_firstDayInView**が2月23日になります)。つまり、ユーザーがこの月を選択していない場合、 **\_minDate**は新しい **@no__t 3firstDayOfMonth**より大きくなり、 **if**関数は**true**を返します。 コードが実行され、コレクションと変数が更新されます。

    - **MyCalendarEvents**は、 [GetEventsCalendarViewV2](https://docs.microsoft.com/connectors/office365/#get-calendar-view-of-events--v2-)操作を使用して、選択したカレンダーからイベントを取得します。 日付範囲は **\_ Firstdayinview** date と **\_minDate** -1 の間です。 **MyCalendarEvents**には既に 2minDate date **@no__t**のイベントが含まれているため、この新しい日付範囲の最大値については、その日付から1が減算されます。

    - **1minDate**は現在の **\_firstDayInView**に設定されています。これは、イベントが取得された最初の日付であるためです。 @no__t 前の月のシェブロンを選択してこの日付に戻った場合、 **if**関数は**false**を返します。このビューのイベントは**MyCalendarEvents**に既にキャッシュされているため、このコードは実行されません。

## <a name="next-month-chevron"></a>翌月のシェブロン

![iconNextMonth コントロール](media/calendar-screen/calendar-forward.png)

- "**OnSelect**<br>
    数値カレンダーギャラリーで次の月を表示する4つの**セット**関数と**If**関数。

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
    > 1firstDayOfMonth、 **\_firstDayInView**、および **@no__t** **@no__t**の定義は、このトピックの「 [Calendar (予定表](#calendar-drop-down))」セクションに記載されているものとほぼ同じです。

    前のコードの最初の3行は、ユーザーが次の月のシェブロンを選択したときに実行され、適切なカレンダービューを表示するために必要な変数を設定します。 残りのコードは、ユーザーが選択した予定表の今月を選択していない場合にのみ実行されます。

    その場合 @no__t、 **1maxDate**は前月に表示される最後の日になります。 ユーザーが次の月のシェブロンを選択する前に、 **@no__t 1maxDate**は翌月の13番目の値を使用できます。 (2 月1日がうるう年以外の日曜日になると、 **@no__t 1maxDate**は3月13日になります。これは、 **\_firstDayInView** + 40 日) です。つまり、ユーザーがこの月を選択していない場合、 **\_maxDate**は新しい **@no__t 3lastDayOfMonth**より大きくなり、 **if**関数は**true**を返します。 コードが実行され、コレクションと変数が更新されます。

    - **MyCalendarEvents**は、 [GetEventsCalendarViewV2](https://docs.microsoft.com/connectors/office365/#get-calendar-view-of-events--v2-)操作を使用して、選択したカレンダーからイベントを取得します。 日付範囲は、 **\_maxDate** + 1 日、 **\_firstDayInView** + 40 日までです。 MyCalendarEvents には既に **-2minDate** date の @no__t イベントが含まれているので、この新しい日付範囲の最小値に対して1が追加されます。 **\_firstDayInView** + 40 は、 **@no__t 3maxDate**の数式であるため、範囲の2番目の日付は新しい **\_maxDate**にすぎません。

    - **@no__t-** **3firstDayInView** + 40 days @no__t に設定されています。これは、イベントが取得された最後の日であるためです。 ユーザーが次の月のシェブロンを選択してこの日付に戻ると、 **if**関数は**false**を返します。このビューのイベントは**MyCalendarEvents**に既にキャッシュされているため、このコードは実行されません。

## <a name="calendar-gallery"></a>カレンダーギャラリー

![MonthDayGallery コントロール](media/calendar-screen/calendar-month-gall.png)

- "**品目**<br>
    値: `[0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,
    20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41]`
  
  カレンダーギャラリーの項目には 0 ~ 41 のセットが使用されます。これは、最悪のシナリオでは、カレンダービューには42日を表示する必要があるためです。 このエラーは、月の最初のが土曜日に発生し、その月の最後のが日曜日に発生した場合に発生します。 この場合、カレンダーには、月の最初の行を含む行の前の月から6日が表示されます。月の最後の行には、次の月の6日が表示されます。 これは42の一意の値で、選択した月の30個です。

- "**WrapCount**<br>
    値: `7`

  この値には7日の週が反映されます。

### <a name="title-control-in-the-calendar-gallery"></a>カレンダーギャラリーのタイトルコントロール

![MonthDayGallery Title コントロール](media/calendar-screen/calendar-month-text.png)

- " **[Text (テキスト)]**<br>
    値: `Day( DateAdd( _firstDayInView, ThisItem.Value, Days ) )`

    **@No__t-1firstDayInView**は、( **@no__t 3firstDayOfMonth** -その曜日の値) + 1 として定義されていることを思い出してください。 これにより、 **\_ Firstdayinview**は常に日曜日で、 **@no__t 3firstDayOfMonth**は常に**MonthDayGallery**の最初の行になります。 これらの2つのファクトのため、 **\_firstDayInView**は常に**MonthDayGallery**の最初のセルにあります。 ここでは、 **MonthDayGallery** item プロパティのセルの番号を**指定します。** そのため、開始点として **\_firstDayInView**を実行すると、各セルに **\_firstDayInView**と、それぞれのセル値の増分が表示されます。

- "**入力**<br>
    数値1つの**If**関数:

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

  **Text**プロパティの説明で説明したように、`DateAdd(_firstDayInView, ThisItem.Value)` は、表示されているセルの日を表します。 これを考慮すると、上記のコードでは次の比較が実行されます。
  1. セルの値が今日の日付で、このセルが **\_ Dateselected**と等しい場合は、fill 値を指定しないでください。
  1. セルの値が今日の日付で、 **\_ Dateselected**と等価でない場合は、 **colorfade**の塗りつぶしを指定します。
  1. 最後の比較は明確ではありません。 これは、セル内の実際のテキスト値とセルアイテムの値 (表示されている数値と項目番号) の比較です。<br>

      これについて理解を深めるには、2018年9月に開始され、土曜日から日曜日に終了します。 この場合、カレンダーには8月31日の26日が表示され、1 @no__t 行目は9月1日で、9月1日までは0になります。 次に、`Abs(Title.Text - ThisItem.Value) = 5` です。 カレンダーの最後の行から5月30日から6月1日までと表示されます。 その `Abs(Title.Text - ThisItem.Value)` は9月30日に5になりますが、10月の日付では35になります。<br>

      このパターンは次のとおりです。前の月の日を表示する場合、`Abs(Title.Text - ThisItem.Value)` は常に表示の最初の日の `Title.Text` の値と等しくなります。 翌月に表示される日については、`Abs(Title.Text - ThisItem.Value)` は常にその月の最初のセルの**MonthDayGallery** item 値 (この場合は10月1日) から1を引いた値と等しくなります。 また、最も重要な点として、現在選択されている月に表示される日数については、`Abs(Title.Text - ThisItem.Value)` も、その月の最初の項目の値から1を引いた値と等しくなります。前の例で示すように、5を超えることはありません。 数式を @no__t 0 として記述することは、完全に有効です。

      このステートメントでは、日付の値が現在選択されている月の範囲外であるかどうかを確認します。 設定されている場合は、**塗りつぶし**が部分的に不透明な灰色になります。

    > [!NOTE]
    > この最後の比較の有効性を確認するには、ギャラリーに**ラベル**コントロールを挿入し、その**Text**プロパティを次の値に設定します。<br>`Abs(Title.Text - ThisItem.Value)`。

- "**さ**<br>
    数値

    ```powerapps-dot
    !(
        DateAdd( _firstDayInView, ThisItem.Value, Days ) - 
            Weekday( DateAdd( _firstDayInView, ThisItem.Value,Days ) ) + 1 
        > _lastDayOfMonth
    )
    ```

    前のステートメントは、現在選択されている月の日付がない行にセルがあるかどうかをチェックします。 日付値から任意の日の曜日値を減算し、1を追加すると、その日が存在する行の最初の項目が常に返されることを思い出してください。 このステートメントでは、行の最初の日が、表示可能な月の最終日より後かどうかを確認します。 含まれている場合は、行全体に次の月の日付が含まれているため表示されません。

- "**OnSelect**<br>
    数値 **@No__t-2dateSelected**変数を、選択したセルの日付に設定する**Set**関数:

    ```powerapps-dot
    Set( _dateSelected, DateAdd( _firstDayInView, ThisItem.Value, Days ) )
    ```

### <a name="circle-control-in-the-calendar-gallery"></a>カレンダーギャラリーの円コントロール

![MonthDayGallery Circle コントロール](media/calendar-screen/calendar-month-event.png)

- "**さ**<br>
    数値選択した日付に対してイベントがスケジュールされているかどうか、および**サブ円**と**タイトル**のコントロールを表示するかどうかを決定する数式。

    ```powerapps-dot
    CountRows(
        Filter( MyCalendarEvents, 
            DateValue( Text( Start ) ) = DateAdd( _firstDayInView, ThisItem.Value, Days )
        )
    ) > 0 && !Subcircle.Visible && Title.Visible
    ```

    任意のイベントの **[開始]** フィールドがそのセルの日付と等しい場合、**タイトル**コントロールが表示されていて、 **subcircle**コントロールが表示されていない場合は、**円**コントロールが表示されます。 つまり、この日に少なくとも1つのイベントが発生し、この日が選択されていない場合に、このコントロールが表示されます。 選択されている場合、その日のイベントは**CalendarEventsGallery**コントロールに表示されます。

### <a name="subcircle-control-in-the-calendar-gallery"></a>カレンダーギャラリーの subcircle コントロール

![MonthDayGallery Subcircle コントロール](media/calendar-screen/calendar-month-selected.png)

- "**さ**<br>
    数値

    ```powerapps-dot
    DateAdd( _firstDayInView, ThisItem.Value ) = _dateSelected && Title.Visible
    ```

  **@No__t-2dateSelected**がセルの日付と同じであり、**タイトル**コントロールが表示されている場合は、 **subcircle**コントロールが表示されます。 言い換えると、このコントロールは、セルが現在選択されている日付のときに表示されます。

## <a name="events-gallery"></a>イベントギャラリー

![CalendarEventsGallery コントロール](media/calendar-screen/calendar-events-gall.png)

- "**品目**<br>
    数値イベントギャラリーの並べ替えとフィルター処理を行う数式は次のとおりです。

    ```powerapps-dot
    SortByColumns(
        Filter( MyCalendarEvents,
            Text( Start, DateTimeFormat.ShortDate ) = Text( _dateSelected, DateTimeFormat.ShortDate )
        ),
        "Start"
    )
    ```

   MyCalendarEvents コレクションには、と @no__t **@no__t**間のすべてのイベントが含まれています。 選択した日付のみのイベントを表示するには、 **MyCalendarEvents**にフィルターを適用して、**選択さ**れた開始日と同じ開始日を持つイベントを表示します。 次に、項目が開始日順に並べ替えられ、順番に配置されます。

## <a name="next-steps"></a>次の手順

- [この画面の詳細情報](./calendar-screen-overview.md)
- [PowerApps での Office 365 Outlook コネクタについての詳細情報](../connections/connection-office365-outlook.md)
- [PowerApps での Office 365 Users コネクタについての詳細情報](../connections/connection-office365-users.md)

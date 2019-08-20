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
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61539105"
---
# <a name="reference-information-about-the-calendar-screen-template-for-canvas-apps"></a>キャンバス アプリの予定表画面テンプレートに関する参照情報

PowerApps キャンバス アプリの場合は、カレンダー画面テンプレートの重要な各コントロールが画面全体の既定機能にどのように貢献するかを説明します。 この詳細情報は、動作の数式とその他のコントロールがユーザー入力に応答する方法を決定するプロパティの値を表示します。 この画面の既定の機能の概要については、[カレンダー画面概要](calendar-screen-overview.md) をご覧ください。

このトピックでは、いくつかの重要なコントロールに焦点を当て、これらコントロールのさまざまなプロパティ(**Item**と**OnSelect** など)が設定される式または数式について説明します。

- [予定表のドロップダウン (dropdownCalendarSelection)](#calendar-drop-down)
- [予定表アイコン (iconCalendar)](#calendar-icon)
- [前の月のシェブロン (iconPrevMonth)](#previous-month-chevron)
- [翌月のシェブロン (iconNextMonth)](#next-month-chevron)
- [予定表のギャラリー (MonthDayGallery) (+ 子コントロール)](#calendar-gallery)
- [イベントのギャラリー (CalendarEventsGallery)](#events-gallery)

## <a name="prerequisite"></a>前提条件

[PowerApps でアプリを作成する](../data-platform-create-app-scratch.md) ときの画面やその他コントロールを追加及び構成する方法を理解している。

## <a name="calendar-drop-down"></a>ドロップダウンの予定表

![dropdownCalendarSelection コントロール](media/calendar-screen/calendar-dropdown.png)

- プロパティ: **Items**<br>
    値: `Office365.CalendarGetTables().value`

    この値は、アプリ ユーザーの Outlook の予定表を取得するコネクタの操作です。 この操作で取得する[値](https://docs.microsoft.com/connectors/office365/#entitylistresponse[table]) を確認できます。

- プロパティ:**OnChange**<br>値: `Select(dropdownCalendarSelection)`

    ユーザーが、コントロールの関数の一覧でオプションを選択すると**OnSelect**プロパティを実行します。

- プロパティ:**OnSelect**<br>
    値: 次のコードブロックに表示される **If** 関数、およびその後のコード ブロックに表示されるいくつかの追加の関数。

   数式の部分は、ユーザーがアプリを開いた後にドロップダウン リストでオプションを初めて選択するときにのみ実行されます。

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
    
  - **\_userDomain**: ユーザーの電子メール アドレスに反映されるアプリユーザーの会社ドメイン。
  - **\_dateSelected**: 今日の日付 (既定)。 カレンダー ギャラリーが、この日付を強調表示し、イベント ギャラリーには、その日付にスケジュールされたイベントが表示されます。
  - **\_firstDayOfMonth**: 今月の最初の日。 `(Today + (1 - Today)) = Today - Today + 1 = 1`、この **DateAdd** 関数は、常に、1 か月の最初の日を返します。
  - **\_firstDayInView**: 予定表ギャラリーが表示する最初の日。 この値は、月が日曜日から始まらない限り、月の最初の日と同じではありません。前月の週全体を表示しないようにするには **\_firstDayInView** の値は`_firstDayOfMonth - Weekday(_firstDayOfMonth) + 1` にします。
  - **\_lastDayOfMonth**: 今月の最後の日。翌月の最初の日から１日引いた日です。

   **If** 関数の後の関数は、ユーザーがカレンダーのドロップダウンリストでオプションを選択するたびに実行されます(ユーザーがアプリを最初に開いたときだけではありません)。

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

    - **\_calendarVisible** : **false** 設定時、新しい選択範囲の読み込み中に、カレンダーが表示されないようにします。
    -- **\_showLoading**: **true** 設定時、新しい選択範囲の読み込み中に、インジケーターが表示されるようになります。
    - **\_myCalendar**: 適切なカレンダーからイベントを取得されるように、**calendar drop-down** コントロールに現在の値を設定します。
    - **\_minDate**: **\_firstDayInView** と同じ値に設定します。 この変数は、Outlook から既に取得され、アプリでキャッシュされているイベントを決定します。
    - **\_maxDate**: カレンダーで表示可能な最後の日に設定します。 数式は`_firstDayInView + 40`にします。 カレンダーには、最大 41 日間が表示されるため、 **\_maxDate** 変数は常に表示可能な最後の日を反映し、Outlook から既に取得して、アプリにキャッシュしたイベントを決定します。
    - **MyCalendarEvents**: **\_minDate** から **\_maxDate** の範囲で、選択したカレンダーから、イベントのコレクションを設定します。
    - **\_showLoading**: **false** 設定時、**\_calendarVisible** は、他のすべてが読み込まれた後に、 **true** に設定されます。

## <a name="calendar-icon"></a>カレンダーのアイコン

![iconCalendar コントロール](media/calendar-screen/calendar-today-icon.png)

- プロパティ:**OnSelect**<br>
    値: カレンダーギャラリーを今日の日付にリセットする 4 つの **Set** 関数。	

    ```powerapps-dot
    Set( _dateSelected, Today() );
    Set( _firstDayOfMonth, DateAdd( Today(), 1 - Day( Today() ), Days) );
    Set( _firstDayInView, DateAdd(_firstDayOfMonth, -(Weekday( _firstDayOfMonth ) - 2 + 1), Days));
    Set( _lastDayOfMonth, DateAdd( DateAdd( _firstDayOfMonth, 1, Months ), -1, Days ) )
    ```

    上記のコードでは、適切なカレンダー ビューを表示するために必要なすべての日付変数をリセットします。

    - **\_dateSelected**今日にリセットされます。
    - **\_firstDayOfMonth** は今月の最初の日にリセットされます。
    - **\_firstDayInView** に現在の月を選択すると、表示可能な最初の日にリセットされます。
    - **\_lastDayOfMonth** は今月の最終日にリセットされます。

    この [**calendar drop-down**](#calendar-drop-down) トピックのセクションでは、これらの変数について詳しく説明しています。

## <a name="previous-month-chevron"></a>前の月のシェブロン

![iconPrevMonth コントロール](media/calendar-screen/calendar-back.png)

- プロパティ: **OnSelect** <br>値: 前月をカレンダー ギャラリーに表示する 4 つの **Set** 関数と **If** 関数。

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
    > **\_firstDayOfMonth** 、 **\_firstDayInView** 、および **\_lastDayOfMonth** の定義は、この [カレンダー ドロップダウン](#calendar-drop-down) トピックのセクションとほぼ同じです。

    上記のコードの最初の 3 つの行は、ユーザーは、前月のシェブロンを選択するたびに実行します。 コードでは、適切なカレンダー ビューを表示するために必要な変数を設定します。 残りのコードは、ユーザーが選択したカレンダーの月が前月を選択していない場合のみ実行されます。

    この場合は、 **\_minDate** は、前月を表示するときに表示される最初の日になります。 ユーザーが、アイコンを選択する前に **\_minDate** が 現在の月の 23 の最小有効値が選択されています。 (3 月 1 日が土曜日の場合、3 月の **\_firstDayInView** は、2 月 23 日です)。つまり、ユーザーがまだ、今月を選択していない場合 **\_minDate** は新しい **\_firstDayOfMonth** より大きく、**If** 関数は **true** を返します。コードを実行し、コレクションと変数を更新します。

    - **MyCalendarEvents** は、 [Office365.GetEventsCalendarViewV2](https://docs.microsoft.com/connectors/office365/#get-calendar-view-of-events--v2-) 操作を使用して、選択したカレンダーからイベントを取得します。日付範囲は、 **\_firstDayInView** 日付と **\_minDate** - 1 の間です。  **MyCalendarEvents** には既に **\_minDate** 日付のイベントが含まれているため、この新しい日付の範囲の最大値のについては、その日付から 1 が減算されます。

    - **\_minDate** は、イベントが取得された最初の日付けで、現在の **\_firstDayInView** に設定されます。ユーザーが、前月のシェブロンを選択して、この日付に戻った場合、**If** 関数は、 **false** を返します。このビューのイベントが既に **MyCalendarEvents** にキャッシュされているため、コードは実行されません。

## <a name="next-month-chevron"></a>翌月のシェブロン

![iconNextMonth コントロール](media/calendar-screen/calendar-forward.png)

- プロパティ:**OnSelect**<br>
    値: カレンダーギャラリーで翌月を表示する 4 つの **Set** 関数と **If** 関数。
    
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
    > **\_firstDayOfMonth** 、 **\_firstDayInView** 、および **\_lastDayOfMonth** 定義は、このトピックの[カレンダー ドロップダウン](#calendar-drop-down) セクションの定義とほぼ同じです。


    上記のコードの最初の 3 行では、ユーザーが翌月のシェブロンを選択したときに実行され、適切なカレンダー ビューを表示するために必要な変数を設定します。 残りのコードは、ユーザーが選択したカレンダーの月の前月を選択していない場合のみ実行されます。


    その場合は、 **\_maxDate** は、前月を表示するときに表示される最後の日になります。 ユーザーが、翌月のシェブロンを選択する前は **\_maxDate** の最大値は翌月の 13 です。 (2 月 1 日がうるう年でない日曜日の場合、 **\_maxDate** は 3 月 13 日に、これは、 **\_firstDayInView** + 40 日間です)。つまり、ユーザーがまだ、今月を選択していない場合 **\_maxDate** は、新しい **\_lastDayOfMonth** より大きく、**If** 関数は、 **true** を返します。 コードを実行し、コレクションと変数を更新します。

    - **MyCalendarEvents** は、 [Office365.GetEventsCalendarViewV2](https://docs.microsoft.com/connectors/office365/#get-calendar-view-of-events--v2-) 操作を利用して、選択したカレンダーからイベントを取得します。日付範囲は **\_maxDate** + 1 日から **\_firstDayInView** + 40 日です。 **MyCalendarEvents** には、 **\_minDate** の日付のイベントが既に含まれているため、この新しい日付範囲の最小値に対して、1 がその日付に追加されます。 **\_firstDayInView** + 40 は、 **\_maxDate** の式なので、範囲の 2 つ目の日付は新しい **\_maxDate** になります。

    - **\_maxDate** は、 **\_firstDayInView** + 40 日に設定されます。これは、イベントが取得された最終日であるためです。ユーザーが、翌月のシェブロンを選択してこの日付に戻ると、**If** 関数は **false** を返します。このビューのイベントは既に **MyCalendarEvents** にキャッシュされているため、コードは実行されません。

## <a name="calendar-gallery"></a>予定表のギャラリー

![MonthDayGallery コントロール](media/calendar-screen/calendar-month-gall.png)

- プロパティ: **Items**<br>
    値: `[0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,
    20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41]`
  
  最悪のシナリオでは、カレンダー ビューが 42 の完全な日を表示する必要があるために、予定表のギャラリー内の項目の 0 ~ 41 のセットが使用されます。 これには、月の最初が土曜日で、月の最後が日曜日になる場合に起こります。 この場合は、カレンダーは、月の最初を含む行に前月から 6 日間、月の最後を含む行に翌月から 6 日間 を表示します。これは、42 の一意の値で、そのうち 30は、選択した月のものです。

- プロパティ:**WrapCount**<br>
    値: `7`

  この値は、7 日間の週を反映します。

### <a name="title-control-in-the-calendar-gallery"></a>カレンダー ギャラリー内のコントロールのタイトル

![MonthDayGallery タイトル コントロール](media/calendar-screen/calendar-month-text.png)


- プロパティ: **Text**<br>
    値: `Day( DateAdd( _firstDayInView, ThisItem.Value, Days ) )`

    **\_firstDayInView** は、( **\_firstDayOfMonth** -曜日の値) + 1 として定義されています。 これにより **\_firstDayInView** は常に日曜日であり、 **\_firstDayOfMonth** は常に **MonthDayGallery** の最初の行にあることがわかります。 これら 2 つの事実により **\_firstDayInView** は、常に  **MonthDayGallery** の最初のセルになります。 **ThisItem.Value** は、 **MonthDayGallery** アイテム プロパティ内のそのセルの番号です。 そのため、 **\_firstDayInView** を開始点として、各セルには **\_firstDayInView** 増分の各セルの値が表示されます。


- プロパティ: **Fill**<br>	
    値: 1 つの **If** 関数。

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

  **Text** プロパティで説明したように、`DateAdd(_firstDayInView, ThisItem.Value)` は表示セルの日を表します。 これを考慮して、上記のコードは、これらの比較を実行します。
  1. セルの値が今日の日付であり、このセルが **\_dateSelected** と同等の場合、fill 値を指定しないでください。
  1. セルの値が今日の日付であり、このセルが **\_dateSelected** と同等で無い場合、**ColorFade** 塗りつぶしを指定します。
  1. 最後の比較はそれほど明確ではありません。セルの実際のテキスト値とセルの項目の値 (表示されている数字と項目番号)の比較です。<br>

      これをより理解するために、 2018 年 9 月、土曜日で始まり日曜日に終わる月を考えてみます。この場合、予定表の最初の行には 8 月 26 日から 31 日まで、 9 月 1 日が表示され、 `Abs(Title.Text - ThisItem.Value) = 26` が表示されます。その後、 `Abs(Title.Text - ThisItem.Value) = 5`となり、最後の行まで 5 のままで、 9 月 30 日と 10 月 1 日 から 6 日まで表示されます。`Abs(Title.Text - ThisItem.Value)` は、 9 月 30 日では 5 のままですが、 10 月の日付では 35 になります。<br>

      これは、パターンです。前月から表示された日については、 `Abs(Title.Text - ThisItem.Value)` は常に表示された最初の日の `Title.Text` 値と等しくなります。 翌月に表示される日については、 `Abs(Title.Text - ThisItem.Value)` は常にその月の最初のセル(この例では、 10 月 1 日)から 1 を引いた **MonthDayGallery** 項目に等しくなります。そして、最も重要なことは、現在選択されている月に表示される日については、 `Abs(Title.Text - ThisItem.Value)` は常にその月の最初の項目から 1 を引いた値に等しく、前の例が示すように 5 を超えることはありません。したがって、数式を `Abs(Title.Text - ThisItem.Value) > 5` として記述することは完全に有効です。

      このステートメントでは、日付の値は、現在選択されている月の外部にあるかどうかを確認します。 その場合は、**Fill** 部分は不透明な灰色です。

    > [!NOTE]
    > **Label** コントロールをギャラリーに挿入し、その **テキスト** プロパティをこの値に設定することにより、この最後の比較の有効性を確認できます。<br>`Abs(Title.Text - ThisItem.Value)`.
    
	- プロパティ: **Visible**<br>
    値:

    ```powerapps-dot
    !(
        DateAdd( _firstDayInView, ThisItem.Value, Days ) - 
            Weekday( DateAdd( _firstDayInView, ThisItem.Value,Days ) ) + 1 
        > _lastDayOfMonth
    )
    ```

    前のステートメントは、現在選択されている月の日付が発生しない行に、セルがあるかどうかを確認します。 日付の値から任意の日の平日の値を減算し、 1 を加算すると、その日が属する行の最初の項目が常に返されることを思い出してください。このため、このステートメントは、行の最初の日が表示可能な月の最終日の後かどうかを確認します。 その場合、行全体翌月の日が含まれているために表示されません。

- プロパティ:**OnSelect**<br>
    値: **\_dateSelected** 変数を選択したセルの日付に設定する **Set** 関数。
    
    ```powerapps-dot
    Set( _dateSelected, DateAdd( _firstDayInView, ThisItem.Value, Days ) )
    ```

### <a name="circle-control-in-the-calendar-gallery"></a>カレンダー ギャラリー内のコントロールの円

![MonthDayGallery 円コントロール](media/calendar-screen/calendar-month-event.png)

- プロパティ: **Visible**<br>
    値: 選択した日付にイベントをスケジュールするかどうか、および **Subcircle** と **Title** コントロールを表示するかどうかを決定する式

    ```powerapps-dot
    CountRows(
        Filter( MyCalendarEvents, 
            DateValue( Text( Start ) ) = DateAdd( _firstDayInView, ThisItem.Value, Days )
        )
    ) > 0 && !Subcircle.Visible && Title.Visible
    ```

    **Circle** コントロールは、 **Start** フィールドがそのセルの日付に等しい場合、 **Title** コントロールが表示されている場合、 **Subcircle** コントロールは表示されていない場合に表示されます。 つまり、このコントロールは、この日に少なくとも 1 つのイベントが発生し、この日が選択されていないときに表示されます。選択されている場合、その日のイベントが **CalendarEventsGallery** コントロールに表示されます。

### <a name="subcircle-control-in-the-calendar-gallery"></a>予定表のギャラリーで subcircle コントロール

![MonthDayGallery Subcircle コントロール](media/calendar-screen/calendar-month-selected.png)

- プロパティ: **Visible**<br>
    値:

    ```powerapps-dot
    DateAdd( _firstDayInView, ThisItem.Value ) = _dateSelected && Title.Visible
    ```

  **\_dateSelected** がセルの日付と同等の場合、 **Subcircle** コントロールが表示され、 **Title** コントロールが表示されます。 つまり、セルが現在選択されている日付のときにこのコントロールが表示されます。

## <a name="events-gallery"></a>イベントのギャラリー

![CalendarEventsGallery コントロール](media/calendar-screen/calendar-events-gall.png)

- プロパティ: **Items**<br>
    値: イベント ギャラリーを並べ替えてフィルターする式。
    
    ```powerapps-dot
    SortByColumns(
        Filter( MyCalendarEvents,
            Text( Start, DateTimeFormat.ShortDate ) = Text( _dateSelected, DateTimeFormat.ShortDate )
        ),
        "Start"
    )
    ```

   **MyCalendarEvents** コレクションには、 **\_minDate** から **\_maxDate** までのすべてのイベントが含まれます。選択された日付のみのイベントを表示するために **MyCalendarEvents** にフィルターが適用され、 **\_dateSelected** と同等の開始日を持つイベントが表示されます。項目は開始日でソートされ、順番に並べられます。

## <a name="next-steps"></a>次の手順

- [この画面を詳細します。](./calendar-screen-overview.md)
- [PowerApps での Office 365 Outlook コネクタの詳細します。](../connections/connection-office365-outlook.md)
- [PowerApps での Office 365 Users コネクタの詳細します。](../connections/connection-office365-users.md)

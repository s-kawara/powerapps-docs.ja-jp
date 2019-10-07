---
title: キャンバスアプリのミーティング画面テンプレートのリファレンス |Microsoft Docs
description: PowerApps でのキャンバスアプリのミーティング画面テンプレートの動作の詳細について説明します。
author: emcoope-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 01/03/2019
ms.author: emcoope
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: c62c3de56534201a81e9f4d453796ebd9b3a0366
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "71989568"
---
# <a name="reference-information-about-the-meeting-screen-template-for-canvas-apps"></a>キャンバスアプリのミーティング画面テンプレートに関するリファレンス情報

PowerApps のキャンバスアプリの場合、ミーティング画面テンプレートの各重要なコントロールが画面全体の既定の機能にどのように影響するかを理解します。 この詳細では、動作の数式と、コントロールがユーザー入力にどのように応答するかを決定するその他のプロパティの値を示します。 この画面の既定の機能の概要については、[ミーティング画面の概要](meeting-screen-overview.md)に関するページを参照してください。

ここでは、いくつかの重要なコントロールについて説明し、これらのコントロールのさまざまなプロパティ ( **Items**や**onselect**など) が設定される式または数式について説明します。

* [[招待] タブ (LblInviteTab)](#invite-tab)
* [[スケジュール] タブ (LblScheduleTab)](#schedule-tab)
* [テキスト検索ボックス](#text-search-box)
* [[追加] アイコン (AddIcon)](#add-icon)
* [People 閲覧ギャラリー](#people-browse-gallery) (+ 子コントロール)
* [会議の people ギャラリー](#meeting-people-gallery) (+ 子コントロール)
* [会議の日付の選択 (会議の Dateselect)](#meeting-date-picker)
* [会議の期間のドロップダウン (MeetingDurationSelect)](#meeting-duration-drop-down)
* [会議時間の検索ギャラリー](#find-meeting-times-gallery) (+ 子コントロール)
* [ルーム参照ギャラリー](#room-browse-gallery) (+ 子コントロール)
* [バックシェブロン (RoomsBackNav)](#back-chevron) (テナントにルーム一覧がない場合、表示されない可能性があります)
* [送信アイコン](#send-icon)

## <a name="prerequisite"></a>前提条件

[PowerApps でアプリを作成](../data-platform-create-app-scratch.md)するときに、画面やその他のコントロールを追加および構成する方法について理解します。

## <a name="invite-tab"></a>[招待] タブ

   ![LblInviteTab コントロール](media/meeting-screen/meeting-invite-text.png)

* "**色**<br>
    値: `If( _showDetails, LblRecipientCount.Color, RectQuickActionBar.Fill )`

    **Showdetails**は、 **LblInviteTab**コントロールまたは**LblScheduleTab**コントロールが選択されているかどうかを判断するために使用される変数です。 **[詳細]** の値が**true**の場合は、 **LblScheduleTab**が選択されます。値が**false**の場合は、 **LblInviteTab**が選択されます。 つまり、 **Showdetails**の値が**true**の場合 (このタブが選択されて*い*ない場合)、タブの色は**LblRecipientCount**の色と一致します。 それ以外の場合は、 **RectQuickActionBar**の fill 値と一致します。

* "**OnSelect**<br> 
    値: `Set( _showDetails, false )`

    **詳細**変数 を**false**に設定します。これは 招待 タブの内容が表示され、**スケジュール** タブの内容が非表示になることを意味します。

## <a name="schedule-tab"></a>[スケジュール] タブ

   ![LblInviteTab コントロール](media/meeting-screen/meeting-schedule-text.png)

* "**色**<br>
    値: `If( !_showDetails, LblRecipientCount.Color, RectQuickActionBar.Fill )`

    **Showdetails**は、 **LblInviteTab**コントロールまたは**LblScheduleTab**コントロールが選択されているかどうかを判断するために使用される変数です。 True の場合、 **LblScheduleTab**が選択されます。false の場合、 **LblInviteTab**はです。 つまり、 **[詳細]** が true の場合 (このタブ*が*選択されている場合)、タブの色は**RectQuickActionBar**の fill 値と一致します。 それ以外の場合は、 **LblRecipientCount**の色の値と一致します。

* "**OnSelect**<br>
    値: `Set( _showDetails, true )`

    **詳細**変数 を **true** に設定します。これは、スケジュール タブの内容が表示され、招待 タブの内容が非表示になることを意味します。

## <a name="text-search-box"></a>テキスト検索ボックス

   ![Texttexttextコントロール](media/meeting-screen/meeting-search-box.png)

<!--Include description of text search box control?-->

画面内の他のいくつかのコントロールには、次のような依存関係があります。

* ユーザーがテキストの入力を開始すると、 **PeopleBrowseGallery**が表示されます。
* ユーザーが有効な電子メールアドレスを入力すると、 **Addicon**が表示されます。
* ユーザーが**PeopleBrowseGallery**内で人物を選択すると、検索内容がリセットされます。

## <a name="add-icon"></a>[追加] アイコン

   ![AddIcon コントロール](media/email-screen/email-add-icon.png)

ユーザーはこのコントロールを使用して、組織内に存在しないユーザーを、構成されている会議の出席者リストに追加できます。

* "**さ**<br>
    数値コントロールを表示するには、すべてが**true**に評価される必要がある3つの論理チェック。

    ```powerapps-dot
    !IsBlank( TextSearchBox.Text ) &&
        IsMatch( TextSearchBox.Text, Match.Email ) &&
        Not( Trim( TextSearchBox.Text ) in MyPeople.UserPrincipalName )
    ```

  行ごとに、このコードブロックは、次の場合にのみ**Addicon**コントロールが表示されることを示します。

  * **Texttexttextに**はテキストが含まれています。
  * **Texttextの**テキストは、有効な電子メールアドレスです。
  * **Textsearchbox**コレクション内のテキストは、既に存在しません。

* "**OnSelect**<br> 
    数値ユーザーを出席者リストに追加する**Collect**ステートメント、利用可能な会議時間を更新するための、およびいくつかの変数の切り替え。

    ```powerapps-dot
    Collect( MyPeople,
        { 
            DisplayName: TextSearchBox.Text, 
            UserPrincipalName: TextSearchBox.Text, 
            Mail: TextSearchBox.Text
        }
    );
    Concurrent(
        Reset( TextSearchBox ),
        Set( _showMeetingTimes, false ),
        UpdateContext( { _loadMeetingTimes: true } ),
        Set( _selectedMeetingTime, Blank() ),
        Set( _selectedRoom, Blank() ),
        Set( _roomListSelected, false ),
        ClearCollect( MeetingTimes, 
            AddColumns(
                'Office365'.FindMeetingTimes(
                    { 
                        RequiredAttendees: Concat(MyPeople, UserPrincipalName & ";")
                        MeetingDuration: MeetingDurationSelect.Selected.Minutes,
                        Start: Text( DateAdd( MeetingDateSelect.SelectedDate, 8, Hours ), UTC ),
                        End: Text( DateAdd( MeetingDateSelect.SelectedDate, 17, Hours ), UTC ),
                        MaxCandidates: 15, 
                        MinimumAttendeePercentage:1, 
                        IsOrganizerOptional: false, 
                        ActivityDomain: "Work"
                    }
                ).MeetingTimeSuggestions,
                "StartTime", MeetingTimeSlot.Start.DateTime, 
                "EndTime", MeetingTimeSlot.End.DateTime
            )
        )
    );
    UpdateContext( { _loadingMeetingTimes: false } );
    Set( _showMeetingTimes, true )
    ```

  このコントロールを選択すると、有効な電子メールアドレス ( **texttexttextに**有効な電子メールアドレスが入力されている場合にのみ表示されます) が**MyPeople**コレクションに追加され (このコレクションは出席者リストになります)、利用可能なミーティング時間が新しいもので更新されます。ユーザーエントリ。

  低レベルでは、このコードブロックは次のようになります。
  1. 電子メールアドレスを**MyPeople**コレクションに収集し、その電子メールアドレスを**DisplayName**、 **UserPrincipalName**、および**Mail**の各フィールドに収集します。
  1. **Texttexttextコントロール**の内容をリセットします。
  1. **Showtimes**変数を**false**に設定します。 この変数は、選択した参加者が満たすことのできる open 時間を表示する**Findmeetingtimesgallery**の表示を制御します。
  1. 値のコンテキスト変数を**true**に設定**します。** この変数は、読み込み状態を設定します。これにより、 **_LblTimesEmptyState**のような状態コントロールの読み込みの可視性が切り替わり、データが読み込まれていることをユーザーに示すことができます。
  1. 空にする**時間**を設定します **()** 。 **Selectedtimestime**は、 **Findmeetingtimesgallery**コントロールから選択されたレコードです。 (_s) ここでは、別の出席者を追加することによって、その出席者に対して**以前の定義**を使用できないということが原因である可能性があるため、ここでは何も表示されません。
  1. **オブジェクト om**を**Blank ()** に設定します。 **RoomBrowseGallery**から選択されたルーム**レコードを選択**します。 部屋の利用能力は、 **selectedroom time**の値によって決まります。 その値を空白にした場合、**その値は**無効になっているため、非空白にする必要があります。
  1. **_RoomListSelected**を**false**に設定します。 この行は、すべてのユーザーに適用されるとは限りません。 Office では、部屋を別の "部屋の一覧" でグループ化できます。 部屋の一覧がある場合は、この画面でそのアカウントを使用して、リスト内から部屋を選択する前に、まず部屋の一覧を選択できます。 **_RoomListSelected**の値は、(部屋の一覧のみを持つテナント内の) ユーザーが部屋の一覧または一連の部屋リスト内の部屋を表示するかどうかを決定します。 この値は**false**に設定されているため、ユーザーは新しい部屋リストを再選択できます。
  1. [Office365. findmeeting times](https://docs.microsoft.com/connectors/office365/#find-meeting-times)操作を使用して、出席者の利用可能なミーティング時間を特定し、収集します。 この操作は次のように合格します。
      * 指定された各ユーザーの**UserPrincipalName**を*Requiredatの dees*パラメーターに指定します。
      * **MeetingDurationSelect**。[] を選択して、[*会議継続時間*] パラメーターに分数を指定します。
      * 会議の Dateselect. SelectedDate + 8 時間を*開始*パラメーターに指定します。 既定では、カレンダーコントロールの完全な日付/時刻が、選択した日付の 12:00 AM であるため、8時間が追加されます。 通常の稼働時間内で利用能力を取得することがあります。 通常の作業開始時刻は午前8:00 時になります。
      * **[会議 dateselect]** 。*終了*パラメーターには、"SelectedDate + 17 時間" を指定します。 12:00 AM + 17 = 5:00 PM のため、17時間が加算されます。 通常の作業終了時刻は 5:00 PM です。
      * *Maxcandidates*のパラメーターに*15*を指定します。 つまり、この操作では、選択した日付に対して使用可能な上位15回だけが返されます。 これは、8時間の作業日に 16 30 分のチャンクのみが存在し、30分間の会議がこの画面で設定できる最小のものであるため、意味があります。
      * *MinimumAttendeePercentage*パラメーターに*1*を指定します。 基本的に、参加者が使用できない場合を除き、会議時間が取得されます。
      * *Isオーガナイザー Eroptional*パラメーターに**false**が指定されています。 アプリユーザーは、この会議のオプションの出席者ではありません。
      * *Activitydomain*パラメーターに "Work" を使用します。 つまり、取得された時間は、通常の作業時間内にのみ発生します。
  1. **Clearcollect**関数は、次の2つの列も追加します。"StartTime" と "EndTime"。 これにより、返されるデータが簡略化されます。 
  使用可能な開始時刻と終了時刻が含まれているフィールドは、 **[タイムスパン]** フィールドです。 このフィールドは、開始レコードと終了レコードを含むレコードで、それ自体にそれぞれの候補の**日時**と**タイムゾーン**の値が含まれています。 このようなレコードの入れ子を取得するのではなく、"StartTime" 列と "EndTime" 列を **[会議時間]** コレクションに追加すると、その**開始 > datetime**と**終了 > datetime**値がコレクションのサーフェイスに追加されます。
  1. これらの関数がすべて完了すると、 **Loadingtimestimes**変数が**false**に設定され、読み込み状態が削除され、 **[true]** に**設定さ**れます。

## <a name="people-browse-gallery"></a>People 閲覧ギャラリー

   ![PeopleBrowseGallery コントロール](media/meeting-screen/meeting-browse-gall.png)

* "**品目**<br>
    数値 
    ```powerapps-dot
    If( !IsBlank( Trim( TextSearchBox.Text ) ), 
        'Office365Users'.SearchUser( { searchTerm: Trim(TextSearchBox.Text), top: 15 } )
    )
    ```

このギャラリーの項目は、 [Office365 ユーザー](https://docs.microsoft.com/connectors/office365users/#searchuser)操作の検索結果によって設定されます。 操作は、検索語として `Trim(**TextSearchBox**)` のテキストを取得し、その検索に基づいて上位15件の結果を返します。
  
空白を検索するユーザーが有効でないため、 **Texttexttextは** **Trim**関数でラップされます。 ユーザーが検索する前に検索結果を取得すると、パフォーマンスが低下するため、`Office365Users.SearchUser` 操作は `If(!IsBlank(Trim(TextSearchBox.Text)) ... )` 関数でラップされます。

### <a name="people-browse-gallery-title"></a>People 閲覧ギャラリーのタイトル

   ![PeopleBrowseGallery Title コントロール](media/meeting-screen/meeting-browse-gall-title.png)

* " **[Text (テキスト)]**<br>
    値: `ThisItem.DisplayName`

    Office 365 プロファイルからのユーザーの表示名を表示します。

* "**OnSelect**<br>
    数値ユーザーを出席者リストに追加する**Collect**ステートメント、利用可能な会議時間を更新するための、およびいくつかの変数の切り替え。

    ```powerapps-dot
    Concurrent(
        Reset( TextSearchBox ),
        Set( _selectedUser, ThisItem ),
        If( Not( ThisItem.UserPrincipalName in MyPeople.UserPrincipalName ), 
            Collect( MyPeople, ThisItem ); 
            Concurrent(
                Set( _showMeetingTimes, false ),
                UpdateContext( { _loadMeetingTimes: true } ),
                Set( _selectedMeetingTime, Blank() ),
                Set( _selectedRoom, Blank() ),
                Set( _roomListSelected, false ),
                ClearCollect( MeetingTimes, 
                    AddColumns(
                        'Office365'.FindMeetingTimes(
                            {
                                RequiredAttendees: Concat( MyPeople, UserPrincipalName & ";" ),
                                MeetingDuration: MeetingDurationSelect.Selected.Minutes,
                                Start: Text( DateAdd( MeetingDateSelect.SelectedDate, 8, Hours ), UTC ),
                                End: Text( DateAdd( MeetingDateSelect.SelectedDate, 17, Hours ), UTC ),
                                MaxCandidates: 15, 
                                MinimumAttendeePercentage: 1, 
                                IsOrganizerOptional: false, 
                                ActivityDomain: "Work"
                            }
                        ).MeetingTimeSuggestions,
                        "StartTime", MeetingTimeSlot.Start.DateTime, 
                        "EndTime", MeetingTimeSlot.End.DateTime
                    )
                )
            );
            UpdateContext( { _loadingMeetingTimes: false } );
            Set( _showMeetingTimes, true )
        )
    )
    ```

    大まかに言えば、このコントロールを選択すると、ユーザーが**MyPeople**コレクション (アプリの出席者一覧のストレージ) に追加され、新しいユーザーの追加に基づいて、使用可能なミーティング時間が更新されます。

    このコントロールを選択することは、 **Addicon**コントロールを選択することとよく似ています。唯一の違いは、`Set(_selectedUser, ThisItem)` ステートメントと操作の実行順序です。 そのため、この説明は詳細なものではありません。 詳細については、「 [Addicon コントロール](#add-icon)」セクションを参照してください。

    このコントロールを選択すると、 **texttexttextが**リセットされます。 次に、選択範囲が**MyPeople**コレクション内にない場合、コントロールは次のようになります。
    1. 値を**true**に**設定し、** 値を false に設定**します。** また、値 の値を  **false** に設定し **、値** を空白**にして**、値の取得 を空に**します。** 新しい**MyPeople**コレクションに追加されたコレクション。 
    1. 値**loadtimes**の状態を**false**に設定し、 **show会議の時間**を**true**に設定します。 選択範囲が既に**MyPeople**コレクション内にある場合、 **texttexttextの**内容のみがリセットされます。

## <a name="meeting-people-gallery"></a>会議の people ギャラリー

   ![MeetingPeopleGallery コントロール](media/meeting-screen/meeting-people-gall.png)

* "**品目**<br>
    値: `MyPeople`

    **MyPeople**コレクションは、 **PeopleBrowseGallery Title**コントロールを選択することによって、に初期化または追加された人間のコレクションです。

* "**上下**<br>
    数値ギャラリーが最大の高さ350に拡大できるようにするためのロジック。

    ```powerapps-dot
    Min( 
        76 * RoundUp( CountRows( MeetingPeopleGallery.AllItems ) / 2, 0 ),
        350
    )
    ```

  
   このギャラリーの高さは、ギャラリー内の項目の数に合わせて調整されます。最大の高さは350です。 この数式は、 **MeetingPeopleGallery**の1行の高さとして76を受け取り、行の数で乗算します。 **WrapCount**プロパティは2に設定されているため、true 行の数は `RoundUp(CountRows(MeetingPeopleGallery.AllItems) / 2, 0)` になります。

* "**ShowScrollbar**<br>
    値: `MeetingPeopleGallery.Height >= 350`

    ギャラリーの最大の高さ (350) に達すると、スクロールバーが表示されます。

### <a name="meeting-people-gallery-title"></a>会議の people ギャラリーのタイトル

   ![MeetingPeopleGallery Title コントロール](media/meeting-screen/meeting-people-gall-title.png)

* "**OnSelect**<br>
    
    値: `Set(_selectedUser, ThisItem)`
    
    **MeetingPeopleGallery**で選択した項目に**selecteduser**変数を設定します。

### <a name="meeting-people-gallery-iconremove"></a>会議の people ギャラリーアイコンの削除

   ![MeetingPeopleGallery iconRemove コントロール](media/meeting-screen/meeting-people-gall-delete.png)

* "**OnSelect**<br>
    数値出席者リストからユーザーを削除するための**remove**ステートメント、利用可能な会議時間を更新するための**Collect**ステートメント、およびいくつかの変数が切り替わります。

    ```powerapps-dot
    Remove( MyPeople, LookUp( MyPeople, UserPrincipalName = ThisItem.UserPrincipalName ) );
    Concurrent(
        Reset( TextSearchBox ),
        Set( _showMeetingTimes, false ),
        UpdateContext( { _loadMeetingTimes: true } ),
        Set( _selectedMeetingTime, Blank() ),
        Set( _selectedRoom, Blank() ),
        Set( _roomListSelected, false ),
        ClearCollect( MeetingTimes, 
            AddColumns(
                'Office365'.FindMeetingTimes(
                    {
                        RequiredAttendees: Concat( MyPeople, UserPrincipalName & ";" ), 
                        MeetingDuration: MeetingDurationSelect.Selected.Minutes,
                        Start: Text( DateAdd( MeetingDateSelect.SelectedDate, 8, Hours ), UTC ), 
                        End: Text( DateAdd( MeetingDateSelect.SelectedDate, 17, Hours ), UTC ),
                        MaxCandidates: 15, 
                        MinimumAttendeePercentage: 1, 
                        IsOrganizerOptional: false, 
                        ActivityDomain: "Work"
                    }
                ).MeetingTimeSuggestions,
                "StartTime", MeetingTimeSlot.Start.DateTime, 
                "EndTime", MeetingTimeSlot.End.DateTime
            )
        )
    );
    UpdateContext( { _loadingMeetingTimes: false } );
    Set( _showMeetingTimes, true )
    ```

  大まかに言えば、このコントロールを選択すると、出席者リストからユーザーが削除され、このユーザーの削除に基づいて、利用可能なミーティング時間が更新されます。

  前のコードの最初の行の後に、このコントロールを選択することは、 **Addicon**コントロールを選択することとほぼ同じです。 そのため、この説明は深いものではありません。 詳細については、 [「Addicon コントロール」セクション](#add-icon)を参照してください。

  最初のコード行では、選択した項目が**MyPeople**コレクションから削除されます。 コードは次のようになります。
  1. **Texttexttextを**リセットし、 **MyPeople**コレクションから選択を削除します。 
  1. 値を**true**に**設定し、** 値を false に設定**します。** また、値 の値を  **false** に設定し **、値** を空白**にして**、値の取得 を空に**します。** 新しい**MyPeople**コレクションに追加されたコレクション。 
  1. 値**loadtimes**の状態を**false**に設定し、 **show会議の時間**を**true**に設定します。

## <a name="meeting-date-picker"></a>会議の日付の選択

   ![会議の日付の選択コントロール](media/meeting-screen/meeting-datepicker.png)

* "**DisplayMode**<br>
    値: `If( IsEmpty(MyPeople), DisplayMode.Disabled, DisplayMode.Edit )`

    少なくとも1人の出席者が**MyPeople**コレクションに追加されるまで、会議の日付を選択することはできません。

* "**OnChange**<br>
    値: `Select( MeetingDateSelect )`

    選択した日付を変更すると、このコントロールの**Onselect**プロパティのコードがトリガーされ、実行されます。

* "**OnSelect**<br>
    数値利用可能なミーティング時間を更新するための**Collect**ステートメントと、いくつかの変数の切り替え。
  
    ```powerapps-dot
    Concurrent(
        Reset( TextSearchBox ),
        Set( _showMeetingTimes, false ),
        UpdateContext( { _loadingMeetingTimes: true } ),
        Set( _selectedMeetingTime, Blank() ),
        Set( _selectedRoom, Blank() ),
        Set( _roomListSelected, false ),
        ClearCollect( MeetingTimes, 
            AddColumns(
                'Office365'.FindMeetingTimes(
                    {
                        RequiredAttendees: Concat( MyPeople, UserPrincipalName & ";" ), 
                        MeetingDuration: MeetingDurationSelect.Selected.Minutes,
                        Start: Text( DateAdd( MeetingDateSelect.SelectedDate, 8, Hours ), UTC ), 
                        End: Text( DateAdd( MeetingDateSelect.SelectedDate, 17, Hours ), UTC ),
                        MaxCandidates: 15, 
                        MinimumAttendeePercentage: 1, 
                        IsOrganizerOptional: false, 
                        ActivityDomain: "Work"
                    }
                ).MeetingTimeSuggestions,
                "StartTime", MeetingTimeSlot.Start.DateTime, 
                "EndTime", MeetingTimeSlot.End.DateTime
            )
        )
    );
    UpdateContext( { _loadingMeetingTimes: false } );
    Set( _showMeetingTimes, true )
    ```

  高レベルでは、このコントロールを選択すると、利用可能なミーティング時間が更新されます。 ユーザーが日付を変更した場合は、使用可能なミーティング時間を更新して、その日の出席者の利用能力を反映する必要があります。

  最初の**Collect**ステートメントを除き、これは**Addicon**コントロールの**onselect**機能と同じです。 そのため、この説明は深いものではありません。 詳細については、「 [Addicon コントロール](#add-icon)」セクションを参照してください。

  このコントロールを選択すると、 **texttexttextが**リセットされます。 次のようになります。 
  1. 値を**true**に**設定し、** 値を false に設定**します。** また、値 の値を  **false** に設定し **、値** を空白**にして**、値の取得 を空に**します。** 新しい日付の選択を含むコレクション。 
  1. 値**loadtimes**の状態を**false**に設定し、 **show会議の時間**を**true**に設定します。

## <a name="meeting-duration-drop-down"></a>会議の期間のドロップダウン

   ![会議の日付の選択コントロール](media/meeting-screen/meeting-timepicker.png)

* "**DisplayMode**<br>
    値: `If( IsEmpty(MyPeople), DisplayMode.Disabled, DisplayMode.Edit )`

    少なくとも1人の出席者が**MyPeople**コレクションに追加されるまで、会議の期間を選択することはできません。

* "**OnChange**<br>
    値: `Select(MeetingDateSelect1)`

    選択された期間を変更すると、実行する **[会議**の選択] コントロールの**onselect**プロパティのコードがトリガーされます。

## <a name="find-meeting-times-gallery"></a>会議時間の検索ギャラリー

   ![FindMeetingTimesGallery コントロール](media/meeting-screen/meeting-time-gall.png)

* "**品目**<br>
    値: `MeetingTimes`

    [Office365. findmeeting times](https://docs.microsoft.com/connectors/office365/#find-meeting-times)操作から取得される可能性のあるミーティング時間のコレクション。

* "**さ**<br>
    値: `_showMeetingTimes && _showDetails && !IsEmpty( MyPeople )`

    ギャラリーが表示されるのは、ユーザーが**LblScheduleTab**コントロールを選択し、少なくとも1人の出席者が会議に追加されている場合に、 **[showmeeting 時間]** が**true**に設定されている場合のみです。

### <a name="find-meeting-times-gallery-title"></a>会議時間の検索ギャラリーのタイトル

   ![FindMeetingTimesGallery タイトルコントロール](media/meeting-screen/meeting-time-gall-title.png)

* " **[Text (テキスト)]**<br>
    数値ユーザーのローカル時刻に表示される開始時刻の変換。

    ```powerapps-dot
    Text(
        DateAdd(
            DateTimeValue( ThisItem.StartTime ),
            - TimeZoneOffset(), 
            Minutes
        ),
        DateTimeFormat.ShortTime
    )
    ```

  取得される**StartTime**の値は UTC 形式です。 [UTC から現地時刻に変換](../functions/function-dateadd-datediff.md#converting-from-utc)するには、 **DateAdd**関数が適用されます。
  [Text 関数](../functions/function-text.md#datetime)は、最初の引数として日付/時刻を受け取り、2番目の引数に基づいて書式設定します。 この項目をローカル時刻に変換し、 **StartTime**を**DateTimeFormat**として表示します。

* "**OnSelect**<br>
    数値会議室とその提案された利用能力を収集するためのいくつかの**Collect**ステートメントと、いくつかの変数の切り替え。

    ```powerapps-dot
    Set( _selectedMeetingTime, ThisItem );
    UpdateContext( { _loadingRooms: true } );
    If( IsEmpty( RoomsLists ),
        ClearCollect( RoomsLists, 'Office365'.GetRoomLists().value) );
    If( CountRows( RoomsLists ) <= 1,
        Set( _noRoomLists, true );
        ClearCollect( AllRooms, 'Office365'.GetRooms().value );
        Set( _allRoomsConcat, Concat( FirstN( AllRooms, 20 ), Address & ";" ) );
        ClearCollect( RoomTimeSuggestions, 
            'Office365'.FindMeetingTimes(
                {
                    RequiredAttendees: _allRoomsConcat, 
                    MeetingDuration: MeetingDurationSelect.Selected.Minutes,
                    Start: _selectedMeetingTime.StartTime & "Z", 
                    End: _selectedMeetingTime.EndTime & "Z", 
                    MinimumAttendeePercentage: "1",
                    IsOrganizerOptional: "false", 
                    ActivityDomain: "Unrestricted"
                }
            ).MeetingTimeSuggestions
        );
        ClearCollect( AvailableRooms, 
            AddColumns(
                AddColumns(
                    Filter( 
                        First( RoomTimeSuggestions ).AttendeeAvailability,
                        Availability="Free"
                    ), 
                    "Address", Attendee.EmailAddress.Address
                ), 
                "Name", LookUp( AllRooms, Address = Attendee.EmailAddress.Address ).Name 
            )
        );
        ClearCollect( AvailableRoomsOptimal, 
            DropColumns(
                DropColumns( AvailableRooms, "Availability" ), 
                "Attendee" 
            )
        ),
        Set( _roomListSelected, false) 
    );
    UpdateContext( {_loadingRooms: false} )
    ```

  大まかに言えば、このコードブロックでは、会議の選択した日付/時刻に基づいて、部屋の一覧がないユーザーに対して利用可能なルームが収集されます。 それ以外の場合は、単にルームの一覧を取得します。

  低レベルでは、このコードブロックは次のようになります。
  1. 選択された項目に対して時間を設定します **(_a)** これは、その期間に利用可能なルームを見つけるために使用されます。
  1. 読み込み状態の変数を**true**に設定し、読み込み状態を**オンにし**ます。
  1. **RoomsLists**コレクションが空の場合は、ユーザーの tenant's ルームリストを取得し、 **RoomsLists**コレクションに格納します。
  1. ユーザーが部屋リストまたは1つの部屋リストを持っていない場合:
      1. **Noroomlists**変数は**true**に設定され、この変数は**RoomBrowseGallery**コントロールに表示される項目を決定するために使用されます。
      1. @No__t-0 操作は、テナント内の最初の100ルームを取得するために使用されます。 これらは**Allrooms**コレクションに格納されます。
      1. **_AllRoomsConcat**変数は、 **allrooms**コレクション内のルームの最初の20個の電子メールアドレスをセミコロンで区切った文字列に設定されます。 これは、 [Office365 の Findtimes](https://docs.microsoft.com/connectors/office365/#find-meeting-times)は、1回の操作で20人の person オブジェクトの使用可能な時間を検索する場合に限られます。
      1. **RoomTimeSuggestions**コレクションでは、 [Office365](https://docs.microsoft.com/connectors/office365/#find-meeting-times)を使用して、 **allrooms**コレクション内の最初の20個のルームの可用性を取得します。これは、[ **selected] の時間**変数の値に基づきます。 **DateTime**値を適切に書式設定するには、`& "Z"` が使用されていることに注意してください。
      1. **AvailableRooms** collection が作成されます。 これは、次の2つの列が追加された参加者の利用能力の**RoomTimeSuggestions**コレクションです。"Address" と "Name"。 "Address" は、部屋の電子メールアドレスです。 "Name" はルームの名前です。
      1. 次に、 **AvailableRoomsOptimal**コレクションが作成されます。 これは、"Availability" 列と "出席者" 列が削除された**AvailableRooms**コレクションにすぎません。 これは、 **AvailableRoomsOptimal**と**allrooms**のスキーマに一致します。 これにより、 **RoomBrowseGallery**の**Items**プロパティで両方のコレクションを使用できるようになります。
      1. **_roomListSelected**が**false**に設定されています。
  1. 他のすべての実行が完了すると、読み込み中の状態 (" **Loading室")** は**false**に設定されます。

## <a name="room-browse-gallery"></a>ルーム参照ギャラリー

   ![RoomBrowseGallery コントロール](media/meeting-screen/meeting-rooms-gall.png)

* "**品目**<br>
    数値ユーザーがルームリストを選択したか、またはテナントにルームリストを持っているかに応じて、同じスキーマの2つの内部コレクションに論理的に設定されます。

    ```powerapps-dot
    Search(
        If( _roomListSelected || _noRoomLists, AvailableRoomsOptimal, RoomsLists ),
        Trim(TextMeetingLocation1.Text), 
        "Name", 
        "Address"
    )
    ```

  このギャラリーには、 **AvailableRoomsOptimal**コレクションが表示されます。 **_RoomListSelected**または**noroomlists**は**true**です。 それ以外の場合は、 **RoomsLists**コレクションが表示されます。 これらのコレクションのスキーマは同一であるため、これを行うことができます。

* "**さ**<br>
    値: ```_showDetails && !IsBlank( _selectedMeetingTime ) && !_loadingRooms```

    ギャラリーは、前の3つのステートメントが**true**と評価された場合にのみ表示されます。

### <a name="roombrowsegallery-title"></a>RoomBrowseGallery のタイトル

   ![RoomBrowseGallery Title コントロール](media/meeting-screen/meeting-rooms-gall-title.png)

* "**OnSelect**<br>
    数値ユーザーがルームリストまたはルームを表示しているかどうかに応じて、論理的にバインドされた**Collect**および**set**ステートメントのセット。これらはトリガーされない可能性があります。

    ```powerapps-dot
    UpdateContext( { _loadingRooms: true } );
    If( !_roomListSelected && !noRoomLists,
        Set( _roomListSelected, true );
        Set( _selectedRoomList, ThisItem.Name );
        ClearCollect( AllRooms, 'Office365'.GetRoomsInRoomList( ThisItem.Address ).value );
        Set( _allRoomsConcat, Concat( FirstN( AllRooms, 20 ), Address & ";" ) );
        ClearCollect( RoomTimeSuggestions, 
            'Office365'.FindMeetingTimes(
                {
                    RequiredAttendees: _allRoomsConcat, 
                    MeetingDuration: MeetingDurationSelect.Selected.Minutes,
                        Start: _selectedMeetingTime.StartTime & "Z", 
                    End: _selectedMeetingTime.EndTime & "Z", 
                    MinimumAttendeePercentage: "1",
                    IsOrganizerOptional: "false", 
                    ActivityDomain: "Unrestricted"
                }
            ).MeetingTimeSuggestions
        );
        ClearCollect( AvailableRooms, 
            AddColumns(
                AddColumns(
                    Filter(
                        First( RoomTimeSuggestions ).AttendeeAvailability, 
                        Availability = "Free"
                    ),
                    "Address", Attendee.EmailAddress.Address 
                ), 
                "Name", LookUp( AllRooms, Address = Attendee.EmailAddress.Address ).Name
            )
        );
        ClearCollect( AvailableRoomsOptimal, 
            DropColumns(
                DropColumns( AvailableRooms, "Availability" )
            ), 
            "Attendee" )
        ),
        Set( _selectedRoom, ThisItem )
    );
    UpdateContext( {_loadingRooms: false} )
    ```

  このコントロールが選択されているときに実行されるアクションは、ユーザーが現在、一連のルームリストまたはルームのセットを表示しているかどうかによって異なります。 前者の場合は、このコントロールを選択すると、選択した部屋の一覧から選択した時間に利用可能なルームが取得されます。 後者の場合は、このコントロールを選択すると、選択した項目に対して選択した**om**変数が設定されます。 前のステートメントは、 [**Findmeetingtimesgallery タイトル**](#find-meeting-times-gallery)の**Select**ステートメントによく似ています。

  低いレベルでは、上記のコードブロックは次のようになります。
  1. ルームを**true** **に設定し**て、ルームの読み込み状態をオンにします。
  1. 部屋リストが選択されているかどうか、およびテナントにスペースリストがあるかどうかを確認します。 そうすれば：
      1. **_RoomListSelected**を**true**に設定し、選択した**項目に設定**します。
      1. **_AllRoomsConcat**変数は、 **allrooms**コレクション内のルームの最初の20個の電子メールアドレスをセミコロンで区切った文字列に設定されます。 これは、 [Office365 の findtimes](https://docs.microsoft.com/connectors/office365/#find-meeting-times)操作が、1回の操作で20人の person オブジェクトの使用可能な時間を検索することに限定されるためです。
      1. **RoomTimeSuggestions**コレクションでは、 [Office 365. findの待ち時間](https://docs.microsoft.com/connectors/office365/#find-meeting-times)操作を使用して、 **allrooms**コレクション内の最初の20個のルームの可用性を**取得し**ます。変動. **DateTime**値を適切に書式設定するには、`& "Z"` が使用されていることに注意してください。
      1. **AvailableRooms** collection が作成されます。 これは、次の2つの列が追加された参加者の利用能力の**RoomTimeSuggestions**コレクションです。"Address" と "Name"。 "Address" は、部屋の電子メールアドレスです。 "Name" はルームの名前です。
      1. 次に、 **AvailableRoomsOptimal**コレクションが作成されます。 これは、"Availability" 列と "出席者" 列が削除された**AvailableRooms**コレクションにすぎません。 これは、 **AvailableRoomsOptimal**と**allrooms**のスキーマに一致します。 これにより、 **RoomBrowseGallery**の**Items**プロパティで両方のコレクションを使用できるようになります。
      1. **_roomListSelected**が**false**に設定されています。
  1. 他のすべての実行が完了すると、読み込み中の状態 (" **Loading室")** は**false**に設定されます。

## <a name="back-chevron"></a>前のシェブロン

   ![RoomsBackNav コントロール](media/meeting-screen/meeting-back.png)

* "**さ**<br>
    値: `_roomListSelected && _showDetails`

    このコントロールは、部屋リストが選択されていて、 **[スケジュール]** タブが選択されている場合にのみ表示されます。

* "**OnSelect**<br>
    値: `Set( _roomListSelected, false )`

    **_RoomListSelected**が**false**に設定されている場合、 **RoomsLists** collection の項目を表示するように**RoomBrowseGallery**コントロールが変更されます。

## <a name="send-icon"></a>送信アイコン

   ![IconSendItem コントロール](media/meeting-screen/meeting-send-icon.png)

* "**DisplayMode**<br>
    数値アイコンが編集可能になる前に、ユーザーが特定の会議の詳細を入力するように強制するロジック。
    
    ```powerapps-dot
    If( Len( Trim( TextMeetingSubject1.Text ) ) > 0
        && !IsEmpty( MyPeople ) && !IsBlank( _selectedMeetingTime ),
        DisplayMode.Edit, DisplayMode.Disabled
    )
    ```
  このアイコンは、会議の件名が入力されていて、会議の参加者が少なくとも1人いる場合にのみ選択できます。 それ以外の場合は無効になります。

* "**OnSelect**<br>

    数値会議の招待を選択した参加者に送信し、すべての入力フィールドをクリアするコード:

    ```powerapps-dot
    Set( _myCalendarName, LookUp( 'Office365'.CalendarGetTables().value, DisplayName = "Calendar" ).Name );
    Set( _myScheduledMeeting, 
        'Office365'.V2CalendarPostItem( _myCalendarName,
            TextMeetingSubject1.Text, 
            Text(DateAdd(DateTimeValue( _selectedMeetingTime.StartTime), -TimeZoneOffset(), Minutes) ),
            Text(DateAdd(DateTimeValue( _selectedMeetingTime.EndTime), -TimeZoneOffset(), Minutes) ),
            {
                RequiredAttendees: Concat( MyPeople, UserPrincipalName & ";" ) & _selectedRoom.Address, 
                Body: TextMeetingMessage1.Text, 
                Location: _selectedRoom.Name, 
                Importance: "Normal", 
                ShowAs: "Busy", 
                ResponseRequested: true
            }
        )
    );
    Concurrent(
        Reset( TextMeetingLocation1 ),
        Reset( TextMeetingSubject1 ),
        Reset( TextMeetingMessage1 ),
        Clear( MyPeople ),
        Set( _selectedMeetingTime, Blank() ),
        Set( _selectedRoomList, Blank() ),
        Set( _selectedRoom, Blank() ),
        Set( _roomListSelected, false )
    )
    ```
  
  低レベルでは、このコードブロックは次のようになります。
  1. "Calendar" の**DisplayName**を使用して、 [Office 365. calendargettables ()](https://docs.microsoft.com/connectors/office365/#get-calendars)操作のカレンダーに**mycalendarname**を設定します。
  1. [V2CalendarPostItem](https://docs.microsoft.com/connectors/office365/#create-event--v2-)操作を使用して、ユーザーが画面全体で行ったさまざまな選択項目のすべての入力値を使用して会議をスケジュールします。
  1. 会議の作成に使用されるすべての入力フィールドと変数をリセットします。

> [!NOTE]
> 地域によっては、表示名が "Calendar" でない場合があります。 Outlook に移動して予定表のタイトルを確認し、アプリで適切な変更を行います。

## <a name="next-steps"></a>次の手順

* [この画面の詳細情報](./meeting-screen-overview.md)
* [PowerApps での Office 365 Outlook コネクタについての詳細情報](../connections/connection-office365-outlook.md)
* [PowerApps での Office 365 Users コネクタについての詳細情報](../connections/connection-office365-users.md)

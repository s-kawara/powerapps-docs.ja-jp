---
title: キャンバス アプリの会議画面テンプレートのリファレンス |Microsoft Docs
description: PowerApps でキャンバス アプリの会議画面テンプレートのしくみの詳細を理解します。
author: emcoope-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 01/03/2019
ms.author: emcoope
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: a7559f84b43d3c0372dea71d49c35461ba9d4e57
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61539704"
---
# <a name="reference-information-about-the-meeting-screen-template-for-canvas-apps"></a>キャンバス アプリの会議画面テンプレートに関する参照情報

PowerApps のキャンバス アプリの場合、会議画面テンプレートの重要な各コントロールが、画面の全体的な既定機能に貢献する方法について説明します。 この詳細情報は、動作の数式とその他のコントロールがユーザー入力に応答する方法を決定するプロパティの値を表示します。 この画面の既定の機能の概要については、 [ミーティング画面概要](meeting-screen-overview.md) をご参照ください。

このトピックでは、いくつかの重要なコントロールに焦点を当て、これらのコントロールのさまざまなプロパティ( **Item** と **OnSelect** など)が設定される式または数式について説明します。

* [[招待] タブ (LblInviteTab)](#invite-tab)
* [[スケジュール] タブ (LblScheduleTab)](#schedule-tab)
* [テキスト検索ボックス](#text-search-box)
* [[追加] アイコン (AddIcon)](#add-icon)
* [ユーザーがギャラリーを参照](#people-browse-gallery)(+ 子コントロール)
* [会議人ギャラリー](#meeting-people-gallery) (+ 子コントロール)
* [会議の日付の選択 (MeetingDateSelect)](#meeting-date-picker)
* [会議時間ボックスの一覧 (MeetingDurationSelect)](#meeting-duration-drop-down)
* [会議の時間を検索するギャラリー](#find-meeting-times-gallery) (+ 子コントロール)
* [ルーム参照ギャラリー](#room-browse-gallery) (+ 子コントロール)
* [バック シェブロン (RoomsBackNav)](#back-chevron) (テナントが部屋のリストを持っていない場合は、表示されない場合があります)
* [[送信] アイコン](#send-icon)

## <a name="prerequisite"></a>前提条件

[PowerApps でアプリを作成](../data-platform-create-app-scratch.md) するときに画面やその他のコントロールを追加および構成する方法を理解している方。

## <a name="invite-tab"></a>[招待] タブ

   ![LblInviteTab コントロール](media/meeting-screen/meeting-invite-text.png)

* プロパティ:**Colorr**<br>
    値: `If( _showDetails, LblRecipientCount.Color, RectQuickActionBar.Fill )`

    **_showDetails** は、 **LblInviteTab** コントロールまたは **LblScheduleTab** コントロールが選択されているかどうかを判断するために使用される変数です。 **_showDetails** の値が **true** の場合、 **LblScheduleTab** が選択されます。値が、 **false** の場合、 **LblInviteTab** が選択されます。つまり、 **_showDetails** の値が、 **true** (このタブが選択されていない)の場合、タブの色は **LblRecipientCount** の色と一致します。それ以外の場合、 **RectQuickActionBar** の塗りつぶし値と一致します。

* プロパティ:**OnSelect**<br> 
    値: `Set( _showDetails, false )`

    **_showDetails** 変数を **false** に設定します。つまり、招待タブの内容が表示され、**スケジュール** タブは表示されません。	

## <a name="schedule-tab"></a>[スケジュール] タブ

   ![LblInviteTab コントロール](media/meeting-screen/meeting-schedule-text.png)

* プロパティ:**Color**<br>
    値: `If( !_showDetails, LblRecipientCount.Color, RectQuickActionBar.Fill )`

    **_showDetails** は、 **LblInviteTab** コントロールまたは **LblScheduleTab** コントロールが選択されているかどうかを判断するために使用される変数です。 true の場合、 **LblScheduleTab** が選択されています。 false の場合、 **LblInviteTab** です。つまり、 **_showDetails** が  true (このタブが選択されている)の場合、タブの色は **RectQuickActionBar** の塗りつぶしと一致します。それ以外の場合、 **LblRecipientCount** の色と値と一致します。

* プロパティ:**OnSelect**<br>
    値: `Set( _showDetails, true )`

    **_showDetails** 変数を **true** に設定します。つまり、 [スケジュール] タブの内容は表示され、 [招待] タブの内容は表示されません。

## <a name="text-search-box"></a>テキスト検索ボックス

   ![TextSearchBox コントロール](media/meeting-screen/meeting-search-box.png)

<!--Include description of text search box control?-->

画面内のその他のいくつかのコントロールは、このコントロールに依存しています。

* ユーザーが任意のテキストの入力を始めると **PeopleBrowseGallery** が表示されます。
* ユーザーが有効な電子メール アドレスを入力すると、 **AddIcon** が表示されます。
* ユーザーが **PeopleBrowseGallery** 内で人を選択すると検索内容がリセットされます。

## <a name="add-icon"></a>[追加] アイコン

   ![AddIcon コントロール](media/email-screen/email-add-icon.png)

このコントロールで構成される会議の出席者の一覧に、組織内に存在しないユーザーを追加することができます。

* プロパティ: **Visible**<br>
値: コントロールを表示するには、すべてが **true** と評価される必要がある 3 つの論理チェック。

    ```powerapps-dot
    !IsBlank( TextSearchBox.Text ) &&
        IsMatch( TextSearchBox.Text, Match.Email ) &&
        Not( Trim( TextSearchBox.Text ) in MyPeople.UserPrincipalName )
    ```

  行ごとに、このコード ブロックは、 **AddIcon** コントロールが次の場合のみ表示されます。

  * **TextSearchBox** にはテキストが含まれています。
* **TextSearchBox** のテキストは有効な電子メール アドレスです。
* **TextSearchBox** のテキストは **MyPeople** コレクションには存在していません。

* プロパティ:**OnSelect**<br> 
    値: ユーザーを出席者リストに追加する **Collect** ステートメント、使用可能な会議時間を更新する別のステートメントおよびいくつかの変数を更新します。

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

  このコントロールを選択すると、有効な電子メール アドレス (有効な電子メール アドレスが、 **TextSearchBox** に入力された場合のみ表示) が、  **MyPeople** コレクション (このコレクションは、出席者リスト)に追加され、新しいユーザー エントリで使用可能な会議時間が更新されます。

  低レベルの場合は、次のコード ブロック。
  1. 電子メール アドレスを **MyPeople** コレクションに収集し、電子メール アドレスを **DisplayName** 、 **UserPrincipalName** 、および**Mail** フィールドに収集します。
  1. **TextSearchBox** コントロールの内容をリセットします。
  1. **_showMeetingTimes** 変数を **false** に設定します。 この変数は、 **FindMeetingTimesGallery** の可視性を制御し、出席者が合う時間を表示します。
  1. **_loadMeetingTimes** コンテキスト変数を **true** に設定します。 この変数は、 **_LblTimesEmptyState** などの読み込み状態コントロールの表示を切り替えて、データが読み込まれている状態をユーザーに示します。
  1. **_selectedMeetingTime** を **Blank()** に設定します。 **_selectedMeetingTime** は、 **FindMeetingTimesGallery** コントロールから選択されたレコードです。他の出席者を追加すると、その出席者は、 **_selectedMeetingTime** の以前の定義を使用できなくなる可能性があるため、ここでは空白になっています。
  1. **_selectedRoom** を **Blank()** に設定します。 **_selectedRoom** は、 **RoomBrowseGallery** から選択されたルームレコードです。ルームの空室状況は、 **_selectedMeetingTime** の値から決定されます。その値を空白にすると、 **_selectedRoom** 値は無効になるため、空白にする必要があります。
  1. **_roomListSelected** を **false** に設定します。 この行は、すべてのユーザーに適用できるわけではありません。 Office では、ルームをさまざまな「ルームリスト」でグループ化できます。ルームリストがある場合、この画面はそのことを考慮し、最初にルームリストを選択してから、そのリスト内からルームを選択できます。 **_roomListSelected** の値は、ユーザー (ルームリストを持つテナントのみ) がルームリスト内のルームまたはルームリストのセットを表示するかどうかを決定します。ユーザーに新しい会議室リストの再選択を強制するには、 **false** に設定されます。
  1.  [Office365.FindMeetingTimes](https://docs.microsoft.com/connectors/office365/#find-meeting-times) 操作を使用して、出席者が利用できる会議時間を決定および収集します。この操作は、以下を渡します。
      * **RequiredAttendees** パラメーターに選択された各ユーザーの **UserPrincipalName** を追加。
      * **MeetingDuration** パラメーターに **MeetingDurationSelect**.Selected.Minutes を追加。
      * MeetingDateSelect.SelectedDate + 8 時間を、 *Start*パラメーターに設定。 既定では、カレンダーコントロールの完全な日付/時刻は選択した日付の午前 12 時 00 分 であるため、 8 時間が追加されます。通常の業務時間内で利用可能を取得する可能性があります。 通常の作業の開始時刻は午前 8 時 00 分になります。
      * **MeetingDateSelect**.SelectedDate + 17 時間を、 *End* パラメーターに設定。午前 12 時 00 分 + 17 時間 = 午後 5 時 00 分であるため、17 時間が追加されます。通常の作業の終了時刻は午後 5 時 00 分になります。
      * *15* を *MaxCandidates* パラメーターに入力します。これは、選択された日付の上位 15 回の利用可能な時間のみが操作によって返されることを意味します。8 時間の勤務日に 30 分間のチャンクが 16 個しかなく、この画面で設定できる最少の会議は 30 分の会議だからです。
      * *1* を *MinimumAttendeePercentage* パラメーターに設定。 基本的には、出席者がいない場合を除き、会議の時間が取得されます。
      * **false** を *IsOrganizerOptional* パラメーターに設定。 アプリのユーザーは、この会議のオプションの出席者ではありません。
      * 「Work」を *ActivityDomain* パラメーターに設定。 つまり、取得される時間は通常の作業時間内の時間のみです。。
  1. **ClearCollect** 関数は、"StartTime" と "EndTime" という 2 つの列も追加します。 これにより、返されるデータが簡略化されます。使用可能な開始と終了時刻を格納しているフィールドは、 **MeetingTimeSlot** フィールドです。 このフィールドは、開始レコードと終了レコードを含むレコードです。これらのレコード自体には、それぞれの提案の **DateTime** と **TimeZone** 値が含まれています。 この入れ子のレコードを取得しようとする代わりに  "StartTime" と "EndTime" 列を **MeetingTimes** コレクションに追加すると、これらの **Start > DateTime** および **End >DateTime** 値が画面コレクションに追加されます。
  1. これらの関数がすべて完了すると、 **_loadingMeetingTimes** 変数が **false** に設定されて読み込み状態が削除され、 **_showMeetingTimes** が  **true** に設定されて、 **FindMeetingTimesGallery** が表示されます。

## <a name="people-browse-gallery"></a>ユーザーがギャラリーを参照します。

   ![PeopleBrowseGallery コントロール](media/meeting-screen/meeting-browse-gall.png)

* プロパティ:**Items**<br>
    値: 
    ```powerapps-dot
    If( !IsBlank( Trim( TextSearchBox.Text ) ), 
        'Office365Users'.SearchUser( { searchTerm: Trim(TextSearchBox.Text), top: 15 } )
    )
    ```

このギャラリーの項目には、 [Office365.SearchUser](https://docs.microsoft.com/connectors/office365users/#searchuser) 操作の検索結果が表示されます。 この操作では、`Trim(**TextSearchBox**)` テキストを検索用語として使用し、その検索に基づいて上位 15 件の結果を返します。
  
**TextSearchBox** は、スペースでのユーザー検索が有効でないため、 **Trim** 関数でラップされます。 `Office365Users.SearchUser` 操作は、ユーザーが検索する前に検索結果を取得するとパフォーマンスが無駄になるため、 `If(!IsBlank(Trim(TextSearchBox.Text)) ... )` 関数でラップされます。

### <a name="people-browse-gallery-title"></a>ユーザーがギャラリーのタイトルを参照します。

   ![PeopleBrowseGallery タイトル コントロール](media/meeting-screen/meeting-browse-gall-title.png)

* プロパティ:**[Text (テキスト)]**<br>
    値: `ThisItem.DisplayName`

    Office 365 プロファイルからユーザーの表示名が表示されます。

* プロパティ:**OnSelect**<br>
    値: ユーザーを出席者リストに追加する **Collect** ステートメント、使用可能な会議時間を更新する別のステートメントおよびいくつかの変数を更新します。

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

    大まかに言えば、このコントロールを選択するユーザーが、 **MyPeople** コレクション(アプリの出席者リストの記憶域) に追加され、新しいユーザーの追加に基づいて利用可能な会議時間が更新されます。

    このコントロールの選択は、 **AddIcon** コントロールの選択と非常に似ています。唯一の違いは、 `Set(_selectedUser, ThisItem)` ステートメントと操作の実行順序です。 そのため、この説明はそれほど深くなりません。詳細な説明については、 [AddIcon コントロール](#add-icon) セクションをご覧ください。

    このコントロールを選択すると、 **TextSearchBox** がリセットされます。 その後、選択が **MyPeople** にない場合、コントロールは次のことを行います。
    1. **_loadMeetingTimes** 状態を **true** に設定し、 **_showMeetingTimes** 状態を **false** に設定し、 **_selectedMeetingTime** と  **_selectedRoom** 変数を空白にし、 **MyPeople** コレクションを新しく追加して **MeetingTimes** コレクションを更新します。 
    1. **_loadMeetingTimes** 状態を **false** に設定し、 **_showMeetingTimes** を **true** に設定します。 選択が既に **MyPeople** コレクションにある場合、 **TextSearchBox** のコンテンツのみがリセットされます。

## <a name="meeting-people-gallery"></a>会議人ギャラリー

   ![MeetingPeopleGallery コントロール](media/meeting-screen/meeting-people-gall.png)

* プロパティ:**Items**<br>
    値: `MyPeople`

    **MyPeople** コレクションは、 **PeopleBrowseGallery Title** コントロールを選択することにより初期化または追加されるユーザーのコレクションです。
* プロパティ: **Height**<br>
値: ギャラリーを最大 350 まで拡大できるようにするロジック。

    ```powerapps-dot
    Min( 
        76 * RoundUp( CountRows( MeetingPeopleGallery.AllItems ) / 2, 0 ),
        350
    )
    ```

  
   このギャラリーの高さは、ギャラリー内の項目の数、最大の高さである 350 に調整されます。式は、 **MeetingPeopleGallery** の一行の高さとして 76 を取得し、行数で乗算します。 **WrapCount** プロパティは 2 に設定されているため、実際の行の数は、 `RoundUp(CountRows(MeetingPeopleGallery.AllItems) / 2, 0)` です。

* プロパティ:**ShowScrollbar**<br>
    値: `MeetingPeopleGallery.Height >= 350`

    ギャラリーの最大高さ( 350 )に達すると、スクロール バーが表示されます。

### <a name="meeting-people-gallery-title"></a>会議人ギャラリーのタイトル

   ![MeetingPeopleGallery タイトル コントロール](media/meeting-screen/meeting-people-gall-title.png)

* プロパティ:**OnSelect**<br>
    
    値: `Set(_selectedUser, ThisItem)`
    
    **_selectedUser** 変数を **MeetingPeopleGallery** で選択された項目に設定します。

### <a name="meeting-people-gallery-iconremove"></a>会議人ギャラリー iconRemove

   ![MeetingPeopleGallery iconRemove コントロール](media/meeting-screen/meeting-people-gall-delete.png)

* プロパティ:**OnSelect**<br>
    値: 出席者リストからユーザーを削除する **Remove** ステートメント、使用可能な会議時間を更新する **Collect** ステートメント、およびいくつかの変数を更新するステートメント。

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

  大まかに言えば、このコントロールを選択すると、出席者リストから、そのユーザーを削除し、このユーザーの削除に基づいて使用可能な会議の時間が更新されます。

  上記のコードの最初の行の後、このコントロールを選択することは、 **AddIcon** コントロールを選択することと殆んど同じです。 そのため、この説明はそれほど深くなりません。 詳細について、 [AddIcon コントロール セクション](#add-icon) をご覧ください。

  コードの最初の行で選択した項目が、 **MyPeople** コレクションから削除されます。 次の後のコード:
  1. **TextSearchBox** をリセットし、 **MyPeople** コレクションから選択を削除します。 
  1. **_loadMeetingTimes** 状態を **true** に設定し、 **_showMeetingTimes** 状態を **false** に設定し、 **_selectedMeetingTime** 変数と  **_selectedRoom** 変数を空白にし、**MyPeople** コレクションに新しく追加して **MeetingTimes** コレクションを更新します。
  1. **_loadMeetingTimes** 状態を **false** に設定し、 **_showMeetingTimes** を **true** に設定します。

## <a name="meeting-date-picker"></a>ミーティングの日付の選択

   ![MeetingDateSelect コントロール](media/meeting-screen/meeting-datepicker.png)

* プロパティ:**DisplayMode**<br>
    値: `If( IsEmpty(MyPeople), DisplayMode.Disabled, DisplayMode.Edit )`

    **MyPeople** コレクションに少なくとも１人の参加者が追加されるまで、会議の日付は選択できません。

* プロパティ:**OnChange**<br>
    値: `Select( MeetingDateSelect )`

    選択した日付を変更すると、このコントロールの **OnSelect** プロパティのコードが実行されます。

* プロパティ:**OnSelect**<br>
    値: 利用可能な会議時間を更新するための **Collect** ステートメントおよびいくつかの変数を更新するステートメント。
    
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

  大まかに言えば、このコントロールを選択すると、利用可能な会議時間が更新されます。ユーザーが日付を変更した場合、利用可能な会議時間を更新して、その日の出席者の空き時間を反映する必要があるため貴重です。

  最初の **Collect** ステートメントを除き、これは **AddIcon** コントロールの **OnSelect** 機能と同じです。 そのため、この説明はそれほど深くなりません。詳細については、 [AddIcon コントロール](#add-icon) セクションをご覧ください。

  このコントロールを選択すると、 **TextSearchBox** がリセットされます。その後: 
  1. **_loadMeetingTimes** 状態を **true** に設定し、 **_showMeetingTimes** 状態を **false** に設定し、 **_selectedMeetingTime** 変数と  **_selectedRoom** 変数を空白にし、新しい日付で **MeetingTimes** コレクションを更新します。 
  1. **_loadMeetingTimes** 状態を **false** に設定し、 **_showMeetingTimes** を **true** に設定します。

## <a name="meeting-duration-drop-down"></a>会議の継続時間ドロップダウン

   ![MeetingDateSelect コントロール](media/meeting-screen/meeting-timepicker.png)

* プロパティ:**DisplayMode**<br>
    値: `If( IsEmpty(MyPeople), DisplayMode.Disabled, DisplayMode.Edit )`

    会議の期間は、少なくとも 1 人の参加者が **MyPeople** コレクションに追加されるまで選択できません。

* プロパティ:**OnChange**<br>
    値: `Select(MeetingDateSelect1)`

    選択された期間を変更すると、**MeetingDateSelect** コントロールの **OnSelect** のプロパティのコードが実行されます。

## <a name="find-meeting-times-gallery"></a>会議の時間を検索するギャラリー

   ![FindMeetingTimesGallery コントロール](media/meeting-screen/meeting-time-gall.png)

* プロパティ:**Items**<br>
    値: `MeetingTimes`

    [Office365.FindMeetingTimes](https://docs.microsoft.com/connectors/office365/#find-meeting-times) 操作から取得された潜在的な会議時間のコレクション。

* プロパティ:**Visible**<br>
    値: `_showMeetingTimes && _showDetails && !IsEmpty( MyPeople )`

    ギャラリーは、 **_showMeetingTimes** が **true** に設定され、ユーザーが **LblScheduleTab** コントロールを選択し、会議に少なくとも 1 人の出席者が追加されている場合のみ表示されます。

### <a name="find-meeting-times-gallery-title"></a>会議の時間を検索するギャラリーのタイトル

   ![FindMeetingTimesGallery タイトル コントロール](media/meeting-screen/meeting-time-gall-title.png)

* プロパティ:**[Text (テキスト)]**<br>
    値:ユーザーのローカル時刻で表示する開始時刻の変換:

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

  **StartTime** の取得値は UTC 形式です。 [UTC から現地時刻に変換する](../functions/function-dateadd-datediff.md#converting-from-utc) には、  **DateAdd** 関数が適用されます。
  [Text 関数](../functions/function-text.md#datetime)は、最初の引数として日付/時刻を受け取り、 2 番目の引数に基づいて形式を変換します。  **ThisItem.StartTime** のローカル時間変換を渡し、 **DateTimeFormat.ShortTime** として表示します。

* プロパティ:**OnSelect**<br>
    値: 会議室とそれらの推奨される利用可能性を収集するための複数の **Collect** ステートメントおよびいくつかの変数を切り替えるステートメント。

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

  大まかに言えば、このコード ブロックは、会議の選択された日付/時刻に基づいて、部屋リストを持たないユーザーが利用できる部屋を収集します。それ以外の場合は、部屋リストだけを取得します。

  細かく言えば、次のコード ブロックになります。
  1. **_selectedMeetingTime** を選択した項目に設定します。 これは、その時間に利用可能な部屋を見つけるために使用されます。
  1. 読み込みの状態変数 **_loadingRooms** を **true** に設定し、読み込みの状態を有効にします。
  1. **RoomsLists** コレクションが空の場合、ユーザーのテナントの部屋リストを取得し、それらを **RoomsLists** コレクションに保存します。
  1. ユーザーに部屋リストがないか、部屋リストが 1 つある場合。
      1. **NoRoomLists** に変数は **true** に設定され、この変数は **RoomBrowseGallery** コントロールに表示される項目を決定するために使用されます。。
      1. `Office365.GetRooms()` 操作は、テナントの最初の 100 個の部屋を取得するために使用します。 これらは、 **AllRooms** コレクションに保存されます。
      1. **_AllRoomsConcat** 変数は、 **AllRooms** コレクション内の部屋の最初の 20 個の電子メールアドレスのセミコロン区切り文字列に設定されます。これは、  [Office365.FindMeetingTimes](https://docs.microsoft.com/connectors/office365/#find-meeting-times) が 1 回の操作で 20 人のオブジェクトの利用可能な時間を検索することに制限されているためです。
      1. **RoomTimeSuggestions** コレクションは、 [Office365.FindMeetingTimes](https://docs.microsoft.com/connectors/office365/#find-meeting-times) を使用して、 **_selectedMeetingTime** 変数の時間値に基づいて、 **AllRooms** コレクションの最初の 20 室の可用性を取得します。 **DateTime** 値を適切にフォーマットするために `& "Z"` が使用されることに注意してください。
      1. **AvailableRooms** コレクションが作成されます。 これは、出席者の可用性の **RoomTimeSuggestions** コレクションに、「Address」と「Name」の 2 つの列が追加されたものです。「Address」は部屋の メール アドレス で、「Name」は部屋の名前です。
      1. 次に、 **AvailableRoomsOptimal** コレクションが作成されます。 これは、「Availability」と「Attendee」が削除された **AvailableRooms** コレクションです。これを行うと、 **AvailableRoomsOptimal** および **AllRooms** のスキーマーと一致します。これにより **RoomBrowseGallery** の **Items** プロパティで両方のコレクションを使用できます。
      1. **_roomListSelected**に設定されている**false**します。
  1. 読み込みの状態、 **_loadingRooms** は、他のすべての実行が完了すると **false** に設定されます。

## <a name="room-browse-gallery"></a>ルーム ギャラリーの参照

   ![RoomBrowseGallery コントロール](media/meeting-screen/meeting-rooms-gall.png)

* プロパティ:**Items**<br>
    値:ユーザーが部屋リストを選択したか、テナントに部屋リストがあるかに応じて、同一のスキーマの 2 つの内部コレクションに論理的に設定します。

    ```powerapps-dot
    Search(
        If( _roomListSelected || _noRoomLists, AvailableRoomsOptimal, RoomsLists ),
        Trim(TextMeetingLocation1.Text), 
        "Name", 
        "Address"
    )
    ```

  **_roomListSelected** または **_noRoomLists** が **true** の場合、このギャラリーには **AvailableRoomsOptimal** コレクションが表示されます。それ以外の場合は、 **RoomsLists** コレクションが表示されます。 これらのコレクションのスキーマが同じであるために実行できます。

* プロパティ:**Visible**<br>
    値: ```_showDetails && !IsBlank( _selectedMeetingTime ) && !_loadingRooms```

    ギャラリーは、上記の 3 つのステートメントが **true**と評価された場合のみ表示されます。

### <a name="roombrowsegallery-title"></a>RoomBrowseGallery タイトル

   ![RoomBrowseGallery タイトル コントロール](media/meeting-screen/meeting-rooms-gall-title.png)

* プロパティ:**OnSelect**<br>
    値: 論理的にバインドされた **Collect** および **Set** ステートメントのセット。ユーザーが部屋リストまたは部屋のどちらかを表示しているかによって、トリガーされる場合とトリガーされない場合があります。

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

  このコントロールが選択されているときに発生するアクションは、ユーザーが現在部屋セットのセットを表示しているか、部屋のセットを表示しているかによって異なります。前者の場合、このコントロールを選択すると、選択した部屋リストから選択した時間に利用可能な部屋が取得されます。後者の場合、このコントロールを選択すると、 **_selectRoom** 変数が選択された項目に設定されます。操作は、ユーザーが部屋のリストのセットまたは一連のルーム表示現在かどうかによって異なります。 このコントロールを選択し、前者の場合、選択した部屋リストから選択した時間で使用できる会議室を取得します。 後者の場合、このコントロールを選択すると設定、 **_selectedRoom**変数を選択した項目に設定されます。上記のステートメントは、[ **FindMeetingTimesGallery Title**](#find-meeting-times-gallery)の **Select** ステートメントに非常に似ています。

  細かく言えば、以下のコード ブロックになります。
  1. **_loadingRooms** を **true** に設定して、部屋の読み込み状態をオンにします。
  1. 部屋リストが選択されているかどうか、およびテナントに部屋リストがあるかどうかを確認します。その場合；
      1. **_roomListSelected** を **true** に設定して、 **_selectedRoomList**選択された項目に設定します。
      1. **_AllRoomsConcat** 変数は、**AllRooms** コレクション内の部屋の最初の 20 個の電子メールアドレスのセミコロン区切り文字列に設定されます。これは、 [Office365.FindMeetingTimes](https://docs.microsoft.com/connectors/office365/#find-meeting-times) 操作が、 1 回の操作で 20 人のオブジェクトの利用可能な時間を検索することに制限されているためです。
      1. **RoomTimeSuggestions** コレクションは、 [Office365.FindMeetingTimes](https://docs.microsoft.com/connectors/office365/#find-meeting-times) 操作を使用して、 **_selectedMeetingTime** 変数の時間値に基づいて、**AllRooms** コレクションの最初の 20 個の部屋の利用可能性を取得します。 なお`& "Z"` は、**DateTime** 関数を適切にフォーマットするために使用されることに注意してください。
      1. **AvailableRooms** コレクションが作成されます。 これは、出席者の可能性を **RoomTimeSuggestions** コレクションに、「Address」と「Name」の 2 つの列が追加されたものです。「Address」は部屋のメールアドレスで、「Name」は、部屋の名前です。
      1. 次に、 **AvailableRoomsOptimal** コレクションが作成されます。 これは、「Availability」と「Attendee」列が削除された **AvailableRoomsOptimal** および **AllRooms** スキーマーと一致します。これにより **RoomBrowseGallery** の **Items** プロパティで両方のコレクションを使用できます。
      1. **_roomListSelected** は **false** に設定されます。
  1. 読み込みの状態、 **_loadingRooms** は、他のすべての実行が完了すると **false** に設定されます。

## <a name="back-chevron"></a>シェブロンをバックアップします。

   ![RoomsBackNav コントロール](media/meeting-screen/meeting-back.png)

* プロパティ:**Visible**<br>
    値: `_roomListSelected && _showDetails`

    このコントロールは、部屋リストが選択され、 **スケジュール** タブが選択されている場合にのみ表示されます。

* プロパティ:**OnSelect**<br>
    値: `Set( _roomListSelected, false )`

    **_roomListSelected** を **false** に設定すると、 **RoomBrowseGallery** コントロールが変更され、 **RoomsLists** コレクションの項目が表示されます。

## <a name="send-icon"></a>[送信] アイコン

   ![IconSendItem コントロール](media/meeting-screen/meeting-send-icon.png)

* プロパティ:**DisplayMode**<br>
    値: アイコンが編集可能になる前に、特定の会議の詳細をユーザーに入力させるロジック。
    
    ```powerapps-dot
    If( Len( Trim( TextMeetingSubject1.Text ) ) > 0
        && !IsEmpty( MyPeople ) && !IsBlank( _selectedMeetingTime ),
        DisplayMode.Edit, DisplayMode.Disabled
    )
    ```
  このアイコンは、会議の件名が入力されており、会議の参加者が少なくとも 1 人いて、会議の時間が選択されている場合にのみ選択できます。それ以外の場合、無効になります。

* プロパティ:**OnSelect**<br>

    値: 選択した参加者に会議招集を送信し、全ての入力フィールドをクリアするコード:

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
  
 細かく言えば、次のコード ブロックになります。
1. **_myCalendarName** を [Office365.CalendarGetTables()](https://docs.microsoft.com/connectors/office365/#get-calendars) 操作の **DisplayName** が「Calendar」のカレンダーに設定します。
1. ユーザーが、 [Office365.V2CalendarPostItem](https://docs.microsoft.com/connectors/office365/#create-event--v2-) 操作を使用して画面前で行ったさまざまな選択からのすべての入力値を使用して、会議をスケジュールします。
1. 会議の作成に使用されたすべての入力フィールドと変数をリセットします。

> [!NOTE]
> 地域によっては、目的のカレンダーに「カレンダー」という表示名が無い場合があります。Outlook に移動してカレンダーのタイトルを確認し、アプリで適切な変更を加えます。

## <a name="next-steps"></a>次の手順

* [この画面を詳細します。](./meeting-screen-overview.md)
* [PowerApps での Office 365 Outlook コネクタの詳細します。](../connections/connection-office365-outlook.md)
* [PowerApps での Office 365 Users コネクタの詳細します。](../connections/connection-office365-users.md)

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

* プロパティ:**Color**<br>
    値: `If( _showDetails, LblRecipientCount.Color, RectQuickActionBar.Fill )`

    **_showDetails**決定に使用する変数かどうか、 **LblInviteTab**コントロールまたは**LblScheduleTab**コントロールを選択します。 場合の値 **_showDetails**は**true**、 **LblScheduleTab**が選択されている場合です値の場合**false**、 **LblInviteTab。** が選択されています。 場合の値を意味 **_showDetails**は**true** (このタブ*いない*選択)、タブの色のものと一致する**LblRecipientCount**. 塗りつぶしの値が一致する場合は、 **RectQuickActionBar**します。

* プロパティ:**OnSelect**<br> 
    値: `Set( _showDetails, false )`

    セット、 **_showDetails**変数を**false**、招待 タブの内容が表示され、つまりおよびの内容、**スケジュール** タブは表示されません。

## <a name="schedule-tab"></a>[スケジュール] タブ

   ![LblInviteTab コントロール](media/meeting-screen/meeting-schedule-text.png)

* プロパティ:**Color**<br>
    値: `If( !_showDetails, LblRecipientCount.Color, RectQuickActionBar.Fill )`

    **_showDetails**決定に使用する変数かどうか、 **LblInviteTab**コントロールまたは**LblScheduleTab**コントロールを選択します。 場合は true、 **LblScheduleTab**が選択されている場合は。 false の場合、 **LblInviteTab**です。 つまり、 **_showDetails**が true (このタブ*は*選択)、タブの色の塗りつぶしの値に一致**RectQuickActionBar**します。 色の値が一致する場合は、 **LblRecipientCount**します。

* プロパティ:**OnSelect**<br>
    値: `Set( _showDetails, true )`

    セット、 **_showDetails**変数を**true**つまりが [スケジュール] タブの内容が表示されて、および、[招待] タブの内容は表示されません。

## <a name="text-search-box"></a>テキスト検索ボックス

   ![TextSearchBox コントロール](media/meeting-screen/meeting-search-box.png)

<!--Include description of text search box control?-->

画面内のその他のいくつかのコントロールは、このコントロールに依存しています。

* ユーザーが任意のテキストの入力を始める場合**PeopleBrowseGallery**が表示されます。
* 場合は、ユーザーが有効な電子メール アドレス、 **AddIcon**が表示されます。
* ユーザーが内のユーザーを選択すると**PeopleBrowseGallery**検索内容がリセットされます。

## <a name="add-icon"></a>[追加] アイコン

   ![AddIcon コントロール](media/email-screen/email-add-icon.png)

このコントロールで構成される会議の出席者の一覧に、組織内に存在しないユーザーを追加することができます。

* プロパティ:**Visible**<br>
    値:コントロールを表示するには、すべてが **true** と評価される必要がある 3 つの論理チェック。

    ```powerapps-dot
    !IsBlank( TextSearchBox.Text ) &&
        IsMatch( TextSearchBox.Text, Match.Email ) &&
        Not( Trim( TextSearchBox.Text ) in MyPeople.UserPrincipalName )
    ```

  行ごとに、このコード ブロックは、 **AddIcon** コントロールが次の場合のみ表示されます。

  * **TextSearchBox**にはテキストが含まれています。
  * **TextSearchBox**のテキストは有効な電子メール アドレスです。
  * **TextSearchBox** のテキストは **MyPeople** コレクションには存在していません。

* プロパティ:**OnSelect**<br> 
    値:ユーザーを出席者リストに追加する **Collect** ステートメント、使用可能な会議時間を更新する別のステートメントおよびいくつかの変数を更新します。

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

  このコントロールを選択すると、有効な電子メール アドレス (有効な電子メール アドレスが、 **TextSearchBox** に入力された場合のみ表示) が、 **MyPeople** コレクション (このコレクションは、出席者リスト)に追加され、新しいユーザー エントリで使用可能な会議時間が更新されます。

  細かく言えば、次のコード ブロックになります。
  1. 電子メール アドレスを収集、 **MyPeople**に電子メール アドレスを収集して、コレクション、 **DisplayName**、 **UserPrincipalName**、および**メール**フィールド。
  1. 内容をリセット、 **TextSearchBox**コントロール。
  1. セット、 **_showMeetingTimes**変数を**false**します。 この変数の表示を制御する**FindMeetingTimesGallery**、開いているを満たすために選択した参加者の時間を表示します。
  1. セット、 **_loadMeetingTimes**にコンテキスト変数**true**します。 この変数のような状態のコントロールの読み込みの表示を切り替えた読み込み中の状態を設定する **_LblTimesEmptyState**データが読み込まれていることをユーザーに示すためにします。
  1. セット **_selectedMeetingTime**に**Blank()** します。 **_selectedMeetingTime**から選択したレコードは、 **FindMeetingTimesGallery**コントロール。 他の出席者の追加された可能性があります、前の定義のため、ここでは空は **_selectedMeetingTime**出席者のことはできません。
  1. セット **_selectedRoom**に**Blank()** します。 **_selectedRoom**から選択したルーム レコード**RoomBrowseGallery**します。 ルームの利用可能性の値によって決まります **_selectedMeetingTime**します。 空にすると、その値を持つ、 **_selectedRoom**値が有効で不要になったため、非表示にする必要があります。
  1. セット **_roomListSelected**に**false**します。 この行は、すべてのユーザーに適用しない場合があります。 Office では、ルームをグループ別で「ルームの一覧」。 部屋のリストがある場合は、この画面は、許可する最初の select に部屋リストからそのリスト内でのルームを選択する前にアカウントします。 値 **_roomListSelected**ユーザー (部屋リストのみを使用したテナント) であるかどうかが決まります部屋リストまたは一連の部屋のリスト内の部屋を表示します。 設定されている**false**新しい会議室の一覧をユーザーに強制します。
  1. 使用して、 [Office365.FindMeetingTimes](https://docs.microsoft.com/connectors/office365/#find-meeting-times)操作を決定し、出席者の会議に出席できる時間を収集します。 この操作に渡されます。
      * **UserPrincipalName**に選択した各ユーザーの*RequiredAttendees*パラメーター。
      * **MeetingDurationSelect**します。Selected.Minutes、 *MeetingDuration*パラメーター。
      * MeetingDateSelect.SelectedDate + に 8 時間、*開始*パラメーター。 既定では、予定表コントロールの完全な日付/時刻には、選択した日付の 12時 00分 AM、8 時間が追加されます。 通常の業務時間内で利用可能を取得する可能性があります。 通常の作業の開始時刻は午前 8時 00分になります。
      * **MeetingDateSelect**します。SelectedDate + に 17 時間、*エンド*パラメーター。 17 時間が追加されますので、12時 00分 AM + 17 = 5時 00分 PM。 通常の作業の終了時刻は午後 5時 00分になります。
      * *15*に、 *MaxCandidates*パラメーター。 つまり、操作は、選択した日付の使用可能な時間が 15 上位のみを返します。 これは、8 時間の作業日の場合は、16 のみ 30 分間のチャンクがある、30 分間ミーティングは、この画面で設定できる 1 つ以上の意味です。
      * *1*に、 *MinimumAttendeePercentage*パラメーター。 基本的には、出席者がない限り、会議の時間が取得されます。
      * **false**に、 *IsOrganizerOptional*パラメーター。 アプリのユーザーは、この会議の出席者ではありません。
      * 「作業」、 *ActivityDomain*パラメーター。 つまり、通常の作業時間内のみの取得時間が期間。
  1. **ClearCollect**関数では、2 つの列も追加されます。"StartTime"と"EndTime"。 これには、返されるデータが簡略化します。 
  使用可能な開始と終了時刻を格納しているフィールドは、 **MeetingTimeSlot**フィールド。 このフィールドは、開始を含むレコードと自体終了レコードが含まれて、 **DateTime**と**タイムゾーン**それぞれの提案の値。 この入れ子のレコードを取得しようとすると、代わりに"StartTime"と"EndTime"列を追加する、 **MeetingTimes**コレクションにより、**開始 > DateTime**と**終了 >DateTime**画面コレクションの値。
  1. これらの関数がすべて完了すると、 **_loadingMeetingTimes**に変数が設定されている**false**、読み込み中の状態を削除して **_showMeetingTimes** に設定されています。**true**表示、 **FindMeetingTimesGallery**します。

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

* プロパティ: **[Text (テキスト)]**<br>
    値: `ThisItem.DisplayName`

    Office 365 プロファイルからユーザーの表示名が表示されます。

* プロパティ:**OnSelect**<br>
    値:ユーザーを出席者リストに追加する **Collect** ステートメント、使用可能な会議時間を更新する別のステートメントおよびいくつかの変数を更新します。

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

    選択とよく似ていますがこのコントロールを選択すると、 **AddIcon**コントロール; のみされる点が異なります、`Set(_selectedUser, ThisItem)`ステートメントと、操作の実行順序。 そのため、この説明と高さを調整できません。 詳細について読み取り、 [AddIcon コントロール](#add-icon)セクション。

    このコントロールを選択すると、 **TextSearchBox** がリセットされます。 その後、選択が **MyPeople** にない場合、コントロールは次のことを行います。
    1. **_loadMeetingTimes** 状態を **true** に設定し、 **_showMeetingTimes** 状態を **false** に設定し、 **_selectedMeetingTime** と **_selectedRoom** 変数を空白にし、 **MyPeople** コレクションを新しく追加して **MeetingTimes** コレクションを更新します。 
    1. **_loadMeetingTimes** 状態を **false** に設定し、 **_showMeetingTimes** を **true** に設定します。 選択が既に **MyPeople** コレクションにある場合、 **TextSearchBox** のコンテンツのみがリセットされます。

## <a name="meeting-people-gallery"></a>会議人ギャラリー

   ![MeetingPeopleGallery コントロール](media/meeting-screen/meeting-people-gall.png)

* プロパティ:**Items**<br>
    値: `MyPeople`

    **MyPeople**コレクションは初期化するか、または選択に追加のユーザーのコレクション、 **PeopleBrowseGallery タイトル**コントロール。

* プロパティ:**Height**<br>
    値:ギャラリーを最大 350 まで拡大できるようにするロジック。

    ```powerapps-dot
    Min( 
        76 * RoundUp( CountRows( MeetingPeopleGallery.AllItems ) / 2, 0 ),
        350
    )
    ```

  
   このギャラリーの高さは、350 の最大の高さをギャラリー内の項目の数を調整します。 数式では、1 つの行の高さの 76 **MeetingPeopleGallery**行の数を掛けたします。 **WrapCount**プロパティが 2 に設定は true。 行の数が`RoundUp(CountRows(MeetingPeopleGallery.AllItems) / 2, 0)`します。

* プロパティ:**ShowScrollbar**<br>
    値: `MeetingPeopleGallery.Height >= 350`

    ギャラリーの最大高さ( 350 )に達すると、スクロール バーが表示されます。

### <a name="meeting-people-gallery-title"></a>会議人ギャラリーのタイトル

   ![MeetingPeopleGallery タイトル コントロール](media/meeting-screen/meeting-people-gall-title.png)

* プロパティ:**OnSelect**<br>
    
    値: `Set(_selectedUser, ThisItem)`
    
    セット、 **_selectedUser**変数で選択した項目を**MeetingPeopleGallery**します。

### <a name="meeting-people-gallery-iconremove"></a>会議人ギャラリー iconRemove

   ![MeetingPeopleGallery iconRemove コントロール](media/meeting-screen/meeting-people-gall-delete.png)

* プロパティ:**OnSelect**<br>
    値:出席者リストからユーザーを削除する **Remove** ステートメント、使用可能な会議時間を更新する **Collect** ステートメント、およびいくつかの変数を更新するステートメント。

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

  上記のコードの最初の行の後に選択するとほぼ同じですこのコントロールを選択すると、 **AddIcon**コントロール。 そのため、この説明と高さを調整できません。 詳細について読み取り、 [AddIcon コントロール セクション](#add-icon)します。

  コードの最初の行で選択した項目はから削除、 **MyPeople**コレクション。 次のコード:
  1. リセット**TextSearchBox**、し、選択項目を削除します、 **MyPeople**コレクション。 
  1. **_loadMeetingTimes** 状態を **true** に設定し、 **_showMeetingTimes** 状態を **false** に設定し、 **_selectedMeetingTime** と **_selectedRoom** 変数を空白にし、 **MyPeople** コレクションを新しく追加して **MeetingTimes** コレクションを更新します。 
  1. **_loadMeetingTimes** 状態を **false** に設定し、 **_showMeetingTimes** を **true** に設定します。

## <a name="meeting-date-picker"></a>ミーティングの日付の選択

   ![MeetingDateSelect コントロール](media/meeting-screen/meeting-datepicker.png)

* プロパティ:**DisplayMode**<br>
    値: `If( IsEmpty(MyPeople), DisplayMode.Disabled, DisplayMode.Edit )`

    少なくとも 1 つの参加者に追加されるまでミーティングの日付を選択することはできません、 **MyPeople**コレクション。

* プロパティ:**OnChange**<br>
    値: `Select( MeetingDateSelect )`

    選択した日付を変更すると、このコントロールの **OnSelect** プロパティのコードが実行されます。

* プロパティ:**OnSelect**<br>
    値:利用可能な会議時間を更新するための **Collect** ステートメントおよびいくつかの変数を更新するステートメント。
  
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

  大まかに言えば、このコントロールを選択すると、利用可能な会議時間が更新されます。 ユーザーが日付を変更した場合、利用可能な会議時間を更新して、その日の出席者の空き時間を反映する必要があるため貴重です。

  初期を除き**収集**ステートメントと同じです、 **OnSelect**の機能、 **AddIcon**コントロール。 そのため、この説明と高さを調整できません。 詳細について読み取り、 [AddIcon コントロール](#add-icon)セクション。

  このコントロールを選択すると、 **TextSearchBox** がリセットされます。 その後: 
  1. セット、 **_loadMeetingTimes**状態**true**と **_showMeetingTimes**状態**false**、空白、 **_selectedMeetingTime**と **_selectedRoom**変数、および更新、 **MeetingTimes**新しい日付を選択した場合のコレクション。 
  1. **_loadMeetingTimes** 状態を **false** に設定し、 **_showMeetingTimes** を **true** に設定します。

## <a name="meeting-duration-drop-down"></a>会議の継続時間ドロップダウン

   ![MeetingDateSelect コントロール](media/meeting-screen/meeting-timepicker.png)

* プロパティ:**DisplayMode**<br>
    値: `If( IsEmpty(MyPeople), DisplayMode.Disabled, DisplayMode.Edit )`

    会議の期間は、少なくとも 1 人の参加者が **MyPeople** コレクションに追加されるまで選択できません。

* プロパティ:**OnChange**<br>
    値: `Select(MeetingDateSelect1)`

    選択された期間を変更するコードでは、トリガー、 **OnSelect**のプロパティ、 **MeetingDateSelect**コントロールを実行します。

## <a name="find-meeting-times-gallery"></a>会議の時間を検索するギャラリー

   ![FindMeetingTimesGallery コントロール](media/meeting-screen/meeting-time-gall.png)

* プロパティ:**Items**<br>
    値: `MeetingTimes`

    [Office365.FindMeetingTimes](https://docs.microsoft.com/connectors/office365/#find-meeting-times) 操作から取得された潜在的な会議時間のコレクション。

* プロパティ:**Visible**<br>
    値: `_showMeetingTimes && _showDetails && !IsEmpty( MyPeople )`

    ギャラリーが表示される場合にのみ **_showMeetingTimes**に設定されている**true**、ユーザーが選択、 **LblScheduleTab**コントロールに追加された少なくとも 1 つの参加者があると、ミーティングです。

### <a name="find-meeting-times-gallery-title"></a>会議の時間を検索するギャラリーのタイトル

   ![FindMeetingTimesGallery タイトル コントロール](media/meeting-screen/meeting-time-gall-title.png)

* プロパティ: **[Text (テキスト)]**<br>
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

  取得した値の**StartTime**が UTC 形式でします。 [UTC から現地時刻に変換する](../functions/function-dateadd-datediff.md#converting-from-utc)、 **DateAdd**関数が適用されます。
  [Text 関数](../functions/function-text.md#datetime)は、最初の引数と 2 番目の引数に基づいての形式として日付/時刻を受け取ります。 ローカル時刻の変換を渡す**ThisItem.StartTime**、として表示**DateTimeFormat.ShortTime**します。

* プロパティ:**OnSelect**<br>
    値:会議室とそれらの推奨される利用可能性を収集するための複数の **Collect** ステートメントおよびいくつかの変数を切り替えるステートメント。

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

  大まかに言えば、このコード ブロックがないユーザーの利用可能なルームを収集部屋、会議の選択した日付/時刻に基づいて、一覧。 それ以外の場合、部屋リストだけを取得します。

  細かく言えば、次のコード ブロックになります。
  1. セット **_selectedMeetingTime**選択された項目にします。 これは、その期間中にどのようなルームが使用可能な検索に使用されます。
  1. 読み込みの設定状態変数 **_loadingRooms**に**true**読み込みの状態を有効にします。
  1. 場合、 **RoomsLists**コレクションが空の場合に保存し、ユーザーのテナントのルームの一覧を取得する、 **RoomsLists**コレクション。
  1. 場合は、ユーザーには、部屋リストまたは 1 つの部屋のリストがあるありません。
      1. **NoRoomLists**に変数が設定されている**true**に表示される項目を決定するこの変数を使用して、 **RoomBrowseGallery**コントロール。
      1. `Office365.GetRooms()`操作は、テナントの最初の 100 個の部屋を取得するために使用します。 格納される、 **AllRooms**コレクション。
      1. **_AllRoomsConcat**の部屋の最初の 20 のメール アドレスのセミコロン区切りの文字列に変数が設定されている、 **AllRooms**コレクション。 これは、ため、 [Office365.FindMeetingTimes](https://docs.microsoft.com/connectors/office365/#find-meeting-times)単一の操作で 20 の person オブジェクトの使用可能な時間の検索に制限されます。
      1. **RoomTimeSuggestions**コレクションは、 [Office365.FindMeetingTimes](https://docs.microsoft.com/connectors/office365/#find-meeting-times)の最初の 20 個の部屋の利用可能性を取得する、 **AllRooms**ベースのコレクション時刻値に、 **_selectedMeetingTime**変数。 なお、`& "Z"`正しく書式設定するために使用、 **DateTime**値。
      1. **AvailableRooms**コレクションが作成されます。 これは単に、 **RoomTimeSuggestions**出席者の利用可能性を追加、2 つの列のコレクション。"Address"と「名前」。 「アドレス」が、部屋の電子メール アドレスと、"Name"は、ルームの名前。
      1. 次に、 **AvailableRoomsOptimal**コレクションが作成されます。 これは単、 **AvailableRooms** 「出席者」と「可用性」の列を含むコレクションを削除します。 スキーマと一致するこの**AvailableRoomsOptimal**と**AllRooms**します。 これを使用すると、両方のコレクションを使用して、**項目**のプロパティ、 **RoomBrowseGallery**します。
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

  このギャラリーが表示されます、 **AvailableRoomsOptimal**コレクション場合 **_roomListSelected**または **_noRoomLists**は**true**します。 それ以外の場合、表示、 **RoomsLists**コレクション。 これは、これらのコレクションのスキーマが同じであるために実行できます。

* プロパティ:**Visible**<br>
    値: ```_showDetails && !IsBlank( _selectedMeetingTime ) && !_loadingRooms```

    ギャラリーは、上記の 3 つのステートメントが **true**と評価された場合のみ表示されます。

### <a name="roombrowsegallery-title"></a>RoomBrowseGallery タイトル

   ![RoomBrowseGallery タイトル コントロール](media/meeting-screen/meeting-rooms-gall-title.png)

* プロパティ:**OnSelect**<br>
    値:論理的にバインドされた **Collect** および **Set** ステートメントのセット。ユーザーが部屋リストまたは部屋のどちらかを表示しているかによって、トリガーされる場合とトリガーされない場合があります。

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

  操作は、ユーザーが部屋のリストのセットまたは一連のルーム表示現在かどうかによって異なります。 このコントロールを選択し、前者の場合、選択した部屋リストから選択した時間で使用できる会議室を取得します。 後者の場合、このコントロールを選択すると設定、 **_selectedRoom**変数を選択した項目に設定されます。 上記のステートメントは、[**FindMeetingTimesGallery Title**](#find-meeting-times-gallery)の **Select** ステートメントに非常に似ています。

  細かく言えば、以下のコード ブロックになります。
  1. **_loadingRooms** を **true** に設定して、部屋の読み込み状態をオンにします。
  1. 部屋リストが選択されているかどうか、およびテナントに部屋リストがあるかどうかを確認します。 その場合；
      1. **_roomListSelected** を **true** に設定して、 **_selectedRoomList**選択された項目に設定します。
      1. **_allRoomsConcat** 変数は、**AllRooms** コレクション内の部屋の最初の 20 個の電子メールアドレスのセミコロン区切り文字列に設定されます。 これは、 [Office365.FindMeetingTimes](https://docs.microsoft.com/connectors/office365/#find-meeting-times) 操作が、 1 回の操作で 20 人のオブジェクトの利用可能な時間を検索することに制限されているためです。
      1. **RoomTimeSuggestions** コレクションは、 [Office365.FindMeetingTimes](https://docs.microsoft.com/connectors/office365/#find-meeting-times) 操作を使用して、 **_selectedMeetingTime** 変数の時間値に基づいて、**AllRooms** コレクションの最初の 20 個の部屋の利用可能性を取得します。 なお`& "Z"` は、**DateTime** 関数を適切にフォーマットするために使用されることに注意してください。
      1. **AvailableRooms** コレクションが作成されます。 これは、出席者の可能性を **RoomTimeSuggestions** コレクションに、「Address」と「Name」の 2 つの列が追加されたものです。 「Address」は部屋のメールアドレスで、「Name」は、部屋の名前です。
      1. 次に、 **AvailableRoomsOptimal** コレクションが作成されます。 これは、「Availability」と「Attendee」列が削除された **AvailableRoomsOptimal** および **AllRooms** スキーマーと一致します。 これにより **RoomBrowseGallery** の **Items** プロパティで両方のコレクションを使用できます。
      1. **_roomListSelected** は **false** に設定されます。
  1. 読み込みの状態、 **_loadingRooms** は、他のすべての実行が完了すると **false** に設定されます。

## <a name="back-chevron"></a>シェブロンをバックアップします。

   ![RoomsBackNav コントロール](media/meeting-screen/meeting-back.png)

* プロパティ:**Visible**<br>
    値: `_roomListSelected && _showDetails`

    このコントロールは、部屋リストが選択され、 **スケジュール** タブが選択されている場合にのみ表示されます。

* プロパティ:**OnSelect**<br>
    値: `Set( _roomListSelected, false )`

    ときに **_roomListSelected**に設定されている**false**、変更、 **RoomBrowseGallery**項目を表示するコントロール、 **RoomsLists**コレクションです。

## <a name="send-icon"></a>[送信] アイコン

   ![IconSendItem コントロール](media/meeting-screen/meeting-send-icon.png)

* プロパティ:**DisplayMode**<br>
    値:アイコンが編集可能になる前に、特定の会議の詳細をユーザーに入力させるロジック。
    
    ```powerapps-dot
    If( Len( Trim( TextMeetingSubject1.Text ) ) > 0
        && !IsEmpty( MyPeople ) && !IsBlank( _selectedMeetingTime ),
        DisplayMode.Edit, DisplayMode.Disabled
    )
    ```
  このアイコンは、会議の件名が入力されており、会議の参加者が少なくとも 1 人いて、会議の時間が選択されている場合にのみ選択できます。 それ以外の場合、無効になります。

* プロパティ:**OnSelect**<br>

    値:選択した参加者に会議招集を送信し、全ての入力フィールドをクリアするコード:

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
> 地域によっては、目的のカレンダーに「カレンダー」という表示名が無い場合があります。 Outlook に移動してカレンダーのタイトルを確認し、アプリで適切な変更を加えます。

## <a name="next-steps"></a>次の手順

* [この画面を詳細します。](./meeting-screen-overview.md)
* [PowerApps での Office 365 Outlook コネクタの詳細します。](../connections/connection-office365-outlook.md)
* [PowerApps での Office 365 Users コネクタの詳細します。](../connections/connection-office365-users.md)

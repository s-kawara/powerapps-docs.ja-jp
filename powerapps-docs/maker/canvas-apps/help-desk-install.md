---
title: Help Desk PowerApps サンプルをインストールして構成する | Microsoft Docs
description: Help Desk PowerApps サンプルをインストールして構成する詳細な手順を示します。
services: ''
suite: powerapps
documentationcenter: na
author: caburk
manager: ''
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/08/2018
ms.author: caburk
ms.openlocfilehash: be5a2f1994a55abf6936ded4dfddf84d145115c5
ms.sourcegitcommit: 4710a56d308efe67fe60a7688143e61f5e5f2b44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/16/2018
---
# <a name="install-and-configure-the-help-desk-powerapps-sample"></a>Help Desk PowerApps サンプルをインストールして構成する

Help Desk PowerApps サンプルをインストールして構成する詳細な手順を示します。

この手順の推定所要時間: **10 - 15 分**

この手順のデモを見たい場合は、次のビデオをご覧ください。

[![Help Desk のインストールのビデオ](./media/help-desk-install/help-desk-install-video.png)](https://youtu.be/z4cdtD6hB_4 )

## <a name="help-desk-powerapps-sample-overview"></a>Help Desk PowerApps サンプルの概要
Help Desk は、手軽な操作でエンド ユーザーをサポート担当者に繋ぐことのできるアプリです。 極めて重要な質問に対する回答をすぐに入手したり、開いたチケットの進捗状況を追跡したりできるほか、以前のリクエストの詳細を確認することも可能です。 このアプリをお使いの環境に合わせるには、少し設定が必要です。

![Help Desk PowerApp の開始画面](./media/help-desk-install/Login-screen.png)

Help Desk PowerApp サンプルの使い方については、次のビデオをご覧ください。

[![Help Desk のデモ ビデオ](./media/help-desk-install/help-desk-demo-video.png)](https://youtu.be/sl5fXwwnvzI)

## <a name="prerequisites"></a>前提条件

- PowerApps に[サインアップ](https://web.powerapps.com/)。

## <a name="create-the-helpdesk-sharepoint-list"></a>HelpDesk (ヘルプデスク) SharePoint リストを作成する

このリストは、Help Desk のチケットを格納します。

1. Web ブラウザーを開き、https://portal.office.com に移動します。
2. リストを作成するアクセス許可を持つアカウントでログインします。
3. HelpDesk (ヘルプデスク) リストを作成するサイト コレクションに移動します。
4. Web ページの右上にある**歯車アイコン**をクリックします。
5. **[アプリの追加]** をクリックします。
6. **[アプリの検索]** ボックスに、「**Custom (カスタム)**」と入力します。
7. **検索アイコン**をクリックします。
8. **[カスタム リスト]** アプリをクリックします。
9. **[名前]** ボックスに、「**HelpDesk (ヘルプデスク)**」と入力します。

    > [!IMPORTANT]
    > リストに別の名前を使う場合は、書き留めておいてください。以降のインストールと構成のプロセスで、HelpDesk (ヘルプデスク) となっているすべての箇所を置き換える必要があります。

10. **[作成]** をクリックします。

### <a name="create-description-column"></a>Description (説明) 列を作成する

1. **[列の作成]** をクリックします。
2. **[列名]** ボックスに「**Description (説明)**」と入力します。
3. **[type of information in this column is]\(この列の情報の種類\)** ラジオ ボタン リストで、**[複数行テキスト]** を選択します。
4. **[Require that this column contains information]\(この列への情報の入力を必須にする\)** ラジオ ボタン リストで、**[はい]** を選択します。
5. **[Specify the type of text to allow]\(使用可能なテキストの種類を指定してください\)** ラジオ ボタン リストで、**[書式なしテキスト]** を選択します。
6. **[OK]** をクリックします。

### <a name="create-category-column"></a>Category (カテゴリ) 列を作成する

1. **[列の作成]** をクリックします。
2. **[列名]** ボックスに「**Category (カテゴリ)**」と入力します。
3. **[type of information in this column is]\(この列の情報の種類\)** ラジオ ボタン リストで、**[選択肢]** を選択します。
4. **[Type each choice on a separate line]\(それぞれの行に選択肢を入力してください\)** ボックスに、次の値をそれぞれ別の行に入力します。 
    - ラップトップ/PC 機器の問題
    - ラップトップ/PC ソフトウェアの問題
5. **[固有の値を適用する]** ラジオ ボタン リストで、**[いいえ]** を選択します。
6. **[選択肢の表示形式]** ラジオ ボタン リストで、**[ドロップダウン メニュー]** を選択します。
7. **[既定値]** ボックスに、「**ラップトップ/PC 機器の問題**」と入力します。
8. **[OK]** をクリックします。

### <a name="create--complete-column"></a>% Complete (完了率) 列を作成する

1. **[列の作成]** をクリックします。
2. **[列名]** ボックスに「**% Complete (完了率)**」と入力します。
3. **[type of information in this column is]\(この列の情報の種類\)** ラジオ ボタン リストで、**[Number (1, 10, 100)]\(数値 (1、1.0、100)\)** を選択します。
4. **[Require that this column contains information]\(この列への情報の入力を必須にする\)** ラジオ ボタン リストで、**[いいえ]** を選択します。
5. **[OK]** をクリックします。

### <a name="create-priority-column"></a>Priority (優先度) 列を作成する

1. **[列の作成]** をクリックします。
2. **[列名]** ボックスに「**Priority (優先度)**」と入力します。
3. **[type of information in this column is]\(この列の情報の種類\)** ラジオ ボタン リストで、**[選択肢]** を選択します。
4. **[Type each choice on a separate line]\(それぞれの行に選択肢を入力してください\)** ボックスに、次の値をそれぞれ別の行に入力します。 
    - 高
    - M
    - 低
5. **[固有の値を適用する]** ラジオ ボタン リストで、**[いいえ]** を選択します。
6. **[選択肢の表示形式]** ラジオ ボタン リストで、**[ドロップダウン メニュー]** を選択します。
7. **[既定値]** ボックスに、「**低**」と入力します。
8. **[OK]** をクリックします。

### <a name="create-taskstatus-column"></a>タスク ステータス列を作成します。

1. **[列の作成]** をクリックします。
2. **[列名]** ボックスに「**TaskStatus (タスク ステータス)**」と入力します。
3. **[type of information in this column is]\(この列の情報の種類\)** ラジオ ボタン リストで、**[選択肢]** を選択します。
4. **[Type each choice on a separate line]\(それぞれの行に選択肢を入力してください\)** ボックスに、次の値をそれぞれ別の行に入力します。 
    - 未開始
    - 進行中
    - 完了
    - 延期
    - CSR 待ち
5. **[固有の値を適用する]** ラジオ ボタン リストで、**[いいえ]** を選択します。
6. **[選択肢の表示形式]** ラジオ ボタン リストで、**[ドロップダウン メニュー]** を選択します。
7. **[既定値]** ボックスに、「**未開始**」と入力します。
8. **[OK]** をクリックします。

### <a name="create-assignedto-column"></a>AssignedTo (担当者) 列を作成する

1. **[列の作成]** をクリックします。
2. **[列名]** ボックスに「**AssignedTo (担当者)**」と入力します。
3. **[type of information in this column is]\(この列の情報の種類\)** ラジオ ボタン リストで、**[ユーザーまたはグループ]** を選択します。
4. **[Require that this column contains information]\(この列への情報の入力を必須にする\)** ラジオ ボタン リストで、**[いいえ]** を選択します。
5. **[複数選択できるようにする]** ラジオ ボタン リストで、**[いいえ]** を選択します。
6. **[OK]** をクリックします。

### <a name="edit-title-column"></a>"タイトル" 列を編集する

1. **[タイトル]** 列のリンクをクリックします。
2. **[Require that this column contains information]\(この列への情報の入力を必須にする\)** ラジオ ボタン リストで、**[いいえ]** を選択します。
3. **[OK]** をクリックします。

## <a name="download-the-help-desk-powerapp"></a>Help Desk PowerApp をダウンロードする

1.  Web ブラウザーで、http://pappsfeprodwestuscontent.blob.core.windows.net/sampleapps/helpdesk/docs/HelpDesk(SP_List).zip に移動します。
2.  PowerApps パッケージをダウンロードし、コンピューターに保存します。

## <a name="create-connections"></a>接続を作成する

1.  Web ブラウザーで、https://web.powerapps.com に移動します。
2.  サインアップに使用したものと同じ資格情報でサインインします。
3.  左側のメニューで **[接続]** を選択します。
    
### <a name="create-office-365-outlook-connection"></a>Office 365 Outlook 接続を作成する

1.  **[+ 新しい接続]** をクリックします。
2.  **[検索]** ボックスに、「**Office 365 Outlook**」と入力します。
3.  一覧で **Office 365 Outlook** を選びます。
4.  **[作成]** をクリックします。
5.  ポップアップ ウィンドウで、ログインに使ったアカウントを選びます。

### <a name="create-sharepoint-connection"></a>SharePoint 接続を作成する

1.  **[+ 新しい接続]** をクリックします。
2.  **[検索]** ボックスに、「**Outlook**」と入力します。
3.  一覧で **SharePoint** を選びます。
4.  **[作成]** をクリックします。
5.  ポップアップ ウィンドウで、ログインに使ったアカウントを選びます。

### <a name="create-office-365-users-connection"></a>Office 365 ユーザー接続を作成する

1.  **[+ 新しい接続]** をクリックします。
2.  **[検索]** ボックスに、「**Office 365 ユーザー**」と入力します。
3.  一覧で **Office 365 ユーザー**を選びます。
4.  **[作成]** をクリックします。
5.  ポップアップ ウィンドウで、ログインに使ったアカウントを選びます。

## <a name="import-the-help-desk-powerapp"></a>Help Desk PowerApp をインポートする

1.  Web ブラウザーで、https://web.powerapps.com に移動します。
2.  サインアップに使用したものと同じ資格情報でサインインします。
3.  左側のメニューで **[アプリ]** を選択します。 
4.  **[パッケージのインポート (プレビュー)]** をクリックします。
    
    ![パッケージ インポート画面](./media/help-desk-install/import-package.png)

5.  **[アップロード]** ボタンをクリックして、前のステップでダウンロードした PowerApp パッケージを選びます。
6.  **[アプリ]** および **[フロー]** リソースの種類で、**[インポートの設定]** を **[新しく作成する]** に設定します。
7.  **SharePoint** と **Outlook** の接続で、**[インポートの設定]** を **[インポート時に選択する]** に設定します。
    
    ![インポート設定画面](./media/help-desk-install/import-settings.png)

8.  **SharePoint 接続**の**赤いアイコン**をクリックします。
9.  接続の一覧で、自分のユーザー名の項目をクリックします。

    ![インポート設定画面](./media/help-desk-install/import-settings-sharepoint.png)

10. **[保存]** をクリックします。
11.  **Office 365 Outlook 接続**の**赤いアイコン**をクリックします。
12.  接続の一覧で、自分のユーザー名の項目をクリックします。

    ![インポート設定画面](./media/help-desk-install/import-settings-office365outlook.png)

13. **[保存]** をクリックします。

    > [!TIP] 
    > 完了すると次のようになります。

    ![インポート設定画面](./media/help-desk-install/import-settings-done.png)

14. **[インポート]** をクリックして、プロセスが完了するまで待ちます。

    ![インポート設定画面](./media/help-desk-install/import-done.png)

## <a name="configure-the-powerapp-to-use-the-sharepoint-list"></a>SharePoint リストを使用するように PowerApp を構成する

1. Web ブラウザーで **[アプリ]** をクリックします。
2. HelpDesk (ヘルプデスク) PowerApp の隣の**省略記号**をクリックします。
3. **[Web で編集]** をクリックします。
4. **[許可]** をクリックします。

### <a name="delete-connections"></a>接続を削除する

1. **[表示]** をクリックします。
2. **[データ ソース]** をクリックします。
3. **[データ]** ウィンドウで、**HelpDesk (ヘルプデスク)** の隣の**省略記号**をクリックします。
4. **[削除]** をクリックします。

### <a name="helpdesk-list"></a>HelpDesk (ヘルプデスク) リスト

1. **[表示]** をクリックします。
2. **[データ ソース]** をクリックします。
3. **[データ]** ウィンドウで、**[+ データ ソースの追加]** をクリックします。
4. **SharePoint** を選びます。
5. **[作成]** をクリックします。
6. **[最近利用したサイト]** 一覧で、HelpDesk (ヘルプデスク) リストを作成した SharePoint サイトを選びます。

    > [!TIP] 
    > サイトが一覧に表示されない場合は、テキスト ボックスに SharePoint サイトの URL を入力し、**[移動]** をクリックします。

7. 一覧の先頭にある **[検索]** ボックスに、「**HelpDesk (ヘルプデスク)**」と入力します。
8. **HelpDesk (ヘルプデスク)** リストのチェック ボックスをオンにします。
9. **[接続]** をクリックします。

### <a name="update-admin-list"></a>管理者一覧を更新する

1. **LoginScreen** を選びます。
2. ドロップダウンで **OnStart** を選びます。
3. 式ウィンドウを展開し、**AdminList** コレクションを探します。
4. **user@microsoft.com** を実際のヘルプデスク管理者に置き換えます。

    ![管理者一覧を更新する](./media/help-desk-install/Change-admin.png)
    
    > [!TIP] 
    > 複数の管理者がいる場合は、コンマを使って区切ります。例: "admin1@microsoft.com","admin2@microsoft.com"。

5. **[ファイル]** をクリックします。
6. **[保存]** をクリックします。
7. **[発行]** をクリックします。
8. **[このバージョンの発行]** をクリックします。

## <a name="modify-the-flow"></a>フローを変更する

1.  左側のメニューで **[フロー]** をクリックします。
2.  サインインを求められたら、サインアップに使用したものと同じ資格情報でサインインします。
3.  上部のメニューで **[マイ フロー]** を選択します。
4.  **HelpDeskFlow** フローの隣の**鉛筆アイコン**をクリックします。 
 
    ![フロー編集画面](./media/help-desk-install/edit-flow.png)

5.  **Get items** アクションを展開します。 
6.  作成した HelpDesk (ヘルプデスク) SharePoint リストと一致するように、**[サイト アドレス]** と **[リスト名]** を変更します。
    
    ![フロー編集画面](./media/help-desk-install/edit-flow-getitems.png)

    > [!TIP] 
    > 手入力する必要はありません。ドロップダウン リストで選択できます。

7.  **Switch** を展開します。
8.  **未開始**ケースを展開します。
9.  **Send an email** アクションを展開します。
10. **[宛先]** をヘルプデスク管理者のメール アドレスに変更します。

    ![フロー編集画面](./media/help-desk-install/edit-flow-condition-send-email.png) 

11. **[フローの更新]** をクリックします。

## <a name="play-the-powerapp"></a>PowerApp を再生する

1. Web ブラウザーで **[アプリ]** をクリックします。
2. HelpDesk (ヘルプデスク) PowerApp の隣の**省略記号**をクリックします。
3. **[開く]** をクリックします。 

Help Desk PowerApp サンプルの使い方については、次のビデオをご覧ください。

[![Help Desk のデモ ビデオ](./media/help-desk-install/help-desk-demo-video.png)](https://youtu.be/sl5fXwwnvzI)

##<a name="next-steps"></a>次の手順
- [SharePoint リスト フォームをカスタマイズ](https://docs.microsoft.com/en-us/powerapps/maker/canvas-apps/customize-list-form)
- [コントロールの追加と構成](https://docs.microsoft.com/en-us/powerapps/maker/canvas-apps/add-configure-controls)
- [SharePoint リストまたはライブラリのアクセス許可の編集と管理](https://support.office.com/en-us/article/edit-and-manage-permissions-for-a-sharepoint-list-or-library-02d770f3-59eb-4910-a608-5f84cc297782)
 

---
title: Expense Report PowerApps サンプルをインストールして構成する | Microsoft Docs
description: Expense Report PowerApps サンプルをインストールして構成する詳細な手順を示します。
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
ms.date: 02/20/2018
ms.author: caburk
ms.openlocfilehash: 0a4c35fe756e6ba9baf899a302d739467e21b591
ms.sourcegitcommit: eac8ad7b54a0b0eba6444a38a952dbfd17bc64b5
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/08/2018
---
# <a name="install-and-configure-the-expense-report-powerapps-sample"></a>Expense Report PowerApps サンプルをインストールして構成する

Expense Report PowerApps サンプルをインストールして構成する詳細な手順を示します。

この手順の推定所要時間: **10 - 15 分**

この手順のデモを見たい場合は、次のビデオをご覧ください。

[![Expense Report インストールのビデオ](./media/expense-report-install/expense-report-install-video.png)](https://youtu.be/DOR28V5kCkw)

## <a name="expense-report-powerapps-sample-overview"></a>Expense Report PowerApps サンプルの概要
経費レポートを提出から承認まで追跡できます。 明細項目を個人の経費として集計し、準備ができたら承認を受けるために送信できます。 このアプリをお使いの環境に合わせるには、少し設定が必要です。

![Expense Report PowerApp の開始画面](./media/expense-report-install/expense-report-powerapp.png)

Expense Report PowerApp サンプルの使い方については、次のビデオをご覧ください。

[![Expense Report インストールのビデオ](./media/expense-report-install/expense-report-demo-video.png)](https://youtu.be/h6E9cdrOvMU)

## <a name="prerequisites"></a>前提条件

- PowerApps に[サインアップ](../signup-for-powerapps.md)。

## <a name="create-the-expenses-sharepoint-list"></a>Expenses (経費) SharePoint リストを作成する

このリストは経費レポートを格納します。

1. Web ブラウザーを開き、https://portal.office.com に移動します。
2. リストを作成するアクセス許可を持つアカウントでログインします。
3. Expenses (経費) リストを作成するサイト コレクションに移動します。
4. Web ページの右上にある**歯車アイコン**をクリックします。
5. **[アプリの追加]** をクリックします。
6. **[アプリの検索]** ボックスに、「**Custom (カスタム)**」と入力します。
7. **検索アイコン**をクリックします。
8. **[カスタム リスト]** アプリをクリックします。
9. **[名前]** ボックスに「**Expenses**」と入力します。

    > [!IMPORTANT]
    > リストに別の名前を使う場合は、書き留めておいてください。以降のインストールと構成のプロセスで、Expenses となっているすべての箇所を置き換える必要があります。

10. **[作成]** をクリックします。

### <a name="create-costcenter-column"></a>CostCenter (コスト センター) 列を作成する

1. **Expenses (経費)** リストをクリックします。
2. Web ページの右上にある**歯車アイコン**をクリックします。
3. **[リストの設定]** をクリックします。
4. **[列の作成]** をクリックします。
5. **[列名]** ボックスに「**CostCenter (コスト センター)**」と入力します。
6. **[type of information in this column is]\(この列の情報の種類\)** ラジオ ボタン リストで、**[選択肢]** を選択します。
7. **[Type each choice on a separate line]\(それぞれの行に選択肢を入力してください\)** ボックスに、次の値をそれぞれ別の行に入力します。 
    - Microsoft
    - Contoso
8. **[既定値]** ボックスに、「**Microsoft**」と入力します。
9. **[OK]** をクリックします。

### <a name="create-comments-column"></a>Comments (コメント) 列を作成する

1. **[列の作成]** をクリックします。
2. **[列名]** ボックスに「**コメント**」と入力します。
3. **[type of information in this column is]\(この列の情報の種類\)** ラジオ ボタン リストで、**[複数行テキスト]** を選択します。
4. **[OK]** をクリックします。

### <a name="create-status-column"></a>Status (状態) 列を作成する

1. **Expenses (経費)** リストをクリックします。
2. Web ページの右上にある**歯車アイコン**をクリックします。
3. **[リストの設定]** をクリックします。
4. **[列の作成]** をクリックします。
5. **[列名]** ボックスに「**Status (状態)**」と入力します。
6. **[type of information in this column is]\(この列の情報の種類\)** ラジオ ボタン リストで、**[選択肢]** を選択します。
7. **[Type each choice on a separate line]\(それぞれの行に選択肢を入力してください\)** ボックスに、次の値をそれぞれ別の行に入力します。 
    - オープン
    - Pending
    - Approved
8. **[既定値]** ボックスに、「**オープン**」と入力します。
9. **[OK]** をクリックします。

### <a name="create-approvername-column"></a>ApproverName (承認者名) 列を作成する

1. **[列の作成]** をクリックします。
2. **[列名]** ボックスに「**Column name (承認者名)**」と入力します。
3. **[type of information in this column is]\(この列の情報の種類\)** ラジオ ボタン リストで、**[ユーザーまたはグループ]** を選択します。
4. **[Require that this column contains information]\(この列への情報の入力を必須にする\)** ラジオ ボタン リストで、**[はい]** を選択します。
5. **[OK]** をクリックします。

### <a name="create-datesubmitted-column"></a>DateSubmitted (提出日) 列を作成する

1. **[列の作成]** をクリックします。
2. **[列名]** ボックスに「**DateSubmitted (提出日)**」と入力します。
3. **[type of information in this column is]\(この列の情報の種類\)** ラジオ ボタン リストで、**[日付と時刻]** を選択します。
4. **[Require that this column contains information]\(この列への情報の入力を必須にする\)** ラジオ ボタン リストで、**[はい]** を選択します。
5. **[OK]** をクリックします。

### <a name="create-startdate-column"></a>StartDate (開始日) 列を作成する

1. **[列の作成]** をクリックします。
2. **[列名]** ボックスに「**StartDate (開始日)**」と入力します。
3. **[type of information in this column is]\(この列の情報の種類\)** ラジオ ボタン リストで、**[日付と時刻]** を選択します。
4. **[Require that this column contains information]\(この列への情報の入力を必須にする\)** ラジオ ボタン リストで、**[はい]** を選択します。
5. **[OK]** をクリックします。

### <a name="create-enddate-column"></a>EndDate (終了日) 列を作成する

1. **[列の作成]** をクリックします。
2. **[列名]** ボックスに「**EndDate (終了日)**」と入力します。
3. **[type of information in this column is]\(この列の情報の種類\)** ラジオ ボタン リストで、**[日付と時刻]** を選択します。
4. **[Require that this column contains information]\(この列への情報の入力を必須にする\)** ラジオ ボタン リストで、**[はい]** を選択します。
5. **[OK]** をクリックします。

## <a name="create-the-line-items-sharepoint-list"></a>Line Items (明細項目) SharePoint リストを作成する

このリストは、経費レポートに関連付けられている明細項目を格納します。

1. Expense (明細項目) リストを作成したサイト コレクションに移動します。
2. Web ページの右上にある**歯車アイコン**をクリックします。
3. **[アプリの追加]** をクリックします。
4. **[アプリの検索]** ボックスに、「**Custom (カスタム)**」と入力します。
5. **検索アイコン**をクリックします。
6. **[カスタム リスト]** アプリをクリックします。
7. **[名前]** ボックスに「**LineItems**」と入力します。

    > [!IMPORTANT] 
    > リストに別の名前を使う場合は、書き留めておいてください。以降のインストールと構成のプロセスで、LineItems となっているすべての箇所を置き換える必要があります。

8. **[作成]** をクリックします。
 
### <a name="create-category-column"></a>Category (カテゴリ) 列を作成する

1. **LineItems (明細項目)** リストをクリックします。
2. Web ページの右上にある**歯車アイコン**をクリックします。
3. **[リストの設定]** をクリックします。
4. **[列の作成]** をクリックします。
5. **[列名]** ボックスに「**Category (カテゴリ)**」と入力します。
6. **[type of information in this column is]\(この列の情報の種類\)** ラジオ ボタン リストで、**[選択肢]** を選択します。
7. **[Type each choice on a separate line]\(それぞれの行に選択肢を入力してください\)** ボックスに、次の値をそれぞれ別の行に入力します。 
    - 食べ物と飲み物
    - 輸送
    - ビジネス ニーズ
8. **[既定値]** ボックスに、「**食べ物と飲み物**」と入力します。
9. **[OK]** をクリックします。

### <a name="create-cost-column"></a>Cost (コスト) 列を作成する

1. **[列の作成]** をクリックします。
2. **[列名]** ボックスに「**Cost (コスト)**」と入力します。
3. **[type of information in this column is]\(この列の情報の種類\)** ラジオ ボタン リストで、**[Number (1, 10, 100)]\(数値 (1、1.0、100)\)** を選択します。
4. **[Require that this column contains information]\(この列への情報の入力を必須にする\)** ラジオ ボタン リストで、**[はい]** を選択します。
5. **[OK]** をクリックします。

### <a name="create-date-column"></a>Date (日付) 列を作成する

1. **[列の作成]** をクリックします。
2. **[列名]** ボックスに「**Date (日付)**」と入力します。
3. **[type of information in this column is]\(この列の情報の種類\)** ラジオ ボタン リストで、**[日付と時刻]** を選択します。
4. **[Require that this column contains information]\(この列への情報の入力を必須にする\)** ラジオ ボタン リストで、**[はい]** を選択します。
5. **[OK]** をクリックします。

### <a name="create-description-column"></a>Description (説明) 列を作成する

1. **[列の作成]** をクリックします。
2. **[列名]** ボックスに「**Description (説明)**」と入力します。
3. **[type of information in this column is]\(この列の情報の種類\)** ラジオ ボタン リストで、**[複数行テキスト]** を選択します。
4. **[Require that this column contains information]\(この列への情報の入力を必須にする\)** ラジオ ボタン リストで、**[はい]** を選択します。
5. **[Specify the type of text to allow]\(使用可能なテキストの種類を指定してください\)** ラジオ ボタン リストで、**[書式なしテキスト]** を選択します。
6. **[OK]** をクリックします。

### <a name="create-reportid-column"></a>ReportID (レポート ID) 列を作成する

1. **[列の作成]** をクリックします。
2. **[列名]** ボックスに「**ReportID (レポート ID)**」と入力します。
3. **[type of information in this column is]\(この列の情報の種類\)** ラジオ ボタン リストで、**[参照 (このサイトにある既存の情報)]** を選択します。
4. **[Require that this column contains information]\(この列への情報の入力を必須にする\)** ラジオ ボタン リストで、**[はい]** を選択します。
5. **[情報の取得先]** ドロップダウン リストで、作成した **Expense (経費)** リストを選びます。
6. **[この列]** ドロップダウン リストで、**ID** を選びます。
7. **[OK]** をクリックします。

### <a name="edit-title-column"></a>"タイトル" 列を編集する

1. **[タイトル]** 列のリンクをクリックします。
2. **[Require that this column contains information]\(この列への情報の入力を必須にする\)** ラジオ ボタン リストで、**[いいえ]** を選択します。
3. **[OK]** をクリックします。

## <a name="download-the-expense-report-powerapp"></a>Expense Report PowerApp をダウンロードする

1.  Web ブラウザーで次のリンクに移動します。

    http://pappsfeprodwestuscontent.blob.core.windows.net/sampleapps/myexpenses/docs/MyExpenses(SP_List).zip。

2.  Expense Report PowerApps サンプル パッケージをダウンロードして、お使いのコンピューターに保存します。

## <a name="create-connections"></a>接続を作成する

1.  Web ブラウザーで、https://web.powerapps.com に移動します。
2.  サインアップに使用したものと同じ資格情報でサインインします。
3.  左側のメニューで **[接続]** を選択します。

### <a name="create-approvals-connection"></a>承認接続を作成する

1.  **[+ 新しい接続]** をクリックします。
2.  **[検索]** ボックスに、「**承認**」と入力します。
3.  一覧で "**承認**" を選びます。
4.  **[作成]** をクリックします。
    
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

## <a name="import-the-expense-report-powerapp"></a>Expense Report PowerApp をインポートする

1.  Web ブラウザーで、https://web.powerapps.com に移動します。
2.  サインアップに使用したものと同じ資格情報でサインインします。
3.  左側のメニューで **[アプリ]** を選択します。 
4.  **[パッケージのインポート (プレビュー)]** をクリックします。
    
    ![パッケージ インポート画面](./media/expense-report-install/import-package.png)

5.  **[アップロード]** ボタンをクリックして、前のステップでダウンロードした PowerApp パッケージを選びます。
6.  **[アプリ]** および **[フロー]** リソースの種類で、**[インポートの設定]** を **[新しく作成する]** に設定します。
7.  **SharePoint** と **Outlook** の接続で、**[インポートの設定]** を **[インポート時に選択する]** に設定します。
    
    ![インポート設定画面](./media/expense-report-install/import-settings.png)

8.  **SharePoint 接続**の**赤いアイコン**をクリックします。
9.  接続の一覧で、自分のユーザー名の項目をクリックします。

    ![インポート設定画面](./media/expense-report-install/import-settings-sharepoint.png)

10. **[保存]** をクリックします。
11. **SharePoint 接続**の**赤いアイコン**をクリックします。
12. 接続の一覧で、自分のユーザー名の項目をクリックします。

    ![インポート設定画面](./media/expense-report-install/import-settings-approvals.png)

13.  **[保存]** をクリックします。
14.  **Office 365 Outlook 接続**の**赤いアイコン**をクリックします。
15.  接続の一覧で、自分のユーザー名の項目をクリックします。

    ![インポート設定画面](./media/expense-report-install/import-settings-office365outlook.png)

16. **[保存]** をクリックします。

    > [!TIP] 
    > 完了すると次のようになります。

    ![インポート設定画面](./media/expense-report-install/import-settings-done.png)

17. **[インポート]** をクリックして、プロセスが完了するまで待ちます。

    ![インポート設定画面](./media/expense-report-install/import-done.png)

## <a name="configure-the-powerapp-to-use-the-sharepoint-lists"></a>SharePoint リストを使用するように PowerApp を構成する

1. Web ブラウザーで **[アプリ]** をクリックします。
2. Expense Report PowerApp の隣の**省略記号**をクリックします。
3. **[Web で編集]** をクリックします。
4. **[許可]** をクリックします。

### <a name="delete-connections"></a>接続を削除する
1. **[表示]** をクリックします。
2. **[データ ソース]** をクリックします。
3. **[データ]** ウィンドウで、**Expenses (経費)** の隣の**省略記号**をクリックします。
4. **[削除]** をクリックします。
5. **[データ]** ウィンドウで、**LineItems (明細項目)** の隣の**省略記号**をクリックします。
6. **[削除]** をクリックします。

### <a name="expenses-list"></a>Expenses (経費) リスト

1. **[表示]** をクリックします。
2. **[データ ソース]** をクリックします。
3. **[データ]** ウィンドウで、**[+ データ ソースの追加]** をクリックします。
4. **[+ 新しい接続]** をクリックします。
5. **SharePoint** を選びます。
6. **[作成]** をクリックします。
7. **[最近利用したサイト]** 一覧で、Expenses (経費) リストを作成した SharePoint サイトを選びます。

    > [!TIP] 
    > サイトが一覧に表示されない場合は、テキスト ボックスに SharePoint サイトの URL を入力し、**[移動]** をクリックします。

8. 一覧の先頭にある **[検索]** ボックスに、「**Expenses**」と入力します。
9. **Expenses (経費)** リストのチェック ボックスをオンにします。
10. **[接続]** をクリックします。

### <a name="lineitems-list"></a>LineItems (明細項目) リスト

1. **[表示]** をクリックします。
2. **[データ ソース]** をクリックします。
3. **[データ]** ウィンドウで、**[+ データ ソースの追加]** をクリックします。
4. **[+ 新しい接続]** をクリックします。
5. **SharePoint** を選びます。
6. **[作成]** をクリックします。
7. **[最近利用したサイト]** 一覧で、LineItems (明細項目) リストを作成した SharePoint サイトを選びます。

    > [!TIP] 
    > サイトが一覧に表示されない場合は、テキスト ボックスに SharePoint サイトの URL を入力し、**[移動]** をクリックします。

8. 一覧の先頭にある **[検索]** ボックスに、「**LineItems**」と入力します。
9. **LineItems (明細項目)** リストのチェック ボックスをオンにします。
10. **[接続]** をクリックします。
11. **[ファイル]** をクリックします。
12. **[保存]** をクリックします。
13. **[発行]** をクリックします。
14. **[このバージョンの発行]** をクリックします。

## <a name="modify-the-flow"></a>フローを変更する

1.  左側のメニューで **[フロー]** をクリックします。
2.  サインインを求められたら、サインアップに使用したものと同じ資格情報でサインインします。
3.  上部のメニューで **[マイ フロー]** を選択します。
4.  **ApproveExpense** フローの隣の**鉛筆アイコン**をクリックします。
 
    ![フロー編集画面](./media/expense-report-install/edit-flow.png)

5.  **Get items** アクションを展開します。 
6.  作成した Expense (経費) SharePoint リストと一致するように、**[サイト アドレス]** と **[リスト名]** を変更します。
    
    ![フロー編集画面](./media/expense-report-install/edit-flow-getitems.png)

    > [!TIP] 
    > 手入力する必要はありません。ドロップダウン リストで選択できます。

7.  **Condition** を展開します。
8.  **If yes** セクションを展開します。
9.  **Change item status to Approved** アクションを展開します。
10. 作成した Expense (経費) SharePoint リストと一致するように、**[サイト アドレス]** と **[リスト名]** を変更します。

    ![フロー編集画面](./media/expense-report-install/edit-flow-condition-ifyes.png) 

    > [!TIP] 
    > 手入力する必要はありません。ドロップダウン リストで選択できます。

11. **If no** セクションを展開します。
12. **Change item status to Open** アクションを展開します。
13. 作成した Expense (経費) SharePoint リストと一致するように、**[サイト アドレス]** と **[リスト名]** を変更します。 

    ![フロー編集画面](./media/expense-report-install/edit-flow-condition-ifno.png)

    > [!TIP] 
    > 手入力する必要はありません。ドロップダウン リストで選択できます。

14. **[フローの更新]** をクリックします。

## <a name="play-the-powerapp"></a>PowerApp を再生する

1. Web ブラウザーで **[アプリ]** をクリックします。
2. Expense Report PowerApp の隣の**省略記号**をクリックします。
3. **[開く]** をクリックします。

Expense Report PowerApp サンプルの使い方については、次のビデオをご覧ください。

[![Expense Report インストールのビデオ](./media/expense-report-install/expense-report-demo-video.png)](https://youtu.be/h6E9cdrOvMU)






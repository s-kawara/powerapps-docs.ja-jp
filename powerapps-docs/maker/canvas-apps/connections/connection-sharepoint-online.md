---
title: SharePoint 接続の概要 | Microsoft Docs
description: SharePoint の機能、応答、例などの説明を見る
documentationcenter: ''
author: sarafankit
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: reference
ms.component: canvas
ms.date: 07/12/2017
ms.author: ankitsar
ms.openlocfilehash: fe6017ee402f0026aab3ef281a02b472b6a503ad
ms.sourcegitcommit: 8bd4c700969d0fd42950581e03fd5ccbb5273584
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="connect-to-sharepoint-from-powerapps"></a>PowerApps から SharePoint に接続する
![SharePoint](./media/connection-sharepoint-online/sharepointicon.png)

SharePoint サイトに接続して、リストからのアプリの自動生成、アプリのゼロからの作成、または既存アプリの更新を行います。

## <a name="known-issues"></a>既知の問題
カスタム リストからはデータを追加できますが、ライブラリからは追加できません。 また、一部の種類の列はサポートされておらず、列の中には一部の種類のカードしかサポートしていないものもあります。

| 列の種類 | サポート | 既定のカード |
| --- | --- | --- |
| 1 行テキスト |はい |テキストの表示 |
| 複数行テキスト |はい |View text |
| 選択肢 |はい |ルックアップの表示<br>ルックアップの編集<br>複数選択の表示<br>複数選択の編集 |
| Number |はい |パーセンテージの表示<br>評価の表示<br>View text |
| 通貨 |はい |パーセンテージの表示<br>評価の表示<br>View text |
| 日付と時刻 |はい |View text |
| ルックアップ |はい |ルックアップの表示<br>ルックアップの編集<br>複数選択の表示<br>複数選択の編集 |
| ブール値 (はい/いいえ) |はい |View text<br>トグルの表示 |
| 人物またはグループ |はい |ルックアップの表示<br>ルックアップの編集<br>複数選択の表示<br>複数選択の編集 |
| ハイパーリンク |はい |URL の表示<br>View text |
| 画像 |はい (読み取り専用) |画像の表示<br>View text |
| 添付ファイル |はい (読み取り専用) |添付ファイルの表示|
| 集計値 |はい (読み取り専用) | |
| タスクの結果 |いいえ | |
| 外部データ |いいえ | |
| 管理されたメタデータ |はい (読み取り専用) | |
| 評価 |いいえ | |

スペースを含む列を PowerApps で読み取ることはできますが、スペースは 16 進数のエスケープ コード **"\_x0020\_"** に置き換えられます。 たとえば、SharePoint の **"Column Name"** は、PowerApps のデータ レイアウトに表示されるときや数式で使用されるときは **"Column_x0020_Name"** と表示されます。

## <a name="prerequisites"></a>前提条件
次の手順の*どちらか*を実行して、PowerApps を開きます。

* PowerApps に[サインアップ](../../signup-for-powerapps.md)し、[PowerApps Studio for Windows をインストール](http://aka.ms/powerappsinstall)して開きます。その後、サインアップに使用したものと同じ資格情報を入力してサインインします。

* ブラウザーで [PowerApps Studio for the web を開き](https://create.powerapps.com/api/start)ます。

    PowerApps Studio for the web のプレビュー リリースでサポートされているブラウザーと制限の一覧については、「[Create or edit apps in a browser (ブラウザーでのアプリの作成または編集)](../create-app-browser.md)」を参照してください。

## <a name="create-an-app"></a>アプリを作成する
* SharePoint のリストのデータに基づいて[アプリを自動的に生成](../app-from-sharepoint.md)します。

    生成されたアプリには、レコードの閲覧用、レコードの詳細の表示用、レコードの作成/更新用の 3 つの画面が既定で存在します。 アプリの生成後、[閲覧画面](../customize-layout-sharepoint.md)、[詳細画面、編集画面](../customize-forms-sharepoint.md)などをニーズに合わせてカスタマイズする必要のある場合があります。

    **注**: SharePoint のリストに**選択肢**、**ルックアップ**、または**ユーザーまたはグループ**列が含まれている場合は、このトピックの後半にある「[ギャラリーのデータの表示](connection-sharepoint-online.md#show-data-in-a-gallery)」をご覧ください。

* 独自のアプリをゼロから作成するには、[SharePoint に接続](../connect-to-sharepoint.md)し、「[Create an app from scratch (アプリを最初から作成する)](../get-started-create-from-blank.md)」で考え方を確認してから、Excel ではなく SharePoint にその考え方を応用します。

## <a name="add-a-sharepoint-list-to-an-existing-app"></a>既存のアプリに SharePoint リストを追加する
1. PowerApps Studio で、更新するアプリを開きます。

2. リボンの **[ビュー]** タブで、**[データ ソース]** をクリックまたはタップします。

3. 右側のウィンドウで **[データ ソースの追加]** をクリックまたはタップします。

    ![データ ソースの追加](./media/connection-sharepoint-online/add-data-source.png)

4. **[新しい接続]**、**[SharePoint]**、**[接続]** の順にクリックまたはタップします。

    ![SharePoint 接続の追加](./media/connection-sharepoint-online/add-sharepoint.png)

5. 接続する SharePoint サイトの種類を指定します。

    ![接続の種類の指定](./media/connection-sharepoint-online/choose-type.png)

   * SharePoint Online に接続する場合は **[直接接続 (クラウド サービス)]** をクリックまたはタップします。

   * オンプレミスの SharePoint サイトに接続する場合は、**[オンプレミス データ ゲートウェイを使用する接続]** をクリックまたはタップします。

       認証の種類として **[Windows]** を指定し、資格情報を入力します  (資格情報にドメイン名が含まれる場合は、*<ドメイン>\<エイリアス>* 形式で入力します)。

       ![資格情報の指定](./media/connection-sharepoint-online/specify-creds.png)

       **注**: オンプレミス データ ゲートウェイがインストールされていない場合は[インストール](../gateway-reference.md)してから、ゲートウェイの一覧を更新するアイコンをクリックまたはタップします。

       **[ゲートウェイの選択]** で、使用するゲートウェイをクリックまたはタップします。

       ![ゲートウェイの選択](./media/connection-sharepoint-online/choose-gateway.png)

6. **[接続]** をクリックまたはタップします。

7. **[SharePoint サイトに接続]** で、**[最近使ったサイト]** のエントリをクリックまたはタップし (または使用するサイトの URL を入力または貼り付けて)、**[Go]\(移動)** をクリックします。

    ![SharePoint サイトの選択](./media/connection-sharepoint-online/select-sp-site.png)

8. **[一覧の選択]** で、使用する一覧 (複数可) のチェックボックスをオンにして、**[接続]** をクリックまたはタップします。  

    ![SharePoint のテーブルの選択](./media/connection-sharepoint-online/select-sp-tables.png)

    すべての種類のリストが既定で表示されるわけではありません。 使用する目的のリストの名前が表示されていない場合は、一番下までスクロールし、**[カスタム リスト名を入力]** と示されているボックスにリストの名前を入力します。

    ![SharePoint のカスタム リスト](./media/connection-sharepoint-online/custom-list.png)

    データ ソースがアプリに追加されます。

    ![アプリに追加されたデータ ソースの一覧](./media/connection-sharepoint-online/data-sources-list.png)

## <a name="show-data-in-a-gallery"></a>ギャラリーのデータの表示
ギャラリーに含まれる次の種類の列のデータを表示するには、数式バーを使用して、そのギャラリーの**ラベル** コントロール (複数可) の **Text** プロパティを設定します。

* **選択肢**または**ルックアップ**列のデータを表示するには、「**ThisItem.[列名].Value**」と指定します。

    たとえば、**Location** という名前の**選択肢**列がある場合は「**ThisItem.Location.Value**」と指定し、**PostalCode** という名前の**ルックアップ**列がある場合は「**ThisItem.PostalCode.Value**」と指定します。

* **ユーザーまたはグループ**列のユーザーまたはグループの名前を表示するには、「**ThisItem.[列名].DisplayName**」と指定します。

    たとえば、**Manager** という名前の**ユーザーまたはグループ**列の名前を表示する場合は、「**ThisItem.Manager.DisplayName**」と指定します。

    メール アドレスや役職など、ユーザーに関する別の情報を表示することもできます。 オプションの全一覧を表示するには、**ThisItem.[列名].** と指定します (末尾はピリオド)。

    **注**: **CreatedBy** 列のリストの項目を作成したユーザーの表示名を表示するには、「**ThisItem.Author.DisplayName**」と指定します。 **ModifiedBy** 列のリストの項目を変更したユーザーの表示名を表示するには、「**ThisItem.Editor.DisplayName**」と指定します。

* **管理されたメタデータ**列のデータを表示するには、「**ThisItem.[列名].Label**」と指定します。

    たとえば、**Languages** という名前の **管理されたメタデータ**列がある場合は「**ThisItem.Languages.Label**」と指定します。

## <a name="next-steps"></a>次の手順
* [データ ソースからデータを表示する方法](../add-gallery.md)を学習する。
* [詳細を表示する方法とレコードを作成または更新する方法](../add-form.md)を学習する。
* 接続できる他の種類の[データ ソース](../connections-list.md)を確認する。

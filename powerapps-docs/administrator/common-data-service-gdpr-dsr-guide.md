---
title: DSR による Common Data Service (CDS) for Apps の顧客データに対する要求への応答 | Microsoft Docs
description: DSR による Common Data Service (CDS) for Apps の顧客データに対する要求への応答方法のチュートリアルです
author: jamesol-msft
ms.reviewer: paulliew
manager: kfile
ms.service: powerapps
ms.component: pa-admin
ms.topic: conceptual
ms.date: 04/23/2018
ms.author: jamesol
ms.openlocfilehash: ef5d646e30f5d09dbfe5f111a3ad018b030f79d9
ms.sourcegitcommit: b3b6118790d6b7b4285dbcb5736e55f6e450125c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2018
---
# <a name="responding-to-data-subject-rights-dsr-requests-for-common-data-service-for-apps-customer-data"></a>データ主体の権利 (DSR) による Common Data Service for Apps の顧客データに対する要求への応答

## <a name="introduction-to-dsr-requests"></a>DSR 要求の概要
欧州連合 (EU) の一般データ保護規則 (GDPR) は、規制において "*データ主体*" と呼ばれる人に、雇用主または他の種類の機関や組織 ("*データ コントローラー*" または単に "*コントローラー*" と呼ばれます) によって収集された個人データを管理する権限を与えます。 GDPR での個人データは、識別された自然人または識別可能な自然人に関連するすべてのデータと、非常に幅広く定義されています。 GDPR では、データ主体には個人データに関して次のことを行う権利が与えられています。

* コピーを取得する
* 修正を要求する
* 処理を制限する
* 削除する
* 別のコントローラーに移動できるように電子的な形式で受け取る

データ主体がコントローラーに対して個人データへの操作を実行するよう正式に要求することを、データ主体の権利 (DSR) 要求と呼びます。

この記事では、Microsoft が GDPR のために準備していることの説明、PowerApps、Microsoft Flow、Common Data Service (CDS) for Apps の使用時に GDPR コンプライアンスをサポートするためにお客様が実行できる手順の例を示します。 コントローラーのお客様が DSR 要求に対応して Microsoft クラウド内の個人データを検索、アクセス、操作するときに役立つ、Microsoft の製品、サービス、管理ツールの使用方法について説明します。

この記事では次の操作について説明されています。

* **検出** — 検索および検出ツールを使用して、DSR 要求の対象である可能性がある顧客データを簡単に検索します。 可能性のある応答ドキュメントが収集されると、以下の 1 つ以上の DSR アクションを実行して、要求に応答できます。 または、DSR 要求への応答に関する組織のガイドラインを要求が満たしていないと判断する場合もあります。

* **アクセス** — Microsoft のクラウドに存在する個人データを取得し、要求された場合は、データ主体が使用可能なそのデータのコピーを作成します。

* **修正** — 必要に応じて、個人データを変更するか、個人データに対して他の要求されたアクションを実施します。

* **制限** — さまざまなオンライン サービスに対するライセンスを削除するか、または可能な場合は目的のサービスをオフにすることで、個人データの処理を制限します。 また、Microsoft のクラウドからデータを削除して、オンプレミスの場所や別の場所にデータを保持することもできます。

* **削除** — Microsoft のクラウドに存在する個人データを完全に削除します。

* **エクスポート** — 個人データの (コンピューターが判読できる形式の) 電子コピーを、データ主体に提供します。

## <a name="cds-for-apps-customer-data"></a>CDS for Apps 顧客データ

> [!IMPORTANT]
> CDS for Apps と Common Data Service の旧バージョンの両方に適用されます

CDS for Apps と、旧バージョンの Common Data Service (CDS) では、個人データとやり取りするプロセスが異なります。

どちらの種類の CDS 環境を使用しているかを確認するには、[PowerApps](https://web.powerapps.com) にログインして、以下の手順のようにします。

1. **[環境]** ドロップダウン リストで、お使いの環境を選びます。
2. ナビゲーション ウィンドウで、**[データ]**、**[エンティティ]** の順にクリックまたはタップします。

    次のエンティティが一覧に表示される場合、お使いの環境は CDS for Apps です。

    ![PowerApps のエンティティ一覧](./media/common-data-service-gdpr-dsr-guide/powerapps-entities-list.png)

    次のエンティティが一覧に表示される場合、以前のバージョンの CDS です。

    ![PowerApps レガシのエンティティ一覧](./media/common-data-service-gdpr-dsr-guide/powerapps-legacy-entities-list.png)

お使いの CDS 環境の種類を確認した後、以下のセクションの手順に従って、個人データを識別します。

> [!NOTE]
> CDS for Apps の環境と旧バージョンの CDS の環境が混在する場合があり、そのときは組織内の環境ごとに以下のプロセスを繰り返す必要があります。

## <a name="user-personal-data-in-cds-for-apps"></a>CDS for Apps でのユーザーの個人データ

### <a name="prerequisites"></a>前提条件
Office 365 管理センターでユーザーを作成し、適切なユーザー ライセンスおよびセキュリティ ロールを割り当てると、ユーザーは CDS for Apps にアクセスして使用できるようになります。

標準のユーザー個人データ (ユーザー名、ユーザー ID、電話番号、メール アドレス、住所など) は、Office 365 管理センターで保持および管理されています。 システム管理者は Office 365 管理センターでのみこの個人データを更新でき、データはすべての環境において CDS for Apps システムのユーザー エンティティに同期されます。 また、システム管理者は、カスタム属性を作成して、CDS for Apps システムのユーザー エンティティ内で追加のユーザー個人データをキャプチャすることもでき、その場合は属性を手動で維持および管理します。

組織の運営にとって重要なビジネス アプリケーションが中断しないようにするため、ユーザーが Office 365 管理センターから削除された場合でも、CDS for Apps システムのユーザー エンティティからユーザーのレコードが自動的に削除されることはありません。 CDS for Apps でのユーザーの状態は無効に設定されますが、CDS for Apps のシステム管理者はアプリケーション内で CDS for Apps からユーザーの個人データを探して削除する必要があります。

Office 365 の全体管理者と CDS のシステム管理者だけが、以下で説明する検出、修正、エクスポート、削除のアクションを実行できます。

### <a name="discover"></a>Discover
システム管理者は、複数の CDS for Apps インスタンスを作成できます。 これらのインスタンスは、試用、開発、または運用に使用できます。 これらの各インスタンスが、システム管理者によって追加されたカスタム属性を含むシステム ユーザー エンティティのコピーと、Office 365 管理センターから同期されたユーザー個人データを保持しています。

システム管理者は、PowerApps 管理センターから Dynamics 365 管理センターに移動することで、すべての CDS for Apps インスタンスの一覧を検索できます。

[PowerApps 管理センター](https://admin.powerapps.com/)から次のことを行います。

1. ナビゲーション ウィンドウで、**[環境]** をクリックまたはタップし、一覧から環境を選びます。

3.  **[Dynamics 365 管理センター]** をクリックまたはタップします。

    ![PowerApps 環境の詳細](./media/common-data-service-gdpr-dsr-guide/powerapps-environment-details.png)

    すべてのインスタンスの一覧が表示されます。

    ![PowerApps インスタンス ピッカー](./media/common-data-service-gdpr-dsr-guide/powerapps-instance-picker.png)

次のリソース内の CDS for Apps ユーザーから個人データが見つかります。

|リソース | 目的 | Web サイト アクセス | プログラムによるアクセス
| --- | --- | --- | ---
| エンティティ レコード | システム ユーザー エンティティと呼ばれ、ユーザーの個人データを格納します。 | [PowerApps 管理センター](https://admin.powerapps.com) | [Web API](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/webapi/update-delete-entities-using-web-api#basic-update) を使用
| 監査履歴 | ユーザーがエンティティ レベルで作成、アクセス、変更、または削除したリソースを、顧客が識別できるようにします。 | [PowerApps 管理センター](https://admin.powerapps.com) | [Web API](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/webapi/update-delete-entities-using-web-api#basic-update) を使用

#### <a name="user"></a>User
ユーザーの個人データは Azure Active Directory に格納されて、すべての CDS for Apps 環境に自動的に同期されます。 ユーザーがアクティブになっている間は、システム管理者は CDS for Apps 内でこの個人データを直接更新することはできません。Office 365 管理センター内からデータを更新する必要があります。 システム管理者は CDS for Apps に個人データ (たとえば、カスタム属性) を直接追加できますが、このデータは手動で管理する必要があります。

ユーザーとその個人データを検索するには、[PowerApps 管理センター](https://admin.powerapps.com/)に移動して、次のようにします。

1. ナビゲーション ウィンドウで、**[環境]** をクリックまたはタップし、一覧から環境を選びます。

2. **Dynamics 365 管理センター**をクリックまたはタップして、一覧から環境を選択し、**[開く]** をクリックまたはタップします。

3. **[設定]** > **[セキュリティ]** > **[ユーザー]** の順に移動します。

4. **[検索]** ボックスにユーザーの名前を入力し、**[検索]** をクリックまたはタップします。

5. ユーザーの個人データを表示するには、ユーザーの名前をダブルクリックまたはダブルタップします。

    ![PowerApps のユーザー フォーム](./media/common-data-service-gdpr-dsr-guide/powerapps-user-form.png)

#### <a name="audit-history"></a>監査履歴
CDS for Apps でエンティティの[監査の追跡](https://docs.microsoft.com/dynamics365/customer-engagement/admin/audit-data-user-activity)が有効になっていると、ユーザーの個人データはユーザーが実行するアクションと共に監査履歴に記録されます。

### <a name="rectify"></a>修正
データ主体から組織のデータに存在する個人データの修正を要求された場合、管理者と組織は要求に応えるのが適切かどうかを判断する必要があります。 データの修正には、ドキュメントまたは他の種類のアイテムに含まれる個人データの編集、改訂、削除が含まれる場合があります。

Azure Active Directory を使って、CDS for Apps 内のユーザーの ID (個人データ) を管理することができます。 企業の顧客は、特定の Microsoft サービ内の限られた編集機能を使って、DSR 修正要求を管理することができます。 データ プロセッサとしての Microsoft は、システムによって生成されたログを修正する機能を提供していません。ログは実際のアクティビティを反映しており、Microsoft のサービス内でのイベントの履歴レコードを構成しているためです。 詳細については、「[GDPR: Data Subject Requests (DSRs)](https://servicetrust.microsoft.com/ViewPage/GDPRDSR)」(GDPR: データ主体の要求 (DSR)) をご覧ください。

Azure Active Directory からユーザー レコードが削除されると、システム管理者はすべてのインスタンスからそのユーザーに関連する残りの個人データ (カスタム属性など) を削除できます。  

### <a name="export"></a>エクスポート

#### <a name="system-user"></a>システム ユーザー
管理センター内のユーザー一覧から Excel にシステムのユーザー エンティティに格納されているユーザーの個人データをエクスポートすることができます。

[PowerApps 管理センター](https://admin.powerapps.com/)から次のことを行います。

1. ナビゲーション ウィンドウで、**[環境]** をクリックまたはタップし、一覧から環境を選びます。

2. **Dynamics 365 管理センター**をクリックまたはタップして、一覧から環境を選択し、**[開く]** をクリックまたはタップします。

3. **[設定]** > **[セキュリティ]** に移動し、**[Enabled Users View]\(有効なユーザー ビュー\)** を選びます。

4. **[Excel にエクスポート]** をクリックします。

#### <a name="audit-history"></a>監査履歴
管理センター内から監査履歴のスクリーンショットを取得できます。

[PowerApps 管理センター](https://admin.powerapps.com/)から次のことを行います。

1. ナビゲーション ウィンドウで、**[環境]** をクリックまたはタップし、一覧から環境を選びます。

2. **Dynamics 365 管理センター**をクリックまたはタップして、一覧から環境を選択し、**[開く]** をクリックまたはタップします。

3. **[設定]** > **[監査]** に移動して、**[監査概要ビュー]** を選びます。

    ![PowerApps の監査履歴メニュー](./media/common-data-service-gdpr-dsr-guide/powerapps-audit-history-menu.png)

4. ユーザーの監査レコードを探し、Alt + PrtScn キーを押してスクリーンショットを取得します。

    ![PowerApps の監査履歴の詳細](./media/common-data-service-gdpr-dsr-guide/powerapps-audit-history-details.png)

5. スクリーンショットをファイルに保存します。保存したファイルは、DSR の要求元に送信できます。

### <a name="delete"></a>削除

#### <a name="user"></a>User
組織の運営にとって重要なビジネス アプリケーションが中断しないようにするため、ユーザーが Office 365 管理センターから削除された場合でも、CDS for Apps システムのユーザー エンティティからユーザーのレコードが自動的に削除されることはありません。 CDS for Apps でのユーザーの状態は無効に設定されますが、CDS for Apps のシステム管理者はアプリケーション内で CDS for Apps からユーザーの個人データを探して削除する必要があります。

#### <a name="remove-a-users-personal-data-from-the-users-summary-page"></a>ユーザーの [概要] ページからユーザーの個人データを削除する
Azure Active Directory からユーザー レコードが削除されると、ユーザーの [概要] ページに次のメッセージが表示されます。

*このユーザーの情報は、Office 365 では管理されなくなっています。このレコードを更新し、このユーザーに関連付けられているすべての個人データを削除または置換することにより、DSR 要求に応えることができます。*

[PowerApps 管理センター](https://admin.powerapps.com/)から次のことを行います。

1. ナビゲーション ウィンドウで、**[環境]** をクリックまたはタップし、一覧から環境を選びます。

2. **Dynamics 365 管理センター**をクリックまたはタップして、一覧から環境を選択し、**[開く]** をクリックまたはタップします。

3. **[設定]** > **[セキュリティ]** > **[ユーザー]** に移動し、**[Disabled Users View]\(無効なユーザー ビュー\)** を選びます。

4. **[検索]** ボックスにユーザーの名前を入力し、**[検索]** をクリックまたはタップします。

9. 検索結果の一覧でユーザーの名前をダブルクリックします。

10. ユーザーの [概要] ページですべての個人データを削除して、**[保存]** をクリックまたはタップします。

#### <a name="remove-a-users-personal-data-by-using-excel"></a>Excel を使用してユーザーの個人データを削除する
[PowerApps 管理センター](https://admin.powerapps.com/)から次のことを行います。

1. ナビゲーション ウィンドウで、**[環境]** をクリックまたはタップし、一覧から環境を選びます。

2. **Dynamics 365 管理センター**をクリックまたはタップして、一覧から環境を選択し、**[開く]** をクリックまたはタップします。

3. **[設定]** > **[セキュリティ]** > **[ユーザー]** に移動し、**[Disabled Users View]\(無効なユーザー ビュー\)** を選びます。

4. ユーザーの個人データから Excel テンプレート ファイルを作成してダウンロードします。 手順については、「[新しい Excel テンプレートの作成](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/admin/analyze-your-data-with-excel-templates#create-a-new-excel-template)」をご覧ください。

8. ダウンロードした Excel テンプレート ファイルを開き、ユーザーの個人データを削除して、ファイルを保存します。

9. **[Disabled Users View]\(無効なユーザー ビュー\)** ウィンドウに戻り、**[データのインポート]** をクリックまたはタップします。

10. **[データ ファイルのアップロード]** ダイアログ ボックスで Excel テンプレート ファイルを選択し、**[フィールドのマップ]** ウィンドウですべての必要な変更を行います。

12. **[次へ]** をクリックまたはタップしてから、**[送信]** をクリックまたはタップします。

#### <a name="remove-audit-history-from-the-audit-summary-view-page"></a>[監査概要ビュー] ページで監査履歴を削除する
[PowerApps 管理センター](https://admin.powerapps.com/)から次のことを行います。

1. ナビゲーション ウィンドウで、**[環境]** をクリックまたはタップし、一覧から環境を選びます。

2. **Dynamics 365 管理センター**をクリックまたはタップして、一覧から環境を選択し、**[開く]** をクリックまたはタップします。

3. **[設定]** > **[監査]** に移動して、**[監査概要ビュー]** を選びます。

4. ユーザーの変更履歴を検索し、行の横にあるチェック ボックスをオンにして、**[変更履歴を削除します]** をクリックまたはタップします。

## <a name="personal-data-stored-in-databases-of-cds-for-apps"></a>CDS for Apps のデータベースに格納されている個人データ

### <a name="prerequisites"></a>前提条件
ユーザー (顧客など) からの個人データを CDS for Apps のエンティティに保存することができます。  

CDS のシステム管理者は、DSR の要求に応答してデータを特定できるように、各ユーザーのさまざまなエンティティ内で個人データが格納されている場所のインベントリを管理する責任があります。  

そうすれば、製品内の機能を使って、エンティティの個人データをエクスポート、修正、削除することができます。  

### <a name="discover"></a>Discover
CDS のシステム管理者は、ユーザーから DSR 要求を受け取ったら、そのユーザーの個人データが含まれる環境/CDS インスタンスを識別する必要があります。 通常、個人データは主要なエンティティ (アカウント、連絡先、リード、営業案件など) に格納されますが、管理者は、DSR 要求に応答できるように、各ユーザーの個人データが格納されている場所のインベントリを管理するためのポリシーと手順を作成する必要があります。

インベントリを使用することで、CDS システム管理者は、検索エンティティとフィールドを構成し、CDS for Apps 環境にアクセスして個人データを探索することができます。 詳細については、「[組織の関連性検索の構成](https://go.microsoft.com/fwlink/?linkid=872506)」をご覧ください。

[PowerApps 管理センター](https://admin.powerapps.com/)から次のことを行います。

1. ナビゲーション ウィンドウで、**[環境]** をクリックまたはタップし、一覧から環境を選びます。

2. **Dynamics 365 管理センター**をクリックまたはタップして、一覧から環境を選択し、検索ボタンをクリックまたはタップして、**[関連性検索]** をクリックまたはタップします。

    ![PowerApps の [関連性の検索] メニュー](./media/common-data-service-gdpr-dsr-guide/powerapps-relevance-search-menu.png)

3. 検索ボックスにユーザーの個人データを入力して、**[検索]** をクリックまたはタップします。

    ![PowerApps の関連性検索の結果](./media/common-data-service-gdpr-dsr-guide/powerapps-relevance-search-results.png)

### <a name="rectify"></a>修正
CDS のシステム管理者は、関連性検索の結果のリストを使用して、ユーザーの個人データを更新できます。 ただし、ユーザーの個人データは他のカスタム エンティティに格納されている場合もあります。 CDS システム管理者は、これらの他のカスタム エンティティのインベントリを維持し、ユーザーの個人データを適切に更新する責任があります。

関連性検索の結果から次のようにします。

1. ユーザーの個人データが含まれる項目をタップまたはクリックします。

2. 必要に応じて、ユーザーの個人データを更新し、**[保存]** をクリックまたはタップします。

    ![PowerApps アカウントの詳細](./media/common-data-service-gdpr-dsr-guide/powerapps-account-details.png)

### <a name="export"></a>エクスポート
データのスクリーンショットを取得し、DSR の要求元と共有することができます。

[PowerApps 管理センター](https://admin.powerapps.com/)から次のことを行います。

1. ナビゲーション ウィンドウで、**[環境]** をクリックまたはタップし、一覧から環境を選びます。

2. **Dynamics 365 管理センター**をクリックまたはタップして、一覧から環境を選択し、検索ボタンをクリックまたはタップして、**[関連性検索]** をクリックまたはタップします。

    ![PowerApps の [関連性の検索] メニュー](./media/common-data-service-gdpr-dsr-guide/powerapps-relevance-search-menu.png)

3. 検索ボックスにユーザーの個人データを入力して、**[検索]** をクリックまたはタップします。

    ![PowerApps の関連性検索の結果](./media/common-data-service-gdpr-dsr-guide/powerapps-relevance-search-results.png)

4. 検索結果の一覧で項目をダブルクリックします。

5. Alt + PrtScn キーを押して、スクリーンショットを取得します。

6. スクリーンショットをファイルに保存します。保存したファイルは、DSR の要求元に送信できます。

### <a name="delete"></a>削除
CDS システム管理者は、ユーザーの個人データを、そのデータが格納されているレコードから削除できます。  CDS システム管理者は、個人データが格納されているレコードを削除するか、またはレコードから個人データの内容を削除するかを選択できます。  

> [!NOTE]
> CDS 管理者は、レコードがエンティティから削除されないように、環境をカスタマイズできます。 このように構成されている場合は、レコード自体を削除するのではなく、レコードから個人データの内容を削除する必要があります。

関連性検索の結果から次のようにします。

1. ユーザーの個人データが含まれる項目をタップまたはクリックします。

2. リボンの **[削除]** をクリックまたはタップします (レコードを削除できない場合、**[削除]** は無効になっていることに注意してください)。

    ![PowerApps アカウントの削除](./media/common-data-service-gdpr-dsr-guide/powerapps-account-delete.png)

## <a name="personal-data-stored-in-databases-of-the-previous-version-of-cds"></a>旧バージョンの CDS のデータベースに格納されている個人データ

### <a name="prerequisites"></a>前提条件
ユーザー (顧客など) からの個人データを CDS のエンティティに保存することができます。  

CDS のシステム管理者は、DSR の要求に応答してデータを特定できるように、各ユーザーのさまざまなエンティティ内で個人データが格納されている場所のインベントリを管理する責任があります。  

そうすれば、製品内の機能を使って、エンティティの個人データをエクスポート、修正、削除することができます。  

### <a name="discover"></a>Discover
CDS のシステム管理者は、ユーザーから DSR 要求を受け取ったら、そのユーザーの個人データが含まれる環境/CDS インスタンスを識別する必要があります。 通常、個人データは主要なエンティティ (アカウント、連絡先、リード、営業案件など) に格納されますが、管理者は、DSR 要求に応答できるように、各ユーザーの個人データが格納されている場所のインベントリを管理するためのポリシーと手順を作成する必要があります。

旧バージョンの CDS のユーザーの個人データは、次のリソース内で見つかります。

|リソース | 目的 | Web サイト アクセス |  プログラムによるアクセス
| --- | --- | --- | ---
|エンティティ レコード | それぞれのビジネス エンティティでビジネス トランザクションをキャプチャします。 | [PowerApps](https://web.powerapps.com) |      いいえ

#### <a name="entity-records"></a>エンティティ レコード
ユーザーの個人データは、任意のビジネス エンティティに格納できます。

このバージョンの CDS には、独自のデータベース スキーマとインフラストラクチャが含まれます。 独自のエンティティがあり、これらのエンティティは [PowerApps](http://web.powerapps.com/) で管理します。

エンティティの一覧を表示するには次のようにします。

1. **[環境]** ドロップダウン リストで、お使いの環境を選びます。

2. ナビゲーション ウィンドウで、**[データ]**、**[エンティティ]** の順にクリックまたはタップします。

    ![PowerApps レガシ エンティティ](./media/common-data-service-gdpr-dsr-guide/powerapps-legacy-entities.png)

3. 次に示すように、エンティティの一覧でエンティティ (たとえば、アカウント エンティティ) をクリックまたはタップします。

    ![PowerApps レガシ エンティティの詳細一覧](./media/common-data-service-gdpr-dsr-guide/powerapps-legacy-entities-details-list.png)

4. **[データ]** タブをクリックまたはタップします。エンティティのレコードの一覧が表示されます。

    ![PowerApps レガシ アカウントのデータ](./media/common-data-service-gdpr-dsr-guide/powerapps-legacy-account-data.png)

5. **[データのエクスポート]** をクリックまたはタップします。

6. エクスポートが完了したら、**[Excel で開く]**、**[編集を有効にする]** の順にクリックまたはタップします。

7. 検索ボタンをクリックまたはタップし、検索ボックスにユーザーの個人データを入力して、**[検索]** をクリックまたはタップします。

8. インベントリ リストを使用し、ビジネス エンティティごとに上記の手順を繰り返して、ユーザーの個人データをすべて探索します。

### <a name="rectify"></a>修正
データ主体から組織のデータに存在する個人データの修正を要求された場合、管理者と組織は要求に応えるのが適切かどうかを判断する必要があります。 データの修正には、ドキュメントまたは他の種類のアイテムに含まれる個人データの編集、改訂、削除が含まれる場合があります。

Azure Active Directory を使って、CDS の旧バージョン内のユーザーの ID (個人データ) を管理することができます。 企業の顧客は、特定の Microsoft サービ内の限られた編集機能を使って、DSR 修正要求を管理することができます。 データ プロセッサとしての Microsoft は、システムによって生成されたログを修正する機能を提供していません。ログは実際のアクティビティを反映しており、Microsoft のサービス内でのイベントの履歴レコードを構成しているためです。 詳細については、「[GDPR: Data Subject Requests (DSRs)](https://servicetrust.microsoft.com/ViewPage/GDPRDSR)」(GDPR: データ主体の要求 (DSR)) をご覧ください。

CDS 環境に存在する個人データを修正するには、エンティティ データを Excel スプレッドシートにエクスポートし、更新した後、インポートしてデータベースに戻すことができます。

CDS システム管理者は、ユーザーの個人データを含むすべてのエンティティを識別し、各エンティティに対して以下の手順を繰り返す責任があります。

[PowerApps](http://web.powerapps.com/) から次のようにします。

1. ナビゲーション ウィンドウで、**[データ]**、**[エンティティ]** の順にクリックまたはタップします。

    ![PowerApps レガシ エンティティ](./media/common-data-service-gdpr-dsr-guide/powerapps-legacy-entities.png)

2. 次に示すように、エンティティの一覧でエンティティ (たとえば、アカウント エンティティ) をクリックまたはタップします。

    ![PowerApps レガシ エンティティの詳細一覧](./media/common-data-service-gdpr-dsr-guide/powerapps-legacy-entities-details-list.png)

3. **[データ]** タブをクリックまたはタップします。エンティティのレコードの一覧が表示されます。

    ![PowerApps レガシ アカウントのデータ](./media/common-data-service-gdpr-dsr-guide/powerapps-legacy-account-data.png)

4. **[データのエクスポート]** をクリックまたはタップします。

5. エクスポートが完了したら、**[Excel で開く]**、**[編集を有効にする]** の順にクリックまたはタップします。

6. メニュー バーで **[ファイル]** をクリックまたはタップし、**[名前を付けて保存]** をクリックまたはタップして、ファイルを保存する場所を選択します。

7. 個人データを必要に応じて更新し、スプレッドシートを保存します。

10. PowerApps でエンティティの **[データ]** タブに戻り、**[データのインポート]** をクリックまたはタップします。

11. **[検索]** をクリックし、更新した Excel スプレッドシートを選択して開きます。

12. **[インポート]** をクリックします。

### <a name="export"></a>エクスポート
各エンティティの個人データ Excel ワークシートにエクスポートして表示できます。

[PowerApps](http://web.powerapps.com/) から次のようにします。

1. ナビゲーション ウィンドウで、**[データ]**、**[エンティティ]** の順にクリックまたはタップします。

    ![PowerApps レガシ エンティティ](./media/common-data-service-gdpr-dsr-guide/powerapps-legacy-entities.png)

2. 次に示すように、エンティティの一覧でエクスポートして表示するエンティティ (たとえば、アカウント エンティティ) をクリックまたはタップします。

    ![PowerApps レガシ エンティティの詳細一覧](./media/common-data-service-gdpr-dsr-guide/powerapps-legacy-entities-details-list.png)

3. **[データ]** タブをクリックまたはタップします。エンティティのレコードの一覧が表示されます。

    ![PowerApps レガシ アカウントのデータ](./media/common-data-service-gdpr-dsr-guide/powerapps-legacy-account-data.png)

4. **[データのエクスポート]** をクリックまたはタップします。

    エクスポート操作はバックグラウンドで実行され、終わると通知されます。

5. エクスポートされたデータを表示するには、**[Excel で開く]** をクリックまたはタップします。

### <a name="delete"></a>削除
データのエクスポート/インポート機能を使って、エンティティに格納されている個人データを削除できます。

CDS システム管理者は、ユーザーの個人データを含むすべてのエンティティを識別し、各エンティティに対して以下の手順を繰り返す責任があります。

[PowerApps](http://web.powerapps.com/) から次のようにします。

1. ナビゲーション ウィンドウで、**[データ]**、**[エンティティ]** の順にクリックまたはタップします。

    ![PowerApps レガシ エンティティ](./media/common-data-service-gdpr-dsr-guide/powerapps-legacy-entities.png)

2. 次に示すように、エンティティの一覧で個人データを削除するエンティティ (たとえば、アカウント エンティティ) をクリックまたはタップします。

    ![PowerApps レガシ エンティティの詳細一覧](./media/common-data-service-gdpr-dsr-guide/powerapps-legacy-entities-details-list.png)

3. **[データ]** タブをクリックまたはタップします。エンティティのレコードの一覧が表示されます。

    ![PowerApps レガシ アカウントのデータ](./media/common-data-service-gdpr-dsr-guide/powerapps-legacy-account-data.png)

4. **[データのエクスポート]** をクリックまたはタップします。

5. エクスポートが完了したら、**[Excel で開く]**、**[編集を有効にする]** の順にクリックまたはタップします。

6. メニュー バーで **[ファイル]** をクリックまたはタップし、**[名前を付けて保存]** をクリックまたはタップして、ファイルを保存する場所を選択します。

7. エンティティから削除する個人データを含む行を削除し、スプレッドシートを保存します。

10. PowerApps でエンティティの **[データ]** タブに戻り、**[データのインポート]** をクリックまたはタップします。

11. **[検索]** をクリックし、更新した Excel スプレッドシートを選択して開きます。

12. **[インポート]** をクリックします。
---
title: キャンバス アプリを共有する | Microsoft Docs
description: キャンバス アプリを実行または修正するためのアクセス許可を他のユーザーに付与することで、キャンバス アプリを共有します。
author: AFTOwen
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 11/28/2018
ms.author: anneta
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: b070dfad61f3e53e313d4e8891dc44507a910292
ms.sourcegitcommit: edf79033111b50aa3015b55929ce689474edba2d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2019
ms.locfileid: "68917437"
---
# <a name="share-a-canvas-app-in-powerapps"></a>PowerApps でのキャンバス アプリの共有

ビジネス ニーズに対応するキャンバス アプリをビルドした後、アプリを実行できる組織内のユーザー、およびアプリを変更したり、再度共有したりすることもできるユーザーを指定します。 各ユーザーを名前で指定するか、Azure Active Directory のセキュリティ グループを指定します。 すべてのユーザーがアプリから恩恵を受ける場合、組織全体がアプリを実行できるように指定します。

> [!IMPORTANT]
> 共有アプリが期待どおりに機能するためには、アプリの基になるデータソース ( [Common Data Service](#common-data-service)や[Excel](share-app-data.md)など) のアクセス許可も管理する必要があります。 アプリが依存する[その他のリソース](share-app-resources.md) (フロー、ゲートウェイ、接続など) を共有する必要がある場合もあります。

## <a name="prerequisites"></a>前提条件

アプリを共有するには、そのアプリを (ローカルではなく) クラウドに保存して、アプリを発行する必要があります。

- ユーザーがアプリで行う内容を理解し、リストで簡単に見つけられるように、アプリにわかりやすい名前と明確な説明を追加します。 PowerApps Studio の **[ファイル]** メニューで、 **[アプリの設定]** を選択し、説明を入力するか貼り付けます。

- 変更を加えるたびに、他のユーザーがそれらの変更を表示する必要がある場合は、再度アプリを保存および発行する必要があります。

## <a name="share-an-app"></a>アプリを共有する

1. PowerApps に[サインイン](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)し、左端近くにある **[アプリ]** を選びます。

    ![アプリの一覧を表示する](./media/share-app/file-apps.png)

1. アイコンを選択して、共有するアプリを選択します。

    ![アプリを選択する](./media/share-app/select-app.png)

1. バナーで、 **[共有]** を選択します。

    ![共有画面を開く](./media/share-app/banner-share.png)

1. アプリを共有する Azure Active Directory のユーザーまたはセキュリティグループの名前またはエイリアスを指定します。

    - 組織全体でアプリを実行できるようにする (ただし、変更または共有することはできません) には、[共有] パネルで「 **Everyone** 」と入力します。
    - 項目がセミコロンで区切られている場合は、エイリアス、フレンドリ名、またはそれらの組み合わせ (たとえば、 **Jane &lt;Doe jane.doe@contoso.com>** ) の一覧を使用して、アプリを共有できます。 複数の人が同じ名前でエイリアスが異なる場合は、最初に見つかった人がリストに追加されます。 名前またはエイリアスに既にアクセス許可がある場合、または解決できない場合は、ツールヒントが表示されます。 

    ![ユーザーと共同所有者を指定する](./media/share-app/share-everyone.png)

    > [!NOTE]
    > 組織内の配布グループ、または組織外のユーザーまたはグループとアプリを共有することはできません。

1. アプリを共有しているユーザーに対して、アプリの編集と共有を許可する (実行に加えて) 場合は、 **[共同所有者]** チェックボックスをオンにします。

    [ソリューション内からアプリを作成した](add-app-solution.md)場合は、セキュリティグループに**共同所有者**権限を付与することはできません。

    > [!NOTE]
    > アクセス許可に関係なく、2 人のユーザーが同時にアプリを編集できません。 1 人のユーザーが編集のためにアプリを開いた場合、他のユーザーは、実行できますが、編集することはできません。

1. アプリがユーザーがアクセス許可を必要とするデータに接続する場合は、それらを指定します。

    たとえば、アプリが Common Data Service データベースのエンティティに接続する場合があります。 このようなアプリを共有すると、[共有] パネルで、そのエンティティのセキュリティを管理するように求めるメッセージが表示されます。

    > [!div class="mx-imgBorder"]
    > ![セキュリティロールの割り当て](media/share-app/cds-assign-security-role.png)

    エンティティのセキュリティ管理の詳細については、このトピックで後述する「[エンティティのアクセス許可を管理](share-app.md#manage-entity-permissions)する」を参照してください。

1. 他のユーザーがアプリを見つけやすくするには、**新規ユーザーに招待メールを送信**チェック ボックスをオンします。

1. 共有のパネルの下部にある**共有**を選択します。

    アプリを共有したすべてのユーザーが、 モバイル デバイスのPowerApps Mobile または ブラウザーの[Dynamics 365](https://home.dynamics.com) AppSourceで実行できます。 共同所有者は[PowerApps](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)でアプリの編集・共有ができます。

    電子メールの招待状を送信した場合、アプリを共有した相手は全員、招待内のリンクを選択することで実行できます。

    - ユーザーがモバイルデバイスでリンクを選択すると、PowerApps Mobile でアプリが開きます。
    - ユーザーがデスクトップコンピューターでリンクを選択すると、ブラウザーでアプリが開きます。

    招待状を受け取った共同所有者は、PowerApps Studio で編集するためにアプリを開く別のリンクを取得します。

ユーザーまたはセキュリティグループのアクセス許可を変更するには、その名前を選択して、次のいずれかの手順を実行します。

- 共同所有者がアプリを実行できるようにし、それ以上編集または共有しないようにするには、 **[共同所有者]** チェックボックスをオフにします。
- そのユーザーまたはグループとのアプリの共有を停止するには、[削除 (x)] アイコンを選択します。

## <a name="security-group-considerations"></a>セキュリティ グループに関する考慮事項

- セキュリティ グループでアプリを共有すると、そのグループの既存のメンバーとグループに参加するユーザーは、そのグループに指定したアクセス許可が付与されます。 アクセス権がある別のグループに属しているか、個人としてアクセス許可を付与しない限り、グループから脱退する任意のユーザーはそのアクセス許可を失います。

- セキュリティ グループのすべてのメンバーは、アプリに関して、グループ全体と同じアクセス許可を持ちます。 ただし、そのグループの 1 人以上のメンバーに対してより多くのアクセス許可を指定することで、メンバーのアクセス許可を増やすことができます。 たとえば、アプリを実行するアクセス許可をセキュリティグループに付与できますが、そのグループに属するユーザー B に**共同所有者**のアクセス許可を与えることもできます。 セキュリティ グループのすべてのメンバーはアプリを実行できますが、ユーザー B だけは編集することができます。 セキュリティグループに**共同所有者**のアクセス許可を付与し、ユーザー B にアプリを実行するアクセス許可を与えると、そのユーザーは引き続きアプリを編集できます。

## <a name="manage-entity-permissions"></a>エンティティのアクセス許可を管理する

### <a name="common-data-service"></a>Common Data Service

Common Data Service に基づいてアプリを作成する場合は、アプリを共有するユーザーが、アプリが依存しているエンティティまたはエンティティに対する適切なアクセス許可を持っていることも確認する必要があります。 具体的には、これらのユーザーは、関連レコードの作成、読み取り、書き込み、削除などのタスクを実行できるセキュリティロールに属している必要があります。 多くの場合、ユーザーがアプリを実行するために必要なアクセス許可を持つ1つまたは複数のカスタムセキュリティロールを作成する必要があります。 その後、必要に応じて、各ユーザーにロールを割り当てることができます。

> [!NOTE]
> このドキュメントの執筆時点では、セキュリティロールを Azure Active Directory の個々のユーザーおよびセキュリティグループに割り当てることができますが、Office グループに割り当てることはできません。

#### <a name="prerequisite"></a>前提条件

ロールを割り当てるには、Common Data Service データベースの**システム管理者**権限を持っている必要があります。

#### <a name="assign-a-security-group-in-azure-ad-to-a-role"></a>Azure AD のセキュリティグループをロールに割り当てる

1. 共有 パネルで、**データのアクセス許可** で **セキュリティロールの割り当て** を選択します。

1. アプリを共有する Azure AD のユーザーまたはセキュリティグループに割り当てる Common Data Service 内のロールを選択します (複数選択)。

    ![セキュリティロールの一覧](media/share-app/cds-assign-security-role-list.png)

### <a name="common-data-service-previous-version"></a>Common Data Service (以前のバージョン)

以前のバージョンの Common Data Service に基づくアプリを共有する場合は、ランタイムアクセス許可をサービスに個別に共有する必要があります。 この操作を行うためのアクセス許可がない場合は、環境管理者に問い合わせてください。

## <a name="share-with-guests"></a>ゲストと共有する

> [!IMPORTANT]
> - プレビュー機能は、運用環境で使用するためのものではなく、機能が制限されている可能性があります。 これらの機能は、お客様が機能にいち早くアクセスして、フィードバックをお送りいただけるように、正式なリリースの前に利用できるようになっています。 
> - プレビュー機能のサポートは Microsoft サポートによって制限されており、選択した地域でのみ使用できます。 

PowerApps キャンバスアプリは、Azure Active Directory テナントのゲストユーザーと共有できます。 これにより、外部のビジネスパートナー、請負業者、およびサードパーティが会社のキャンバスアプリを実行するための招待を行うことができます。 

ゲストに割り当てることができるのは共同所有者ロールではなく、ユーザーロールだけです。

### <a name="prerequisites"></a>必須コンポーネント
1. Azure Active Directory で、テナントの[B2B 外部コラボレーションを有効に](https://docs.microsoft.com/en-us/azure/active-directory/b2b/delegate-invitations)します。  
- 既定では、この設定はテナント管理者が変更できます。  
- B2B の Azure AD の詳細については、次を参照してください。[Azure AD B2B でのゲストユーザーアクセスとは](https://docs.microsoft.com/en-us/azure/active-directory/b2b/what-is-b2b)  
2. AAD テナントにゲストユーザーを追加できるアカウントへのアクセス。 管理者と "ゲスト招待元" ロールを持つユーザーは、ゲストをテナントに追加できます。   
3. PowerApps ライセンスは、共有されているアプリが関連付けられているテナントのゲストユーザーに割り当てられている必要があります。 Canvas アプリのゲストアクセスの一般提供が開始される前に、ホームテナントで PowerApps ライセンスを持つゲストには、ゲストであるテナントのライセンスを割り当てる必要はありません。

### <a name="steps"></a>手順
1. Azure Active Directory にゲストユーザーを追加します。  
- これについては、次の記事で説明します。[クイック スタート:Azure AD](https://docs.microsoft.com/en-us/azure/active-directory/b2b/b2b-quickstart-add-guest-users-portal)に新しいゲストユーザーを追加します。
![Azure AD にゲストを追加する](media/share-app/guest_access_doc_1.png)
2. ゲストユーザーにライセンスを割り当てます。 
- これについては、次の記事で説明します。[1 人のユーザーにライセンスを割り当てる](https://docs.microsoft.com/en-us/office365/admin/subscriptions-and-billing/assign-licenses-to-users?view=o365-worldwide#assign-licenses-to-one-user)か、ユーザーに対し https://admin.microsoft.com て https://portal.azure.com それぞれおよびの[ライセンスを割り当てまたは削除](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals/license-users-groups)します。  
- ゲストにライセンスを割り当てるには、Microsoft 365 管理センターのプレビューをオフにする必要があることに注意してください。 
3. キャンバスアプリを共有します。 
- にサインインします。 https://make.powerapps.com  
- アプリを選択し、[共有] をクリックします。 
![](media/share-app/guest_access_doc_2.png)
ゲスト![ゲストと共有できるのはユーザーのみです](media/share-app/guest_access_doc_3.png)
4. ゲストは、共有の一部として送信された電子メールから、それらと共有されているアプリを検出してアクセスできます。
![ゲストはアプリ共有電子メールを受け取ります](media/share-app/guest_access_doc_4.png)

### <a name="frequently-asked-questions"></a>よく寄せられる質問

#### <a name="whats-the-difference-between-canvas-app-guest-access-and-powerapps-portal"></a>キャンバスアプリのゲストアクセスと PowerApps ポータルの違いは何ですか。 
キャンバスアプリを使用すると、などの従来のプログラミング言語でコードを記述しなくても、ビジネスプロセスC#をデジタル化することに合わせてアプリを構築できます。 キャンバスアプリのゲストアクセスを使用すると、共通のビジネスプロセスに参加しているさまざまな組織で構成されている個人チームが、さまざまな [Microsoft やサードパーティのソース](https://docs.microsoft.com/en-us/powerapps/maker/canvas-apps/connections-list)と統合されている同じアプリリソースにアクセスできます。

[PowerApps ポータル](https://docs.microsoft.com/en-us/powerapps/maker/portals/overview) を使用すると、外部ユーザーが Common Data Service に格納されているデータを操作できるようにする、低レベルの応答性の高い web サイトを構築することができます。 これにより、組織の外部のユーザーと匿名で、または LinkedIn、Microsoft アカウント、その他の商用ログインプロバイダーなどのログインプロバイダーを介して共有できる web サイトを作成できます。 

次の表は、PowerApps ポータルとキャンバスアプリのいくつかの主要な機能の違いをまとめたものです。  

| | Interface | 認証 | アクセス可能なデータソース |
|------|--------|----------|-------------------|
| PowerApps ポータル | ブラウザーのみのエクスペリエンス | 匿名アクセスと認証されたアクセスを許可する | Common Data Service |
| キャンバス アプリ | ブラウザーとモバイルアプリ | Azure AD による認証が必要 | ~ 150 の既定のコネクタと任意のカスタムコネクタ  |
||

#### <a name="can-guests-access-customized-forms-in-sharepoint"></a>ゲストは、カスタマイズされたフォームに SharePoint でアクセスできますか。
はい。 カスタマイズされたフォームを使用して SharePoint リストにアクセスできるすべてのユーザーは、PowerApps ライセンスなしでフォームを使用して、リスト内の項目を作成および編集できます。

#### <a name="can-guests-access-apps-embedded-in-sharepoint"></a>ゲストは SharePoint に埋め込まれたアプリにアクセスできますか。 
はい。 ただし、キャンバスのスタンドアロンアプリにアクセスするには、埋め込みのアプリを含む PowerApps ライセンスが必要です。 Microsoft PowerApps 埋め込みコントロールを使用して SharePoint にキャンバスアプリを埋め込む場合は、アプリ id をコピーして貼り付けます。 

![ゲストの SharePoint にキャンバスアプリを埋め込む](media/share-app/guest_access_doc_5.PNG)

IFrame HTML タグを使用して SharePoint にキャンバスアプリを埋め込む場合は、「アプリ > 詳細 > web リンクを選択 http://make.powerapps.com >」に記載されている完全な web リンクを使用してアプリを参照します。

![キャンバスアプリの詳細](media/share-app/guest_access_doc_6.PNG)

#### <a name="how-come-guests-can-launch-the-app-shared-with-them-but-connections-fail-to-be-created"></a>ゲストはどのように共有アプリを起動できますが、接続の作成は失敗しますか。
ゲスト以外の場合と同様に、アプリによってアクセスされる基になるデータソースもゲストにアクセスできるようにする必要があります。

#### <a name="what-license-must-be-assigned-to-my-guest-so-they-can-run-an-app-shared-with-them"></a>ゲストに割り当てられているアプリを実行できるようにするには、どのライセンスを割り当てる必要がありますか。
ゲスト以外がアプリを実行するために必要なものと同じライセンス。 たとえば、アプリが premium の登録を使用していない場合、PowerApps P1 ライセンスはゲストに割り当てるのに十分です。  

キャンバスアプリのゲストアクセスの一般提供が開始される前、ホームテナントで PowerApps ライセンスを持つゲストには、ゲストであるテナントのライセンスを割り当てる必要はありません。

|                                 | SharePoint カスタマイズフォーム | Premium 以外のコネクタを使用するスタンドアロンキャンバスアプリ | Premium コネクタを使用したスタンドアロンのキャンバスアプリ | モデル駆動型アプリ |
|---------------------------------|----------------------------|----------------------------------------------------|------------------------------------------------|------------------|
| SharePoint ユーザー (PA ライセンスなし) | x                          |                                                    |                                                |                  |
| Office に含まれる PowerApps    | x                          |                                                    |                                                |                  |
| PowerApps プラン1                | x                          | x                                                  |                                                |                  |
| PowerApps Plan2                 | x                          | ○                                                  | ○                                              | x                |

#### <a name="in-powerapps-mobile-how-does-a-guest-see-apps-for-their-home-tenant"></a>PowerApps Mobile では、ゲストがホームテナントのアプリを表示するにはどうすればよいですか。
自分のモバイルデバイス上にあるキャンバスアプリにアクセスしたユーザーは、そのホームテナントではない Azure AD テナントで公開されているすべてのユーザーが PowerApps からサインアウトし、PowerApps Mobile に再度サインインする必要があります。  

キャンバスアプリのゲストアクセスの一般提供が開始される前に、組織セレクターを使用すると、ユーザーはアプリを明示的にサインアウトすることなく、サインインしている Azure AD テナントを変更できます。  

#### <a name="must-a-guest-accept-the-azure-ad-guest-invitation-prior-to-sharing-an-app-with-the-guest"></a>ゲストとアプリを共有する前に、ゲストが Azure AD ゲストの招待を受け入れる必要がありますか。
No. ゲスト招待を受け入れる前にゲストが共有アプリを起動すると、ゲストは、アプリの起動時にサインインエクスペリエンスの一部として招待に同意するように求められます。  

#### <a name="what-azure-ad-tenant-are-connections-for-a-guest-user-created-in"></a>で作成されたゲストユーザーの接続は Azure AD テナント
アプリの接続は、常にアプリが関連付けられている Azure AD テナントのコンテキストで作成されます。 たとえば、アプリが Contoso テナントに作成された場合、contoso の内部およびゲストユーザーに対して行われた接続は Contoso テナントのコンテキストで作成されます。

#### <a name="can-guests-use-microsoft-graph-via-microsoft-security-graph-connectorhttpsdocsmicrosoftcomen-usconnectorsmicrosoftgraphsecurity-or-a-custom-connector-using-microsoft-graph-apishttpsdevelopermicrosoftcomen-usgraph"></a>ゲストは、 [Microsoft Graph api](https://developer.microsoft.com/en-us/graph)を使用して[Microsoft セキュリティグラフコネクタ](https://docs.microsoft.com/en-us/connectors/microsoftgraphsecurity/)またはカスタムコネクタ経由で Microsoft Graph を使用できますか。
いいえ、ゲストがゲストであるテナントの情報を取得するために、ゲストが Microsoft Graph を照会することは Azure AD ません。

#### <a name="what-intune-policies-apply-to-guests-using-my-powerapps"></a>PowerApps を使用しているゲストにはどのような InTune ポリシーが適用されますか。
InTune では、ユーザーのホームテナントのポリシーのみが適用されます。 たとえば、がとAlice@Contoso.com Vikram@Fabrikam.comアプリを共有している場合、InTune は、実行している PowerApps に関係なく、Fabrikam.com ポリシーを仮想デバイスに適用し続けます。

#### <a name="what-connectors-support-guest-access"></a>ゲストアクセスをサポートするコネクタ
任意の種類の Azure AD 認証を実行しないすべてのコネクタは、ゲストアクセスをサポートします。 次の表に、Azure AD 認証を実行するすべてのコネクタと、現在ゲストアクセスをサポートしているコネクタを列挙します。 これらの多くは、一般公開される前に更新される予定です。

| **ケーブル**                                     | **ゲストアクセスのサポート**                                              |
|---------------------------------------------------|------------------------------------------------------------------------|
| 10to8 Appointment Scheduling                      | いいえ                                                                     |
| Adobe Creative Cloud                              | いいえ                                                                     |
| Adobe Sign                                        | いいえ                                                                     |
| Asana                                             | いいえ                                                                     |
| AtBot 管理者                                       | いいえ                                                                     |
| AtBot Logic                                       | いいえ                                                                     |
| Azure AD                                          | [はい]                                                                    |
| Azure Automation                                  | [はい]                                                                    |
| Azure Container Instance                          | [はい]                                                                    |
| Azure Data Factory                                | [はい]                                                                    |
| Azure Data Lake                                   | [はい]                                                                    |
| Azure DevOps                                      | いいえ                                                                     |
| Azure Event Grid                                  | いいえ                                                                     |
| Azure IoT Central                                 | [はい]                                                                    |
| Azure Key Vault                                   | いいえ                                                                     |
| Azure Kusto                                       | [はい]                                                                    |
| Azure Log Analytics                               | [はい]                                                                    |
| Azure Resource Manager                            | [はい]                                                                    |
| Basecamp 2                                        | いいえ                                                                     |
| Bitbucket                                         | いいえ                                                                     |
| Bitly                                             | いいえ                                                                     |
| bttn                                              | いいえ                                                                     |
| バッファー                                            | いいえ                                                                     |
| 中央部                                  | いいえ                                                                     |
| CandidateZip                                      | いいえ                                                                     |
| Capsule CRM                                       | いいえ                                                                     |
| クラウド PKI の管理                              | いいえ                                                                     |
| Cognito Forms                                     | いいえ                                                                     |
| Common Data Service                               | いいえ                                                                     |
| Common Data Service (レガシ)                      | いいえ                                                                     |
| D & B オプティマイザー                                     | いいえ                                                                     |
| Derdack SIGNL4                                    | いいえ                                                                     |
| Disqus                                            | いいえ                                                                     |
| ドキュメントのマージ                                    | いいえ                                                                     |
| Dynamics 365                                      | いいえ                                                                     |
| Dynamics 365 AI for Sales                         | [はい]                                                                    |
| Fin & Ops 用 Dynamics 365                        | いいえ                                                                     |
| Enadoc my workspace                                            | いいえ                                                                     |
| Eventbrite                                        | いいえ                                                                     |
| Excel Online (Business)                           | いいえ                                                                     |
| Excel Online (OneDrive)                           | いいえ                                                                     |
| 有効期限リマインダー                               | いいえ                                                                     |
| FreshBooks                                        | いいえ                                                                     |
| GoToMeeting                                       | いいえ                                                                     |
| GoToTraining                                      | いいえ                                                                     |
| GoToWebinar                                       | いいえ                                                                     |
| Harvest                                           | いいえ                                                                     |
| HTTP with Azure AD                                | いいえ                                                                     |
| Infusionsoft                                      | いいえ                                                                     |
| Inoreader                                         | いいえ                                                                     |
| Intercom                                          | いいえ                                                                     |
| JotForm                                           | いいえ                                                                     |
| kintone                                           | いいえ                                                                     |
| LinkedIn                                          | いいえ                                                                     |
| マーケティングコンテンツハブ                             | いいえ                                                                     |
| Medium                                            | いいえ                                                                     |
| Metatask                                          | いいえ                                                                     |
| Microsoft Forms                                   | いいえ                                                                     |
| Microsoft Forms Pro                               | いいえ                                                                     |
| Microsoft Graph のセキュリティ                          | いいえ                                                                     |
| Microsoft Kaizala                                 | いいえ                                                                     |
| Microsoft School Data Sync                        | いいえ                                                                     |
| Microsoft StaffHub                                | いいえ                                                                     |
| Microsoft Teams                                   | [はい]                                                                    |
| Microsoft To Do (Business)                        | いいえ                                                                     |
| Muhimbi PDF                                       | いいえ                                                                     |
| NetDocuments                                      | いいえ                                                                     |
| Office 365 グループ                                 | [はい]                                                                    |
| Office 365 Outlook                                | いいえ                                                                     |
| Office 365 Users                                  | [はい]                                                                    |
| Office 365 ビデオ                                  | いいえ                                                                     |
| OneDrive                                          | いいえ                                                                     |
| OneDrive for Business                             | いいえ                                                                     |
| OneNote (ビジネス)                                | いいえ                                                                     |
| Outlook Customer Manager                          | いいえ                                                                     |
| Outlook Tasks                                     | [はい]                                                                    |
| Outlook.com                                       | いいえ                                                                     |
| Paylocity                                         | いいえ                                                                     |
| Planner                                           | いいえ                                                                     |
| Plumsail フォーム                                    | いいえ                                                                     |
| Power BI                                          | [はい]                                                                    |
| Project Online                                    | いいえ                                                                     |
| ProjectWise 設計の統合                    | いいえ                                                                     |
| Projectwise 共有                                 | いいえ                                                                     |
| SharePoint                                        | [はい]                                                                    |
| SignNow                                           | いいえ                                                                     |
| Skype for Business Online                         | いいえ                                                                     |
| Soft1                                             | いいえ                                                                     |
| Stormboard                                        | いいえ                                                                     |
| Survey123                                         | いいえ                                                                     |
| SurveyMonkey                                      | いいえ                                                                     |
| Toodledo                                          | いいえ                                                                     |
| Typeform                                          | いいえ                                                                     |
| Vimeo                                             | いいえ                                                                     |
| Webex チーム                                       | いいえ                                                                     |
| Windows Defender Advanced Threat Protection (ATP) | いいえ                                                                     |
| Word Online (Business)                            | いいえ                                                                     |

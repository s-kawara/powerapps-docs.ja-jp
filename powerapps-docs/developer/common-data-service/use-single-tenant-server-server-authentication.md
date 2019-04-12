---
title: 単一テナント型サーバー間認証を使用する (Common Data Service) | Microsoft Docs
description: 明示的なユーザー認証を行わずにアプリケーションまたはサービスから D365 データにアクセスする方法について説明します。
ms.custom: ''
ms.date: 2/21/2019
ms.reviewer: pehecke
ms.service: powerapps
ms.topic: article
author: paulliew
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="use-single-tenant-server-to-server-authentication"></a>単一テナント型のサーバー間認証を使用する

単一テナント型サーバー間シナリオは通常、認証に Active Directory フェデレーション サービス (AD FS) を使用した複数の Common Data Service 環境を持つエンタープライズ組織に対して適用されます。 ただしアプリケーションが他の環境に配布されない場合は、環境によって適用することが可能です。  
  
 エンタープライズは Web アプリケーションまたはサービスを作成して、単一の Azure Active Directory (AD) テナントに関連付けられている Common Data Service 環境に接続できます。
  
## <a name="differences-from-multi-tenant-scenario"></a>マルチテナント型シナリオの違い  
 単一テナント型サーバー間認証の Web アプリケーションまたはサービスの作成は、マルチテナント型の組織で使用される作成と類似していますが、いくつかの重要な違いがあります。  
  
-   すべての組織がテナント内にあるため、テナント管理者が組織ごとに同意を許可する必要はありません。 アプリケーションはテナントに一度登録するだけです。
  
-   キーよりもむしろ証明書を使用することもできます。 

この記事の最後の [関連項目](#bkmk_seealso) セクションでは、マルチテナント機能への単一テナント アプリケーションのアップグレードに関する情報へのリンクがあります。  

<a name="bkmk_Requirements"></a>
## <a name="requirements"></a>要件  

 サーバー間の (S2S) 認証を使用する単一テナント型アプリケーション テストを作成してテストするには、次のものが必要です:  
  
- 提供されているサンプル アプリケーションを登録するときに使用する Azure AD テナント。
- Azure AD テナントに関連付けられている Common Data Service サブスクリプション。
- Azure AD テナントおよび D365 組織の管理者特権。

<a name="bkmk_registration"></a>
## <a name="azure-application-registration"></a>Azure アプリケーション登録
Azure AD でアプリケーション登録を作成するには、次の手順に従います。

1. https://admin.microsoft.com に移動してサインインするか、D365 組織の Web ページから左上隅のアプリケーション ランチャーを選択します。
2. **管理** > **管理センター** > **Azure Active Directory** を選択します
3. 左パネルで、**Azure Active Directory** > **アプリの登録 (プレビュー)** を選択します
4. **+ 新しい登録** [[イメージ](#bkmk_app-registration-started)] を選択します
5. **アプリケーションの登録** フォームにアプリの名前を指定し、**この組織のディレクトリ内のアカウントのみ** を選択して、**登録** を選択します。 リダイレクト URI は、このチュートリアルと付属のサンプル コードについては不要です。
6. **概要** ページで、**API のアクセス許可** [[イメージ](#bkmk_app-registration-completed)] を選択します
7. **+ アクセス許可の追加** を選択します
8. **Microsoft API** タブで、**Dynamics CRM** を選択します
9. **API アクセス許可の要求** フォームで、**委任されたアクセス許可** を選択し、**user_impersonation** を確認して、**アクセス許可の追加** [[イメージ](#bkmk_api-permission-started)] を選択します
10. **API のアクセス許可** ページの下の **同意する** で、**"org-name" に管理者の同意を与えます** を選択し、確認メッセージが表示されたら **はい** [[イメージ](#bkmk_api-permission-completed)] を選択します
11. ナビゲーション ウィンドウの **概要** をクリックし、アプリ登録の **表示名**、**アプリケーション ID**、**ディレクトリ ID** の値を記録します。 これらの値は、後でコード サンプルで指定します。
12. ナビゲーション ウィンドウで、**証明書とシークレット** を選択します
13. **クライアント シークレット** で、**新しいクライアント シークレットの追加** を選択してシークレットを作成します
14. フォームに説明を入力して **追加** を選択します。 シークレットの文字列を記録します。 現在の画面を離れると、シークレットを再び表示することはできません。

<a name="bkmk_appuser"></a>
## <a name="application-user-creation"></a>アプリケーション ユーザーの作成
Dynamics 365 組織でライセンスを付与されていない「アプリケーション ユーザー」を作成するには、次の手順に従います。 このアプリケーション ユーザーは、アプリケーションを使用しているエンド ユーザーに代わって組織のデータにアクセスできます。

1. Azure Active Directory 管理センターに移動します
2. 左のナビゲーション ウィンドウで、**ユーザー** を選択します
3. **+ 新しいユーザー** を選択します
4. **ユーザー** フォームで、新しいユーザーの名前とユーザー名を入力し、**作成** を選択します。 ユーザー名に D365 テナントの組織ドメイン URL が含まれていることを確認します (たとえば、someuser@myorg.onmicrosoft.com)。 Azure AD を終了します。
5. D365 組織に移動します。
6. **設定** > **セキュリティ** > **ユーザー**の順に移動します
7. ビュー フィルターで **アプリケーション ユーザー** を選択します
8. **+ 新規作成** を選択します
9. **新しいユーザー** フォームで、必要な情報を入力します。 これらの値は、Azure テナントで作成した新しいユーザーの値と一致していることが必要です。 [[イメージ](#bkmk_new-appuser)]
10. すべて問題なく入力して **上書き保存** を選択すると、**アプリケーション ID の URI** と **Azure AD オブジェクト ID** のフィールドに正しい値が自動入力されます
11. ユーザー フォームを終了する前に、アプリケーション ユーザーが目的の組織データにアクセスできるように **ロールの管理** を選択して、このアプリケーションのユーザーにセキュリティ ロールを割り当てます。

> [!IMPORTANT]
> S2S を使用して実際のアプリケーションを開発するときは、ソリューションに格納して、アプリケーションとともに配布できる、ユーザー定義のセキュリティ ロールを使用する必要があります。

<a name="bkmk_coding"></a>
## <a name="application-coding-and-execution"></a>アプリケーションのコーディングと実行

次の手順に従って、サンプル アプリケーションをダウンロード、構築、および実行します。 サンプルは Web API を呼び出して、組織の上位 3 つのアカウント (名前) のリストを返します。

1. Visual Studio 2017 SingleTenantS2S のダウンロード [サンプル](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/webapi/C%23/SingleTenantS2S)。
2. アプリケーション登録とサーバー キーの値で App.config ファイルを更新します。
3. アプリケーションをビルドして実行します。

### <a name="expected-results"></a>予測した結果
D365 組織の上位 3 つのアカウント名の一覧を示す OData の返信。

### <a name="example-console-output"></a>コンソール出力の例
以下に示す例は、「Test Account 1」および「Test Account 2」という 2 つのアカウントのみ持つ D365 組織から取得したコンソール出力です。

```json
{
"@odata.context":"https://crmue2.api.crm.dynamics.com/api/data/v9.1/$metadata#accounts(name)",
"@Microsoft.Dynamics.CRM.totalrecordcount":-1,
"@Microsoft.Dynamics.CRM.totalrecordcountlimitexceeded":false,

"value":[
{"@odata.etag":"W/\"4648334\"","name":"Test Account 1","accountid":"28630624-cac9-e811-a964-000d3a3ac063"},
{"@odata.etag":"W/\"4648337\"","name":"Test Account 2","accountid":"543fd72a-cac9-e811-a964-000d3a3ac063"}]
}
```

<a name="bkmk_seealso"></a>

### <a name="see-also"></a>関連項目

[マルチ テナント型でのサーバー間認証の使用](use-multi-tenant-server-server-authentication.md)   
[サーバー間 (S2S) の認証を使用して Web アプリケーションを作成する](build-web-applications-server-server-s2s-authentication.md)  
[方法: マルチテナント型アプリケーションを使用するユーザーが Azure Active Directory にサインインするパターン](https://docs.microsoft.com/en-us/azure/active-directory/develop/howto-convert-app-to-be-multi-tenant)

## <a name="list-of-figures"></a>図の一覧

<a name="bkmk_app-registration-started"></a>
### <a name="figure-azure-ad-app-registration"></a>図: Azure AD アプリケーション登録
<kbd><img src="media/S2S-app-registration-started.PNG"></kbd><br />
[[戻る](#bkmk_registration)]

<a name="bkmk_app-registration-completed"></a>
### <a name="figure-azure-ad-app-registration-overview"></a>図: Azure AD アプリケーション登録の概要
<kbd><img src="media/S2S-app-registration-completed.PNG"></kbd><br />
[[戻る](#bkmk_registration)]

<a name="bkmk_api-permission-started"></a>
### <a name="figure-setting-app-permissions"></a>図: アプリの権限の設定
<kbd><img src="media/S2S-api-permission-started.PNG" ></kbd><br />
[[戻る](#bkmk_registration)]

<a name="bkmk_api-permission-completed"></a>
### <a name="figure-completed-app-permissions-and-consent"></a>図: 完了済みのアプリの権限と同意
<kbd><img src="media/S2S-api-permission-completed.PNG" ></kbd><br />
[[戻る](#bkmk_registration)]

<a name="bkmk_new-appuser"></a>
### <a name="figure-adding-a-new-application-user-in-d365"></a>図: D365 の新しいアプリケーション ユーザーの追加
<kbd><img src="media/S2S-new-appuser.PNG" ></kbd><br />
[[戻る](#bkmk_appuser)]

---
title: マルチ テナント型でのサーバー間認証の使用 (Common Data Service)| Microsoft Docs
description: サーバー間認証のために、 Common Data Service でアプリケーション ユーザーを構成する方法について説明します。
ms.custom: ''
ms.date: 2/28/2019
ms.reviewer: ''
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
# <a name="use-multi-tenant-server-to-server-authentication"></a>マルチ テナント型でのサーバー間認証の使用

これは、最も一般的なシナリオであり、[Microsoft AppSource] を使用して配布されたアプリケーションに使用されますが、[Microsoft AppSource] でアプリケーションを一覧表示せずにマルチテナント型を使用することができます。  
  
各 Common Data Service 組織は、Azure Active Directory テナントに関連付けられています。 Web アプリケーションまたはサービスは、独自の Azure AD テナントで登録されます。  
  
このシナリオでは、すべての [Common Data Service] テナントは、アプリケーションがデータにアクセスするための同意を取得した後、マルチテナント型アプリケーションを潜在的に使用できます。  
  
<a name="bkmk_Requirements"></a>   

## <a name="requirements"></a>要件  

 サーバー間の (S2S) 認証を使用するマルチテナント型アプリケーション テストを作成してテストするには次のものが必要です:  
  
- アプリケーションまたはサービスの公開に使用する Azure AD テナント。  
  
- 2 Common Data Service サブスクリプション  
  
  -   1 つは、アプリまたはサービスの公開に使用する Azure AD テナントに関連付けられている必要があります。  
  
  -   もう 1 つは、サブスクライバーがアプリケーションにアクセスする方法をテストするための試用版サブスクリプションです。  
  
<a name="bkmk_DevelopAndTest"></a>  
 
## <a name="overview-develop-and-test-your-application"></a>概要: アプリケーションの開発とテスト  

 作成するアプリは、アプリを公開する時に使用する Azure AD テナントに登録する必要があります。  
  
 高いレベルでは、プロセスは次のように構成されます:  
  
1. Azure AD テナントに登録されたマルチテナント型 Web アプリケーションを作成します。  
  
2. [Common Data Service] テナントで登録されたアプリケーションに関連付けられるアプリケーション ユーザーを作成します。  
  
3. カスタム セキュリティ ロールを作成し、[Common Data Service] テナントのアプリケーション ユーザーに割り当てます  
  
4. [Common Data Service] テナントを使用してアプリケーションをテストします  
  
5. 別の [Common Data Service] テナントを使用してアプリケーションをテストします  
  
<a name="bkmk_CreateAMultitenantWebApp"></a>
   
## <a name="create-a-multi-tenant-web-application-registered-with-your-azure-ad-tenant"></a>Azure AD テナントに登録されたマルチテナント型 Web アプリケーションを作成します。 
 
 マルチテナント型 Web アプリケーションまたは Azure AD を認証プロバイダーとして使用するサービスを作成します。  
  
 これをどうやって行うのかは、このトピックの焦点ではありません。 これにアプローチして、要件や好みに合った選択をすることができるいくつかの方法があります。 詳細とサンプルについては、次のリンクを参照してください:  
  
- [ Azure AD &amp; OpenID 接続を使用してマルチテナント型 SaaS Web アプリケーションを構築する](https://azure.microsoft.com/documentation/samples/active-directory-dotnet-webapp-multitenant-openidconnect/)  
  
- [Azure AD を使用して、Web API を呼び出すマルチテナント型 SaaS Web アプリケーションを構築する](https://azure.microsoft.com/documentation/samples/active-directory-webapp-webapi-multitenant-openidconnect-aspnetcore/)  
  
  Azure AD には、アプリを登録するために次の値が必要です。  
  
|値|説明|  
|-----------|-----------------|  
|**アプリケーション ID URI**|アプリケーションの識別子です。 この値は認証中に Azure AD へ送信され、発信者がトークンを要求するアプリケーションを示します。 さらに、この値はトークンに含まれ、対象のターゲットであることがアプリケーションに認識されます。|  
|**返信 URL およびリダイレクト URI**|Web API または Web アプリケーションの場合、応答 URL は、認証が成功した場合のトークンを含めて Azure AD が認証応答を送信する場所です。|  
|**クライアント ID**|アプリケーションの ID は、アプリが登録されるとき、 Azure AD によって生成されます。 認証コードまたはトークンを要求した場合、認証中にクライアント ID およびキーが Azure AD へ送信されます。|  
|**Key**|Azure AD に対して認証し、Web API を呼び出すときにクライアント ID と共に送信されるキー。|  
  
 アプリが登録されると、登録されたアプリの一意の識別子である **Azure Active Directory オブジェクト ID** が割り当てられます。  
  
 新規で [Visual Studio] を使用して [ASP.NET] MVC アプリケーションを作成する場合は、アプリケーションがマルチテナント機能をサポートするように指定するオプションがあります。 MVC アプリケーション用テンプレートには、どのような種類の認証が行われるかを指定するオプションがあります。 プロジェクトの作成時にプロジェクトのプロパティを設定することで、認証方法を選択するオプションがあります。 次の図で使用できるオプションを表示します:  
  
 ![ASP.NET MVC 変更認証ダイアログ](media/mvc-change-authentication-dialog.png "ASP.NET MVC 変更認証ダイアログ")  
  
 これらのオプションを使用してプロジェクトを構成すると、このシナリオをサポートする基本的なアプリケーションの [OWIN] ミドルウェアおよびスキャフォールディングを使用するよう構成されます。 基本的な変更を加えれば、[Common Data Service] で動作するように変更することができます。 
  
 開発用アプリケーションを作成して登録するプロセスについては、[`http://localhost`] を **URL にサインオン**と**返答 URL** 値として使用し、公開前にアプリケーションをローカルでテストしてデバッグすることができます。 アプリの公開前にこれらの値を変更する必要があります。  
  
 アプリを登録する場合、`ClientSecret` としても呼ばれるキーを生成する必要があります。 これらのキーは 1 年、または 2 年間構成することができます。 アプリケーションのホストは、この値をパスワードのように扱う必要があり、期限が切れる前にキーの更新を管理する責任があります。 [Key Vault] を使用することができます。 詳細: [https://azure.microsoft.com/services/key-vault/](https://azure.microsoft.com/services/key-vault/)  
  
<a name="bkmk_GrantApplicationRights"></a>
   
## <a name="grant-your-application-rights-to-access-common-data-service-data"></a>[Common Data Service] データにアクセスする権限を付与します
  
 このため、Common Data Serviceインスタンスは Azure AD テナントに関連付けられている必要があります。 Azure AD テナントが Common Data Service テナントに関連付けられていない場合、次の手順を実行することはできません。  
  
1. [https://portal.azure.com](https://portal.azure.com)に移動し、**Azure Active Directory**を選択します。  
  
2. **アプリ登録**をクリックして、Visual Studio を使用して作成したアプリケーションを検索します。  
  
3. [Common Data Service] データにアクセスするためのアプリケーション特権を付与する必要があります。 **API アクセス**領域で**必要なアクセス許可**をクリックします。 **Windows Azure Active Directory に対して既に許可が与えられていることが確認できます**。  
  
4. **追加**をクリックし、次に **API の選択**をクリックします。 一覧で、**Dynamics 365** を選択し、**選択**ボタンをクリックします。  
  
5. **アクセス許可の選択**で、**組織のユーザーとして Dynamics 365 にアクセスする**を選択します。 次に、**選択**ボタンをクリックします。  
  
6. これらのアクセス許可を追加するには、**完了**をクリックします。 完了したらアクセス許可が適用されていることを確認する必要があります。  
  
   ![Dynamics 365 の許可をアプリケーションに与える](media/grant-crm-permissions-to-application.png "Dynamics 365 の許可をアプリケーションに与える")  
  
<a name="bkmk_CreateAppUser"></a>
   
## <a name="create-an-application-user--associated-with-the-registered-application--in-common-data-service"></a>[Common Data Service] で登録されたアプリケーションに関連付けられるアプリケーション ユーザーを作成します  
 アプリケーションをアプリケーションのサブスクライバーの 1 つである [Common Data Service] データにアクセスする場合、サブスクライバーの [Common Data Service] 組織にアプリケーション ユーザーが必要になります。 任意の [Common Data Service] ユーザーと同様、このアプリケーション ユーザーは、ユーザーがアクセスできるデータを定義する少なくとも 1 つのセキュリティロールに関連付けられている必要があります。  
  
 [SystemUser エンティティ](reference/entities/systemuser.md)には、このデータを保存する 3 つの新しい属性があります。  
  
|スキーマ名|表示名|種類​​|内容|  
|-----------------|------------------|----------|-----------------|  
|[ApplicationId](reference/entities/systemuser.md#BKMK_ApplicationId)|**アプリケーション ID**|UniqueidentifierType|アプリケーションの識別子。 これは、別のアプリケーションのデータにアクセスするために使用されます。|  
|[ApplicationIdUri](reference/entities/systemuser.md#BKMK_ApplicationIdUri)|**アプリケーション ID の URI**|StringType|外部アプリケーションの一意の論理識別子として使用される URI。 これは、アプリケーションを検証するのに使用できます|  
|[AzureActiveDirectoryObjectId](reference/entities/systemuser.md#BKMK_AzureActiveDirectoryObjectId)|**Azure AD オブジェクト ID**|UniqueidentifierType|アプリケーション ディレクトリのオブジェクト ID です。|  
  
 この `systemuser``AzureActiveDirectoryObjectId` プロパティ値は、登録済みアプリケーションの Azure Active Directory オブジェクト ID の参照である必要があります。 この参照は、アプリケーション ユーザーが [`ApplicationId`] 値に基づいて作成されるとき、[Common Data Service] に設定されます。  
  
> [!NOTE]
>  最初に独自の Common Data Service テナントとそれに関連付けられた Azure AD テナントを使用してアプリケーションを開発する場合は、登録済みアプリが既に Azure AD テナントの一部であるため、アプリケーションのユーザーを容易に作成できます。  
> 
>  ただし、テストのために別の組織でアプリケーション ユーザを作成するため、またはユーザがアプリケーションを使用するたびに、まずアプリケーションの同意を取得する必要があるため、プロセスのステップが異なります。 詳細については、「[個別の Dynamics 365 テナントを使用してアプリケーションをテストする](#bkmk_TestUsingSeparateTenant)」を参照してください。  
  
<a name="bkmk_CreateSecurityRole"></a>  
 
### <a name="create-a-security-role-for-the-application-user"></a>アプリケーション ユーザーによるセキュリティ ロールを作成します  

 次の手順で、[Common Data Service] アプリケーション ユーザーを作成します。 このユーザーの特権とアクセス権は、設定したカスタム セキュリティ ロールで定義されます。 アプリケーションでユーザーを作成する前に、カスタム セキュリティ ロールを作成してユーザーを関連付けることができます。 詳細: [セキュリティ ロールの作成または編集](https://technet.microsoft.com/library/dn531130.aspx)  
  
> [!NOTE]
>  アプリケーション ユーザーは既定の Common Data Service セキュリティ ロールの 1 つと関連付けることができません。 アプリケーション ユーザーに関連付ける、ユーザー定義のセキュリティ ロールを作成する必要があります。  
  
<a name="bkmk_ManuallyCreateUser"></a>   

### <a name="manually-create-a-common-data-service-application-user"></a>[Common Data Service] アプリケーション ユーザーを手動で作成します  

 このユーザーを作成する手順は、ライセンスを受けたユーザーを作成する手順とは異なります。 次の手順を実行します。  
  
1. **設定** > **セキュリティ** > **ユーザー**の順に移動します  
  
2. ビュー ドロップダウンで、**アプリケーション ユーザー**を選択します。  
  
3. **新規**をクリックします。 次に**アプリケーション ユーザー**フォームを使用していることを確認します。  
  
    フォーム上に **アプリケーション ID**, **アプリケーション ID URI** 、 **Azure AD オブジェクト ID** フィールドがない場合は、リストから **アプリケーション ユーザー** を選択してください:  
  
   ![アプリケーション ユーザー フォームの選択](media/select-application-user-form.PNG "アプリケーション ユーザー フォームの選択")  
  
4. フィールドに適切な値を追加します:  
  
   |フィールド|Value|  
   |-----------|-----------|  
   |**アプリケーション ID**|Azure AD に登録されたアプリケーションのアプリケーションID の値|  
   |**氏名**|アプリケーションの名前。|  
   |**電子メール 1**|サブスクライバーが連絡するときに使用する電子メール アドレス。|  
  
    **ユーザー名**、**アプリ ID URI** および **Azure AD オブジェクト ID** フィールドはロックされているため、これらのフィールドの一意の値を設定することはできません。  
  
    このユーザーを作成すると、これらフィールドの値には当該ユーザーを保存した際の **アプリケーションID** 値に基づいて Azure AD から取得されます。  
  
5. アプリケーション ユーザーを「[アプリケーション ユーザーによるセキュリティ ロールを作成する](#bkmk_CreateSecurityRole)」で作成されたカスタム セキュリティ ロールに関連付けます。 詳細情報: [Dynamics 365 (online) でのユーザーの作成およびセキュリティ ロールの割り当て](/dynamics365/customer-engagement/admin/create-users-assign-online-security-roles)  
  
<a name="bkmk_TestUsingYourTenant"></a>  
 
## <a name="test-your-application-using-your-common-data-service-tenant"></a>[Common Data Service] テナントを使用してアプリケーションをテストします 
 
 アプリケーションが Azure AD テナントに登録され、また開発組織のアプリケーション ユーザーが既に構成されているため、独自の Common Data Service テナントに対してアプリケーションを開発し続けることができます。 ただし、これは、マルチテナント機能の有効なテストではありません。 別の [Common Data Service] テナントでアプリケーションをテストする必要があります。  
  
<a name="bkmk_TestUsingSeparateTenant"></a>   

## <a name="test-your-application-using-a-separate-common-data-service-tenant"></a>別の [Common Data Service] テナントを使用してアプリケーションをテストします  

 別の Common Data Service テナントでアプリケーションをテストする前に、Azure AD テナントの管理者はアプリケーション向けの同意を取得する必要があります。 管理者は、ブラウザーを使用してアプリケーションに移動し同意を取得します。 初めてアプリケーションにアクセスすると、このようなダイアログが表示されます:  
  
 ![Dynamics 365 データにアクセスする同意を与える](media/grant-consent-to-access-crm-data.PNG "Dynamics 365 データにアクセスする同意を与える")  
  
 同意を取得すると、登録されたアプリケーションは、Azure ADEnterprise アプリケーション リストに追加され、Azure AD テナントのユーザーが使用できるようになります。  
  
 管理者が同意を取得した後でなければ、サブスクライバーの [Common Data Service] テナントでアプリケーション ユーザーを作成する必要があります。 「[Dynamics 365 アプリケーション ユーザーを手動で作成する](#bkmk_ManuallyCreateUser)」に記載された手順を使用してアプリケーション ユーザーを手動で作成することができます。  
  
 初期テストの場合は、これらのステップを手動で実行する必要があります。 サブスクライバーがアプリケーションまたはサービスを利用する準備ができたときに、より効率的なステップを使用します。 これについては、次のセクションで説明します。  
  
<a name="bkmk_PrepareMethodToDeployAppUser"></a>
   
## <a name="prepare-a-method-to-deploy-the-application-user"></a>アプリケーション ユーザーを展開するメソッドを準備します  

 サブスクライバーがアプリケーションまたはサービスの同意を取得した後、[Common Data Service] 組織にアプリケーション ユーザーとその他の必須コンポーネントを追加するための簡単で信頼できる方法が必要になります。  
  
 アプリケーションに必要な特権を定義し、アプリケーション ユーザーがそのカスタム セキュリティ ロールに関連付けられていることを確認するカスタムセキュリティロールを含める必要があります。 カスタム セキュリティ ロールをソリューションに含めることができるため、カスタム セキュリティ ロールの定義とアプリケーションに必要なその他のソリューション コンポーネントを含む管理 ソリューションを準備する必要があります。  
  
 カスタム セキュリティ ロールの作成の詳細については、参照してください  
  
- [セキュリティ ロールの作成または編集](/dynamics365/customer-engagement/admin/create-edit-security-role)  
- [セキュリティ ロールのコピー](/dynamics365/customer-engagement/admin/copy-security-role)  
- [ソリューション コンポーネントの追加](/dynamics365/customer-engagement/customize/create-solution.md#add-solution-components)
  
  [Common Data Service] ソリューションの作成に関する詳細は、次のトピックを参照してください:
  
- [カスタマイズでのソリューションの使用](../../maker/common-data-service/use-solutions-for-your-customizations.md)  
- [ソリューションを使用した拡張機能のパッケージ化および配布](/dynamics365/customer-engagement/developer/package-distribute-extensions-use-solutions)  
  
  ただし、アプリケーション ユーザーをソリューションに含めることはできないため、このアプリケーション ユーザーを作成しカスタム セキュリティ ロールを関連付ける方法を提供する必要があります。  
  
  Web サービスを使用して独自のプログラムを作成したりサブスクライバーにプログラムを実行させるなど、これを達成するにはいくつかの方法があります。  
  
  Dynamics 365 Package Deployer は、ソリューションおよびデータを別の Common Data Service 組織へ自動的に転送するパッケージの準備として使用できるアプリです。 詳細: [Dynamics 365 Package Deployer 用のパッケージを作成する](/dynamics365/customer-engagement/developer/create-packages-package-deployer)  
  
### <a name="see-also"></a>関連項目  
 [単一テナント型のサーバー間認証の使用](use-single-tenant-server-server-authentication.md)   
 [サーバー間 (S2S) の認証を使用して Web アプリケーションを作成する](build-web-applications-server-server-s2s-authentication.md)   
 [Dynamics 365 への接続](/dynamics365/customer-engagement/developer/connect-customer-engagement)

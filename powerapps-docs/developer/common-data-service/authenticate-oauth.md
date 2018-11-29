---
title: アプリ用 Common Data Service で OAuth を使用する (アプリ用 Common Data Service) | Microsoft Docs
description: アプリ用 Common Data Service で OAuth を使用して認証する方法に関する説明
ms.custom: ''
ms.date: 10/31/2018
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
# <a name="use-oauth-with-common-data-service-for-apps"></a>アプリ用 Common Data Service で OAuth を使用する

[OAuth 2.0](https://oauth.net/2/) は、認証の業界標準プロトコルです。 ユーザーが認証に資格情報を提供した後、OAuth はリソースにアクセスする権限があるかどうかを判断します。

クライアント アプリケーションは、Web API を使用してデータにアクセスする OAuth の使用をサポートする必要があります。 OAuth は、サーバー間アプリケーション シナリオの、2 要素認証 (2FA) または証明書ベースの認証を有効にします。

OAuth では、認証に ID プロバイダーが必要です。 アプリ用 Common Data Service での ID プロバイダーは Azure Active Directory (AAD) です。 Microsoft の職場または学校のアカウントを使用する AAD で認証するには、Azure Active Directory 認証ライブラリ (ADAL) を使用します。

> [!NOTE]
> このトピックでは、ADAL ライブラリの OAuth を使用するアプリ用 CDS への接続に関する一般的な概念を紹介します。 このコンテンツは、開発者がアプリ用 CDS に接続する方法に焦点を当てていますが、OAuth や ADAL ライブラリの内部構造には焦点を当てていません。 認証に関連する詳細については、Azure Active Directory のドキュメントを参照してください。 [認証とは何か](/azure/active-directory/develop/authentication-scenarios) のページから参照することをお勧めします。
>
>提供するサンプルは適切な登録値で事前に構成されているため、独自のアプリ登録を生成せずに実行できます。 独自のアプリを公開する場合は、独自の登録値を使用する必要があります。

## <a name="app-registration"></a>アプリ登録

OAuth を使用して接続する場合、最初に Azure AD テナントでアプリの登録をする必要があります。 アプリを登録する方法は、作成するアプリの種類によって異なります。

いずれの場合でも、AAD トピック [クイックスタート: Azure Active Directory v1.0 エンド ポイントでアプリを登録する](/azure/active-directory/develop/quickstart-v1-add-azure-ad-app) で説明されたアプリ登録の基本ステップから始めます。 アプリ用 CDS の具体的な手順については、[チュートリアル: Azure Active Directory でアプリを登録する > アプリケーション登録を作成する](walkthrough-register-app-azure-active-directory.md#create-an-application-registration) を参照してください。

このステップで実行する必要のある決定のほとんどは、アプリケーションの種類の選択に依存します。

### <a name="types-of-app-registration"></a>アプリ登録の種類

Azure AD でアプリを登録する場合、実行する必要のある決定の 1 つはアプリケーションの種類です。 登録できるアプリケーションには 2 種類あります。

|アプリケーションの種類|説明|
|--|--|
|Web アプリ /API|**Web クライアント**<br />Web サーバーですべてのコードを実行する [クライアント アプリケーション](/azure/active-directory/develop/developer-glossary#client-application) の種類。<br /><br />**ユーザー エージェント ベースのクライアント**<br />Single Page Application (SPA) などの Web サーバーからコードをダウンロードし、ユーザー エージェント内で実行する (たとえば、Web ブラウザー) [クライアント アプリケーション](/azure/active-directory/develop/developer-glossary#client-application) の種類。 
|
|ネイティブ モード|デバイスでネイティブにインストールされる [クライアント アプリケーション](/azure/active-directory/develop/developer-glossary#client-application) の種類。 |

**Web アプリ /API** を選択する場合、**サインオン URL** を提供する必要があります。それは認証が成功した場合、Azure AD がトークンを含む認証応答を送信する場所である URL です。 アプリの開発中に、これは通常 `http://localhost/appname:[port]` に設定され、アプリをローカルに開発およびデバッグできます。 アプリを公開する場合、アプリの公開された URL へのこの値を変更する必要があります。

**ネイティブ**を選択する場合、リダイレクト URI を提供する必要があリます。 これは、Azure AD が OAuth 2.0 リクエストでユーザー エージェントをリダイレクトする一意の識別子です。 これは通常、次のように書式設定された値です: `//app:<guid>`。 

### <a name="giving-access-to-cds-for-apps"></a>アプリ用 CDS へのアクセス

アプリが、認証されたユーザーに操作を実行させるクライアントである場合、アクセス許可を委任された組織のユーザーとして Dynamics 365 にアクセスするようアプリケーションを構成する必要があります。

この具体的な手順については、[チュートリアル: Azure Active Directory でアプリを登録する > アクセス許可を適用する](walkthrough-register-app-azure-active-directory.md#apply-permissions) を参照してください。

<!-- TODO Verify this --> アプリがサーバー間 (S2S) の認証を使用する場合、この手順は必要ありません。 その構成には特定のシステム ユーザーが必要であり、その操作は認証が必要である任意のユーザーによるのではなく、そのユーザー アカウントにより実行されます。

### <a name="enable-implicit-flow"></a>暗黙的なフローを有効にする

アプリを Single Page Application (SPA) に構成している場合、マニフェストの `oauth2AllowImplicitFlow` 値を `true` に設定するよう変更する必要があります。 詳細: [チュートリアル: adal.js で SPA アプリケーションを登録および構成する](walkthrough-registering-configuring-simplespa-application-adal-js.md)

### <a name="use-client-secrets--certificates"></a>クライアント シークレット & 証明書の使用

サーバ間のシナリオでは、認証する対話型ユーザー アカウントはありません。 このような場合、アプリケーションが信頼できることを確認するためのいくつかの手段を提供する必要があります。 これはクライアント シークレットまたは証明書を使用して実行されます。

**Web アプリ /API** アプリケーションの種類で登録されるアプリに関しては、シークレットを構成できます。 これらは、アプリ登録の**設定**で **API アクセス** にある**キー**領域を使用して設定されます。 

どちらのアプリケーションの種類でも、証明書をアップロードできます。

詳細: [アプリとして接続](#connect-as-an-app)

## <a name="use-adal-libraries-to-connect"></a>ADAL ライブラリを使用して接続

Microsoft によりサポートされている Azure Active Directory 認証ライブラリ (ADAL) クライアント ライブラリの 1 つを使用します。 [Azure Active Directory 認証ライブラリ > Microsoft によりサポートされているクライアント ライブラリ](/azure/active-directory/develop/active-directory-authentication-libraries#microsoft-supported-client-libraries)。

これらのライブラリは、次の表に表示されるように、さまざまなプラットファームで使用可能です。

|プラットフォーム|ライブラリ|
|--|--|
|.NET クライアント、Windows ストア、UWP、Xamarin |ADAL .NET v3|
|.NET クライアント、Windows ストア、Windows Phone 8.1|ADAL .NET v2|
|JavaScript|ADAL.js|
|iOS、macOS|ADAL|
|Android|ADAL|
|Node.js|ADAL|
|Java|ADAL4J|
|Python|ADAL|

> [!NOTE]
> 現在は、JavaScript ADAL.js ライブラリを使用する [OAuth を使用するクロス オリジン リソース共有を使用して、単一のページ アプリケーションに接続する](oauth-cross-origin-resource-sharing-connect-single-page-application.md) を除くすべてのサンプルは .NET クライアント ライブラリを使用します。

## <a name="adal-net-client-library-versions"></a>ADAL .NET クライアント ライブラリ バージョン

.NET クライアントをサポートする 2 つのライブラリがあります。 ADAL .NET v3 ライブラリは最新ですが ADAL .NET v2 ライブラリを置き換えるものではありません。

> [!IMPORTANT]
> .NET フレームワーク アプリケーションに Xrm.Tooling を使用している場合、ADAL .NET v2 ライブラリを使用する必要があります。

.NET クライアント バージョン間の大きな違いの 1 つは、v2 ライブラリがユーザー資格情報を渡すサポートを提供していることです。 v3 ライブラリでは、ブラウザーのポップアップを使用して対話形式でユーザ資格情報を取得する必要があります。

Xrm.Tooling を使用していない場合、Web API で ADAL .NET v2 または v3 クライアント ライブラリを使用する場合があります。 v3 クライアント ライブラリを使用する例に関しては、[ADAL v3 WhoAmI サンプル](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/webapi/C%23/ADALV3WhoAmI/ADALV3WhoAmI) を参照してください。

## <a name="use-the-accesstoken-with-your-requests"></a>要求で AccessToken を使用します

ADAL ライブラリを使用するポイントは、要求に含めることができるトークンを取得することです。 これにはコードの数行のみが必要で、HttpClient がリクエストを実行するよう構成するにはさらにいくつかの行が必要です。

### <a name="simple-example"></a>単純な例

単一の Web API 要求を実行するために必要な最小コード数は次のとおりですが、推奨されている方法ではありません。

```csharp
class SampleProgram
{
    private static string serviceUrl = "https://yourorg.crm.dynamics.com"; 
    private static string clientId = "51f81489-12ee-4a9e-aaae-a2591f45987d"; 
    private static string userName = "you@yourorg.onmicrosoft.com";
    private static string password = "yourpassword";

    static void Main(string[] args)
    {

        AuthenticationContext authContext = 
        new AuthenticationContext("https://login.microsoftonline.com/common", false);  
        UserCredential credential = new UserCredential(userName, password);
        AuthenticationResult result = authContext.AcquireToken(serviceUrl, clientId, credential);
        //The access token
        string accessToken = result.AccessToken;

        using (HttpClient client = new HttpClient()) {
        client.BaseAddress = new Uri(serviceUrl);
        client.Timeout = new TimeSpan(0, 2, 0);  //2 minutes  
        client.DefaultRequestHeaders.Add("OData-MaxVersion", "4.0");
        client.DefaultRequestHeaders.Add("OData-Version", "4.0");
        client.DefaultRequestHeaders.Accept.Add(
            new MediaTypeWithQualityHeaderValue("application/json"));
        HttpRequestMessage request = 
            new HttpRequestMessage(HttpMethod.Get, "/api/data/v9.0/WhoAmI");
        //Set the access token
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", accessToken);
        HttpResponseMessage response = client.SendAsync(request).Result;
        if (response.IsSuccessStatusCode)
        {
            //Get the response content and parse it.  
            JObject body = JObject.Parse(response.Content.ReadAsStringAsync().Result);
            Guid userId = (Guid)body["UserId"];
            Console.WriteLine("Your system user ID is: {0}", userId);
        }

    }
}
```

`AccessToken` が 1 時間以内に期限切れになるため、この単純な方法は従うべき良いパターンとは言えません。 ADAL ライブラリはトークンをキャッシュし、`AcquireToken` メソッドが呼び出されるたびにそれを更新します。

### <a name="example-demonstrating-a-delegatinghandler"></a>DelegatingHandler を示す例

推奨されている方法は、<xref:System.Net.Http.HttpClient> のコンストラクタに渡される <xref:System.Net.Http.DelegatingHandler> から派生したクラスを実装することです。 このハンドラーでは <xref:System.Net.Http.HttpClient> を上書きすることができるようになります。<xref:System.Net.Http.HttpClient.SendAsync*> メソッドは、http クライアントにより送信される各要求で ADAL が `AcquireToken` メソッドを呼び出すようになります。

次の図は、<xref:System.Net.Http.DelegatingHandler> から派生したカスタム クラスの例を示します。

```csharp
  /// <summary>  
  ///Custom HTTP message handler that uses OAuth authentication thru ADAL.  
  /// </summary>  
  class OAuthMessageHandler : DelegatingHandler
  {
    private UserCredential _credential;
    private AuthenticationContext _authContext = 
      new AuthenticationContext("https://login.microsoftonline.com/common", false);
    private string _clientId;
    private string _serviceUrl;

    public OAuthMessageHandler(string serviceUrl, string clientId, string userName, string password,
            HttpMessageHandler innerHandler)
        : base(innerHandler)
    {
      _credential = new UserCredential(userName, password);
      _clientId = clientId;
      _serviceUrl = serviceUrl;
    }

    protected override Task<HttpResponseMessage> SendAsync(
             HttpRequestMessage request, System.Threading.CancellationToken cancellationToken)
    {
      try
      {
        request.Headers.Authorization =
        new AuthenticationHeaderValue("Bearer", _authContext.AcquireToken(_serviceUrl, _clientId, _credential).AccessToken);
      }
      catch (Exception ex)
      {
        throw ex;
      }      
      return base.SendAsync(request, cancellationToken);
    }
  }
```

この `OAuthMessageHandler` クラスを使用して、上に表示された単純なプログラムはこのようになりますが、いくつかの追加のエラー処理が含まれています。

```csharp
class SampleProgram
{
    private static string serviceUrl = "https://yourorg.crm.dynamics.com"; 
    private static string clientId = "51f81489-12ee-4a9e-aaae-a2591f45987d"; 
    private static string userName = "you@yourorg.onmicrosoft.com";
    private static string password = "yourpassword";

    static void Main(string[] args)
    {
       HttpMessageHandler messageHandler;

      try
      {
        messageHandler = new OAuthMessageHandler(serviceUrl, clientId, userName, password,
                         new HttpClientHandler());
        //Create an HTTP client to send a request message to the CRM Web service.  
        using (HttpClient client = new HttpClient(messageHandler))
        {
          //Specify the Web API address of the service and the period of time each request   
          // has to execute.  
          client.BaseAddress = new Uri(serviceUrl);
          client.Timeout = new TimeSpan(0, 2, 0);  //2 minutes
          client.DefaultRequestHeaders.Add("OData-MaxVersion", "4.0");
          client.DefaultRequestHeaders.Add("OData-Version", "4.0");
          client.DefaultRequestHeaders.Accept.Add(
              new MediaTypeWithQualityHeaderValue("application/json"));

          //Send the WhoAmI request to the Web API using a GET request.   
          var response = client.GetAsync("api/data/v9.0/WhoAmI",
                  HttpCompletionOption.ResponseHeadersRead).Result;
          if (response.IsSuccessStatusCode)
          {
            //Get the response content and parse it.  
            JObject body = JObject.Parse(response.Content.ReadAsStringAsync().Result);
            Guid userId = (Guid)body["UserId"];
            Console.WriteLine("Your system user ID is: {0}", userId);
          }
          else
          {
            throw new Exception(response.ReasonPhrase);
          }
        }
      }
      catch (Exception ex)
      {
        DisplayException(ex);
      }
    }

    /// <summary> Displays exception information to the console. </summary>  
    /// <param name="ex">The exception to output</param>  
    private static void DisplayException(Exception ex)
    {
      Console.WriteLine("The application terminated with an error.");
      Console.WriteLine(ex.Message);
      while (ex.InnerException != null)
      {
        Console.WriteLine("\t* {0}", ex.InnerException.Message);
        ex = ex.InnerException;
      }
    }
}
```

その場合この例では、<xref:System.Net.Http.HttpClient> を使用します。<xref:System.Net.Http.HttpClient.GetAsync*> <xref:System.Net.Http.HttpClient.SendAsync*> を上書きするのではなく、要求に送信される <xref:System.Net.Http.HttpClient> メソッドのいずれかを適用します。


## <a name="connect-as-an-app"></a>アプリとして接続

作成する一部のアプリは、ユーザーが対話的に実行するためのものではありません。 たとえば、アプリ用 CDS のデータまたは何らかのスケジュールされたタスクを実行するコンソール アプリケーションで操作を実行できる Web クライアント アプリケーションを作成するとします。 

一般のユーザーの資格情報を使用してこれらのシナリオを実行することはできますが、そのユーザー アカウントでは有料ライセンスを使用する必要があります。 これは推奨されている方法ではありません。

このような場合、Azure Active Directory に登録されたアプリケーションにバインドされた特別なアプリケーション ユーザーを作成し、そのアプリ用に構成されたキー シークレットを使用するか [X.509](https://www.itu.int/rec/T-REC-X.509/en) 証明書をアップロードします。 この方法の別の利点は、有料ライセンスを使用しないことです。

### <a name="requirements-to-connect-as-an-app"></a>アプリとして接続するための要求

アプリとして接続するには以下の点が必要です。
 - 登録済みアプリ
 - 登録済みアプリにバインドされたアプリ用 CDS のユーザー
 - アプリケーション シークレットまたは証明書サムプリントのいずれかを使用して接続する

#### <a name="register-your-app"></a>アプリの登録

アプリを登録する場合、以下の例外も含め、[チュートリアル: Azure Active Directory でアプリを登録する](walkthrough-register-app-azure-active-directory.md) に記載される同じステップの多くに従います。

 - **組織のユーザーとして Dynamics 365 にアクセスする**アクセス許可の付与は必要ありません。
 
    このアプリケーションは特定のユーザー アカウントにバインドされます。

 - アプリ登録のシークレットを構成するか、公開キー証明書をアップロードする必要があります。

アプリを登録している間に、**設定**ページの**キー**セクションを選択します。

証明書を追加するには:
1. **公開キーのアップロード**を選択します。
2. アップロードするファイルを選択します。 次のいずれかのファイルの種類である必要があります: .cer、.pem、.crt。

パスワードを追加するには:

1. キーに関する説明を追加します。
2. 期間を選択します。
3. **保存**を選びます。 

  構成の変更を保存した後、一番右の列にキー値が表示されます。 このページから一旦離れるとアクセスできないため、クライアント アプリケーション コードで使用するためにキーをコピーしておいてください。

#### <a name="cds-for-apps-user-account-bound-to-the-registered-app"></a>登録済みアプリにバインドされたアプリ用 CDS のユーザー アカウント

最初に行う必要があるのは、ユーザー定義のセキュリティ ロールを作成して、このアカウントがアプリ用 CDS の組織内でどのアクセス権と特権を持つかを定義することです。 詳細: [ユーザー定義セキュリティ ロールの作成または編集](../../administrator/database-security.md#create-or-configure-a-custom-security-role)

ユーザー定義セキュリティ ロールを作成した後、使用するユーザー アカウントを作成する必要があります。

<!-- Almost exactly the same intructions below can be found in powerapps-docs\developer\common-data-service\use-multi-tenant-server-server-authentication.md -->

#### <a name="manually-create-a-cds-for-apps-application-user"></a>アプリ用 CDS のアプリケーション ユーザーを手動で作成します  

 このユーザーを作成する手順は、ライセンスを受けたユーザーを作成する手順とは異なります。 次の手順を実行します。  
  
1. **設定** > **セキュリティ** > **ユーザー**の順に移動します  
  
2. ビュー ドロップダウンで、**アプリケーション ユーザー**を選択します。  
  
3. **新規**をクリックします。 次に**アプリケーション ユーザー**フォームを使用していることを確認します。  
  
    フォームの**アプリケーション ID**、**Application ID URI** および **Azure AD オブジェクト ID** フィールドが表示されない場合は、リストから**アプリケーションのユーザー**フォームを選択する必要があります:  
  
   ![アプリケーション ユーザー フォームの選択](media/select-application-user-form.PNG "アプリケーション ユーザー フォームの選択")  
  
4. フィールドに適切な値を追加します:  
  
   |フィールド|Value|  
   |-----------|-----------|
   |**ユーザー名**| ユーザーの名前|
   |**アプリケーション ID**|Azure AD に登録されたアプリケーションのアプリケーション ID 値。|  
   |**氏名**|アプリケーションの名前。|  
   |**電子メール 1**|ユーザーの電子メール アドレス。|  
  
    **アプリケーション ID URI** および **Azure AD オブジェクト ID** フィールドはロックされているため、これらのフィールドの値を設定することはできません。  
  
    このユーザーを作成するときのこれらのフィールド値は、ユーザーを保存するときの**アプリケーション ID** 値に基づいて Azure AD から取得されます。  
  
5. アプリケーション ユーザーを作成したユーザー定義セキュリティ ロールに関連付けます。

#### <a name="connect-using-the-application-secret"></a>アプリケーション シークレットを使用して接続する

アプリケーション用に構成されたシークレットを使用して接続している場合、`userName` および `password` パラメーターの <xref:Microsoft.IdentityModel.Clients.ActiveDirectory.UserCredential> ではなく、`clientId` および `clientSecret` で渡している <xref:Microsoft.IdentityModel.Clients.ActiveDirectory.ClientCredential> クラスを使用します。
```csharp
string serviceUrl = "https://yourorg.crm.dynamics.com";
string clientId = "<your app id>";
string secret = "<your app secret>";

AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/common", false);
ClientCredential credential = new ClientCredential(clientId, secret);

AuthenticationResult result = authContext.AcquireToken(serviceUrl, credential);

string accessToken = result.AccessToken;
```
#### <a name="connect-using-a-certificate-thumbprint"></a>証明書サムプリントを使用して接続する

証明書を使用し <xref:Microsoft.Xrm.Tooling.Connector> を使用して接続している場合。<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient> 次のようなコードを使用できます。

```csharp
string CertThumbPrintId = "DC6C689022C905EA5F812B51F1574ED10F256FF6";
string AppID = "545ce4df-95a6-4115-ac2f-e8e5546e79af";
string InstanceUri = "https://yourorg.crm.dynamics.com";

string ConnectionStr = $@"AuthType=Certificate;
                        SkipDiscovery=true;url={InstanceUri};
                        thumbprint={CertThumbPrintId};
                        ClientId={AppID};
                        RequireNewInstance=true";
using (CrmServiceClient svc = new CrmServiceClient(ConnectionStr))
{
    if (svc.IsReady)
    {
    //your code goes here
    }

}
```


### <a name="see-also"></a>関連項目

[アプリ用 Common Data Service Web サービスでの認証](authentication.md)<br />
[.NET Framework アプリケーションでの認証](authenticate-dot-net-framework.md)
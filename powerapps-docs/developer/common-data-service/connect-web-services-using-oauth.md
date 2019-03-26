---
title: OAuth を使用してアプリ用 Common Data Service Web サービスに接続 (アプリ用 Common Data Service) | Microsoft Docs
description: OAuthを使用してDynamics 365 Customer Engagement Webサービスに接続する方法、およびDynamics 365 WebサービスIDプロバイダーで、ADAL APIによりOAuth 2.0認証を管理する方法について説明します
ms.custom: ''
ms.date: 01/25/2019
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
# <a name="connect-to-web-services-using-oauth"></a>OAuth を使用した Web サービスへの接続

OAuth はアプリ用 Common Data Service Web API によってサポートされる認証方法で、組織サービスの 2 つの認証方法のうちの 1 つです。もう 1 つは Azure Active Directory 認証です。 OAuth を使用する利点は、アプリケーションが複数要素認証をサポートできることです。 アプリケーションが組織サービスまたは探索サービスに接続するときに、OAuth 認証を使用することができます。  
  
 Web サービスのメソッド呼び出しは、サービス エンドポイントの ID プロバイダーによって承認される必要があります。 認証は、有効な OAuth 2.0 (ユーザー) アクセス トークンが Azure Active Directory により発行されるとき承認され、メッセージ要求ヘッダーに提供されます。  
  
 アプリ用 CDS Web API を使用する認証 API として、[Azure Active Directory 認証ライブラリ (ADAL)](https://azure.microsoft.com/en-us/documentation/articles/active-directory-authentication-libraries/) をお勧めします。これは各種のプラットフォームとプログラミング言語で使用することができます。 ADAL API はアプリ用 CDS Web サービス ID プロバイダーを使用した OAuth 2.0 認証を管理します。 使用されている実際の OAuth プロトコルの詳細については、[CRM サービスでの認証に OAuth を使用](http://blogs.msdn.com/b/crm/archive/2013/12/12/use-oauth-to-authenticate-with-the-crm-service.aspx) を参照してください。  
 
> [!NOTE]
> ADAL 2.0 ライブラリを使用する必要があります。 すべての Dynamics 365 Customer Engagement のツール、アセンブリ、およびユーティリティでは、ADAL 2.0 でサポートされるパターンが必要です。
> ADAL 3.0 ライブラリはユーザーのアカウント情報を取得するためのサインイン画面を必要とし、Dynamics 365 Customer Engagement で要求されるヘッドレス形式でこのアカウント情報を提供しません。 

OAuth 認証を使用してアプリ用 CDS Web サービスに接続する前に、アプリケーションは最初に Azure Active Directory に登録されている必要があります。 Azure Active Directory は、アプリ用 CDS テナントに保存されているビジネス データへのアクセスを許可するアプリケーションを確認するために使用されます。  
  
## <a name="authenticate-using-adal"></a>ADAL を使用した認証  
 ADAL を使用した基本的な OAuth Web サービスの認証は、コードを数行使用することで行われます。  
  
```csharp  
// TODO Substitute your correct CRM root service address,   
string resource = "https://mydomain.crm.dynamics.com";  
  
// TODO Substitute your app registration values that can be obtained after you  
// register the app in Active Directory on the Microsoft Azure portal.  
string clientId = "e5cf0024-a66a-4f16-85ce-99ba97a24bb2";  
string redirectUrl = "http://localhost/SdkSample";  
  
// Authenticate the registered application with Azure Active Directory.  
AuthenticationContext authContext =   
    new AuthenticationContext("https://login.windows.net/common", false);  
AuthenticationResult result = authContext.AcquireToken(resource, clientId, new Uri(redirectUrl));  
```  
  
 認証コンテキストは、有名な権限プロバイダーを使用して返されます。 呼び出している CDS for Apps インスタンスに関連した Azure Active Directory テナントが分からない場合、` https://login.microsoftonline.com` の固定の文字列、複数のテナント シナリオのための権限である URL を使用できます。 実行時に動的に権限を検索する代替方法については、このトピックの後半で説明します。  
  
 次のコード行で、検索するアクセス トークンを含む認証結果が表示されます。 このトークンを使用して Web サービスにメッセージの要求を送信できます。  
  
 このコードでいくつかの関心のある項目とは、使用されている文字列値です。 リソースの変数は、Transport Layer Security (TLS)またはドメインを含む、アプリ用 CDS サーバーの Secure Sockets Layer (SSL) のルート アドレスを含めます。 `clientId` および `redirectUrl` 変数には、Azure Active Directory で登録したアプリによる、アプリ登録情報が含まれています。 アプリ登録の詳細については、[チュートリアル: Azure Active Directory に Dynamics 365 アプリを登録する](/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory) を参照してください。  
  
## <a name="use-the-access-token-in-message-requests"></a>メッセージ要求にアクセス トークンを使用します  
 使用しているアプリ用 CDS API に応じて、Web サービスにメッセージ要求を送信する 2 つの異なった方法があります。 Web API の場合、通常は HTTP メッセージ要求を送信します。 組織サービスの場合には、Web クライアント プロキシを使用してメッセージ要求を送信します。  
  
### <a name="http-message-request"></a>HTTP メッセージ要求  
 トークンへアクセスした後は、Web サービスに送信するメッセージ要求の認証ヘッダーをアクセス トークンの値に設定し、トークン タイプを `Bearer` に指定する必要があります。 認証ヘッダーの詳細については、[HTTP/1.1 プロトコル](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html) のセクション 14.8 を参照してください。 次のコードでは、`System.Net.Http.HttpClient` クラスを使用して、これがどのように実行されるかを示します。  
  
```csharp  
using (HttpClient httpClient = new HttpClient())  
{  
    httpClient.Timeout = new TimeSpan(0, 2, 0);  // 2 minutes  
    httpClient.DefaultRequestHeaders.Authorization =   
        new AuthenticationHeaderValue("Bearer", result.AccessToken);  
```  
  
### <a name="web-client-requests"></a>Web クライアントの要求

<xref:Microsoft.Xrm.Sdk.WebServiceClient.OrganizationWebProxyClient> または組織サービスの <xref:Microsoft.Xrm.Sdk.WebServiceClient.DiscoveryWebProxyClient> を使用する場合、<xref:Microsoft.Xrm.Sdk.WebServiceClient.WebProxyClient`1.HeaderToken>プロパティ値をアクセス トークンに簡単に設定します。  
  
## <a name="refresh-the-access-token"></a>アクセス トークンを更新します

アプリ用 CDS Web サービス メソッドの各呼び出しの前にアクセス トークンを更新することは、推奨されるベスト プラクティスです。 ADAL でキャッシュされたアクセス トークンを更新するには、同じコンテキストを使用してもう一度 `AcquireToken` メソッドを呼び出します。  
  
```csharp    
AuthenticationResult result = authContext.AcquireToken(resource, clientId, new Uri(redirectUrl));  
```  
  
その後、Web API を使用する際`result.AccessToken` で認証ヘッダーをもう一度設定し、または組織サービスを使用する際は <xref:Microsoft.Xrm.Sdk.WebServiceClient.WebProxyClient`1.HeaderToken> を設定します。  
  
```csharp    
httpClient.DefaultRequestHeaders.Authorization =   
    new AuthenticationHeaderValue("Bearer", result.AccessToken);  
```  
  
## <a name="discover-the-authority-at-run-time"></a>実行時の権限を確認します

認証の権限 URL、およびリソース URLは、次の ADAL コードを使用して実行時に動的に検出されます。 これは上記のコード スニペットで表示されている有名な権限 URL と比較して使用するための、推奨されている方法です。  
  
```csharp    
AuthenticationParameters ap = AuthenticationParameters.CreateFromResourceUrlAsync(  
                        new Uri("https://mydomain.crm.dynamics.com/api/data/")).Result;  
  
String authorityUrl = ap.Authority;  
String resourceUrl  = ap.Resource;  
```  
  
Web API の場合、権限 URL を取得する別の方法は、Web サービスに、アクセス トークンを指定しないメッセージ要求を送信することです。 これを *ベアラー チャレンジ* と呼びます。 反応は、権限 URL を取得するために解析されます。  
  
```csharp  
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", "");  
```  
  
### <a name="see-also"></a>関連項目  
 [チュートリアル: Azure Active Directory に Dynamics 365 アプリを登録する](/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory)   
 [複数要素認証ドキュメント](https://azure.microsoft.com/en-us/documentation/services/multi-factor-authentication/)   
 [OAuth 2.0](http://oauth.net/2/)

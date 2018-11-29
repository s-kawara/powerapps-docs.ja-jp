---
title: 'Web API Helper code: 認証クラス (アプリ用 Common Data Service)| Microsoft Docs'
description: 認証クラスがアプリ用 Common Data Service Web サービスへの接続の検証を確立することを支援
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: a7b5931c-3142-4616-a331-1e07b4d8845d
caps.latest.revision: 11
author: brandonsimons
ms.author: jdaly
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="web-api-helper-code-authentication-class"></a>Web API Helper code: 認証クラス

`Authentication` クラスを使用してアプリ用 Common Data Service Web サービスへの接続の検証を確立することを支援します。 このクラスは、2 つ認証プロトコルをサポートします: 設置型アプリ用 Common Data Service 用の [Windows 認証](https://docs.microsoft.com/en-us/windows-server/security/windows-authentication/windows-authentication-overview) またはアプリ用 Common Data Service (オンライン) またはインターネットに接続する展開 (IFD) 用の [OAuth 2.0](http://oauth.net/2/)。 このクラスは、OAuth プロトコルを処理するために Microsoft Azure の Active Directory 認証ライブラリ [ADAL](https://docs.microsoft.com/en-us/dotnet/api/microsoft.identitymodel.clients.activedirectory?view=azure-dotnet)) へ依存します。  
  
`Authentication` クラスは、[CRM SDK Web API ヘルパー ライブラリ](https://www.nuget.org/packages/Microsoft.CrmSdk.WebApi.Samples.HelperCode/) の Authentication.cs ファイルにあります。 オブジェクトの種類 System.Net.Http [HttpMessageHandler](https://msdn.microsoft.com/library/hh138091\(v=vs.110\).aspx) を通じて、アプリ用 Common Data Service サービスで保護された接続の確立ができるよう `Configuration` ヘルパー クラスの階層と組み合わせて動作するように設計されています。 詳細については、[アプリ用 Common Data Service Web API Helper Library (C#) の使用](use-microsoft-dynamics-365-web-api-helper-library-csharp.md) を参照してください。  
  
## <a name="authentication-processing"></a>認証プロセス
 
アプリ用 Common Data Service サービスの認証を使用する `Authentication` クラスのメカニズムは、`Configuration` パラメーターを持つコンストラクターが渡す情報によって異なります。 アプリ用 Common Data Service サービスでセキュリティ保護された、永続的な通信セッションを提供する System.Net.Http [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient\(v=vs.110\).aspx) インスタンスを作成するために使用できる HttpMessageHandler-派生したオブジェクトを構築しようとします。  
  
 まず、指定されたアプリ用 Common Data Service サービスが OAuth または Windows ネイティブ認証で使用されるかどうかを決定する簡単な検出ハンドシェイクが実行されます。  
  
- OAuth が使用される場合、[`OAuthMessageHandler`] オブジェクトは、ハンドシェイクで検出された認証を使用して作成されます。 System.Net.Http.[DelegatingHandler](/dotnet/api/system.net.http.delegatinghandler) から派生したこのクラスは、すべての要求が OAuth アクセス トークンに更新されるため、トークンの有効期限を明示的に管理する必要はありません。  
  
- Windows 認証を使用する場合、ユーザーの資格情報を指定すると、これらの資格情報を使用して [HttpClientHandler](/dotnet/api/system.net.http.httpclienthandler) が構築されます。  
  
- Windows 認証が使用されているがユーザー資格情報が指定されていない場合、HttpClientHandle は既定のネットワーク資格情報を使用して構築されます。  
  
## <a name="class-hierarchy-and-members"></a>クラスの階層とメンバー  
 次の表は、`Authentication` クラスのパブリック メンバーを示します。  
<!-- TODO:  
|||  
|-|-|  
|![Common Data Service for Apps Web API Helper Library&#45;Authentication Class Diagram](../media/web-api-helper-library-authentication-class-diagram.png "Common Data Service for Apps Web API Helper Library-Authentication Class Diagram")|**Authentication class**<br /><br /> *Properties:*<br /><br /> `Authority` – the URL of the server that manages OAuth authentication.<br /><br /> `ClientHandler` – the [HttpMessageHandler](https://msdn.microsoft.com/library/hh138091\(v=vs.110\).aspx)-derived object that provides the network credentials or authorization access token for message requests.<br /><br /> `Context` – the [AuthenticationContext](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.authenticationcontext.aspx) for an authentication event.<br /><br /> *Methods:*<br /><br /> `AquireToken` – For OAuth, returns an [AuthenticationResult](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.authenticationresult.aspx),  containing the refresh and access tokens, for the current authentication context.<br /><br /> `Authentication` – Initializes an instance of this class using the `Configuration` parameter.<br /><br /> `DiscoverAuthority` – Discovers the authentication authority of the Common Data Service for Apps web service.<br /><br /> <br /><br /> **OAuthMessageHandler class**<br /><br /> This nested class sets the authorization header for each sent message for Common Data Service for Apps (online) and IFD deployments.|   -->
  
## <a name="usage"></a>使用法  
 `Configuration` および `Authentication` クラスは、アプリ用 Common Data Service サービスへのセキュリティ保護された接続の確立と並行して使用するように設計されています。  まず、[`Configuration`] でオブジェクトの種類を作成し、[`Authentication`] コンストラクターに単一のパラメーターとして渡します。  正常に作成後、アプリ用 Common Data Service サービスに対するセキュリティ保護された、永続的な HTTP クライアント接続を構築するために、`ClientHandler` プロパティを使用することができます。  
  
 ほとんどの Web API C# サンプルで使用されるこの操作を実行するための一般的な方法の １ つは、次の行で示されるように、正常に作成された構成ファイルから接続情報を読み取るための `FileConfiguration`  
  
```csharp  
  
FileConfiguration config = new FileConfiguration(null);  
Authentication auth = new Authentication(config);  
httpClient = new HttpClient(auth.ClientHandler, true);  
  
```  
  
 この使用方法の詳細については、セクション [FileConfiguration 接続の構成](web-api-helper-code-configuration-classes.md#bkmk_FileConfigconnectionsettings) を参照してください。 [`Authentication`] クラスには、他のいくつかのパブリック プロパティとメソッドが含まれていますが、これらは主に [`ClientHandler`] プロパティに対する作成のサポートを提供するものであって、ほとんどのクライアント アプリケーションでは直接にアクセスされません。  
  
## <a name="class-listing"></a>クラスの一覧  

このクラスの最新ソースは、[CRM SDK Web API ヘルパー ライブラリ](https://www.nuget.org/packages/Microsoft.CrmSdk.WebApi.Samples.HelperCode) NuGet パッケージにあります。  
  
```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;  
using System;  
using System.Net;  
using System.Net.Http;  
using System.Net.Http.Headers;  
using System.Security;  
using System.Threading.Tasks;  
  
namespace Microsoft.Crm.Sdk.Samples.HelperCode  
{  
    /// <summary>  
    /// Manages user authentication with the Dynamics CRM Web API (OData v4) services. This class uses Microsoft Azure  
    /// Active Directory Authentication Library (ADAL) to handle the OAuth 2.0 protocol.   
    /// </summary>  
    public class Authentication  
    {  
        private Configuration _config = null;  
        private HttpMessageHandler _clientHandler = null;  
        private AuthenticationContext _context = null;  
        private string _authority = null;  
  
        #region Constructors  
        /// <summary>  
        /// Base constructor.  
        /// </summary>  
        public Authentication() { }  
  
        /// <summary>  
        /// Establishes an authentication session for the service.  
        /// </summary>  
        /// <param name="config">A populated configuration object.</param>  
        public Authentication(Configuration config)  
            : base()  
        {  
            if (config == null)  
                throw new Exception("Configuration cannot be null.");  
  
            _config = config;  
  
            SetClientHandler();  
        }  
  
        /// <summary>  
        /// Custom constructor that allows adding an authority determined asynchronously before   
        /// instantiating the Authentication class.  
        /// </summary>  
        /// <remarks>For a WPF application, first call DiscoverAuthorityAsync(), and then call this  
        /// constructor passing in the authority value.</remarks>  
        /// <param name="config">A populated configuration object.</param>  
        /// <param name="authority">The URL of the authority.</param>  
        public Authentication(Configuration config, string authority)  
            : base()  
        {  
            if (config == null)  
                throw new Exception("Configuration cannot be null.");  
  
            _config = config;  
            Authority = authority;  
  
            SetClientHandler();  
        }  
        #endregion Constructors  
  
        #region Properties  
        /// <summary>  
        /// The authentication context.  
        /// </summary>  
        public AuthenticationContext Context  
        {  
            get  
            { return _context; }  
  
            set  
            { _context = value; }  
        }  
  
        /// <summary>  
        /// The HTTP client message handler.  
        /// </summary>  
        public HttpMessageHandler ClientHandler  
        {  
            get  
            { return _clientHandler; }  
  
            set  
            { _clientHandler = value; }  
        }  
  
        /// <summary>  
        /// The URL of the authority to be used for authentication.  
        /// </summary>  
        public string Authority  
        {  
            get  
            {  
                if (_authority == null)  
                    _authority = DiscoverAuthority(_config.ServiceUrl);  
  
                return _authority;  
            }  
  
            set { _authority = value; }  
        }  
        #endregion Properties  
  
        #region Methods  
        /// <summary>  
        /// Returns the authentication result for the configured authentication context.  
        /// </summary>  
        /// <returns>The refreshed access token.</returns>  
        /// <remarks>Refresh the access token before every service call to avoid having to manage token expiration.</remarks>  
        public AuthenticationResult AcquireToken()  
        {  
            if (_config != null && (!string.IsNullOrEmpty(_config.Username) && _config.Password != null))  
            {  
                UserCredential cred = new UserCredential(_config.Username, _config.Password);  
                return _context.AcquireToken(_config.ServiceUrl, _config.ClientId, cred);  
            }  
            return _context.AcquireToken(_config.ServiceUrl, _config.ClientId, new Uri(_config.RedirectUrl),  
                PromptBehavior.Auto);  
        }  
  
        /// <summary>  
        /// Returns the authentication result for the configured authentication context.  
        /// </summary>  
        /// <param name="username">The username of a CRM system user in the target organization. </param>  
        /// <param name="password">The password of a CRM system user in the target organization.</param>  
        /// <returns>The authentication result.</returns>  
        /// <remarks>Setting the username or password parameters to null results in the user being prompted to  
        /// enter log-on credentials. Refresh the access token before every service call to avoid having to manage  
        /// token expiration.</remarks>  
        public AuthenticationResult AcquireToken(string username, SecureString password)  
        {  
  
            try  
            {  
                if (!string.IsNullOrEmpty(username) && password != null)  
                {  
                    UserCredential cred = new UserCredential(username, password);  
                    return _context.AcquireToken(_config.ServiceUrl, _config.ClientId, cred);  
                }  
            }  
            catch (Exception e)  
            {  
                throw new Exception("Authentication failed. Verify the configuration values are correct.", e);  
            }  
            return null;  
        }  
  
        /// <summary>  
        /// Discover the authentication authority.  
        /// </summary>  
        /// <returns>The URL of the authentication authority on the specified endpoint address, or an empty string  
        /// if the authority cannot be discovered.</returns>  
         public static string DiscoverAuthority(string serviceUrl)  
        {  
            try  
            {  
                AuthenticationParameters ap = AuthenticationParameters.CreateFromResourceUrlAsync(  
                    new Uri(serviceUrl + "api/data/")).Result;  
  
                return ap.Authority;  
            }  
            catch (HttpRequestException e)  
            {  
                throw new Exception("An HTTP request exception occurred during authority discovery.", e);  
            }  
            catch (System.Exception e )  
            {  
                // This exception ocurrs when the service is not configured for OAuth.  
                if( e.HResult == -2146233088 )  
                {  
                    return String.Empty;  
                }  
                else  
                {  
                    throw e;  
                }  
            }  
        }  
  
        /// <summary>  
        /// Discover the authentication authority asynchronously.  
        /// </summary>  
        /// <param name="serviceUrl">The specified endpoint address</param>  
        /// <returns>The URL of the authentication authority on the specified endpoint address, or an empty string  
        /// if the authority cannot be discovered.</returns>  
        public static async Task<string> DiscoverAuthorityAsync(string serviceUrl)  
        {  
            try  
            {  
                AuthenticationParameters ap = await AuthenticationParameters.CreateFromResourceUrlAsync(  
                    new Uri(serviceUrl + "api/data/"));  
  
                return ap.Authority;  
            }  
            catch (HttpRequestException e)  
            {  
                throw new Exception("An HTTP request exception occurred during authority discovery.", e);  
            }  
            catch (Exception e)  
            {  
                // These exceptions ocurr when the service is not configured for OAuth.  
  
                // -2147024809 message: Invalid authenticate header format Parameter name: authenticateHeader  
                if (e.HResult == -2146233088 || e.HResult == -2147024809)  
                {  
                    return String.Empty;  
                }  
                else  
                {  
                    throw e;  
                }  
            }  
        }  
  
        /// <summary>  
        /// Sets the client message handler as appropriate for the type of authentication  
        /// in use on the web service endpoint.  
        /// </summary>  
        private void SetClientHandler()  
        {  
            // Check the Authority to determine if OAuth authentication is used.  
            if (String.IsNullOrEmpty(Authority))  
            {  
                if (_config.Username != String.Empty)  
                {  
                    _clientHandler = new HttpClientHandler()  
                    { Credentials = new NetworkCredential(_config.Username, _config.Password, _config.Domain) };  
                }  
                else  
                // No username is provided, so try to use the default domain credentials.  
                {  
                    _clientHandler = new HttpClientHandler()  
                    { UseDefaultCredentials = true };  
                }  
            }  
            else  
            {  
                _clientHandler = new OAuthMessageHandler(this, new HttpClientHandler());  
                _context = new AuthenticationContext(Authority, false);  
            }  
        }  
        #endregion Methods  
  
        /// <summary>  
        /// Custom HTTP client handler that adds the Authorization header to message requests. This  
        /// is required for IFD and Online deployments.  
        /// </summary>  
        class OAuthMessageHandler : DelegatingHandler  
        {  
            Authentication _auth = null;  
  
            public OAuthMessageHandler( Authentication auth, HttpMessageHandler innerHandler )  
                : base(innerHandler)  
            {  
                _auth = auth;  
            }  
  
            protected override Task<HttpResponseMessage> SendAsync(  
                HttpRequestMessage request, System.Threading.CancellationToken cancellationToken)  
            {  
                // It is a best practice to refresh the access token before every message request is sent. Doing so  
                // avoids having to check the expiration date/time of the token. This operation is quick.  
                request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", _auth.AcquireToken().AccessToken);  
  
                return base.SendAsync(request, cancellationToken);  
            }  
        }  
    }  
}  
```  
  
### <a name="see-also"></a>関連項目  

[Web API (C#) を開始する](get-started-dynamics-365-web-api-csharp.md)<br />
[Visual Studio (C#) で Web API プロジェクトを起動する](start-web-api-project-visual-studio-csharp.md)<br />
[アプリ用 Common Data Service Web API Helper Library (C#) の使用](use-microsoft-dynamics-365-web-api-helper-library-csharp.md)<br />
[ヘルパー コード: 構成クラス](web-api-helper-code-configuration-classes.md)<br />
[ヘルパー コード: CrmHttpResponseException クラス](web-api-helper-code-crmhttpresponseexception-class.md)

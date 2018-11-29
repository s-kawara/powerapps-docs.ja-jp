---
title: 'Web API Helper code: 構成クラス (アプリ用 Common Data Service)| Microsoft Docs'
description: 構成クラス階層は、アプリケーションからアプリ用 Common Data Service Web サービスにアクセスするのに必要な接続データを指定するために使用できます
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 3b86c11a-15e1-40a1-aca0-34a9bab2f04a
caps.latest.revision: 14
author: brandonsimons
ms.author: jdaly
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="web-api-helper-code-configuration-classes"></a>Web API Helper code: 構成クラス

構成クラス階層は、アプリケーションからアプリ用 Common Data Service Web サービスにアクセスするのに必要な接続データを指定するために使用します。 `Configuration` 基本クラスを使用して、ユーザー入力などからの値を直接指定することによって、この接続データを提供できます。 通常は、派生クラス、`FileConfiguration` を使用して、アプリケーションの構成ファイルに保存されている設定でこの情報を指定します。  
  
構成クラス階層のソース コードは、[CRM SDK Web API Helper Library](https://www.nuget.org/packages/Microsoft.CrmSdk.WebApi.Samples.HelperCode/) の Configuration.cs ファイルにあります。 構成クラス階層は、アプリ用 Common Data Service サービスへのセキュリティ保護された接続の確立を可能にする `Authentication` クラスと組み合わせて使用するように設計されています。 詳細については、[アプリ用 Common Data Service Web API Helper Library (C#) の使用](use-microsoft-dynamics-365-web-api-helper-library-csharp.md) を参照してください。  
  
<a name="bkmk_Connectiondata"></a>

## <a name="connection-data"></a>接続データ

`Configuration` クラスは、アプリケーション構成ファイルを読み込み、解析し、次の接続データを取得します。  
  
|接続データ|展開|説明|  
|---------------------|-----------------|-----------------|  
|サービス URL|すべて|アプリ用 Common Data Service への基本 URL|  
|ユーザー名|すべて|アプリ用 CDS で登録されたユーザー名|  
|パスワード|すべて|そのユーザーのパスワード|  
|ドメイン|すべて|Active Directory 認証のアプリ用 Common Data Service のドメイン|  
|クライアント ID|オンラインおよび IFD のみ|アプリ用 Common Data Service の Azure AD で登録されたアプリケーションのクライアント ID|  
|リダイレクト URL|オンラインおよび IFD のみ|現在のアプリケーションのコールバック URI。|  
  
<!-- TODO:
For more information on obtaining a client ID and a redirection URL for an application, see [Walkthrough: Register a Common Data Service for Apps app with Azure Active Directory](../walkthrough-register-app-azure-active-directory.md).  
   -->
<a name="bkmk_FileConfigconnectionsettings"></a>

### <a name="fileconfiguration-connection-settings"></a>FileConfiguration 接続設定

アプリ用 Common Data Service Web API サンプルの大半は派生クラス、`FileConfiguration` を使用し、アプリケーション構成ファイル、App.config から接続データを抽出します。このファイルには異なるアプリ用 Common Data Service サーバー展開モードに適用する複数のアプリケーション設定があります。 `connectionString` 設定には、サービス URL とユーザー名が含まれています。 さらに、`ClientId` と `RedirectUrl` 設定はオンラインまたはインターネットに接続する展開 (IFD) で必要となります。 ほとんどの Web API サンプルで提供された既定となる App.config ファイルから抜粋した次の行には、プレースホルダー値としてこの接続データが含まれています。 これらのプレスホルダーは既存のユーザー、アプリ用 Common Data Service サーバー、およびクライアント アプリケーション固有の値に置き換える必要があります。  
  
```xml  
<connectionStrings> 
    <add name="default" connectionString="Url=http://myserver/myorg/; Username=name; Password=password; Domain=domain" /> 
</connectionStrings> 
<appSettings> 
    <add key="ClientId" value="e5cf0024-a66a-4f16-85ce-99ba97a24bb2" /> 
    <add key="RedirectUrl" value="http://localhost/SdkSample" /> 
</appSettings>  
```  
  
既定の構成ファイルの完全なコンテンツは、[既定の構成ファイルの一覧](#bkmk_Defaultconfigurationfilelisting) で提供されています。  
  
<a name="bkmk_Classhierarchyandmembers"></a>
 
## <a name="class-hierarchy-and-members"></a>クラスの階層とメンバー

次の図には、構成クラス階層のパブリック メンバーが表示されます。  
  
 <!-- TODO:
![Common Data Service for Apps Web API Helper Library&#45;Configuration Class Diagram](../media/web-api-helper-library-configuration-class-diagram.png "Common Data Service for Apps Web API Helper Library-Configuration Class Diagram")   -->
  
 **構成クラス**  
  
 *プロパティ:*  
  
 すべてのプロパティは前述のセクションに記載されている対応する接続データに直接マップされます。  
  
 *メソッド*:  
  
 既定のコンストラクターは、すべてのプロパティを初期化します (null)。  
  
 **FileConfiguration クラス**  
  
 *プロパティ:*  
  
 `Name` は接続文字列の設定エントリー名です。  
  
 `PathToConfig` はアプリケーション構成ファイルのフルまたは相対的パスです。  
  
 *メソッド*:  
  
 既定のコンストラクターは、すべてのプロパティを初期化します (null)。  
  
 既定のコンストラクター以外は、名前付き接続文字列を指定する単一の文字列パラメーターを受け取ります。 空白の文字列または null の文字列値は最初に使用される接続文字列のエントリになります。  
  
 `Load` メソッドは、指定された構成ファイルを開き、読み取り、解析します。 既定のコンストラクター以外で使用されます。  
  
<a name="bkmk_usage"></a>

## <a name="usage"></a>使用法

 `FileConfiguration` と `Authentication` クラスは、App.config の接続データの読み取りおよびターゲット アプリ用 Common Data Service サービスへのセキュリティで保護された接続の確立と連携して使用するように設計されています。 これは、次のステートメントで実行できます。  
  
```csharp  
FileConfiguration config = new FileConfiguration(null); Authentication auth = new Authentication(config); httpClient = new HttpClient(auth.ClientHandler, true);  
```  
  
 `Configuration` クラスの既定のコンストラクター以外は、次の例が示す名前が付けられた接続文字列の使用を有効にします:  
  
```csharp  
Configuration config = new FileConfiguration(“TestServer”);  
```  
  
 null または空白の接続文字列名が `FileConfiguration` クラス コンストラクターに渡されると、最初の接続文字列は構成ファイルの先頭から使用されます。  
  
 さらに、SDK サンプルは、コンストラクターに渡される、目的の接続文字列名を表すランタイム コマンド パラメーターをサポートします。 このオプションは次のコードによって実行されます:  
  
```csharp  
if (cmdargs.Length > 0) { config = new FileConfiguration(cmdargs[0]); } else { config = new FileConfiguration(null); }  
```  
  
<a name="bkmk_Configurationsearchorder"></a>

### <a name="configuration-search-order"></a>検索順序の構成

 既定またはカスタム アプリケーション構成ファイルを使用するかにおいて、任意の `AlternateConfig` アプリケーション設定は代替構成ファイルを指定するファイル内で使用できます。 このファイルが存在する場合、代わりにその接続設定が使用されます。  
  
```xml  
<add key="AlternateConfig" value="C:\Temp\crmsample.exe.config"/>  
```  
  
 この設定の一般的な使い方は、各 App.config ファイルを編集するのではなく、複数のアプリケーション間で共有できるグローバルな構成ファイルを指定することです。 これは、開発やテスト段階を通して、複数のアプリケーション間で構成と登録情報を共有する上で大変役に立ちます。 それゆえ、各アプリケーションにおける一意の構成および登録情報はプロダクション段階でのみ指定します。  
  
<a name="bkmk_Defaultconfigurationfilelisting"></a>

## <a name="default-configuration-file-listing"></a>既定の構成ファイルの一覧

 ほとんどのアプリ用 Common Data Service Web API サンプル付属のファイル App.config には、開発者やサイト管理者によって編集する必要があるプレースホルダー値が含まれています。  
  
```xml  
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
   <startup>
      <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
   </startup>
   <connectionStrings>
      <clear />
      <!-- When providing a password, make  
                sure to set the app.config file's security so that only you can read it. -->
      <add name="default" connectionString="Url=http://myserver/myorg/; Username=name; Password=password; Domain=domain" />
      <add name="CrmOnline" connectionString="Url=https://mydomain.crm.dynamics.com/;                   Username=someone@mydomain.onmicrosoft.com; Password=password" />
   </connectionStrings>
   <appSettings>
      <!--For information on how to register an app and obtain the ClientId and RedirectUrl values see https://msdn.microsoft.com/dynamics/crm/mt149065  
                -->
      <!--Active Directory application registration. -->
      <!--These are dummy values and should be replaced with your actual app registration values.-->
      <add key="ClientId" value="e5cf0024-a66a-4f16-85ce-99ba97a24bb2" />
      <add key="RedirectUrl" value="http://localhost/SdkSample" />
      <!-- Use an alternate configuration file for connection string and setting values. This optional setting enables use of an app.config file shared among multiple applications. If the specified file does not exist,  
                this setting is ignored.-->
      <add key="AlternateConfig" value="C:\Temp\crmsample.exe.config" />
   </appSettings>
</configuration>  
```  
  
## <a name="class-listing"></a>クラスの一覧

 このクラスの最新ソースは、[CRM SDK Web API ヘルパー ライブラリ](https://www.nuget.org/packages/Microsoft.CrmSdk.WebApi.Samples.HelperCode) NuGet パッケージにあります。  
  
```csharp  
using System;
using System.IO;
using System.Security;
using System.Configuration;

namespace Microsoft.Crm.Sdk.Samples.HelperCode
{
    /// <summary>
    /// An application configuration containing user logon, application, and web service information
    /// as required for CRM Web API authentication.
    /// </summary>
    public class Configuration
    {
        #region Properties
        /// <summary>
        /// The root address of the Dynamics CRM service.
        /// </summary>
        /// <example>https://myorg.crm.dynamics.com</example>
        public string ServiceUrl { get; set; }

        /// <summary>
        /// The redirect address provided when the application was registered in Microsoft Azure
        /// Active Directory or AD FS.
        /// </summary>
        /// <remarks>Required only with a web service configured for OAuth authentication.</remarks>
        /// <seealso cref="https://msdn.microsoft.com/library/dn531010.aspx#bkmk_redirect"/>
        public string RedirectUrl { get; set; }

        /// <summary>
        /// The client ID that was generated when the application was registered in Microsoft Azure
        /// Active Directory or AD FS.
        /// </summary>
        /// <remarks>Required only with a web service configured for OAuth authentication.</remarks>
        public string ClientId { get; set; }

        /// <summary>
        /// The user name of the logged on user or null.
        /// </summary>
        public string Username { get; set; }

        /// <summary>
        ///  The password of the logged on user or null.
        /// </summary>
        public SecureString Password { get; set; }

        /// <summary>
        ///  The domain of the logged on user account or null.
        /// </summary>
        /// <remarks>Required only with a web service configured for Active Directory authentication.</remarks>
        public string Domain { get; set; }

        #endregion Properties

        #region Constructors

        /// <summary>
        /// Constructs a configuration object.
        /// </summary>
        public Configuration() { }

        #endregion Constructors
    }

    /// <summary>
    /// A configuration that is persisted to file storage.
    /// </summary>
    /// <remarks>This implementation defaults to using an app.config file. However, you
    /// can derive a subclass and override the virtual methods to make use of other
    /// file formats.
    /// 
    /// One set of application registration settings and multiple named connection strings are supported.</remarks>
    public class FileConfiguration : Configuration
    {
        #region Properties
        /// <summary>
        /// The full or relative path to the application's configuration file.
        /// </summary>
        /// <remarks>The file name is in the format <appname>.exe.config.</appname></remarks>
        public string PathToConfig { get; set; }

        /// <summary>
        /// The name of the connection.
        /// </summary>
        public string Name { get; set; }

        #endregion Properties

        #region Constructors
        /// <summary>
        /// Constructs a file configuration.
        /// </summary>
        public FileConfiguration()
            : base()
        { }

        /// <summary>
        /// Loads a named connection string and application settings from persistent file storage.
        /// The configuration file must have the same name as the application and be located in the 
        /// run-time folder.
        /// </summary>
        /// <param name="name">The name of the target connection string. An empty or null string value 
        /// results in the first named configuration being used.</param>
        /// <remarks>The app.config file must exist in the run-time folder and have the name
        /// <appname>.exe.config. To specify an app.config file path, use the Load() method.</remarks>
        public FileConfiguration(string name)
            : base()
        {
            var path = System.IO.Path.Combine(Directory.GetCurrentDirectory(), Environment.GetCommandLineArgs()[0]);

            Load(name, String.Concat(path, ".config"));
        }

        #endregion Constructors

        #region Methods
        /// <summary>
        /// Loads server connection information and application settings from persistent file storage.
        /// </summary>
        /// <remarks>A setting named OverrideConfig can optionally be added. If a config file that this setting
        /// refers to exists, that config file is read instead of the config file specified in the path parameter.
        /// This allows for an alternate config file, for example a global config file shared by multiple applications.
        /// </summary>
        /// <param name="connectionName">The name of the connection string in the configuration file to use. 
        /// Each CRM organization can have its own connection string. A value of null or String.Empty results
        /// in the first (top most) connection string being used.</param>
        /// <param name="path">The full or relative pathname of the configuration file.</param>
        public virtual void Load(string connectionName, string path)
        {
            // Check passed parameters.
            if (string.IsNullOrEmpty(path) || !System.IO.File.Exists(path))
                throw new ArgumentException("The specified app.config file path is invalid.", this.ToString());
            else
                PathToConfig = path;

            try
            {
                // Read the app.config file and obtain the app settings.
                System.Configuration.Configuration config = null;
                ExeConfigurationFileMap configFileMap = new ExeConfigurationFileMap();
                configFileMap.ExeConfigFilename = PathToConfig;
                config = ConfigurationManager.OpenMappedExeConfiguration(configFileMap, ConfigurationUserLevel.None);

                var appSettings = config.AppSettings.Settings;

                // If an alternate config file exists, load that configuration instead. Note the test
                // for redirectTo.Equals(path) to avoid an infinite loop.
                if (appSettings["AlternateConfig"] != null)
                {
                    var redirectTo = appSettings["AlternateConfig"].Value;
                    if (redirectTo != null && !redirectTo.Equals(path) && System.IO.File.Exists(redirectTo))
                    {
                        Load(connectionName, redirectTo);
                        return;
                    }
                }

                // Get the connection string.
                ConnectionStringSettings connection;
                if (string.IsNullOrEmpty(connectionName))
                {
                    // No connection string name specified, so use the first one in the file.
                    connection = config.ConnectionStrings.ConnectionStrings[0];
                    Name = connection.Name;
                }
                else
                {
                    connection = config.ConnectionStrings.ConnectionStrings[connectionName];
                    Name = connectionName;
                }

                // Get the connection string parameter values.
                if (connection != null)
                {
                    var parameters = connection.ConnectionString.Split(';');
                    foreach (string parameter in parameters)
                    {
                        var trimmedParameter = parameter.Trim();
                        if (trimmedParameter.StartsWith("Url="))
                            ServiceUrl = parameter.Replace("Url=", String.Empty).TrimStart(' ');

                        if (trimmedParameter.StartsWith("Username="))
                            Username = parameters[1].Replace("Username=", String.Empty).TrimStart(' ');

                        if (trimmedParameter.StartsWith("Password="))
                        {
                            var password = parameters[2].Replace("Password=", String.Empty).TrimStart(' ');

                            Password = new SecureString();
                            foreach (char c in password) Password.AppendChar(c);
                        }
                        if (trimmedParameter.StartsWith("Domain="))
                            Domain = parameter.Replace("Domain=", String.Empty).TrimStart(' ');
                    }
                }
                else
                    throw new Exception("The specified connection string could not be found.");

                // Get the Azure Active Directory application registration settings.
                RedirectUrl = appSettings["RedirectUrl"]?.Value;
                ClientId = appSettings["ClientId"]?.Value;
            }
            catch (InvalidOperationException e)
            {
                throw new Exception("Required setting in app.config does not exist or is of the wrong type.", e);
            }
        }

        /// <summary>
        /// Save the current configuration to persistent file storage.
        /// </summary>
        /// <remarks>Any existing configuration is overwritten.</remarks>
        public virtual void Save()
        {
            throw new NotImplementedException();
        }

        /// <summary>
        /// Add a named connection string to persistent file storage.
        /// </summary>
        /// <remarks>A named connection string from the current configuration is added to an existing
        /// configuration file./remarks>
        public virtual void AddConnection()
        {
            throw new NotImplementedException();
        }

        #endregion Methods
    }
} 
```  
  
### <a name="see-also"></a>関連項目

[Web API (C#) を開始する](get-started-dynamics-365-web-api-csharp.md)<br />
[Visual Studio (C#) で Web API プロジェクトを起動する](start-web-api-project-visual-studio-csharp.md)<br />
[アプリ用 Common Data Service Web API Helper Library (C#) の使用](use-microsoft-dynamics-365-web-api-helper-library-csharp.md)<br />
[ヘルパー コード: 認証クラス](web-api-helper-code-authentication-class.md)<br />
[ヘルパー コード: CrmHttpResponseException クラス](web-api-helper-code-crmhttpresponseexception-class.md)<br />
[組織サービス エンドポイント用 SDK サンプル ヘルパー コード](https://www.nuget.org/packages/Microsoft.CrmSdk.Samples.HelperCode-CS)  
---
title: 'Visual Studio (C#) で Common Data Service for Apps Web API プロジェクトを開始する (Common Data Service for Apps)| Microsoft Docs'
description: Common Data Service for Apps Web API を使用するコンソール アプリケーションの構築のために Visual Studio で新しいプロジェクトを作成
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 08377156-32c7-492a-8e66-50a47a330dc6
caps.latest.revision: 14
author: brandonsimons
ms.author: jdaly
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="start-a-common-data-service-for-apps-web-api-project-in-visual-studio-c"></a>Visual Studio (C#) で Common Data Service for Apps Web API プロジェクトを開始する

このトピックでは、Common Data Service for Apps Web API を使用するコンソール アプリケーションを構築するために、Visual Studio で新しいプロジェクトを作成する方法を説明します。 SDK C# サンプルを含む多くのアプリケーションが、Web API ベースのソリューションを実装するのに使用する共通の参照およびプロジェクトのリソースを説明します。  
  
<a name="bkmk_prerequisites"></a> 
  
## <a name="prerequisites"></a>前提条件  

 次の前提条件は、このセクションで説明されているコンソール アプリケーションを作成するのに必要です。  
  
- Visual Studio 2015 は、開発用コンピューターにインストールされています。 [Visual Studio Express](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) など、どのエディションでも Common Data Service for Apps Web API は十分に操作できます。
  
-   次の NuGet クライアントをインストールする必要があります: コマンド ライン ユーティリティまたは Visual Studio 拡張。 詳細については、「[NuGet のインストール](https://docs.nuget.org/consume/installing-nuget)」を参照してください。  
  
-   Common Data Service for Apps Web API Helper Library が含まれている NuGet パッケージおよびその他の依存パッケージをダウンロードするのにインターネット接続が必要です。
  
<a name="bkmk_createProject"></a>
   
## <a name="create-a-project"></a>プロジェクトの作成  

<!-- TODO: The following procedure demonstrates how to create a console application project in C# that uses the Microsoft .NET Framework. For more information on supported versions of the .NET Framework, see [Supported extensions](../supported-extensions.md).   -->
  
<a name="bkmk_newProject"></a>

### <a name="new-project"></a>新しいプロジェクト  
  
1.  Visual Studio で、**新しいプロジェクト** をクリックします。 **新しいプロジェクト**ダイアログが表示されます。  
2.  **テンプレート**の下の左側のナビゲーション ウィンドウで、**Visual C#** を選択します。  
3.  使用可能なテンプレートの一覧の上側で、**.NET Framework 4.6.2** を選択します。  
4.  テンプレートの一覧で、**コンソール アプリケーション**を選択します。 (ソリューションに適したプロジェクトの種類を選択してください)。すべての Web API C# はコンソール アプリケーションです。  
  
 <!-- TODO:
 ![A new console app project dialog in CDS for Apps](../media/new-project.PNG "A new console app project dialog in CDS for Apps")   -->
  
5.  フォームの下部近くのテキスト ボックスに、プロジェクトの名前と場所を入力し、[OK] を選択します。 (このトピックでは、ソリューション名 `StartWebAPI-CS` が使用されています)。最初ソリューションのファイルが作成され、ソリューションは Visual Studio に読み込まれます。  
  
6.  **プロジェクト**メニューで、プロジェクトのプロパティ フォームを開き、ターゲット フレームワークが **.NET Framework 4.6.2** に設定されていることを確認します。  
  
<a name="bkmk_addAllRequiredResources"></a>
   
### <a name="add-all-required-resources-to-your-project"></a>必要なすべてのリソースをプロジェクトに追加する  

次の手順は、プロジェクトに対して、必要とされるすべてのマネージド リファレンスおよびパッケージを追加する方法を説明します。 多数のマネージ コード コンソール アプリケーションで Web API 操作を呼び出すのに必要な基本的な一連のリソースを考慮します。  
  
#### <a name="add-the-helper-library-nuget-package"></a>ヘルパー ライブラリの NuGet パッケージの追加

Common Data Service for Apps Web API ヘルパー ライブラリには、アプリケーション構成、Common Data Service for Apps 認証、例外処理、および Web 通信など、操作を補足するクラスが含まれています。 詳細については、[アプリ用 Common Data Service Web API Helper Library (C#) の使用](use-microsoft-dynamics-365-web-api-helper-library-csharp.md) を参照してください。  これらのクラスを使用することは任意ですが、Web API サンプルでは幅広く使用されています。  Common Data Service for Apps Web API ヘルパー ライブラリは、NuGet パッケージとしてソース コード形式で頒布されます。  今後の更新は、NuGet パッケージの更新として頒布されます。  
  
 NuGet コマンド ライン ユーティリティをインストール、または Visual Studio でパッケージ マネージャー コンソールを使用している場合:  
  
1.  次のコマンドを発行し、ヘルパー ライブラリー パッケージをインストールします。  
  
     `Install-Package Microsoft.CrmSdk.WebApi.Samples.HelperCode`  
  
2.  依存パッケージの処理における複数のメッセージが表示されています。 **ライセンスの同意**ダイアログが表示されている場合、ライセンス条項を読み、**同意**をクリックします。  
  
3.  ヘルパー ライブラリ パッケージのインストールを確認するには、下の手順 6 に進みます。  
  
 NuGet パッケージ マネージャー拡張機能がインストールされている場合:  
  
1.  **プロジェクト**メニューから、**NuGet Packages の管理**を選択します。  **NuGet Package Manager** タブが表示されます。  
  
2.  右上隅では、**パッケージ**ソース ドロップダウンを **Nuget.org** に設定します。  
  
3.  左上隅では、**参照** をクリックし、検索ボックスでは「`CDS for Apps HelperCode`」と入力して、Enter を押します。  
  
 <!-- TODO:
![NuGet Package Manager showing Common Data Service for Apps Helper Code Library &#40;C&#35;&#41;](../media/package-manifest-helper-code.png "NuGet Package Manager showing Common Data Service for Apps Helper Code Library (C#)")   -->
  
4.  **インストール** をクリックします。  **プレビュー** ダイアログが表示されたら、**OK** をクリックします。  
  
5.  **ライセンスの同意**ダイアログが表示されます。 ライセンス条項を検討し、**同意する**をクリックします。  
  
6.  **ソリューション エクスプローラー**ウィンドウに移動します。 **Web API Helper Code** という名前の新しいソリューションのフォルダが追加されていることを確認します。  
  
 <!-- TODO:
 ![VS Solution Explorer showing helper library files](../media/solution-explorer-helper-code.PNG "VS Solution Explorer showing helper library files")   -->
  
 Common Data Service for Apps SDK Web API Helper Library パッケージ、[Microsoft.CrmSdk.WebApi.Samples.HelperCode](https://www.nuget.org/packages/Microsoft.CrmSdk.WebApi.Samples.HelperCode) は、以下のパッケージによって異なりますが、ヘルパー ライブラリ パッケージと共に自動的にダウンロードされ、インストールされます。  
  
-   [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json) – 一般的に使用されている .NET の MIT ライセンス JSON フレームワークである [Json.NET](http://www.newtonsoft.com/json)が含まれています。  
  
-   [Microsoft.IdentityModel.Clients.ActiveDirectory](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) – には .NET クライアントの認証機能を提供する Active Directory Authentication Library ([ADAL](https://msdn.microsoft.com/library/azure/mt417579.aspx)) のバイナリが含まれています。  
  
> [!WARNING]
>  Common Data Service for Apps SDK Web API Helper Library パッケージは、他の 2 つのサポート パッケージの特定バージョンに対して作成されました。  このため、ヘルパー ライブラリの NuGet パッケージのみを直接更新する必要があります。  この操作を実行すると、必要に応じて適切なサポート パッケージが更新されます。  これらのサポート パッケージ 1 つを別に更新する場合は、そのパッケージのより新しいバージョンの方が新しいヘルパー ライブラリと互換性がある可能性があります。  
  
#### <a name="verify-the-required-assembly-references"></a>必要なアセンブリ参照を確認します。  
  
1.  **ソリューション エクスプローラー**では、**参照**ノードを展開します。  
  
2.  次の参照がプロジェクトに追加されていることを確認します。  
  
 <!-- TODO:
![VS Solution Explorer showing references for the helper library](../media/solution-explorer-references-helper-code.png "VS Solution Explorer showing references for the helper library")   -->
  
3.  アプリケーション内で定期的に使用する追加機能がある場合は、必要なアセンブリへ関連する参照を追加することができます。 詳細については、「[[参照の追加] ダイアログ ボックスを使用して参照の追加または削除する方法](/visualstudio/ide/how-to-add-or-remove-references-by-using-the-reference-manager)」を参照してください。  
  
 Common Data Service for Apps Web API は REST の原則をベースとしているので、クライアント側アセンブリがアクセスする必要はありません。 
  
#### <a name="add-typical-using-statements"></a>一般的な using ステートメントの追加  
  
1.  **ソリューション エクスプローラー**で、編集に対して **Program.cs** を開きます。  
  
2.  ファイルの先頭に、Common Data Service for Apps Web API ベースのソリューションで一般的に使用されている名前空間を参照する、次の `using` ステートメントを追加します。  
  
    ```csharp
    using Microsoft.Crm.Sdk.Samples.HelperCode;  
    using Newtonsoft.Json;  
    using Newtonsoft.Json.Linq;  
    using System.Net.Http;  
    using System.Net.Http.Headers;
    ```  
  
3.  前のセクションで日常的に使用されているアセンブリまたは参照を追加した場合は、対応する `using` ステートメントをこれらのリソースに対して追加する必要もあります。  
  
4.  ファイルを保存します。  
  
<a name="bkmk_addConnectionCode"></a>
 
### <a name="add-connection-code"></a>つながりコードの追加

このセクションでは、これらの操作を実行する上で基本となる一連の設定と説明を追加する方法について説明します。  使用される共通コードの詳細については、[アプリ用 Common Data Service Web API Helper Library (C#) の使用](use-microsoft-dynamics-365-web-api-helper-library-csharp.md)を参照してください。  
  
#### <a name="edit-the-application-configuration-file"></a>アプリケーション構成ファイルの編集
  
1.  **ソリューション エクスプローラー**で、編集に対して **App.config** ファイルを開きます。  既存の `<startup>` セクションの後に、次の 2 つのセクションをそれに追加し、ファイルを保存します。  
  
    ```xml  
  
    <connectionStrings>  
        <clear />  
  
        <!-- When providing a password, make sure to set the app.config file's security so that only you can read it. -->  
        <add name="default"   connectionString="Url=http://myserver/myorg/; Username=name; Password=password; Domain=domain" />  
        <add name="CrmOnline" connectionString="Url=https://mydomain.crm.dynamics.com/; Username=someone@mydomain.onmicrosoft.com; Password=password" />  
      </connectionStrings>  
  
      <appSettings>  
        <!--For information on how to register an app and obtain the ClientId and RedirectUrl  
            values see https://msdn.microsoft.com/dynamics/crm/mt149065 -->  
        <!--Active Directory application registration. -->  
        <!--These are dummy values and should be replaced with your actual app registration values.-->  
        <add key="ClientId" value="e5cf0024-a66a-4f16-85ce-99ba97a24bb2" />  
        <add key="RedirectUrl" value="http://localhost/SdkSample" />  
  
        <!-- Use an alternate configuration file for connection string and setting values. This optional setting  
        enables use of an app.config file shared among multiple applications. If the specified file does  
        not exist, this setting is ignored.-->  
        <add key="AlternateConfig" value="C:\Temp\crmsample.exe.config"/>  
      </appSettings>  
  
    ```  
  
2.  ソリューションを開発または展開している時、実際の接続およびアプリケーションの登録値は例のプレースホルダーの値に対して置換する必要があります。  詳細については、「[ヘルパー コード: 構成クラス](web-api-helper-code-configuration-classes.md)」を参照してください。  
  
<a name="bkmk_addCodeToCallHelperLibrary"></a>

#### <a name="add-code-to-call-the-helper-library"></a>ヘルパー ライブラリを呼び出すコードの追加
  
1.  Program.cs ファイルを編集します。  
  
2.  Program クラスに次のプロパティを追加します。  このプロパティは Common Data Service for Apps サーバーへの接続に成功した後に初期化されます。  
  
     `private HttpClient httpClient;`  
  
3.  `Main` メソッドでは、次のステートメントを追加します。  
  
    ```csharp  
  
    Program app = new Program();  
    try  
    {  
        String[] arguments = Environment.GetCommandLineArgs();  
        app.ConnectToCRM(arguments);  
    }  
    catch (System.Exception ex)  
    { ; }  
    finally  
    {  
        if (app.httpClient != null)  
        { app.httpClient.Dispose(); }  
    }  
  
    ```  
  
4.  ヘルパー ライブラリの `Configuration` および `Authentication` クラスを使用する `ConnectToCRM` メソッドを追加します。  次のコードは、Common Data Service for Apps Web API のリリース バージョンに正常にアクセスできるよう、[HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient\(v=vs.118\).aspx) プロパティに割り当てる値を示しています。  
  
    ```csharp  
  
    private void ConnectToCRM(String[] cmdargs)  
    {  
        Configuration config = null;  
        if (cmdargs.Length > 0)  
            config = new FileConfiguration(cmdargs[0]);  
        else  
            config = new FileConfiguration(null);  
        Authentication auth = new Authentication(config);  
        httpClient = new HttpClient(auth.ClientHandler, true);  
        httpClient.BaseAddress = new Uri(config.ServiceUrl + "api/data/v8.1/");  
        httpClient.Timeout = new TimeSpan(0, 2, 0);  
        httpClient.DefaultRequestHeaders.Add("OData-MaxVersion", "4.0");  
        httpClient.DefaultRequestHeaders.Add("OData-Version", "4.0");  
        httpClient.DefaultRequestHeaders.Accept.Add(  
            new MediaTypeWithQualityHeaderValue("application/json"));  
    }  
  
    ```  
  
<a name="bkmk_addErrorHandlingCode"></a>

### <a name="add-error-handling-code"></a>エラー処理コードの追加

 次の修正により、Web API エラーを含むコンソールにおける例外を検出および報告するコードが追加されます。  別の環境を対象とする場合は、その環境における例外処理コードを適切に修正します。  
  
1.  `Main` では、次のステートメントを `catch` ブロックに追加します。  
  
     `DisplayException(ex);`  
  
2.  対応するメソッドを `Program` クラスに追加します。  
  
    ```csharp  
  
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
  
    ```  
  
3.  ソリューションのすべてのファイルを保存します。  
  
<a name="bkmk_nextSteps"></a>

### <a name="next-steps"></a>次のステップ

 この時点では、エラーなしでソリューションを作成できます。  アプリケーション構成ファイルを編集し、Common Data Service for Apps に対して値を入力する場合は、プログラムがそのサーバーに正常に接続される必要もあります。  ソリューションは、Common Data Service for Apps Web API への呼び出しを含め、カスタム コードを承諾する準備が整っている骨格フレームを表します。  
  
> [!TIP]
>  このトピックを閉じる前に、プロジェクト テンプレートとしてプロジェクトを保存することを検討します。 次に、今後の学習プロジェクトのためにそのテンプレートを再利用すると、新しいプロジェクトの設定の時間と労力を節約できます。 これを行うには、プロジェクトを Microsoft Visual Studio で開いている間に、**ファイル**メニューで、**テンプレートのエクスポート**を選択します。 [テンプレート ウィザードのエクスポート](https://msdn.microsoft.com/library/xkh1wxd8.aspx) の指示に従い、テンプレートを作成します。  
  
### <a name="see-also"></a>関連項目

[Web API (C#) を開始する](get-started-dynamics-365-web-api-csharp.md)<br />
[アプリ用 Common Data Service Web API Helper Library (C#) の使用](use-microsoft-dynamics-365-web-api-helper-library-csharp.md)<br />  
[Web API を使用して演算を実行する](perform-operations-web-api.md)

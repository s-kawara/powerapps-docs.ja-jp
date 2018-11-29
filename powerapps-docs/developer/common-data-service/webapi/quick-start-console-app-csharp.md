---
title: 'クイック スタート: Web API サンプル (C#) (Common Data Service for Apps)| Microsoft Docs'
description: このサンプルでは、Common Data Service for Apps サーバーの認証方法、および基本的な Web API 操作、WhoAmI Function を呼び出す方法を示しています。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: brandonsimons
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="quick-start-web-api-sample-c"></a>クイック スタート: Web API のサンプル (C#)

このクイック スタートでは、Web API を使用して Common Data Service for Apps 環境に接続する簡単なコンソール アプリケーションを作成します。

OAuth2 を使用して認証し、[HttpClient](/dotnet/api/system.net.http.httpclient) を使用して `GET` 要求を <xref href="Microsoft.Dynamics.CRM.WhoAmI?text=WhoAmI Function" /> に送信すると、応答は <xref href="Microsoft.Dynamics.CRM.WhoAmIResponse?text=WhoAmIResponse ComplexType" /> になります。 プロパティ `UserId` 値が表示されます。

> [!NOTE]
> このクイック スタートの例には、エラー処理は含まれません。 これは、Web API に接続して使用するための最小の例です。

## <a name="prerequisites"></a>前提条件

 - Visual Studio (2017 を推奨)
 - インターネット接続
 - Common Data Service for Apps インスタンスの有効なユーザー アカウント
    - ユーザー名
    - パスワード
 - 接続に使用する CDS for Apps 環境の URL
 - Visual C# 言語の基本的な理解

> [!NOTE]
> OAuth2 を使用して認証するには、Azure Active Directory に登録されているアプリケーションが必要です。 このクイック スタート サンプルは、Microsoft が公開している実行中のサンプル コードの目的で使用できるアプリ登録 clientid 値を示します。 独自のアプリケーションの場合、アプリを登録する必要があります。 詳細: [チュートリアル: Azure Active Directory にアプリを登録する](../walkthrough-register-app-azure-active-directory.md)

## <a name="create-visual-studio-project"></a>Visual Studio プロジェクトの作成

1. .NET Framework 4.6.2 を使用して新しいコンソール アプリ (.NET Framework) を作成する

    ![コンソール アプリケーション プロジェクトを開始する](../media/quick-start-web-api-console-app-csharp-1.png)

    > [!NOTE]
    > このスクリーンショットは、`WebAPIQuickStart` という名前を示していますが、必要に応じてプロジェクトとソリューションに名前を指定することを選択できます。 

1. **ソリューション エクスプローラー**で、作成したプロジェクトを右クリックして、コンテキスト メニューで **NuGet Packages の管理...** を選択します。

    ![NuGet パッケージの追加](../media/quick-start-web-api-console-app-csharp-2.png)

1. NuGet パッケージ `Microsoft.IdentityModel.Clients.ActiveDirectory` を参照します。
1. **バージョン** 2.29.0 を選択し、をインストールします。

    ![Microsoft.IdentityModel.Clients.ActiveDirectory NuGet パッケージをインストールする](../media/quick-start-web-api-console-app-csharp-3.png)

    > [!IMPORTANT]
    > **この NuGet パッケージの最新バージョンをインストールしないでください。**
    >
    > このサンプルは、このライブラリの 3.x バージョンでは使用できない別個の Azure ログイン ダイアログを持たないユーザーのログイン資格情報を渡す機能に応じて異なります。

    > [!NOTE]
    > **ライセンスの承認** ダイアログで **同意する** を選択する必要があります。

1. NuGet パッケージ `Newtonsoft.Json` を参照して、最新バージョンをインストールします。

    ![Microsoft.IdentityModel.Clients.ActiveDirectory NuGet パッケージをインストールする](../media/quick-start-web-api-console-app-csharp-4.png)

## <a name="edit-programcs"></a>Program.cs を編集する

1. `Program.cs` の一番上にステートメントを使用してこれらを追加する

    ```csharp
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Net.Http.Headers;
    using System.Net.Http;
    using Newtonsoft.Json.Linq;
    ```

1. `Main` メソッドを次のコードに置き換えます。

    ```csharp
    static void Main(string[] args)
    {
        // Set these values:
        // e.g. https://yourorg.crm.dynamics.com
        string url = "<your environment url>";
        // e.g. you@yourorg.onmicrosoft.com
        string userName = "<your user name>";
        // e.g. y0urp455w0rd
        string password = "<your password>";

        // Azure Active Directory registered app clientid for Microsoft samples
        string clientId = "51f81489-12ee-4a9e-aaae-a2591f45987d";

        var userCredential = new UserCredential(userName, password);
        string apiVersion = "9.0";
        string webApiUrl = $"{url}/api/data/v{apiVersion}/";

        //Authenticate using IdentityModel.Clients.ActiveDirectory
        var authParameters = AuthenticationParameters.CreateFromResourceUrlAsync(new Uri(webApiUrl)).Result;
        var authContext = new AuthenticationContext(authParameters.Authority, false);
        var authResult = authContext.AcquireToken(url, clientId, userCredential);
        var authHeader = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);

        using (var client = new HttpClient())
        {
            client.BaseAddress = new Uri(webApiUrl);
            client.DefaultRequestHeaders.Authorization = authHeader;

            // Use the WhoAmI function
            var response = client.GetAsync("WhoAmI").Result;

            if (response.IsSuccessStatusCode)
            {
                //Get the response content and parse it.  
                JObject body = JObject.Parse(response.Content.ReadAsStringAsync().Result);
                Guid userId = (Guid)body["UserId"];
                Console.WriteLine("Your UserId is {0}", userId);
            }
            else
            {
                Console.WriteLine("The request failed with a status of '{0}'",
                            response.ReasonPhrase);
            }

            Console.WriteLine("Press any key to exit.");
            Console.ReadLine();
        }       
    }
    ```

1. 環境の情報を追加するには、次の値を編集します。

    ```csharp
    // e.g. https://yourorg.crm.dynamics.com
    string url = "<your environment url>";
    // e.g. you@yourorg.onmicrosoft.com
    string userName = "<your user name>";
    // e.g. y0urp455w0rd
    string password = "<your password>";
    ```

## <a name="run-the-program"></a>プログラムを実行する

1. F5 キーを押してプログラムを実行します。 出力は次のように表示されます。

    ```
    Your UserId is 969effb0-98ae-478c-b547-53a2968c2e75
    Press any key to exit.
    ```

### <a name="congratulations"></a>ご報告: 

Web API に正常に接続されました。

<!-- TODO: Include link to next steps topics -->
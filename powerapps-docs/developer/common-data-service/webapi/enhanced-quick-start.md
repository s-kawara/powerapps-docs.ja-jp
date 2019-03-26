---
title: '拡張クイック スタート: (アプリ用 Common Data Service)| Microsoft Docs'
description: Common Data Service for Apps Web API を使用するコンソール アプリケーションの構築のために Visual Studio で新しいプロジェクトを作成
ms.custom: ''
ms.date: 02/02/2019
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
manager: ''
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# 拡張クイック スタート

このトピックでは、再利用可能な <xref:System.Net.Http.HttpClient> およびエラー処理方法を追加することによって、[クイック スタート](quick-start-console-app-csharp.md)トピックのコードをどのようにリファクターするかを示します。 このトピックを開始する前に、[クイック スタート](quick-start-console-app-csharp.md) のステップを完了し、新しい Microsoft Visual Studio プロジェクトを作成してください。

## 接続文字列で資格情報を渡すことを有効にする

[クイック スタート](quick-start-console-app-csharp.md) の例が行ったようにユーザーの資格情報をコード内に含めるのは、良い方法ではありません。 

ユーザーの資格情報をどのように取り込むかは、作成しているクライアントのタイプによって異なります。 このコンソール アプリケーション用には、`App.config` 内に資格情報を設定します。資格情報をコード外へ移動する便利な手段だからです。 またこれは [Web API データ操作のサンプル (C#)](web-api-samples-csharp.md) で使用した方法です。よって、この方法を理解していれば、さまざまなサンプルがどのように機能するかが簡単にわかります。

この要求を有効にするには、3 つのステップが必要です。

1. [[Visual Studio プロジェクトで参照を System.Configuration に追加](#1-add-reference-to-systemconfiguration-to-the-visual-studio-project)](#1-add-reference-to-systemconfiguration-to-the-visual-studio-project)
1. [[アプリケーション構成ファイルの編集](#2-edit-the-application-configuration-file)](#2-edit-the-application-configuration-file)
1. [[using ステートメントを Program.cs に追加](#3-add-using-statement-to-programcs)](#3-add-using-statement-to-programcs)


### Visual Studio プロジェクトで参照を System.Configuration に追加

1. **ソリューション エクスプローラー** で、**参照** を右クリックし、**参照の追加...** を選択します。
1. **参照マネージャー** ダイアログで `System.Configuration` を検索し、チェックボックスを選択してこの参照をプロジェクトに追加します。
1. **OK** をクリックして **参照マネージャー** ダイアログ ボックスを閉じます。
  
### アプリケーション構成ファイルの編集

**ソリューション エクスプローラー**で、**App.config** ファイルを開きます。 次のように見えるはずです。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6.2" />
    </startup>
</configuration>
```

`<configuration>` 要素を編集し、以下に示すように `connectionStrings` ノードを加えます。

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6.2" />
    </startup>
  <connectionStrings>
    <!--Online using Office 365-->
    <add name="Connect"
         connectionString="Url=https://yourorg.api.crm.dynamics.com;Username=yourname@yourorg.onmicrosoft.com;Password=y0urp455w0rd; />
  </connectionStrings>
</configuration>
```
これは、名前で参照できる接続文字列を作成します。この場合は `Connect` です。これにより、必要に応じて複数の接続を定義できます。

CDS 環境への接続に必要なものに一致するように、`connectionString` の接続文字列 `Url`、`Username` および `Password` の値を編集します。

### using ステートメントを Program.cs に追加

Program.cs ファイルの先頭に、この using ステートメントを追加します。

```csharp
using System.Configuration;
```

## ヘルパー コードを追加

[クイック スタート](quick-start-console-app-csharp.md) の例では、すべてのコードは `program.cs` ファイル内にあります。 <xref:System.Net.Http.HttpClient> の接続と作成を扱うコードを、ヘルパー メソッドの別のファイルに移動します。 

これらのヘルパーは、 [Web API データ操作のサンプル (C#)](web-api-samples-csharp.md) で使用された [SampleHelper.cs](https://github.com/Microsoft/PowerApps-Samples/blob/master/cds/webapi/C%23/SampleHelpers.cs) でも使用されます。 これらのヘルパーを理解すれば、これらがサンプルでどのように使用されるかを理解します。

1. **ソリューション エクスプローラー**で、プロジェクトを右クリックし、**追加** > **クラス...** を選択して (または `Shift`+`Alt`+`C` を押して) **新しいアイテムの追加** ダイアログを開きます。
1. クラスの名前を指定します。 [Web API データ操作のサンプル (C#) ](web-api-samples-csharp.md) によって使用されるパターンをフォローするには、`SampleHelpers.cs` と名前を付けます。 

    > [!NOTE]
    > クラスの名前によって、 `Program.cs` 内でのこれらのヘルパー プロパティとメソッドの参照方法が決まります。 残りの指示では `SampleHelpers` と名前を付けたとみなしますので、ほかの名前を付けた場合は覚えていてください。

1. 次の `using` ステートメントを追加します。

    ```csharp
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System;
    using System.Linq;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Threading.Tasks;
    ```

1. `SampleHelper` クラスに次のプロパティおよびメソッドを追加します。

    ```csharp
    //These sample application registration values are available for all online instances.
    //You can use these while running sample code, but you should get your own for your own apps
    public static string clientId = "51f81489-12ee-4a9e-aaae-a2591f45987d";
    public static string redirectUrl = "app://58145B91-0C36-4500-8554-080854F2AC97";

    /// <summary>
    /// Method used to get a value from the connection string
    /// </summary>
    /// <param name="connectionString"></param>
    /// <param name="parameter"></param>
    /// <returns>The value from the connection string that matches the parameter key value</returns>
    public static string GetParameterValueFromConnectionString(string connectionString, string parameter)
    {
      try
      {
        return connectionString.Split(';').Where(s => s.Trim().StartsWith(parameter)).FirstOrDefault().Split('=')[1];
      }
      catch (Exception)
      {
        return string.Empty;
      }
    }

    /// <summary>
    /// Returns an HttpClient configured with an OAuthMessageHandler
    /// </summary>
    /// <param name="connectionString">The connection string to use.</param>
    /// <param name="clientId">The client id to use when authenticating.</param>
    /// <param name="redirectUrl">The redirect Url to use when authenticating</param>
    /// <param name="version">The version of Web API to use. Defaults to version 9.1 </param>
    /// <returns>An HttpClient you can use to perform authenticated operations with the Web API</returns>
    public static HttpClient GetHttpClient(string connectionString, string clientId, string redirectUrl, string version = "v9.1")
    {
      string url = GetParameterValueFromConnectionString(connectionString, "Url");
      string username = GetParameterValueFromConnectionString(connectionString, "Username");
      string password = GetParameterValueFromConnectionString(connectionString, "Password");
      try
      {
        HttpMessageHandler messageHandler = new OAuthMessageHandler(url, clientId, redirectUrl, username, password,
                      new HttpClientHandler());

        HttpClient httpClient = new HttpClient(messageHandler)
        {
          BaseAddress = new Uri(string.Format("{0}/api/data/{1}/", url, version)),

          Timeout = new TimeSpan(0, 2, 0)  //2 minutes
        };

        return httpClient;
      }
      catch (Exception)
      {
        throw;
      }
    }

    /// <summary> Displays exception information to the console. </summary>
    /// <param name="ex">The exception to output</param>
    public static void DisplayException(Exception ex)
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

1. `SampleHelpers.cs` ファイルの名前空間内に `OAuthMessageHandler` クラスを追加します。

    > [!NOTE]
    > `SampleHelpers` クラス自体の中にこれを追加しないでください。

    このクラスにより、操作が実行されるたびにアクセス トークンが更新されます。 各アクセス トークンは約 1 時間後に期限切れとなります。 このクラスは <xref:System.Net.Http.DelegatingHandler> を実装します。これは、操作が実行されるたびに Azure Active Directory Authentication Library (ADAL) 認証コンテキストと連携して `AquireToken` を呼び出すため、トークンの有効期限を明示的に管理する必要はありません。

    ```csharp
    /// <summary>
    ///Custom HTTP message handler that uses OAuth authentication thru ADAL.
    /// </summary>
    class OAuthMessageHandler : DelegatingHandler
    {
      private AuthenticationHeaderValue authHeader;

      public OAuthMessageHandler(string serviceUrl, string clientId, string redirectUrl, string username, string password,
              HttpMessageHandler innerHandler)
          : base(innerHandler)
      {
        // Obtain the Azure Active Directory Authentication Library (ADAL) authentication context.
        AuthenticationParameters ap = AuthenticationParameters.CreateFromResourceUrlAsync(
                new Uri(serviceUrl + "/api/data/")).Result;
        AuthenticationContext authContext = new AuthenticationContext(ap.Authority, false);
        //Note that an Azure AD access token has finite lifetime, default expiration is 60 minutes.
        AuthenticationResult authResult;
        if (username != string.Empty && password != string.Empty)
        {

          UserCredential cred = new UserCredential(username, password);
          authResult = authContext.AcquireToken(serviceUrl, clientId, cred);
        }
        else
        {
          authResult = authContext.AcquireToken(serviceUrl, clientId, new Uri(redirectUrl), PromptBehavior.Auto);
        }

        authHeader = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
      }

      protected override Task<HttpResponseMessage> SendAsync(
                HttpRequestMessage request, System.Threading.CancellationToken cancellationToken)
      {
        request.Headers.Authorization = authHeader;
        return base.SendAsync(request, cancellationToken);
      }
    }
    ```

## Program.cs を更新する

これで [接続文字列で資格情報を渡すことを有効にする](#enable-passing-credentials-in-a-connection-string) および [ヘルパー コードを追加する](#add-helper-code) に変更を施したため、 `Program.cs`  で次のものだけを含むように `Main` メソッドを更新できます。

```csharp
static void Main(string[] args)
{
  try
  {
    //Get configuration data from App.config connectionStrings
    string connectionString = ConfigurationManager.ConnectionStrings["Connect"].ConnectionString;

    using (HttpClient client = SampleHelpers.GetHttpClient(connectionString, SampleHelpers.clientId, SampleHelpers.redirectUrl))
    {
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
  catch (Exception ex)
  {
    SampleHelpers.DisplayException(ex);
    Console.WriteLine("Press any key to exit.");
    Console.ReadLine();
  }
}
```

これはコード量がより少なく、`HttpClient` を使うたびにエラー処理とアクセス トークンを更新する手段を追加しました。

F5 キーを押してプログラムを実行します。 [クイック スタート](quick-start-console-app-csharp.md) サンプルのように、出力は次のようになります。

    ```
    Your UserId is 969effb0-98ae-478c-b547-53a2968c2e75
    Press any key to exit.
    ```

## 再利用可能なメソッドを作成

`Program.cs` `main` メソッドでコードの総量を減らしましたが、1 つの操作を呼び出すためだけにプログラムを書くわけではありません。そして、たった 1 つの操作を呼び出すためだけにそれほど多くのコードを書くのは現実的ではありません。

このセクションでは、これを変更する方法を示します。

  ```csharp
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
  ```
結果として、次を実現します。

  ```csharp
  WhoAmIResponse response = WhoAmI(client);
        Console.WriteLine("Your system user ID is: {0}", response.UserId);
  ```

開始する前に、Web API 参照にアクセスして、次のトピックを確認しておくことをお勧めします。
- <xref href="Microsoft.Dynamics.CRM.WhoAmI?text=WhoAmI Function" /> 
- <xref href="Microsoft.Dynamics.CRM.WhoAmIResponse?text=WhoAmIResponse ComplexType" />

<xref href="Microsoft.Dynamics.CRM.WhoAmI?text=WhoAmI Function" />  がどのように<xref href="Microsoft.Dynamics.CRM.WhoAmIResponse?text=WhoAmIResponse ComplexType" /> を返し、<xref href="Microsoft.Dynamics.CRM.WhoAmIResponse?text=WhoAmIResponse ComplexType" /> が次の 3 つの `GUID` プロパティを含んでいることに注意してください: `BusinessUnitId`、`UserId` および `OrganizationId`。

追加するコードは、単にこれらを、パラメーターとして `HttpClient` を受け取る再利用可能なメソッドにモデル化します。

> [!NOTE]
> これをどのように行うかは、個人用な好みの問題です。 この設計は比較的単純なために提供されています。

Visual Studio プロジェクトで、次のステップを実行します。

1. `Program` クラスを編集して部分クラスにします。

    上位では、これを変更します。

    `class Program`

    結果として、次を実現します。

    `partial class Program`

1. `ProgramMethods.cs` という名前の新しいクラスを作成します。 `ProgramMethods.cs`

    `ProgramMethods.cs` では、これを変更します。

    `class ProgramMethods`

    結果として、次を実現します。

    `partial class Program`

    このように、`ProgramMethods.cs` ファイルの `Program` クラスは、`Program.cs` ファイルの元の `Program` クラスの単なる拡張です。 

1. 次の using ステートメントを `ProgramMethods.cs` ファイルの上位に追加します。

    ```csharp
    using Newtonsoft.Json.Linq;
    using System;
    using System.Net.Http;
    ```

1. 次のメソッドを `ProgramMethods.cs` ファイルの `Program` クラスに追加します。

    ```csharp
    public static WhoAmIResponse WhoAmI(HttpClient client) {
      WhoAmIResponse returnValue = new WhoAmIResponse();
      //Send the WhoAmI request to the Web API using a GET request. 
      HttpResponseMessage response = client.GetAsync("WhoAmI",
              HttpCompletionOption.ResponseHeadersRead).Result;
      if (response.IsSuccessStatusCode)
      {
          //Get the response content and parse it.
          JObject body = JObject.Parse(response.Content.ReadAsStringAsync().Result);
          returnValue.BusinessUnitId = (Guid)body["BusinessUnitId"];
          returnValue.UserId = (Guid)body["UserId"];
          returnValue.OrganizationId = (Guid)body["OrganizationId"];
      }
      else
      {
          throw new Exception(string.Format("The WhoAmI request failed with a status of '{0}'",
                  response.ReasonPhrase));
      }
      return returnValue;
    }
    ```

1. 次のクラスを、`Program` クラスの外側で `ProgramMethods.cs` の名前空間内に追加します。

    ```csharp
    public class WhoAmIResponse
    {
        public Guid BusinessUnitId { get; set; } 
        public Guid UserId { get; set; }
        public Guid OrganizationId { get; set; }
    }
    ```

1. 元の `Program.cs` ファイル内の `Program` `main` メソッド:

    編集前: 

    ```csharp
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
    ```
    編集後: 

    ```csharp
    WhoAmIResponse response = WhoAmI(client);
    Console.WriteLine("Your system user ID is: {0}", response.UserId);
    ```

1. F5 キーを押してサンプルを実行します。以前と同じ結果を取得します。


## トラブルシューティング

これらのサンプルを実行するときに問題がある場合、[https://github.com/Microsoft/PowerApps-Samples](https://github.com/Microsoft/PowerApps-Samples) の GitHub のリポジトリから、すべての PowerApps のサンプルをダウンロードできます 。

このサンプルは、`PowerApps-Samples-master\PowerApps-Samples-master\cds\webapi\C#\SimpleWebApi` フォルダーにある [SimpleWebApi](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/webapi/C%23/SimpleWebApi) に基づいています。

Visual Studio の `SimpleWebApi.sln` ファイルを開き、サンプルを実行できます。 有効な資格情報を持っている限り実行できます。

> [!IMPORTANT]
> GitHub レポのすべてのサンプルは、`PowerApps-Samples-master\cds\App.config` にある共通 App.config を使うように設定されています。 接続文字列を設定するとき、このファイルを編集する必要があります。 その場合、資格情報を再度設定することなくすべてのサンプルを実行できます。

## テンプレート プロジェクトを作成

このトピックを閉じる前に、プロジェクト テンプレートとしてプロジェクトを保存することを検討します。 次に、今後の学習プロジェクトのためにそのテンプレートを再利用すると、新しいプロジェクトの設定の時間と労力を節約できます。 これを行うには、プロジェクトを Microsoft Visual Studio で開いている間に、**ファイル**メニューで、**テンプレートのエクスポート**を選択します。 [テンプレート ウィザードのエクスポート](https://docs.microsoft.com/visualstudio/ide/how-to-create-project-templates) の指示に従い、テンプレートを作成します。  
  
## 次のステップ

詳細については、以下のリソースを参照してください。

> [!div class="nextstepaction"]
> [[Web API を使用して演算を実行する](perform-operations-web-api.md)](perform-operations-web-api.md)<br /><br />
> [[Web API データ操作のサンプル (C#) を試す](web-api-samples-csharp.md)](web-api-samples-csharp.md)<br /><br />
> [[GitHub の Web API サンプル (C#) をレビューする](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/webapi/C%23)](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/webapi/C%23)


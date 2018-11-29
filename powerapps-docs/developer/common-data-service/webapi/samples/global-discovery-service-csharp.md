---
title: 'Web API グローバル検索サービスのサンプル (C#) (アプリ用 Common Data Service) | Microsoft Docs'
description: このサンプルは、Web API グローバル検索サービスの使用方法について説明します
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
# <a name="web-api-global-discovery-service-sample-c"></a>Web API グローバル検索サービスのサンプル (C#)

このサンプルは、Web API グローバル検索サービスの使用方法について説明します

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

このサンプルは、Github 上に用意されています [https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/webapi/C%23/GlobalDiscovery](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/webapi/C%23/GlobalDiscovery)。

## <a name="what-this-sample-does"></a>このサンプルの概要

このサンプルは、指定されたユーザー資格情報に対して、利用可能なアプリ用 Common Data Service を返します。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

このサンプルは、App.config ファイル内の資格情報を使用し、接続文字列内で構成された URL は使用しません。
代わりに、ユーザー資格情報および ClientId だけを使用します。

### <a name="demonstrates"></a>説明

このサンプルは、HttpClient を使用して ADAL (v2.29) を使用した認証を行い、グローバル検索サービスを呼び出してユーザーが接続できる利用可能なインスタンスに関する情報を返します。

サンプルは、次のように `GetInstances` メソッドおよび `Instance` クラスに依存しています。

```csharp
    /// <summary>
    /// Uses the global web api discovery service to return instances
    /// </summary>
    /// <param name="clientId">The Azure AD client (app) registration</param>
    /// <param name="username">The user name</param>
    /// <param name="password">The password</param>
    /// <returns>A List of Instances</returns>
    static List<Instance> GetInstances(string clientId, string username, string password)
    {

      string GlobalDiscoUrl = "https://globaldisco.crm.dynamics.com/";
      AuthenticationContext authContext = new AuthenticationContext("https://login.windows.net/common", false);

      UserCredential cred = new UserCredential(username, password);
      AuthenticationResult authResult = authContext.AcquireToken(GlobalDiscoUrl, clientId, cred);

      HttpClient client = new HttpClient();
      client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", authResult.AccessToken);
      client.Timeout = new TimeSpan(0, 2, 0);
      client.BaseAddress = new Uri(GlobalDiscoUrl);

      HttpResponseMessage response = client.GetAsync("api/discovery/v1.0/Instances", HttpCompletionOption.ResponseHeadersRead).Result;


      if (response.IsSuccessStatusCode)
      {
        //Get the response content and parse it.
        string result = response.Content.ReadAsStringAsync().Result;
        JObject body = JObject.Parse(result);
        JArray values = (JArray)body.GetValue("value");

        if (!values.HasValues)
        {
          return new List<Instance>();
        }

        return JsonConvert.DeserializeObject<List<Instance>>(values.ToString());
      }
      else
      {
        throw new Exception(response.ReasonPhrase);
      }
    }
```


```csharp
/// <summary>
  /// Object returned by the discovery service
  /// </summary>
  class Instance
  {
    public string Id { get; set; }
    public string UniqueName { get; set; }
    public string UrlName { get; set; }
    public string FriendlyName { get; set; }
    public int State { get; set; }
    public string Version { get; set; }
    public string Url { get; set; }
    public string ApiUrl { get; set; }
    public DateTime LastUpdated { get; set; }
  }
```


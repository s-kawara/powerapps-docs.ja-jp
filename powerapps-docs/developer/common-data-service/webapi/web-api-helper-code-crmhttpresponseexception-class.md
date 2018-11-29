---
title: 'Web API Helper code: CrmHttpResponseException クラス (アプリ用 Common Data Service)| Microsoft Docs'
description: CrmHttpResponseException クラスを使用して、アプリ用 Common Data Service Web API の呼び出し中に生成される HTTP ステータス エラーを表します
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 8deb0bc5-6f4a-4ca7-a3a2-75c06dc7f967
caps.latest.revision: 11
author: brandonsimons
ms.author: jdaly
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="web-api-helper-code-crmhttpresponseexception-class"></a>Web API Helper code: CrmHttpResponseException クラス

`CrmHttpResponseException` クラスを使用して、アプリ用 Common Data Service Web API の呼び出し中に生成される [HTTP ステータス エラー](https://msdn.microsoft.com/library/gg334391.aspx) を表します。  このクラスは標準的な .NET システムの [例外](https://msdn.microsoft.com/library/system.exception.aspx) クラスから派生していて、既存の例外処理メカニズムと容易に統合できます。 詳細については、「[例外処理とスロー](https://docs.microsoft.com/en-us/dotnet/standard/exceptions/index)」を参照してください。  
  
`CrmHttpResponseException` クラスは [CRM SDK Web API ヘルパー ライブラリ](https://www.nuget.org/packages/Microsoft.CrmSdk.WebApi.Samples.HelperCode/) の Exceptions.cs ファイルにあります。  これは他のヘルパー ライブラリ クラスおよび C# Web API サンプルで特に使用されます。 詳細については、[アプリ用 Common Data Service Web API Helper Library (C#) の使用](use-microsoft-dynamics-365-web-api-helper-library-csharp.md) を参照してください。  
  
このクラスはオープン ソース [Json.NET](http://www.newtonsoft.com/json) ライブラリの JSON 文字列操作機能を使用します。  
  
## <a name="class-members"></a>クラス メンバー  

次の表は、`CrmHttpResponseException` クラスのパブリック メンバーを示します。  
  
<!-- TODO:
|||  
|-|-|  
|![Common Data Service for Apps Web API Helper Library&#45;CrmHttpResponseException Class Diagram](../media/web-api-helper-library-crm-exception-class-diagram.png "Common Data Service for Apps Web API Helper Library-CrmHttpResponseException Class Diagram")|**CrmHttpResponseException  class**<br /><br /> *Properties:*<br /><br /> `StackTrace` – the string representation of the immediate frames on the Common Data Service for Apps server’s call stack when the exception was thrown, if available.<br /><br /> *Methods*:<br /><br /> The constructors initialize an instance of this class, and require a [HttpContent](https://msdn.microsoft.com/library/hh193687\(v=vs.110\).aspx) parameter and an optional inner exception parameter.<br /><br /> `ExtractMessageFromContent` – this static method extracts the error message from the specified HTTP content parameter.|  
   -->
## <a name="usage"></a>使用法  

通常は、HTTP 応答メッセージと共に返されたステータス エラーを処理する場合に、`CrmHttpResponseException` オブジェクトを作成してスローします。 たとえば、次のコードは <xref href="Microsoft.Dynamics.CRM.WhoAmI?text=WhoAmI Function" /> 呼び出しに失敗した場合に、このようなエラーがスローされます。  
  
```csharp  
response = await httpClient.GetAsync("WhoAmI", HttpCompletionOption.ResponseContentRead);  
if (!response.IsSuccessStatusCode)  
{   
    throw new CrmHttpResponseException(response.Content);   
}  
```  
  
 他の標準的な .NET の例外と同様に、スローされた `CrmHttpResponseException` オブジェクトをキャッチおよび処理できます。  
  
> [!IMPORTANT]
>  HttpResponseMessage.[EnsureSuccessStatusCode](/dotnet/api/system.net.http.httpresponsemessage.ensuresuccessstatuscode) メソッドを使用して、HTTP 応答エラーをスローされた  [HttpRequestException](/dotnet/api/system.net.http.httprequestexception) オブジェクトに自動的に変換する場合、この方法では `CrmHttpResponseException` クラスが使用できません。 この方法を使用する場合、ステータス コードを含む応答メッセージの詳細の多くは、例外処理時には使用できないことに注意してください。  
  
## <a name="class-listing"></a>クラスの一覧

 このクラスの最新ソースは、[CRM SDK Web API ヘルパー ライブラリ](https://www.nuget.org/packages/Microsoft.CrmSdk.WebApi.Samples.HelperCode) NuGet パッケージにあります。  
  
```csharp  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using System.Threading.Tasks;  
using System.Net.Http;  
using Newtonsoft.Json;  
using Newtonsoft.Json.Linq;  
  
namespace Microsoft.Crm.Sdk.Samples.HelperCode  
{  
    /// <summary>  
    /// Produces a populated exception from an error message in the content of an HTTP response.   
    /// </summary>  
    public class CrmHttpResponseException : System.Exception  
    {  
        #region Properties  
        private static string _stackTrace;  
  
        /// <summary>  
        /// Gets a string representation of the immediate frames on the call stack.  
        /// </summary>  
        public override string StackTrace  
        {  
            get { return _stackTrace; }  
        }  
        #endregion Properties  
  
        #region Constructors  
        /// <summary>  
        /// Initializes a new instance of the CrmHttpResponseException class.  
        /// </summary>  
        /// <param name="content">The populated HTTP content in Json format.</param>  
        public CrmHttpResponseException(HttpContent content)  
            : base(ExtractMessageFromContent(content)) { }  
  
        /// <summary>  
        /// Initializes a new instance of the CrmHttpResponseException class.  
        /// </summary>  
        /// <param name="content">The populated HTTP content in Json format.</param>  
        /// <param name="innerexception">The exception that is the cause of the current exception, or a null reference  
        /// if no inner exception is specified.</param>  
        public CrmHttpResponseException(HttpContent content, Exception innerexception)  
            : base(ExtractMessageFromContent(content), innerexception) { }  
  
        #endregion Constructors  
  
        #region Methods  
        /// <summary>  
        /// Extracts the CRM specific error message and stack trace from an HTTP content.   
        /// </summary>  
        /// <param name="content">The HTTP content in Json format.</param>  
        /// <returns>The error message.</returns>  
        private static string ExtractMessageFromContent(HttpContent content)  
        {  
            string message = String.Empty;  
            string downloadedContent = content.ReadAsStringAsync().Result;  
            if (content.Headers.ContentType.MediaType.Equals("text/plain"))  
            {  
                message = downloadedContent;  
            }  
            else if (content.Headers.ContentType.MediaType.Equals("application/json"))  
            {  
                JObject jcontent = (JObject)JsonConvert.DeserializeObject(downloadedContent);  
                IDictionary<string, JToken> d = jcontent;  
  
                // An error message is returned in the content under the 'error' key.   
                if (d.ContainsKey("error"))  
                {  
                    JObject error = (JObject)jcontent.Property("error").Value;  
                    message = (String)error.Property("message").Value;  
                }  
                else if (d.ContainsKey("Message"))  
                    message = (String)jcontent.Property("Message").Value;  
  
                if (d.ContainsKey("StackTrace"))  
                    _stackTrace = (String)jcontent.Property("StackTrace").Value;  
            }  
            else if (content.Headers.ContentType.MediaType.Equals("text/html"))  
            {  
                message = "HTML content that was returned is shown below.";  
                message += "\n\n" + downloadedContent;  
            }  
            else  
            {  
                message = String.Format("No handler is available for content in the {0} format.",    
                    content.Headers.ContentType.MediaType.ToString());  
            }  
            return message;  
            #endregion Methods  
        }  
    }  
}  
  
```  
  
### <a name="see-also"></a>関連項目

[Web API (C#) を開始する](get-started-dynamics-365-web-api-csharp.md)<br />
[Visual Studio (C#) で Web API プロジェクトを起動する](start-web-api-project-visual-studio-csharp.md)<br />
[アプリ用 Common Data Service Web API Helper Library (C#) の使用](use-microsoft-dynamics-365-web-api-helper-library-csharp.md)<br />
[ヘルパー コード: 認証クラス](web-api-helper-code-authentication-class.md)<br />
[ヘルパー コード: 構成クラス](web-api-helper-code-configuration-classes.md)

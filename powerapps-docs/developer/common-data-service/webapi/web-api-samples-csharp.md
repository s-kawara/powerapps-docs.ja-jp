---
title: 'Web API データ操作のサンプル (C#) (アプリ用 Common Data Service)| Microsoft Docs'
description: 'このトピックには、C# を使用して実装されたさまざまな Web API サンプルに関する説明が記載されています'
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 66e26684-819e-45f7-bec4-c250be4d6fed
caps.latest.revision: 14
author: brandonsimons
ms.author: jdaly
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="web-api-data-operations-samples-c"></a>Web API データ操作のサンプル (C#)

このトピックでは、C# で実装した Web API のサンプルについて説明します 各サンプルではアプリ用 Common Data Service の様々な側面について扱いますが、同様の特性と構造を備えています。  
  
> [!NOTE]
>  この実装方法では下位レベルのオブジェクト作成と明示的 HTTP メッセージの呼び出しが使用されます。 この方法では Web API の動作を制御する下位レベルのオブジェクト プロパティの制御と表示が可能です。 これは内部構造について理解することを目的としており、必ずしも開発者の生産性が最適化されたエクスペリエンスを提供する手法を表すものではありません。  
>   
>  一方、[OData ライブラリ](https://msdn.microsoft.com/library/hh525392\(v=vs.103\).aspx) などの上位レベルのライブラリでは、この下位レベルのクライアント ロジックの大部分が取り除かれています。  The [OData T4 テンプレート](https://blogs.msdn.microsoft.com/odatateam/2012/07/02/trying-out-the-prerelease-odata-client-t4-template/) は任意で OData ライブラリと組み合わせて、自動生成クライアント エンティティ クラスへの使用が可能です。  

<a name="bkmk_prerequisites"></a>
   
## <a name="prerequisites"></a>前提条件

以下は、アプリ用 Common Data Service Web API C# のサンプルの構築および実行に必要です。  
  
-   Microsoft Visual Studio 2015 以降のバージョン。  無料バージョンである [Visual Studio Community](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) は [ここから](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx) ダウンロードして入手できます。  
  
-   参照先の NuGet パッケージをダウンロードおよび更新するにはインターネットに接続されている必要があります。  
  
-   CRUD 操作を行う特権でアプリ用 Common Data Service にアクセスします。  
  
<!-- TODO:
-   In order to run samples against CDS for Apps, you must register your application with Azure Active Directory to obtain a client ID and redirect URL. For more information, see [Walkthrough: Register a Common Data Service for Apps app with Azure Active Directory](../walkthrough-register-app-azure-active-directory.md).   -->

> [!NOTE]
> これらのサンプルは、OAuth ベースの認証用のアセンブリ [Microsoft.IdentityModel.Client.ActiveDirectory](https://docs.microsoft.com/en-us/dotnet/api/microsoft.identitymodel.clients.activedirectory?view=azure-dotnet) のバージョン 2.x が必要です。
  
<a name="bkmk_webApiSamplesListing"></a>

## <a name="web-api-samples-listing-c"></a>Web API サンプルの一覧 (C#)

次の表は、C# で実行されたサンプルを示します。  [Web API のサンプル](web-api-samples.md) で説明されているように、HTTP 要求および応答メッセージに重点を置いている対応するサンプル グループ トピックで、各サンプルはより一般的な方法で説明されています。  
  
|サンプル|サンプル グループ|内容|  
|------------|------------------|-----------------|  
|[Web API 基本操作のサンプル (C#)](samples/basic-operations-csharp.md)|[Web API Operations 操作のサンプル](web-api-basic-operations-sample.md)|アプリ用 Common Data Service エンティティ レコードの作成、取得、更新、削除、関連付け、および関連付け解除の各操作を実行する方法を説明します。|  
|[Web API クエリ データのサンプル (C#)](samples/query-data-csharp.md)|[Web API クエリ データのサンプル](web-api-query-data-sample.md)|OData v4 クエリ構文と機能およびアプリ用 Common Data Service クエリ機能を使用する方法を説明します。 定義済みクエリに関する作業の例を含み、FetchXML を使用してクエリを実行します。|  
|[Web API 条件付き演算サンプル (C#)](samples/conditional-operations-csharp.md)|[Web API 条件付き演算サンプル](web-api-conditional-operations-sample.md)|ETag の条件を指定する条件付き演算の実行方法を示します。|  
|[Web API 機能およびアクションのサンプル (C#)](samples/functions-actions-csharp.md)|[Web API 機能およびアクションのサンプル](web-api-functions-actions-sample.md)|ユーザー定義アクションを含む、バインドされた関数とバインドされていない関数およびアクションの使用方法を説明します。|  
  
<a name="bkmk_howDownloadRun"></a>

## <a name="how-to-download-and-run-the-samples"></a>サンプルのダウンロードおよび実行方法
  
各サンプルのソース・コードは [MSDN コード ギャラリー](https://code.msdn.microsoft.com/site/search?f%5b0%5d.type=user&f%5b0%5d.value=microsoft%20dynamics%20crm%20sdk%20documentation%20team) で入手可能です。 各サンプルをダウンロードするリンクはサンプル トピックに含まれています。 ダウンロードするサンプルは Visual Studio 2015 ソリューション ファイルを格納する圧縮ファイルです。 詳細については、各サンプル トピックの「**このサンプルの実行**」セクションを参照してください。  
  
<a name="bkmk_commonElements"></a>

## <a name="common-elements-found-in-each-sample"></a>各サンプルの共通要素

ほとんどのサンプルには、通常 Web API C# プログラムの基本構造を提供する類似する構造および共通のメソッドやリソースが含まれています。  
  
また、これらの要素の大半は、アプリ用 CDS Web API にアクセスする新しいソリューションを作成するときに表示されます。 詳細については、「[Visual Studio (C#) で Web API プロジェクトを起動](start-web-api-project-visual-studio-csharp.md)」を参照してください。  
  
### <a name="utilized-libraries-and-frameworks"></a>ライブラリやフレームワークの使用
 
この C# の実装は、HTTP 通信、アプリケーション構成、認証、エラー処理、および JSON のシリアル化の以下のヘルパー コードによって異なります。  
  
-   [System.Net.Http namespace](/dotnet/api/system.net.http) に含まれている標準 .NET Framework HTTP メッセージング クラスは、特に [HttpClient](/dotnet/api/system.net.http.httpclient)、[HttpRequestMessage](/dotnet/api/system.net.http.httprequestmessage)、および [HttpResponseMessage](/dotnet/api/system.net.http.httpresponsemessage) は HTTP メッセージングに使用されます。  
  
-   アプリ用 Common Data Service Web API Helper Library は、アプリケーション構成ファイルの読み込み、アプリ用 CDS サーバーでの認証、およびエラー処理操作の支援に使用されます。  詳細については、[アプリ用 Common Data Service Web API Helper Library (C#) の使用](use-microsoft-dynamics-365-web-api-helper-library-csharp.md) を参照してください。  
  
-   Newtonsoft [Json.NET](http://www.newtonsoft.com/json) ライブラリは JSON データ形式をサポートします。  
  
#### <a name="jsonnet-library"></a>Json.NET Library

C# およびその他の管理言語は JSON データ形式をネイティブにサポートしていないため、最適な方法として、この機能のライブラリを使用することです。 詳細については、「[JavaScript および .NET の JavaScript Object Notation (JSON) の概要](https://msdn.microsoft.com/library/bb299886.aspx)」を参照してください。 Json.NET は .NET プロジェクトによく使用されます。 JSON データのシリアル化、変換、クエリ、および形式設定を行う堅牢で、パフォーマンスの高い、オープンソース ([MIT ライセンス](https://opensource.org/licenses/MIT)) のフレームワークを提供します。 詳細については、「[Json.NET ドキュメント](http://www.newtonsoft.com/json/help/html/Introduction.htm)」を参照してください。  
  
C# サンプルでは、このライブラリは主に .NET オブジェクトと HTTP のメッセージ本文間でのデータのシリアル化に使用されます。 ライブラリには、このタスクを実行する複数のメソッドがありますが、サンプルで使用されている方法では、個々の [JObject](http://www.newtonsoft.com/json/help/html/T_Newtonsoft_Json_Linq_JObject.htm) インスタンスを作成し、アプリ用 Common Data Service エンティティ インスタンス (レコード) を表示します。  たとえば、次のコードはアプリ用 Common Data Service <xref href="Microsoft.Dynamics.CRM.contact?text=contact EntityType" /> インスタンスを表示する様々な `contact1` を作成し、この種類における一部のプロパティの値を指定します。  
  
```csharp  
  
JObject contact1 = new JObject();  
contact1.Add("firstname", "Peter");  
contact1.Add("lastname", "Cambel");  
contact1.Add("annualincome", 80000);  
contact1["jobtitle"] = "Junior Developer";  
  
```  
  
 最後のステートメントでのブラケット記法の使用は、[Add](http://www.newtonsoft.com/json/help/html/M_Newtonsoft_Json_Linq_JObject_Add.htm) メソッドと同じです。 また、[Parse](http://www.newtonsoft.com/json/help/html/M_Newtonsoft_Json_Linq_JObject_Parse.htm) 静的メソッドを使用することによって、このインスタンス化を実行できます。  
  
```csharp  
  
JObject contact1 = JObject.Parse(@"{firstname: 'Peter', lastname: 'Cambel', "  
+ @"annualincome: 80000, jobtitle: 'Junior Developer'}");  
  
```  
  
 `JObject` は全般的な JSON の種類を示すため、ランタイムの読み取りは多くの場合除外されます。  たとえば、次のステートメントは構文的には有効ですが、<xref href="Microsoft.Dynamics.CRM.contact?text=contact EntityType" /> には `age` プロパティがないためランタイム エラーが発生する可能性があります。  
  
 `contact1.Add("age", 37);    //Possible error--no age property exists in contact!`  
  
 エンティティの変数が初期化されると、複数の System.Net.Http クラスからのサポートにより、それをメッセージ本文に送信できます。例:  
  
```csharp  
  
HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Post, "contacts");  
request.Content = new StringContent(contact1.ToString(), Encoding.UTF8, "application/json");  
HttpResponseMessage response = await httpClient.SendAsync(request1);  
  
```  
  
 検索操作中にエンティティ インスタンスのシリアル化解除することによって、JObject インスタンスを作成することもできます。例:  
  
```csharp  
  
//contact2Uri contains a reference to an existing CRM contact instance.  
string queryOptions = "?$select=fullname,annualincome,jobtitle,description";  
HttpResponseMessage response = await httpClient.GetAsync(contact2Uri + queryOptions);  
JObject contact2 = JsonConvert.DeserializeObject<JObject>(await response.Content.ReadAsStringAsync());  
  
```  
  
### <a name="response-success-and-error-handling"></a>正常な応答とエラーの処理

一般には、サンプルでは HTTP 応答を処理するシンプルな方法が使用されています。 要求が成功すると、操作における情報は通常、コンソールに出力されます。 応答により JSON ペイロードまたは役立つヘッダーも送信される場合は、この情報は要求が成功した場合にのみ処理されます。 最後に、アプリ用 Common Data Service エンティティが作成された場合は、`entityUris` コレクションはそのリソースの URI によって更新されます。 [DeleteRequiredRecords](#bkmk_deleteRequiredRecords) メソッドはこのコレクションを使用し、オプションで、アプリ用 Common Data Service サーバーのサンプルから作成されたデータを削除します。  
  
要求が失敗した場合は、失敗した操作に関するコンテキスト メッセージを出力し、`CrmHttpResponseException` のユーザー定義の例外メッセージが表示されます。 例外ハンドラーは、例外についての詳細を出力し、`DeleteRequiredRecords` を呼び出すクリーンアップ ロジックを含む `finally` ブロックに制御パスします。 次のコードはレコードを作成する POST 要求のエラー処理方法について示しています。  
  
```csharp  
  
if (response.StatusCode == HttpStatusCode.NoContent)  //204  
{  
Console.WriteLine("POST succeeded, entity created!");  
//optionally process response message headers or body here, for example:  
entityUri = response.Headers.GetValues("OData-EntityId").FirstOrDefault();  
entityUris.Add(entityUri);  
}  
else  
{  
Console.WriteLine("Operation failed: {0}", response.ReasonPhrase);  
throw new CrmHttpResponseException(response.Content);  
}  
  
```  
  
 [HttpStatusCode](https://msdn.microsoft.com/library/hh435235.aspx).NoContent は HTTP ステータス コード 204 (コンテンツなし) と同じです。 このステータス コードは POST 要求が成功したことを意味します。 詳細については、「[HTTP 要求の作成とエラーの処理](https://msdn.microsoft.com/en-us/library/gg334391.aspx)」を参照してください。  
  
### <a name="characteristics-and-methods"></a>特性とメソッド
  
多くのサンプルでは、ー般的な構造上のパターンと同じパターンが示され、次の特性を備えています:  
  
- すべての適切な C# サンプル コードには `Program.cs` という名前の主要ソース ファイルが含まれており、サンプル プロジェクトと同じ名前の単一クラスが含まれています。  
  
- サンプル クラスと [アプリ用 Common Data Service Web API Helper Library](use-microsoft-dynamics-365-web-api-helper-library-csharp.md) は名前空間である `Microsoft.Crm.Sdk.Samples` に含まれています。  
  
- サンプルには次のコメントが含まれています: 概要がクラスおよびメソッド レベルに提供され、ほとんどの主要な個々のステートメントは同じコメントまたは 1 行のコメントを関連付けています。  また、アプリケーション構成ファイル `App.config` などの補足ファイルには、多くの場合、重要なコメントも含まれています。  
  
- 主要サンプル クラスは、通常、以下のメソッドの共通セットを含むように構成されています: [Main](#bkmk_main)、[ConnectToCRM](#bkmk_connectToCrm)、[CreateRequiredRecords](#bkmk_createRequiredRecords)、[RunAsync](#bkmk_runAsync)、[DisplayException](#bkmk_displayException)、および [DeleteRequiredRecords](#bkmk_deleteRequiredRecords) です。  
  
<a name="bkmk_main"></a>
   
#### <a name="main-method"></a>メイン メソッド

定義では、このメソッドはサンプルの実行を開始します。  上位レベルの制御フローおよび例外処理コード ロジックのみが含まれ、多くの場合、コードはまさに以下の通りになります:  
  
```csharp  
  
static void Main(string[] args)  
{  
FunctionsAndActions app = new FunctionsAndActions();  
try  
{  
//Read configuration file and connect to specified CRM server.  
app.ConnectToCRM(args);  
app.CreateRequiredRecords();  
Task.WaitAll(Task.Run(async () => await app.RunAsync()));  
}  
catch (System.Exception ex) { DisplayException(ex);  
}  
finally  
{  
if (app.httpClient != null)  
{  
app.DeleteRequiredRecords(true);  
app.httpClient.Dispose();  
}  
Console.WriteLine("Press <Enter> to exit the program.");  
Console.ReadLine();  
}  
}  
  
```  
  
<a name="bkmk_connectToCrm"></a>

#### <a name="connecttocrm-method"></a>ConnectToCRM メソッド
 
このメソッドはヘルパー ライブラリを呼び出し、アプリケーション構成ファイルを読み込み、次に、指定したアプリ用 Common Data Service サーバーへの接続を確立します。 これらの手順によって、Web 要求の送信および応答の受信を行うプログラムを介して使用される [HttpClient](https://msdn.microsoft.com/en-us/library/system.net.http.httpclient\(v=vs.110\).aspx) クラスのプロパティを初期化します。  次のプロパティがこのオブジェクトに設定されている点に注意します:  
  
```csharp  
  
//Define the Web API address, the max period of execute time, the Odata  
// version, and the expected response payload format.  
httpClient.BaseAddress = new Uri(config.ServiceUrl + "api/data/v8.1/");  
httpClient.Timeout = new TimeSpan(0, 2, 0);  // 2 minute timeout  
httpClient.DefaultRequestHeaders.Add("OData-MaxVersion", "4.0");  
httpClient.DefaultRequestHeaders.Add("OData-Version", "4.0");  
httpClient.DefaultRequestHeaders.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));  
  
```  
  
 サンプルのアプリケーション構成および認証の詳細については、「[アプリ用 Common Data Service Web API Helper Library (C#) の使用](use-microsoft-dynamics-365-web-api-helper-library-csharp.md)」を参照してください。  
  
<a name="bkmk_createRequiredRecords"></a>

#### <a name="createrequiredrecords-method"></a>CreateRequiredRecords メソッド
 
このメソッドは、サンプルでこれらの操作が主要事項とみなされない場合にのみ、サンプルで必要とするエンティティ レコードを作成し、初期化します。  たとえば、サンプルではレコードの作成を主要なタスクとみなすため、[Web API 基本操作のサンプル (C#)](samples/basic-operations-csharp.md) にはこのメソッドは含まれません。  
  
<a name="bkmk_runAsync"></a>

#### <a name="runasync-method"></a>RunAsync メソッド

この非同期メソッドは、適切なソース・コードを格納するか、またはさらに長いプログラムに対しては、適切なサンプル コードをグループ化するメソッドを呼び出します。 含まれているコードは埋め込まれているコメントにより説明されており、コメントはそれぞれに対応するサンプル トピックの**備考**セクションで検索できます。  
  
<a name="bkmk_displayException"></a>
  
#### <a name="displayexception-method"></a>DisplayException メソッド

このヘルパー メソッドは、内部例外を含む例外情報を標準コンソールに表示します。  
  
<a name="bkmk_deleteRequiredRecords"></a>
  
#### <a name="deleterequiredrecords-method"></a>DeleteRequiredRecords メソッド

この付属メソッドは、特に [CreateRequiredRecords](#bkmk_createRequiredRecords) メソッドによって、サンプル レコードとプログラムで作成されたそのほかのアプリ用 Common Data Service サーバー プログラムを任意で削除します。 この操作の検証をユーザーにクエリし、`entityUris` コレクションで繰り返し、HTTP DELETE メッセージを使用して、各要素を削除しようとします。  
  
### <a name="see-also"></a>関連項目  

[アプリ用 Common Data Service Web API を使用する](overview.md)<br />
[Web API のサンプル](web-api-samples.md)<br />
[Web API のサンプル (クライアント側の JavaScript)](web-api-samples-client-side-javascript.md)<br />
[Web API 基本操作のサンプル (C#)](samples/basic-operations-csharp.md)<br />
[Web API クエリ データのサンプル (C#)](samples/query-data-csharp.md)<br />
[Web API 条件付き演算サンプル (C#)](samples/conditional-operations-csharp.md)<br />
[Web API 機能およびアクションのサンプル (C#)](samples/functions-actions-csharp.md)

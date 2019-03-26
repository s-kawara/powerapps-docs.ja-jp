---
title: 'Web API 条件付き演算サンプル (C#) (アプリ用 Common Data Service) | Microsoft Docs'
description: 'このサンプルでは、アプリ用 Common Data Service Web API および C# を使用して、条件付き演算を実行する方法を説明します。'
ms.custom: ''
ms.date: 1/09/2019
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 48a6322c-51f3-4368-ae7b-748d0c771a82
caps.latest.revision: 17
author: KumarVivek
ms.author: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="web-api-conditional-operations-sample-c"></a>Web API 条件付き演算サンプル (C#)

このサンプルでは、アプリ用 CDS Web API と C# を使用して、条件付き演算を実行する方法を説明します。  
  
> [!NOTE]
> このアプリ用 Common Data Service 操作のサンプルの実装とコンソール出力は「[Web API 条件付き演算サンプル](../web-api-conditional-operations-sample.md)」で詳しく説明されています。またコモン C# の構成の使用は「[Web API のサンプル (C#)](../web-api-samples-csharp.md)」で説明されています。  
  
<a name="bkmk_Prereqs"></a>

## <a name="prerequisites"></a>前提条件

すべてのアプリ用 CDS Web API C# サンプルの前提条件は、親トピック [Web API サンプル (C#)](../web-api-samples-csharp.md) の [前提条件](../web-api-samples-csharp.md#bkmk_prerequisites) セクションで説明されています。  
  
<a name="bkmk_RunSample"></a>
 
## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[Web API 条件付き演算サンプル (C#)](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/webapi/C%23) に移動してサンプル リポジトリをクローンもしくはダウンロードし、コンピューターのフォルダにファイルの内容を解凍してください。 抽出されたフォルダーには、次のファイルが含まれている必要があります。

|ファイル|説明|  
|----------|-----------------|  
|SampleProgram.cs|このサンプルのソース コードが含まれます。|  
|App.config|プレースホルダー アプリ用 CDS サーバー接続情報を含むアプリケーション構成ファイルです。 このファイルはリポジトリのすべての Web API のサンプルと共有されます。 ひとつのサンプル用に接続情報を構成する場合、同じ構成の他のサンプルを実行できます。|  
|SampleHelper.cs|設定、認証、`HTTP` レスポンス エラー処理などの一般的なタスクの実行を支援するためのヘルパーコードを含みます。 <br/> このファイルはリポジトリのすべての Web API のサンプルと共有されます。 これには例外および OAuthトークンを管理するためのヘルパー メソッドも含まれます。 このファイル内のメソッドの詳細については、簡単な Web API のサンプルを参照してください。|
|SampleMethod.cs|サンプルのソース・コードをサポートするすべてのメソッドが含まれます。 SampleProgram.cs で使用する関数をこのファイルで定義できます。 |
|ConditionalOperations.sln<br /> ConditionalOperations.csproj<br /> Packages.config<br /> AssemblyInfo.cs|このサンプルの標準 Visual Studio 2017 ソリューション、プロジェクト、NuGet パッケージ、およびアセンブリ情報ファイルです。|  
  
1. ConditionalOperations.sln ファイルをダブルクリックして、Visual Studio でソリューションを開きます。  
  
1. ソリューションを作成します (**作成** > **ソリューションを作成**)。 これにより、必要なすべての NuGet パッケージは自動的にダウンロードおよび更新されます。  
  
1. ソリューションの App.Config ファイルを編集し、このサンプルを実行するアプリ用 CDS サーバー インスタンスを指定します。  
  
1. プロジェクトを実行します。  すべてのサンプル プロジェクトは、既定では、デバッグ モードで実行するように構成されています。  
  
     サンプル コードの出力はコンソール ウィンドウに表示されます。  
  
<a name="bkmk_CodeSample"></a>

## <a name="code-sample"></a>コード サンプル

 `SampleProgram.cs`  
  
```csharp  
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;
using System;
using System.Collections.Generic;
using System.Configuration;
using System.Linq;
using System.Net;
using System.Net.Http;
using System.Text;
using System.Threading.Tasks;

namespace PowerApps.Samples
{
  public partial class SampleProgram
   {
     static void Main(string[] args)
      {
        try
         {
          //Get configuration data from App.config connectionStrings
          string connectionString = ConfigurationManager.ConnectionStrings["Connect"].ConnectionString;

           using (HttpClient client = SampleHelpers.GetHttpClient(
           connectionString,
            SampleHelpers.clientId,
            SampleHelpers.redirectUrl,"v9.0"))
             {
              // <summary> Creates the CRM entity instance used by this sample. </summary>

               // Create a CRM account record.
               Console.WriteLine("\nCreate sample data");
               account.Add("name", "Contoso Ltd");
               account.Add("telephone1", "555-0000"); //Phone number value will increment with each update attempt
               account.Add("revenue", 5000000);
               account.Add("description", "Parent company of Contoso Pharmaceuticals, etc.");

               HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Post, client.BaseAddress + "accounts");
               request.Content = new StringContent(account.ToString(), Encoding.UTF8, "application/json");

              HttpResponseMessage response = client.SendAsync(request, HttpCompletionOption.ResponseContentRead).Result;

                 if (response.IsSuccessStatusCode)
                  {
                    accountUri = response.Headers.GetValues("OData-EntityId").FirstOrDefault();
                    entityUri = accountUri;
                  }
                  else
                   {
                     throw new Exception(string.Format("Failed to create accounts", response.Content));
                   }

                //Retrieve the account record you created.
                 queryOptions = "?$select=name,revenue,telephone1,description";
                    //JObject entity = null;

                 HttpResponseMessage response1 = client.GetAsync(entityUri + queryOptions).Result;
                  if (response1.IsSuccessStatusCode) //200
                   {
                     account = JObject.Parse(response1.Content.ReadAsStringAsync().Result);
                     Console.WriteLine("Account entity created:");
                     Console.WriteLine(account.ToString(Newtonsoft.Json.Formatting.Indented));
                     initialAcctETagVal = account["@odata.etag"].ToString();
                   }

             #region Conditional GET

             Console.WriteLine("\n--Conditional GET section started--");
             // Attempt to retrieve using conditional GET with current ETag value.
             request = new HttpRequestMessage(HttpMethod.Get, accountUri + queryOptions);

             // Retrieve only if it doesn't match previously retrieved version.
             request.Headers.Add("If-None-Match", initialAcctETagVal);
             response = client.SendAsync(request, HttpCompletionOption.ResponseHeadersRead).Result;

              if (response.StatusCode == HttpStatusCode.NotModified)  // 304; expected.
                {
                  Console.WriteLine("Instance retrieved using ETag: {0}", initialAcctETagVal);
                  Console.WriteLine("Expected outcome: Entity was not modified so nothing was returned.");
                }

                else if (response.StatusCode == HttpStatusCode.OK)  // 200; not expected
                 {
                   Console.WriteLine("Instance retrieved using ETag: {0}", initialAcctETagVal);
                   account = JObject.Parse(response.Content.ReadAsStringAsync().Result);
                    Console.WriteLine(account.ToString(Formatting.Indented));
                 }

                else
                 {
                   throw new Exception(string.Format("Failed to retrieve", response.Content));
                  }

                // Modify the account instance by updating telephone1

                 string accountPhoneUri = string.Format("{0}/{1}", accountUri, "telephone1");
                 JObject phoneProperty = new JObject();
                 phoneProperty.Add("value", "555-0001");
                 request = new HttpRequestMessage(HttpMethod.Put, accountPhoneUri);
                 request.Content = new StringContent(phoneProperty.ToString(), Encoding.UTF8, "application/json");
                 response = client.SendAsync(request, HttpCompletionOption.ResponseContentRead).Result;
                 if (response.StatusCode == HttpStatusCode.NoContent)
                  {
                    Console.WriteLine("\nAccount telephone number updated.");
                  }
                 else
                  {
                   throw new Exception(string.Format("Failed to update the account telephone number", response.Content));
                  }

                 // Reattempt conditional GET with original ETag value.
                 request = new HttpRequestMessage(HttpMethod.Get, accountUri + queryOptions);
                 request.Headers.Add("If-None-Match", initialAcctETagVal);
                 response = client.SendAsync(request, HttpCompletionOption.ResponseHeadersRead).Result;

                 if (response.StatusCode == HttpStatusCode.OK) //200; expected
                  {
                    Console.WriteLine("Instance retrieved using ETag: {0}", initialAcctETagVal);
                  }
                 else if (response.StatusCode == HttpStatusCode.NotModified) // 304; not expected
                  {
                    Console.WriteLine("Unexpected status code: '{0}'.", (int)response.StatusCode);
                  }
                   else
                    { throw new Exception(string.Format("Failed to get original ETag value", response.Content)); }

                 // Retrieve and output current account state.
                 account = JObject.Parse(response.Content.ReadAsStringAsync().Result);
                 updatedAcctETagVal = account["@odata.etag"].ToString(); // Capture updated ETag
                  Console.WriteLine(account.ToString(Formatting.Indented));

                 #endregion Conditional GET

                 #region Optimistic concurrency on delete and update
                 Console.WriteLine("\n--Optimistic concurrency section started--");

                 // Attempt to delete original account (if matches original ETag value).
                 request = new HttpRequestMessage(HttpMethod.Delete, accountUri);
                 // If you replace "initialAcctETagVal" with "updatedAcctETagVal", 
                 // delete will succeed.
                 request.Headers.Add("If-Match", initialAcctETagVal); 
                 response = client.SendAsync(request, HttpCompletionOption.ResponseHeadersRead).Result;
                 // 412; Precondition failed error expected

              if (response.StatusCode == HttpStatusCode.PreconditionFailed) 
               {
                Console.WriteLine("Expected Error: The version of the existing record doesn't match the property provided.");
                Console.WriteLine("\tAccount not deleted using ETag '{0}', status code: '{1}'.",
                initialAcctETagVal, (int)response.StatusCode);
               }
               else if (response.IsSuccessStatusCode) // 200-299; not expected
                    {
                      Console.WriteLine("Account deleted!");
                    }

               else
                {
                 throw new Exception(string.Format("Failed to delete original count",response.Content));
                }

                 //Attempt to update account (if matches original ETag value).
                 JObject accountUpdate = new JObject();
                 accountUpdate.Add("telephone1", "555-0002");
                 accountUpdate.Add("revenue", 6000000);
                 request = new HttpRequestMessage(new HttpMethod("PATCH"), accountUri);
                 request.Content = new StringContent(accountUpdate.ToString(),
                 Encoding.UTF8, "application/json");
                 request.Headers.Add("If-Match", initialAcctETagVal);
                 response = client.SendAsync(request, HttpCompletionOption.ResponseHeadersRead).Result;

             if (response.StatusCode == HttpStatusCode.PreconditionFailed) // 412;
                    //Precondition failed error expected
              {
                Console.WriteLine("Expected Error: The version of the existing record doesn't match the property provided.");
                Console.WriteLine("\tAccount not updated using ETag '{0}', status code: '{1}'.",
                initialAcctETagVal, (int)response.StatusCode);
               }
             else if (response.StatusCode == HttpStatusCode.NoContent)  // 204; not expected
               {
                Console.WriteLine("Account updated using ETag: {0}, status code: '{1}'.",
                initialAcctETagVal, (int)response.StatusCode);
               }
             else
              {
                throw new Exception(string.Format("Failed to update account (if original ETag value matches)", response.Content));
              }

                  // Reattempt update if matches current ETag value.
                  accountUpdate["telephone1"] = "555-0003";
                  request = new HttpRequestMessage(new HttpMethod("PATCH"), accountUri);
                  request.Content = new StringContent(accountUpdate.ToString(),
                  Encoding.UTF8, "application/json");
                  request.Headers.Add("If-Match", updatedAcctETagVal);
                  response = client.SendAsync(request, HttpCompletionOption.ResponseHeadersRead).Result;

                 if (response.StatusCode == HttpStatusCode.NoContent) // 204; expected
                  {
                    Console.WriteLine("\nAccount successfully updated using ETag: {0}, status code: '{1}'.",
                    updatedAcctETagVal, (int)response.StatusCode);
                  }
                 else if (response.StatusCode == HttpStatusCode.PreconditionFailed) // 412; not expected
                  {
                    Console.WriteLine("Unexpected status code: '{0}'", (int)response.StatusCode);
                  }
                 else
                  {
                    throw new Exception(string.Format("Failed to update if matches current ETag value", response.Content));
                  }

                 // Retrieve and output current account state.
                 account = GetCurrentRecord(client,accountUri, queryOptions);
                 updatedAcctETagVal = account["@odata.etag"].ToString(); //Capture updated ETag
                 Console.WriteLine(account.ToString(Formatting.Indented));

                 #endregion Optimistic concurrency on delete and update

                 #region Controlling upsert operations
                 Console.WriteLine("\n--Controlling upsert operations section started--");
                 //Attempt to insert without update some properties for this account
                 accountUpdate = new JObject();
                 accountUpdate.Add("telephone1", "555-0004");
                 accountUpdate.Add("revenue", 7500000);

                 request = new HttpRequestMessage(new HttpMethod("PATCH"), accountUri);
                 request.Content = new StringContent(accountUpdate.ToString(),
                 Encoding.UTF8, "application/json");
                 
                 //Perform operation only if matching resource does not exist. 
                 request.Headers.Add("If-None-Match", "*");
                 response = client.SendAsync(request, HttpCompletionOption.ResponseHeadersRead).Result;

                 if (response.StatusCode == HttpStatusCode.PreconditionFailed) // 412; expected
                  {
                    Console.WriteLine("Expected Error: A record with matching key values already exists.");
                    Console.WriteLine("\tAccount not updated using ETag '{0}, status code: '{1}'.",
                    initialAcctETagVal, (int)response.StatusCode);
                  }
                 else if (response.StatusCode == HttpStatusCode.NoContent) // 204; unexpected
                  {
                    Console.WriteLine("Account updated using If-None-Match '*'");
                  }

                 else
                  {
                    throw new Exception(string.Format("Failed to perform operations", response.Content));
                  }

                 //Attempt to perform same update without creation. 
                 accountUpdate["telephone1"] = "555-0005";
                 request = new HttpRequestMessage(new HttpMethod("PATCH"), accountUri);
                 request.Content = new StringContent(accountUpdate.ToString(),
                 Encoding.UTF8, "application/json");
                 //Perform operation only if matching resource exists. 
                 request.Headers.Add("If-Match", "*");
                 response = client.SendAsync(request, HttpCompletionOption.ResponseHeadersRead).Result;

                 if (response.StatusCode == HttpStatusCode.NoContent)  // 204; expected
                  {
                    Console.WriteLine("Account updated using If-Match '*'");
                  }
                 else if (response.StatusCode == HttpStatusCode.PreconditionFailed) // 412; not expected
                  {
                    Console.WriteLine("Account not updated using If-Match '*', status code: '{0}'.",
                    (int)response.StatusCode);
                  }
                 else
                  {
                   throw new Exception(string.Format("Failed to perform operations", response.Content));
                  }

                //Retrieve and output current account state.
                 account = GetCurrentRecord(client,accountUri, queryOptions);
                 Console.WriteLine(account.ToString(Formatting.Indented));

                 // Delete the account record
                 HttpResponseMessage deleteResponse;
                 deleteResponse = client.DeleteAsync(accountUri).Result;
                 if (deleteResponse.IsSuccessStatusCode) // 200-299
                  {
                    Console.WriteLine("\nAccount was deleted.");
                  }
                 else if (deleteResponse.StatusCode == HttpStatusCode.NotFound)
                  // 404; entity record may have been deleted by another user.
                   {
                    Console.WriteLine("Account could not be found.");
                   }
                 else // Failed to delete
                   {
                        // Throw last failure.
                    throw new Exception(string.Format("Failed to delete account record", response.Content));
                   }

                // Attempt to update it
                 accountUpdate["telephone1"] = "555-0006";
                 request = new HttpRequestMessage(new HttpMethod("PATCH"), accountUri);
                 request.Content = new StringContent(accountUpdate.ToString(),
                 Encoding.UTF8, "application/json");

                 // Perform operation only if matching resource exists.
                 request.Headers.Add("If-Match", "*");
                 response = client.SendAsync(request, HttpCompletionOption.ResponseHeadersRead).Result;

                 if (response.StatusCode == HttpStatusCode.PreconditionFailed ||
                             response.StatusCode == HttpStatusCode.NotFound)  // 412 or 404; expected
                  {
                    Console.WriteLine("Expected Error: Account with Id = {0} does not exist.", account["accountid"]);
                    Console.WriteLine("Account not updated because it does not exist, status code: '{0}'.",
                    (int)response.StatusCode);
                  }
                  else if (response.StatusCode == HttpStatusCode.NoContent)  // 204; not expected                                                                       
                   {
                    Console.WriteLine("Account upserted using If-Match '*'");
                   }
                   else
                    {
                      throw new Exception(string.Format("Failed to perform operations", response.Content));
                    }

                    #endregion Controlling upsert operations
                }
            }
            catch (Exception ex)
            {
                SampleHelpers.DisplayException(ex);
                throw;
            }
            finally
            {
                Console.WriteLine("Press <Enter> to exit the program.");
                Console.ReadLine();
            }
        }
    }
}

```  
  
### <a name="see-also"></a>関連項目

[アプリ用 Common Data Service Web API を使用する](../overview.md)<br />
[Web API を使用する条件付き演算を実行する](../perform-conditional-operations-using-web-api.md)<br />
[Web API のサンプル](../web-api-samples.md)<br />
[Web API 条件付き演算サンプル](../web-api-conditional-operations-sample.md)
[Web API 基本操作のサンプル (C#)](basic-operations-csharp.md)<br />
[Web API クエリ データのサンプル (C#)](query-data-csharp.md)<br />
[Web API 機能およびアクションのサンプル (C#)](functions-actions-csharp.md)

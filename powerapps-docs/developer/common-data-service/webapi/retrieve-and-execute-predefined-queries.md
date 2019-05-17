---
title: 定義済みクエリの取得と実行 (Common Data Service)| Microsoft Docs
description: Common Data Service は、すべてのユーザーが利用できるシステム ビューを管理者が作成する方法を提供します。 データを取得するために事前定義クエリを構成する方法および FetchXML を使用してクエリ文字列を作成する方法を説明します。
ms.custom: ''
ms.date: 10/31/2018
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 3d771a18-3dc5-4372-a7c7-40b3b1f986d8
caps.latest.revision: 16
author: brandonsimons
ms.author: jdaly
ms.reviewer: susikka
manager: annbe
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="retrieve-and-execute-predefined-queries"></a>定義済みクエリの取得と実行

Common Data Service は、すべてのユーザーが利用できるシステム ビューを管理者が作成する方法を提供します。 個々のユーザーはアプリケーション再利用できるように高度な検索のクエリを保存できます。 これらはどちらも、Web API を使用して取得して実行できる定義済みクエリです。 また、FetchXml を使用してクエリを構成し、そのクエリを使用してデータを取得することもできます。

<a name="bkmk_predefinedQueries"></a>

## <a name="predefined-queries"></a>定義済みクエリ

Common Data Service では、ここに示す 2 種類のクエリを定義、保存、および実行できます。

|クエリの種類|内容|
|----------------|-----------------|
|**保存済みクエリ**|エンティティのシステム定義ビュー。 このビューは <xref href="Microsoft.Dynamics.CRM.savedquery?text=savedquery EntityType" /> に格納されます。 詳細: [エンティティ ビューのカスタマイズ](../../model-driven-apps/customize-entity-views.md)| 
|**ユーザー クエリ**|エンティティについてユーザーが保存する高度な検索の内容。 このビューは <xref href="Microsoft.Dynamics.CRM.userquery?text=userquery EntityType" /> に格納されます。 詳細: [UserQuery (保存されたビュー) エンティティ](../saved-queries.md)|

これらの両方の種類のエンティティのレコードには、返すデータに対する FetchXML 定義が含まれています。 それぞれのエンティティの種類をクエリして、主キーの値を取得できます。 主キーの値を使用する場合、主キー値を渡すことでクエリを実行できます。 たとえば、**アクティブなアカウント**の保存済みクエリを実行するには、このようなクエリを使用して最初に主キーを取得する必要があります。

```http
GET [Organization URI]/api/data/v9.0/savedqueries?$select=name,savedqueryid&$filter=name eq 'Active Accounts'
```

次に、`savedqueryid` 値を使用して、その値を savedQuery パラメーターへの値として、 取引先企業エンティティ セットに渡すことができます。

```http
GET [Organization URI]/api/data/v9.0/accounts?savedQuery=00000000-0000-0000-00aa-000010001002
```

同じ方法を使用して userqueryid を取得し、その値を `userQuery` パラメータへの値として、保存したクエリの対応する `returnedtypecode` に一致するエンティティ セットに渡します。

```http
GET [Organization URI]/api/data/v9.0/accounts?userQuery=121c6fd8-1975-e511-80d4-00155d2a68d1
```

### <a name="apply-a-query-to-any-collection-of-the-appropriate-type"></a>適切な種類のコレクションにクエリを適用する

メイン エンティティ セットのコレクションに保存済みクエリを単純に適用することに加えて、保存済みクエリまたはユーザー クエリを使用して、適切な種類のエンティティのコレクションに同じフィルタリングを適用することもできます。 たとえば、特定のエンティティに関連するエンティティだけにクエリを適用する場合は、同じパターンを適用できます。 たとえば、次の URL は、`opportunity_parent_account` コレクション値を持つナビゲーション プロパティを使用して、**オープンされている営業案件**クエリを特定の取引先企業に関連する営業案件に適用します。

```http
GET [Organization URI]/api/data/v9.0/accounts(8f390c24-9c72-e511-80d4-00155d2a68d1)/opportunity_parent_account/?savedQuery=00000000-0000-0000-00aa-000010003001
```

<a name="bkmk_useFetchXML"></a>

## <a name="use-custom-fetchxml"></a>ユーザー定義の FetchXML を使用する

FetchXML は集計を実行する機能を提供する独自のクエリ言語です。 詳細: [FetchXML でデータをクエリする](../use-fetchxml-construct-query.md)

`fetchXml` クエリ文字列パラメーターを使用して、クエリのルート エンティティに対応するエンティティ セットに URL エンコードした FetchXML をクエリとして渡して、Web API から結果を返すことができます。 たとえば、取引先企業をエンティティとして含んでいる次の FetchXML を使用できます。  

```xml  
<fetch mapping='logical'>
   <entity name='account'>
      <attribute name='accountid'/>
      <attribute name='name'/>
</entity>
</fetch>
```

この URL にはこの FetchXML のエンコード値が次のように表示されます。

```text
%3Cfetch%20mapping='logical'%3E%3Centity%20name='account'%3E%3Cattribute%20name='accountid'/%3E%3Cattribute%20name='name'/%3E%3C/entity%3E%3C/fetch%3E
```

ほとんどのプログラミング言語には、文字列を URL エンコードする関数が含まれています。 たとえば、JavaScript では、[encodeURI](http://www.ecma-international.org/ecma-262/5.1/) 関数を使用します。 RESTful Web サービスに送信する要求を URL エンコードする必要があります。 URL をブラウザーのアドレス バーに貼り付ける場合、ブラウザーはそのアドレスを自動的に URL エンコードする必要があります。 次の例は、取引先企業用のエンティティ セット パスを使用して、先に示した FetchXML を使用して GET 要求を示します。

**要求**

```http
GET [Organization URI]/api/data/v9.0/accounts?fetchXml=%3Cfetch%20mapping='logical'%3E%3Centity%20name='account'%3E%3Cattribute%20name='accountid'/%3E%3Cattribute%20name='name'/%3E%3C/entity%3E%3C/fetch%3E HTTP/1.1
Accept: application/json
OData-MaxVersion: 4.0
OData-Version: 4.0
```

**応答**

```http
HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal
OData-Version: 4.0

{  
  "@odata.context":"[Organization URI]/api/data/v9.0/$metadata#accounts(accountid,name)","value":[  
    {  
      "@odata.etag":"W/\"506678\"","accountid":"89390c24-9c72-e511-80d4-00155d2a68d1","name":"Fourth Coffee (sample)"  
    },{  
      "@odata.etag":"W/\"502172\"","accountid":"8b390c24-9c72-e511-80d4-00155d2a68d1","name":"Litware, Inc. (sample)"  
    },{  
      "@odata.etag":"W/\"502174\"","accountid":"8d390c24-9c72-e511-80d4-00155d2a68d1","name":"Adventure Works (sample)"  
    },{  
      "@odata.etag":"W/\"506705\"","accountid":"8f390c24-9c72-e511-80d4-00155d2a68d1","name":"Fabrikam, Inc. (sample)"  
    },{  
      "@odata.etag":"W/\"506701\"","accountid":"91390c24-9c72-e511-80d4-00155d2a68d1","name":"Blue Yonder Airlines (sample)"  
    },{  
      "@odata.etag":"W/\"502180\"","accountid":"93390c24-9c72-e511-80d4-00155d2a68d1","name":"City Power & Light (sample)"  
    },{  
      "@odata.etag":"W/\"502182\"","accountid":"95390c24-9c72-e511-80d4-00155d2a68d1","name":"Contoso Pharmaceuticals (sample)"  
    },{  
      "@odata.etag":"W/\"506704\"","accountid":"97390c24-9c72-e511-80d4-00155d2a68d1","name":"Alpine Ski House (sample)"  
    },{  
      "@odata.etag":"W/\"502186\"","accountid":"99390c24-9c72-e511-80d4-00155d2a68d1","name":"A. Datum Corporation (sample)"  
    },{  
      "@odata.etag":"W/\"502188\"","accountid":"9b390c24-9c72-e511-80d4-00155d2a68d1","name":"Coho Winery (sample)"  
    },{  
      "@odata.etag":"W/\"504177\"","accountid":"0a3238d4-f973-e511-80d4-00155d2a68d1","name":"Litware, Inc."  
    }  
  ]  
}  
```

<a name="bkmk_WebAPIFetchPaging"></a>

### <a name="paging-with-fetchxml"></a>FetchXML によるページング

FetchXML では、`fetch` 要素の `count` 属性と `page` 属性を設定することで、ページングを適用することができます。 たとえば、取引先企業に対するクエリを設定し、エンティティ数を 2 に制限するには、また最初のページだけを返すには、次の fetchXML は以下を行う必要があります。

```xml
<fetch mapping="logical" page="1" count="2">  
 <entity name="account">  
  <attribute name="accountid" />  
  <attribute name="name" />  
  <attribute name="industrycode" />  
 <order attribute="name" />  
 </entity>  
</fetch>
```

<!-- TODO:
With a request using FetchXML you can also request a paging cookie and include it with your query. More information:[Page large result sets with FetchXML](../org-service/page-large-result-sets-with-fetchxml.md)   -->

ページング クッキーは注釈として要求される必要があります。 `Microsoft.Dynamics.CRM.fetchxmlpagingcookie` を使用する (または含める) `odata.include-annotations` 基本設定を指定すると、`@Microsoft.Dynamics.CRM.fetchxmlpagingcookie` プロパティが結果といっしょに返されます。

<a name="bkmk_FetchXMLwithinBatch"></a>

### <a name="use-fetchxml-within-a-batch-request"></a>バッチ要求内で FetchXML を使用する

`GET` 要求内の URL の長さは制限されています。 URL に FetchXML をパラメーターとして含めると、この制限に達する可能性があります。  この制限が適用されない要求本体に URL から FetchXML を移動する方法として、`POST` 要求を使用する `$batch` オペレーションを実行することができます。 詳細: [Web API を使用してバッチ操作を実行する](execute-batch-operations-using-web-api.md)。

#### <a name="example"></a>例

**要求**

```http
POST [Organization URI]/api/data/v9.0/$batch HTTP/1.1

Content-Type:multipart/mixed;boundary=batch_AAA123
Accept:application/json
OData-MaxVersion:4.0
OData-Version:4.0

--batch_AAA123
Content-Type: application/http
Content-Transfer-Encoding: binary

GET [Organization URI]/api/data/v9.0/accounts?fetchXml=%3Cfetch%20mapping='logical'%3E%3Centity%20name='account'%3E%3Cattribute%20name='accountid'/%3E%3Cattribute%20name='name'/%3E%3Cattribute%20name='telephone1'/%3E%3Cattribute%20name='accountid'/%3E%3Cattribute%20name='creditonhold'/%3E%3C/entity%3E%3C/fetch%3E HTTP/1.1
Content-Type: application/json
OData-Version: 4.0
OData-MaxVersion: 4.0

--batch_AAA123--
```

**応答**

```json
--batchresponse_cbfd44cd-a322-484e-913b-49e18af44e34
Content-Type: application/http
Content-Transfer-Encoding: binary

HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal
OData-Version: 4.0

{  
   "@odata.context":"[Organization URI]/api/data/v9.0/$metadata#accounts(accountid,name,telephone1,creditonhold)",
   "value":[  
      {  
         "@odata.etag":"W/\"563737\"",
         "accountid":"1f55c679-485e-e811-8151-000d3aa3c22a",
         "name":"Fourth Coffee (sample)",
         "telephone1":"+1-425-555-0121",
         "creditonhold":false
      },
      {  
         "@odata.etag":"W/\"563739\"",
         "accountid":"2555c679-485e-e811-8151-000d3aa3c22a",
         "name":"Litware, Inc. (sample)",
         "telephone1":"+1-425-555-0120",
         "creditonhold":false
      }
   ]
}
--batchresponse_cbfd44cd-a322-484e-913b-49e18af44e34--
```



## <a name="see-also"></a>関連項目

[Web API クエリ データのサンプル (C#)](samples/query-data-csharp.md)<br />
[Web API クエリ データのサンプル (クライアント側の JavaScript)](samples/query-data-client-side-javascript.md)<br />
[Web API を使用して演算を実行する](perform-operations-web-api.md)<br />
[HTTP 要求の作成とエラーの処理](compose-http-requests-handle-errors.md)<br />
[Web API を使用したクエリ データ](query-data-web-api.md)<br />
[Web API を使用してエンティティを作成する](create-entity-web-api.md)<br />
[Web API を使用してエンティティを取得する](retrieve-entity-using-web-api.md)<br />
[Web API を使用したエンティティの更新と削除](update-delete-entities-using-web-api.md)<br />
[Web API を使用したエンティティの関連付けと関連付け解除](associate-disassociate-entities-using-web-api.md)<br />
[Web API 関数の使用](use-web-api-functions.md)<br />
[Web API アクションの使用](use-web-api-actions.md)<br />
[Web API を使用してバッチ操作を実行する](execute-batch-operations-using-web-api.md)<br />
[Web API を使用して別のユーザーを偽装する](impersonate-another-user-web-api.md)<br />
[Web API を使用する条件付き演算を実行する](perform-conditional-operations-using-web-api.md)<br />

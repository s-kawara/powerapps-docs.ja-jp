---
title: Web API クエリ データのサンプル (Common Data Service) | Microsoft Docs
description: 'このサンプル グループは、Web API を使用してデータをクエリする方法を示します。 これらは、クライアント側の JavaScript と C# を使用して実装されます'
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 9457ce4f-0ef6-4085-8346-fe3134ec7106
caps.latest.revision: 18
author: brandonsimons
ms.author: jdaly
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="web-api-query-data-sample"></a>Web API クエリ データのサンプル

このサンプル グループは、Common Data Service Web API を使用してデータをクエリする方法を説明します。 このサンプルは次の言語に対する別個のプロジェクトとして実装されます。

- [Web API クエリ データのサンプル (クライアント側の JavaScript)](samples/query-data-client-side-javascript.md)

- [クエリ データのサンプル (C#)](samples/query-data-csharp.md)

このトピックでは、この各グループに対して実装される共通の一連の操作について説明します。 このトピックでは、このグループの各サンプルが言語固有の詳細な情報なしで実行する HTTP 要求と応答とテキスト出力について説明します。 この操作を実行する方法に関する詳細については、言語に特有の説明および個別のサンプルを参照してください。

## <a name="demonstrates"></a>説明

このサンプルは次の主要なセクションに分かれています。それには関連する概念的なトピックでより詳しく説明される Web API クエリ データ処理が含まれます。

|トピック セクション|関連するトピック|
|-------------------|---------------------------|
|[指定されたプロパティの選択](#bkmk_selectproperties)|[特定のプロパティの取得](retrieve-entity-using-web-api.md#bkmk_requestProperties)<br /><br /> [書式設定値を含める](query-data-web-api.md#bkmk_includeFormattedValues)|
|[クエリ機能の使用](#bkmk_queryfunctions)|[結果のフィルター](query-data-web-api.md#bkmk_filter)<br /><br /> [標準クエリ機能](query-data-web-api.md#bkmk_buildInQueryFunctions)<br /><br /> [関数を使用してクエリを作成する](use-web-api-functions.md#bkmk_composeQueryWithFunctions)<br /><br /> <xref:Microsoft.Dynamics.CRM.QueryFunctionIndex>|
|[演算子の使用](#bkmk_operators)|[標準フィルタ演算子](query-data-web-api.md#bkmk_buildInFilterOperators)|
|[優先順位の設定](#bkmk_prededence)|[標準フィルタ演算子](query-data-web-api.md#bkmk_buildInFilterOperators)|
|[順番の結果](#bkmk_orderresults)|[順番の結果](query-data-web-api.md#bkmk_order)<br /><br /> [結果のフィルター](query-data-web-api.md#bkmk_filter)|
|[パラメーターのエイリアス](#bkmk_parameteralias)|[システム クエリ オプションを持つパラメーター エイリアスを使用します](query-data-web-api.md#bkmk_useParameterAliases)|
|[結果の制限](#bkmk_limitresults)|[結果の制限](query-data-web-api.md#bkmk_limitResults)<br /><br /> [返されるエンティティ数の制限](query-data-web-api.md#bkmk_limits)|
|[結果の展開](#bkmk_expandresults)|[ナビゲーション プロパティの拡張による関連エンティティの取得](query-data-web-api.md#bkmk_expandRelated)|
<!-- TODO:
|[FetchXML queries](#bkmk_fetchxml)|[FetchXML schema](../org-service/fetchxml-schema.md)<br /><br /> [Page large result sets with FetchXML](../org-service/page-large-result-sets-with-fetchxml.md)<br /><br /> [Use custom FetchXML](retrieve-and-execute-predefined-queries.md#bkmk_useFetchXML)| -->
|[定義済みクエリ](#bkmk_predefinedqueries)|[定義済みクエリの取得と実行](retrieve-and-execute-predefined-queries.md)<br /><br /> <xref href="Microsoft.Dynamics.CRM.userquery?text=userquery EntityType" /><br /><br /> <xref href="Microsoft.Dynamics.CRM.savedquery?text=savedquery EntityType" />|

次のセクションには、Common Data Service Web API 操作の実行に関する簡単な説明が、対応する HTTP メッセージおよび関連するコンソール出力と共に示されています。

<a name="bkmk_sampleData"></a>

## <a name="sample-data"></a>サンプル データ

このサンプルのクエリが正常に動作するためには、このサンプルによる、サンプル レコードの標準セットが 1 つは作成される必要があります。 これらのサンプル レコードは、ユーザーがレポートの削除をしないという選択をしない限り削除されます。 これはサンプルがクエリを実行するデータです。 環境の既存のデータにより結果が異なる可能性があります。  
  
*ディープ挿入* を使用して 1 つの `POST` 要求にデータが追加されます。これは次の構造に一致します。  
  
```json  
  
 {  
        "name": "Contoso, Ltd. (sample)",  
        "primarycontactid": {  
            "firstname": "Yvonne", "lastname": "McKay (sample)", "jobtitle": "Coffee Master",  
            "annualincome": 45000, "Contact_Tasks": [  
            { "subject": "Task 1", "description": "Task 1 description" },  
            { "subject": "Task 2", "description": "Task 2 description" },  
            { "subject": "Task 3", "description": "Task 3 description" }  
            ]  
        },   
                            "Account_Tasks": [  
        { "subject": "Task 1", "description": "Task 1 description" },  
        { "subject": "Task 2", "description": "Task 2 description" },  
        { "subject": "Task 3", "description": "Task 3 description" }  
        ],  
        "contact_customer_accounts": [  
            {  
                "firstname": "Susanna", "lastname": "Stubberod (sample)", "jobtitle": "Senior Purchaser",  
                "annualincome": 52000, "Contact_Tasks": [  
            { "subject": "Task 1", "description": "Task 1 description" },  
            { "subject": "Task 2", "description": "Task 2 description" },  
            { "subject": "Task 3", "description": "Task 3 description" }  
                ]  
            },  
            {  
                "firstname": "Nancy", "lastname": "Anderson (sample)", "jobtitle": "Activities Manager",  
                "annualincome": 55500, "Contact_Tasks": [  
                { "subject": "Task 1", "description": "Task 1 description" },  
                { "subject": "Task 2", "description": "Task 2 description" },  
                { "subject": "Task 3", "description": "Task 3 description" }  
                ]  
            },  
            {  
                "firstname": "Maria", "lastname": "Cambell (sample)", "jobtitle": "Accounts Manager",  
                "annualincome": 31000, "Contact_Tasks": [  
                { "subject": "Task 1", "description": "Task 1 description" },  
                { "subject": "Task 2", "description": "Task 2 description" },  
                { "subject": "Task 3", "description": "Task 3 description" }  
                ]  
            },  
            {  
                "firstname": "Nancy", "lastname": "Anderson (sample)", "jobtitle": "Logistics Specialist",  
                "annualincome": 63500, "Contact_Tasks": [  
                { "subject": "Task 1", "description": "Task 1 description" },  
                { "subject": "Task 2", "description": "Task 2 description" },  
                { "subject": "Task 3", "description": "Task 3 description" }  
                ]  
            },  
            {  
                "firstname": "Scott", "lastname": "Konersmann (sample)", "jobtitle": "Accounts Manager",  
                "annualincome": 38000, "Contact_Tasks": [  
                { "subject": "Task 1", "description": "Task 1 description" },  
                { "subject": "Task 2", "description": "Task 2 description" },  
                { "subject": "Task 3", "description": "Task 3 description" }  
                ]  
            },  
            {  
                "firstname": "Robert", "lastname": "Lyon (sample)", "jobtitle": "Senior Technician",  
                "annualincome": 78000, "Contact_Tasks": [  
                { "subject": "Task 1", "description": "Task 1 description" },  
                { "subject": "Task 2", "description": "Task 2 description" },  
                { "subject": "Task 3", "description": "Task 3 description" }  
                ]  
            },  
            {  
                "firstname": "Paul", "lastname": "Cannon (sample)", "jobtitle": "Ski Instructor",  
                "annualincome": 68500, "Contact_Tasks": [  
                { "subject": "Task 1", "description": "Task 1 description" },  
                { "subject": "Task 2", "description": "Task 2 description" },  
                { "subject": "Task 3", "description": "Task 3 description" }  
                ]  
            },  
            {  
                "firstname": "Rene", "lastname": "Valdes (sample)", "jobtitle": "Data Analyst III",  
                "annualincome": 86000, "Contact_Tasks": [  
                { "subject": "Task 1", "description": "Task 1 description" },  
                { "subject": "Task 2", "description": "Task 2 description" },  
                { "subject": "Task 3", "description": "Task 3 description" }  
                ]  
            },  
            {  
                "firstname": "Jim", "lastname": "Glynn (sample)", "jobtitle": "Senior International Sales Manager",  
                "annualincome": 81400, "Contact_Tasks": [  
                { "subject": "Task 1", "description": "Task 1 description" },  
                { "subject": "Task 2", "description": "Task 2 description" },  
                { "subject": "Task 3", "description": "Task 3 description" }  
                ]  
            }  
        ]  
    }  
```  
  
<a name="bkmk_selectproperties"></a>
   
## <a name="selecting-specific-properties"></a>指定されたプロパティの選択
  
`$select` クエリ オプションを使用して、常にクエリを作成します。それ以外の場合、サーバーは各エンティティのすべてのプロパティを返すのでパフォーマンスが低下します。 この例は、<xref href="Microsoft.Dynamics.CRM.contact?text=contact EntityType" /> の 3 つのプロパティの選択することにより、基本的なクエリを作成する方法を説明します。 そのプロパティは、`fullname`、`jobtitle`、`annualincome` です。 このセクションは、取引先担当者の `annualincome` プロパティの結果に見られる、書式設定された値および書式設定されていない値の違いについても示します。 詳細: [特定のプロパティの要求](query-data-web-api.md#bkmk_requestProperties)、[書式設定値を含める](query-data-web-api.md#bkmk_includeFormattedValues)。  
  
この例では、特定の取引先担当者に要求します。 この場合、それは取引先企業の取引先責任者である `Yvonne McKay (sample)` です。  
  
 **HTTP 要求**  
  
```  
GET http://[Organization URI]/api/data/v9.0/contacts(b848fdee-c143-e611-80d5-00155da84802)?$select=fullname,jobtitle,annualincome HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Prefer: odata.maxpagesize=10, odata.include-annotations=OData.Community.Display.V1.FormattedValue  
```  
  
 **HTTP 応答**  
  
```  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Preference-Applied: odata.include-annotations="OData.Community.Display.V1.FormattedValue"  
Preference-Applied: odata.maxpagesize=10  
Content-Length: 517  
  
{  
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#contacts(fullname,jobtitle,annualincome)/$entity",  
   "@odata.etag":"W/\"619718\"",  
   "fullname":"Yvonne McKay (sample)",  
   "jobtitle":"Coffee Master",  
   "annualincome@OData.Community.Display.V1.FormattedValue":"$45,000.00",  
   "annualincome":45000.0000,  
   "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
   "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
   "contactid":"15c364b2-bf43-e611-80d5-00155da84802"  
}  
```  
  
 **コンソール出力**  
  
```  
Contact basic info:  
    Fullname: 'Yvonne McKay (sample)'  
    Jobtitle: 'Coffee Master'  
    Annualincome: '45000' (unformatted)  
    Annualincome: $45,000.00 (formatted)  
  
```  
  
<a name="bkmk_queryfunctions"></a>
  
## <a name="using-query-functions"></a>クエリ機能の使用
 
フィルター オプションを使用して適切な結果を得られるように条件を設定します。 クエリ関数、比較演算子、および論理演算子を組み合わせて使用することにより、簡単なフィルターあるいは複雑なフィルターを作成できます。 詳細: [結果のフィルター](query-data-web-api.md#bkmk_filter)。  
  
クエリ関数は、クエリ内のフィルター条件として使用できる関数です。 標準のクエリ関数および Common Data Service 固有のクエリ関数があります。 これらの関数は、パラメーターを受け入れ、`Boolean` 値を返します。 このサンプルは、各種類のクエリを作成する方法を説明します。  
  
### <a name="standard-query-functions"></a>標準クエリ機能

Common Data Service は、OData の組み込みクエリ関数の小さなサブセットをサポートします。`contains`、`endswith`、および `startswith` を特にサポートします。 たとえば、`contains` 標準クエリ関数は、文字列に一致したプロパティでフィルター処理することができます。 この操作では、`(sample)` を含む文字列で、すべての取引先の担当者の `fullname` に対してクエリを実行します。 詳細: [標準クエリ機能](query-data-web-api.md#bkmk_buildInQueryFunctions)。  
  
 **HTTP 要求**  
  
```  
GET http://[Organization URI]/api/data/v9.0/contacts?$select=fullname,jobtitle,annualincome&$filter=contains(fullname,'(sample)') HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Prefer: odata.maxpagesize=10, odata.include-annotations=OData.Community.Display.V1.FormattedValue  
```  
  
 **HTTP 応答**  
  
```  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Preference-Applied: odata.include-annotations="OData.Community.Display.V1.FormattedValue"  
Preference-Applied: odata.maxpagesize=10  
Content-Length: 4284  
  
{  
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#contacts(fullname,jobtitle,annualincome)",  
   "value":[  
      {  
         "@odata.etag":"W/\"619718\"",  
         "fullname":"Yvonne McKay (sample)",  
         "jobtitle":"Coffee Master",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$45,000.00",  
         "annualincome":45000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"15c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619839\"",  
         "fullname":"Susanna Stubberod (sample)",  
         "jobtitle":"Senior Purchaser",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$52,000.00",  
         "annualincome":52000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"1cc364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619841\"",  
         "fullname":"Nancy Anderson (sample)",  
         "jobtitle":"Activities Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$55,500.00",  
         "annualincome":55500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"20c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619843\"",  
         "fullname":"Maria Cambell (sample)",  
         "jobtitle":"Accounts Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$31,000.00",  
         "annualincome":31000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"24c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619845\"",  
         "fullname":"Nancy Anderson (sample)",  
         "jobtitle":"Logistics Specialist",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$63,500.00",  
         "annualincome":63500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"28c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619847\"",  
         "fullname":"Scott Konersmann (sample)",  
         "jobtitle":"Accounts Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$38,000.00",  
         "annualincome":38000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"2cc364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619849\"",  
         "fullname":"Robert Lyon (sample)",  
         "jobtitle":"Senior Technician",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$78,000.00",  
         "annualincome":78000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"30c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619851\"",  
         "fullname":"Paul Cannon (sample)",  
         "jobtitle":"Ski Instructor",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$68,500.00",  
         "annualincome":68500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"34c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619853\"",  
         "fullname":"Rene Valdes (sample)",  
         "jobtitle":"Data Analyst III",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$86,000.00",  
         "annualincome":86000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"38c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619855\"",  
         "fullname":"Jim Glynn (sample)",  
         "jobtitle":"Senior International Sales Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$81,400.00",  
         "annualincome":81400.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"3cc364b2-bf43-e611-80d5-00155da84802"  
      }  
   ]  
}  
```  
  
 **コンソール出力**  
  
```  
Contacts filtered by fullname containing '(sample)':  
    1) Yvonne McKay (sample), Coffee Master, $45,000.00  
    2) Susanna Stubberod (sample), Senior Purchaser, $52,000.00  
    3) Nancy Anderson (sample), Activities Manager, $55,500.00  
    4) Maria Cambell (sample), Accounts Manager, $31,000.00  
    5) Nancy Anderson (sample), Logistics Specialist, $63,500.00  
    6) Scott Konersmann (sample), Accounts Manager, $38,000.00  
    7) Robert Lyon (sample), Senior Technician, $78,000.00  
    8) Paul Cannon (sample), Ski Instructor, $68,500.00  
    9) Rene Valdes (sample), Data Analyst III, $86,000.00  
    10) Jim Glynn (sample), Senior International Sales Manager, $81,400.00  
  
```  
  
### <a name="common-data-service-query-functions"></a>Common Data Service クエリ関数

Common Data Service クエリ関数は、Common Data Service に関連付けられているクエリを作成するための多数のオプションを提供します。 これらの関数の完全な一覧については、「<xref:Microsoft.Dynamics.CRM.QueryFunctionIndex>」を参照してください。 詳細: [関数を使用してクエリを作成する](use-web-api-functions.md#bkmk_composeQueryWithFunctions)  
  
標準クエリ関数と類似した方法で、これらのクエリ関数を使用します。 大きな違いは、Common Data Service クエリ関数を使用する場合は、パラメーター名を含む関数のフル ネームを使用する必要があります。 たとえば、前回の時間に作成された取引先担当者の一覧を取得するには、<xref href="Microsoft.Dynamics.CRM.LastXHours?text=LastXHours Function" /> を使用してクエリを作成します。  
  
 **HTTP 要求**  
  
```  
GET http://[Organization URI]/api/data/v9.0/contacts?$select=fullname,jobtitle,annualincome&$filter=Microsoft.Dynamics.CRM.LastXHours(PropertyName='createdon',PropertyValue='1') HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Prefer: odata.maxpagesize=10, odata.include-annotations=OData.Community.Display.V1.FormattedValue  
```  
  
 **HTTP 応答**  
  
```  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Preference-Applied: odata.include-annotations="OData.Community.Display.V1.FormattedValue"  
Preference-Applied: odata.maxpagesize=10  
Content-Length: 4284  
  
{  
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#contacts(fullname,jobtitle,annualincome)",  
   "value":[  
      {  
         "@odata.etag":"W/\"619718\"",  
         "fullname":"Yvonne McKay (sample)",  
         "jobtitle":"Coffee Master",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$45,000.00",  
         "annualincome":45000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"15c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619839\"",  
         "fullname":"Susanna Stubberod (sample)",  
         "jobtitle":"Senior Purchaser",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$52,000.00",  
         "annualincome":52000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"1cc364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619841\"",  
         "fullname":"Nancy Anderson (sample)",  
         "jobtitle":"Activities Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$55,500.00",  
         "annualincome":55500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"20c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619843\"",  
         "fullname":"Maria Cambell (sample)",  
         "jobtitle":"Accounts Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$31,000.00",  
         "annualincome":31000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"24c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619845\"",  
         "fullname":"Nancy Anderson (sample)",  
         "jobtitle":"Logistics Specialist",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$63,500.00",  
         "annualincome":63500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"28c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619847\"",  
         "fullname":"Scott Konersmann (sample)",  
         "jobtitle":"Accounts Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$38,000.00",  
         "annualincome":38000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"2cc364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619849\"",  
         "fullname":"Robert Lyon (sample)",  
         "jobtitle":"Senior Technician",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$78,000.00",  
         "annualincome":78000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"30c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619851\"",  
         "fullname":"Paul Cannon (sample)",  
         "jobtitle":"Ski Instructor",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$68,500.00",  
         "annualincome":68500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"34c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619853\"",  
         "fullname":"Rene Valdes (sample)",  
         "jobtitle":"Data Analyst III",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$86,000.00",  
         "annualincome":86000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"38c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619855\"",  
         "fullname":"Jim Glynn (sample)",  
         "jobtitle":"Senior International Sales Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$81,400.00",  
         "annualincome":81400.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"3cc364b2-bf43-e611-80d5-00155da84802"  
      }  
   ]  
}  
```  
  
 **コンソール出力**  
  
```  
Contacts that were created within the last 1hr:  
    1) Yvonne McKay (sample), Coffee Master, $45,000.00  
    2) Susanna Stubberod (sample), Senior Purchaser, $52,000.00  
    3) Nancy Anderson (sample), Activities Manager, $55,500.00  
    4) Maria Cambell (sample), Accounts Manager, $31,000.00  
    5) Nancy Anderson (sample), Logistics Specialist, $63,500.00  
    6) Scott Konersmann (sample), Accounts Manager, $38,000.00  
    7) Robert Lyon (sample), Senior Technician, $78,000.00  
    8) Paul Cannon (sample), Ski Instructor, $68,500.00  
    9) Rene Valdes (sample), Data Analyst III, $86,000.00  
    10) Jim Glynn (sample), Senior International Sales Manager, $81,400.00  
```  
  
<a name="bkmk_operators"></a>
 
## <a name="using-operators"></a>演算子の使用

[標準フィルタ演算子](query-data-web-api.md#bkmk_buildInFilterOperators) (`eq`、`ne`、`gt`、`ge`、`lt`、`le`、`and`、`or`、`not`) を使用して、結果をさらに絞り込みます。 この例では、`(sample)` および `55000` 以上の年収を含む取引先担当者すべての一覧の `fullname` を要求しています。  
  
 **HTTP 要求**  
  
```  
GET http://[Organization URI]/api/data/v9.0/contacts?$select=fullname,jobtitle,annualincome&$filter=contains(fullname,'(sample)')%20and%20annualincome%20gt%2055000 HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Prefer: odata.maxpagesize=10, odata.include-annotations=OData.Community.Display.V1.FormattedValue  
```  
  
 **HTTP 応答**  
  
```  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Preference-Applied: odata.include-annotations="OData.Community.Display.V1.FormattedValue"  
Preference-Applied: odata.maxpagesize=10  
Content-Length: 2629  
  
{  
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#contacts(fullname,jobtitle,annualincome)",  
   "value":[  
      {  
         "@odata.etag":"W/\"619841\"",  
         "fullname":"Nancy Anderson (sample)",  
         "jobtitle":"Activities Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$55,500.00",  
         "annualincome":55500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"20c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619845\"",  
         "fullname":"Nancy Anderson (sample)",  
         "jobtitle":"Logistics Specialist",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$63,500.00",  
         "annualincome":63500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"28c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619849\"",  
         "fullname":"Robert Lyon (sample)",  
         "jobtitle":"Senior Technician",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$78,000.00",  
         "annualincome":78000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"30c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619851\"",  
         "fullname":"Paul Cannon (sample)",  
         "jobtitle":"Ski Instructor",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$68,500.00",  
         "annualincome":68500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"34c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619853\"",  
         "fullname":"Rene Valdes (sample)",  
         "jobtitle":"Data Analyst III",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$86,000.00",  
         "annualincome":86000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"38c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619855\"",  
         "fullname":"Jim Glynn (sample)",  
         "jobtitle":"Senior International Sales Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$81,400.00",  
         "annualincome":81400.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"3cc364b2-bf43-e611-80d5-00155da84802"  
      }  
   ]  
}  
```  
  
 **コンソール出力**  
  
```  
Contacts filtered by fullname and annualincome (<$55,000):  
    1) Nancy Anderson (sample), Activities Manager, $55,500.00  
    2) Nancy Anderson (sample), Logistics Specialist, $63,500.00  
    3) Robert Lyon (sample), Senior Technician, $78,000.00  
    4) Paul Cannon (sample), Ski Instructor, $68,500.00  
    5) Rene Valdes (sample), Data Analyst III, $86,000.00  
    6) Jim Glynn (sample), Senior International Sales Manager, $81,400.00  
```  
  
<a name="bkmk_prededence"></a>
   
## <a name="setting-precedence"></a>優先順位の設定
 
要件が評価される順序を設定するためにかっこを使用します。  
  
 この例では、`(sample)`、`jobtitle` を含み、`senior` または `specialist` で、`annualincome` が `55000` 以上の取引先担当者すべての一覧の `fullname` を要求しています。 必要な結果を取得するために、`jobtitle` フィルターを一緒にグループ化するためにかっこが使用されます。 すべての演算子に同じ優先順位があるために、かっこを省略すると、`or` 演算子は `and` 演算子と同じ優先順位になります。  フィルターは左から右に適用されます。 これらのステートメントがフィルターに表示される順序は結果に影響します。 この例でのクエリは、次のように表示されます: `$filter=contains(fullname,'(sample)') and (contains(jobtitle,'senior') or contains(jobtitle,'specialist')) and annualincome gt 55000`。  
  
 **HTTP 要求**  
  
```  
GET http://[Organization URI]/api/data/v9.0/contacts?$select=fullname,jobtitle,annualincome&$filter=contains(fullname,'(sample)')%20and%20(contains(jobtitle,'senior')%20or%20contains(jobtitle,'specialist'))%20and%20annualincome%20gt%2055000 HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Prefer: odata.maxpagesize=10, odata.include-annotations=OData.Community.Display.V1.FormattedValue  
```  
  
 **HTTP 応答**  
  
```  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Preference-Applied: odata.include-annotations="OData.Community.Display.V1.FormattedValue"  
Preference-Applied: odata.maxpagesize=10  
Content-Length: 1393  
  
{  
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#contacts(fullname,jobtitle,annualincome)",  
   "value":[  
      {  
         "@odata.etag":"W/\"619845\"",  
         "fullname":"Nancy Anderson (sample)",  
         "jobtitle":"Logistics Specialist",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$63,500.00",  
         "annualincome":63500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"28c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619849\"",  
         "fullname":"Robert Lyon (sample)",  
         "jobtitle":"Senior Technician",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$78,000.00",  
         "annualincome":78000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"30c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619855\"",  
         "fullname":"Jim Glynn (sample)",  
         "jobtitle":"Senior International Sales Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$81,400.00",  
         "annualincome":81400.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"3cc364b2-bf43-e611-80d5-00155da84802"  
      }  
   ]  
}  
```  
  
 **コンソール出力**  
  
```  
Contacts filtered by fullname, annualincome and jobtitle (Senior or Specialist):  
    1) Nancy Anderson (sample), Logistics Specialist, $63,500.00  
    2) Robert Lyon (sample), Senior Technician, $78,000.00  
    3) Jim Glynn (sample), Senior International Sales Manager, $81,400.00  
```  
  
<a name="bkmk_orderresults"></a>

## <a name="ordering-results"></a>順番の結果

`$orderby` フィルター オプションの使用により、昇順または降順のいずれかに順序を指定できます。 この例では、`(sample)` を含む `fullname` の取引先担当者すべてをクエリし、`jobtitle` プロパティ値に基づいて昇順でデータを要求し、次に `$orderby=jobtitle asc, annualincome desc` 構文を使用して `annualincome` プロパティ値に基づいてデータを降順で要求します。 詳細: [順番の結果](query-data-web-api.md#bkmk_order)。  
  
 **HTTP 要求**  
  
```  
GET http://[Organization URI]/api/data/v9.0/contacts?$select=fullname,jobtitle,annualincome&$filter=contains(fullname,'(sample)')%20&$orderby=jobtitle%20asc,%20annualincome%20desc HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Prefer: odata.maxpagesize=10, odata.include-annotations=OData.Community.Display.V1.FormattedValue  
```  
  
 **HTTP 応答**  
  
```  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Preference-Applied: odata.include-annotations="OData.Community.Display.V1.FormattedValue"  
Preference-Applied: odata.maxpagesize=10  
Content-Length: 4284  
  
{  
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#contacts(fullname,jobtitle,annualincome)",  
   "value":[  
      {  
         "@odata.etag":"W/\"619847\"",  
         "fullname":"Scott Konersmann (sample)",  
         "jobtitle":"Accounts Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$38,000.00",  
         "annualincome":38000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"2cc364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619843\"",  
         "fullname":"Maria Cambell (sample)",  
         "jobtitle":"Accounts Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$31,000.00",  
         "annualincome":31000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"24c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619841\"",  
         "fullname":"Nancy Anderson (sample)",  
         "jobtitle":"Activities Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$55,500.00",  
         "annualincome":55500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"20c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619718\"",  
         "fullname":"Yvonne McKay (sample)",  
         "jobtitle":"Coffee Master",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$45,000.00",  
         "annualincome":45000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"15c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619853\"",  
         "fullname":"Rene Valdes (sample)",  
         "jobtitle":"Data Analyst III",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$86,000.00",  
         "annualincome":86000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"38c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619845\"",  
         "fullname":"Nancy Anderson (sample)",  
         "jobtitle":"Logistics Specialist",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$63,500.00",  
         "annualincome":63500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"28c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619855\"",  
         "fullname":"Jim Glynn (sample)",  
         "jobtitle":"Senior International Sales Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$81,400.00",  
         "annualincome":81400.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"3cc364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619839\"",  
         "fullname":"Susanna Stubberod (sample)",  
         "jobtitle":"Senior Purchaser",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$52,000.00",  
         "annualincome":52000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"1cc364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619849\"",  
         "fullname":"Robert Lyon (sample)",  
         "jobtitle":"Senior Technician",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$78,000.00",  
         "annualincome":78000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"30c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619851\"",  
         "fullname":"Paul Cannon (sample)",  
         "jobtitle":"Ski Instructor",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$68,500.00",  
         "annualincome":68500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"34c364b2-bf43-e611-80d5-00155da84802"  
      }  
   ]  
}  
```  
  
 **コンソール出力**  
  
```  
Contacts ordered by jobtitle (ascending) and annualincome (descending):  
    1) Scott Konersmann (sample), Accounts Manager, $38,000.00  
    2) Maria Cambell (sample), Accounts Manager, $31,000.00  
    3) Nancy Anderson (sample), Activities Manager, $55,500.00  
    4) Yvonne McKay (sample), Coffee Master, $45,000.00  
    5) Rene Valdes (sample), Data Analyst III, $86,000.00  
    6) Nancy Anderson (sample), Logistics Specialist, $63,500.00  
    7) Jim Glynn (sample), Senior International Sales Manager, $81,400.00  
    8) Susanna Stubberod (sample), Senior Purchaser, $52,000.00  
    9) Robert Lyon (sample), Senior Technician, $78,000.00  
    10) Paul Cannon (sample), Ski Instructor, $68,500.00  
```  
  
<a name="bkmk_parameteralias"></a>

## <a name="parameter-alias"></a>パラメーターのエイリアス

パラメーターのエイリアスを使用して、フィルターのパラメーターをより容易に再利用します。 パラメーターのエイリアスは、`$filter` および `$orderby` オプションで使用されます。 エイリアスが値が割り当てられていない場合は、空白であると判断します。 また、関数を呼び出すとき、パラメーター エイリアスを使用することもできます。 詳細: [Web API 関数の使用](use-web-api-functions.md)、[システム クエリ オプションを持つパラメーター エイリアスの使用](query-data-web-api.md#bkmk_useParameterAliases)。 例えば、受注結果の操作に対して、パラメーターを使用してそのクエリを再度作成し、同じ結果を出力することができます。  
  
 **HTTP 要求**  
  
```  
GET http://[Organization URI]/api/data/v9.0/contacts?$select=fullname,jobtitle,annualincome&$filter=contains(@p1,'(sample)')%20&$orderby=@p2%20asc,%20@p3%20desc&@p1=fullname&@p2=jobtitle&@p3=annualincome HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Prefer: odata.maxpagesize=10, odata.include-annotations=OData.Community.Display.V1.FormattedValue  
```  
  
 **HTTP 応答**  
  
```  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Preference-Applied: odata.include-annotations="OData.Community.Display.V1.FormattedValue"  
Preference-Applied: odata.maxpagesize=10  
Content-Length: 4284  
  
{  
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#contacts(fullname,jobtitle,annualincome)",  
   "value":[  
      {  
         "@odata.etag":"W/\"619847\"",  
         "fullname":"Scott Konersmann (sample)",  
         "jobtitle":"Accounts Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$38,000.00",  
         "annualincome":38000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"2cc364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619843\"",  
         "fullname":"Maria Cambell (sample)",  
         "jobtitle":"Accounts Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$31,000.00",  
         "annualincome":31000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"24c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619841\"",  
         "fullname":"Nancy Anderson (sample)",  
         "jobtitle":"Activities Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$55,500.00",  
         "annualincome":55500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"20c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619718\"",  
         "fullname":"Yvonne McKay (sample)",  
         "jobtitle":"Coffee Master",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$45,000.00",  
         "annualincome":45000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"15c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619853\"",  
         "fullname":"Rene Valdes (sample)",  
         "jobtitle":"Data Analyst III",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$86,000.00",  
         "annualincome":86000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"38c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619845\"",  
         "fullname":"Nancy Anderson (sample)",  
         "jobtitle":"Logistics Specialist",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$63,500.00",  
         "annualincome":63500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"28c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619855\"",  
         "fullname":"Jim Glynn (sample)",  
         "jobtitle":"Senior International Sales Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$81,400.00",  
         "annualincome":81400.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"3cc364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619839\"",  
         "fullname":"Susanna Stubberod (sample)",  
         "jobtitle":"Senior Purchaser",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$52,000.00",  
         "annualincome":52000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"1cc364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619849\"",  
         "fullname":"Robert Lyon (sample)",  
         "jobtitle":"Senior Technician",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$78,000.00",  
         "annualincome":78000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"30c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619851\"",  
         "fullname":"Paul Cannon (sample)",  
         "jobtitle":"Ski Instructor",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$68,500.00",  
         "annualincome":68500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"34c364b2-bf43-e611-80d5-00155da84802"  
      }  
   ]  
}  
```  
  
 **コンソール出力**  
  
```  
Contacts list using parameterized aliases:  
    1) Scott Konersmann (sample), Accounts Manager, $38,000.00  
    2) Maria Cambell (sample), Accounts Manager, $31,000.00  
    3) Nancy Anderson (sample), Activities Manager, $55,500.00  
    4) Yvonne McKay (sample), Coffee Master, $45,000.00  
    5) Rene Valdes (sample), Data Analyst III, $86,000.00  
    6) Nancy Anderson (sample), Logistics Specialist, $63,500.00  
    7) Jim Glynn (sample), Senior International Sales Manager, $81,400.00  
    8) Susanna Stubberod (sample), Senior Purchaser, $52,000.00  
    9) Robert Lyon (sample), Senior Technician, $78,000.00  
    10) Paul Cannon (sample), Ski Instructor, $68,500.00  
```  
  
<a name="bkmk_limitresults"></a>

## <a name="limit-results"></a>結果の制限

必要以上に多くのデータを返すことはパフォーマンスに悪影響を及ぼします。 サーバーは、要求ごとに最大 5000 のエンティティを返します。 `$top` クエリ オプションを使用するか、または結果のヘッダーに `odata.maxpagesize` を追加することにより返される結果数を制限します。 `$top` クエリ オプションは、結果セットから上位のエンティティ数値のみを返し、残りは無視します。 `odata.maxpagesize` 要求ヘッダーは、次のページの結果を取得するために、`@odata.nextLink` プロパティを使用してページごとに返されるエンティティ数を指定します。 `odata.maxpagesize` に関する詳細については、「[改ページ](#bkmk_filterPagination)」のセクション、および「[返されるエンティティ数の制限](query-data-web-api.md#bkmk_limits)」も参照してください。  
  
<a name="bkmk_topResults"></a>
 
### <a name="top-results"></a>上位の結果

`$top` クエリ オプションを適応して、`(sample)` が含まれている `fullname` の最初の 5 つの取引先担当者に対して基本的なクエリ操作を行うように制限できます。 この場合、この要求は、実際には少なくとも 10 件の結果が生成されますが、最初の 5 つのエントリのみが応答として返されます。  
  
 **HTTP 要求**  
  
```  
GET http://[Organization URI]/api/data/v9.0/contacts?$select=fullname,jobtitle,annualincome&$filter=contains(fullname,'(sample)')&$top=5 HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Prefer: odata.maxpagesize=10, odata.include-annotations=OData.Community.Display.V1.FormattedValue  
```  
  
 **HTTP 応答**  
  
```  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Preference-Applied: odata.include-annotations="OData.Community.Display.V1.FormattedValue"  
Content-Length: 2209  
  
{  
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#contacts(fullname,jobtitle,annualincome)",  
   "value":[  
      {  
         "@odata.etag":"W/\"619718\"",  
         "fullname":"Yvonne McKay (sample)",  
         "jobtitle":"Coffee Master",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$45,000.00",  
         "annualincome":45000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"15c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619839\"",  
         "fullname":"Susanna Stubberod (sample)",  
         "jobtitle":"Senior Purchaser",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$52,000.00",  
         "annualincome":52000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"1cc364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619841\"",  
         "fullname":"Nancy Anderson (sample)",  
         "jobtitle":"Activities Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$55,500.00",  
         "annualincome":55500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"20c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619843\"",  
         "fullname":"Maria Cambell (sample)",  
         "jobtitle":"Accounts Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$31,000.00",  
         "annualincome":31000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"24c364b2-bf43-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"619845\"",  
         "fullname":"Nancy Anderson (sample)",  
         "jobtitle":"Logistics Specialist",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$63,500.00",  
         "annualincome":63500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"28c364b2-bf43-e611-80d5-00155da84802"  
      }  
   ]  
}  
```  
  
 **コンソール出力**  
  
```  
Contacts top 5 results:  
    1) Yvonne McKay (sample), Coffee Master, $45,000.00  
    2) Susanna Stubberod (sample), Senior Purchaser, $52,000.00  
    3) Nancy Anderson (sample), Activities Manager, $55,500.00  
    4) Maria Cambell (sample), Accounts Manager, $31,000.00  
    5) Nancy Anderson (sample), Logistics Specialist, $63,500.00  
  
```  
  
<a name="bkmk_resultCount"></a>

### <a name="result-count"></a>結果数

コレクション値プロパティに指定された数またはフィルターに一致するエンティティ数のレコード数のみを取得できます。 カウントを取得すると、結果として可能なエンティティ数が分かります。 ただし、Common Data Service サーバーは、5000 以上の結果がある場合でも、最大 5000 のカウントを返します。 この例では、`Senior` または `Manager` のいずれかを含む `jobtitle` でフィルターを作成しました。また結果として、`$count` も要求しました。 応答には、`@odata.count` プロパティのカウントとクエリの結果が含まれています。 詳細: [エンティティ数の取得](query-data-web-api.md#bkmk_retrieveCount)。  
  
 **HTTP 要求**  
  
```  
GET http://[Organization URI]/api/data/v9.0/contacts?$select=fullname,jobtitle,annualincome&$filter=contains(jobtitle,'senior')%20or%20contains(jobtitle,%20'manager')&$count=true HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Prefer: odata.maxpagesize=10, odata.include-annotations=OData.Community.Display.V1.FormattedValue  
```  
  
 **HTTP 応答**  
  
```  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Preference-Applied: odata.include-annotations="OData.Community.Display.V1.FormattedValue"  
Preference-Applied: odata.maxpagesize=10  
Content-Length: 2654  
  
{  
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#contacts(fullname,jobtitle,annualincome)",  
   "@odata.count":6,  
   "value":[  
      {  
         "@odata.etag":"W/\"620258\"",  
         "fullname":"Susanna Stubberod (sample)",  
         "jobtitle":"Senior Purchaser",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$52,000.00",  
         "annualincome":52000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"bf48fdee-c143-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620260\"",  
         "fullname":"Nancy Anderson (sample)",  
         "jobtitle":"Activities Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$55,500.00",  
         "annualincome":55500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"c348fdee-c143-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620262\"",  
         "fullname":"Maria Cambell (sample)",  
         "jobtitle":"Accounts Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$31,000.00",  
         "annualincome":31000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"c748fdee-c143-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620266\"",  
         "fullname":"Scott Konersmann (sample)",  
         "jobtitle":"Accounts Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$38,000.00",  
         "annualincome":38000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"cf48fdee-c143-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620268\"",  
         "fullname":"Robert Lyon (sample)",  
         "jobtitle":"Senior Technician",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$78,000.00",  
         "annualincome":78000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"d348fdee-c143-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620274\"",  
         "fullname":"Jim Glynn (sample)",  
         "jobtitle":"Senior International Sales Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$81,400.00",  
         "annualincome":81400.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"df48fdee-c143-e611-80d5-00155da84802"  
      }  
   ]  
}  
```  
  
 **コンソール出力**  
  
```  
6 contacts have either 'Manager' or 'Senior' designation in their jobtitle.  
Manager or Senior:  
    1) Susanna Stubberod (sample), Senior Purchaser, $52,000.00  
    2) Nancy Anderson (sample), Activities Manager, $55,500.00  
    3) Maria Cambell (sample), Accounts Manager, $31,000.00  
    4) Scott Konersmann (sample), Accounts Manager, $38,000.00  
    5) Robert Lyon (sample), Senior Technician, $78,000.00  
    6) Jim Glynn (sample), Senior International Sales Manager, $81,400.00  
  
```  
  
<a name="bkmk_filterPagination"></a>

### <a name="pagination"></a>改ページ

大量のエンティティを返す連続したクエリの結果を取得する場合、`odata.maxpagesize` を `$top` の代わりに使用してください。 詳細: [ページに戻すエンティティ数の指定](query-data-web-api.md#bkmk_specifyNumber)。  
  
この例では、`$count` を要求して、`odata.maxpagesize` を `4` に設定します。 このフィルターでは、10 の取引先担当者が一致しますが、1 度に 4 つを取得します。 カウントおよび最大ページサイズを使用して合計ページ数も確認します。 この要求では最初のページの結果が返されます。  
  
 **HTTP 要求**  
  
```  
GET http://[Organization URI]/api/data/v9.0/contacts?$select=fullname,jobtitle,annualincome&$filter=contains(fullname,'(sample)')&$count=true HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Prefer: odata.maxpagesize=4, odata.include-annotations=OData.Community.Display.V1.FormattedValue  
```  
  
 **HTTP 応答**  
  
```  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Preference-Applied: odata.include-annotations="OData.Community.Display.V1.FormattedValue"  
Preference-Applied: odata.maxpagesize=4  
Content-Length: 2294  
  
{  
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#contacts(fullname,jobtitle,annualincome)",  
   "@odata.count":10,  
   "value":[  
      {  
         "@odata.etag":"W/\"620138\"",  
         "fullname":"Yvonne McKay (sample)",  
         "jobtitle":"Coffee Master",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$45,000.00",  
         "annualincome":45000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"b848fdee-c143-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620258\"",  
         "fullname":"Susanna Stubberod (sample)",  
         "jobtitle":"Senior Purchaser",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$52,000.00",  
         "annualincome":52000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"bf48fdee-c143-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620260\"",  
         "fullname":"Nancy Anderson (sample)",  
         "jobtitle":"Activities Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$55,500.00",  
         "annualincome":55500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"c348fdee-c143-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620262\"",  
         "fullname":"Maria Cambell (sample)",  
         "jobtitle":"Accounts Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$31,000.00",  
         "annualincome":31000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"c748fdee-c143-e611-80d5-00155da84802"  
      }  
   ],  
   "@odata.nextLink":"http://[Organization URI]/api/data/v9.0/contacts?$select=fullname,jobtitle,annualincome&$filter=contains(fullname,'(sample)')&$count=true&$skiptoken=%3Ccookie%20pagenumber=%222%22%20pagingcookie=%22%253ccookie%2520page%253d%25221%2522%253e%253ccontactid%2520last%253d%2522%257bC748FDEE-C143-E611-80D5-00155DA84802%257d%2522%2520first%253d%2522%257bB848FDEE-C143-E611-80D5-00155DA84802%257d%2522%2520%252f%253e%253c%252fcookie%253e%22%20istracking=%22False%22%20/%3E"  
}  
```  
  
 **コンソール出力**  
  
```  
Contacts total: 10  Contacts per page: 4.  
Page 1 of 3:  
    1) Yvonne McKay (sample), Coffee Master, $45,000.00  
    2) Susanna Stubberod (sample), Senior Purchaser, $52,000.00  
    3) Nancy Anderson (sample), Activities Manager, $55,500.00  
    4) Maria Cambell (sample), Accounts Manager, $31,000.00  
  
```  
  
 2 ページ目を取得するには、`@odata.nextLink` プロパティの値で、`GET` 要求を使用します。  
  
 **HTTP 要求**  
  
```  
GET http://[Organization URI]/api/data/v9.0/contacts?$select=fullname,jobtitle,annualincome&$filter=contains(fullname,'(sample)')&$count=true&$skiptoken=%3Ccookie%20pagenumber=%222%22%20pagingcookie=%22%253ccookie%2520page%253d%25221%2522%253e%253ccontactid%2520last%253d%2522%257bC748FDEE-C143-E611-80D5-00155DA84802%257d%2522%2520first%253d%2522%257bB848FDEE-C143-E611-80D5-00155DA84802%257d%2522%2520%252f%253e%253c%252fcookie%253e%22%20istracking=%22False%22%20/%3E HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Prefer: odata.maxpagesize=4, odata.include-annotations=OData.Community.Display.V1.FormattedValue  
```  
  
 **HTTP 応答**  
  
```  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Preference-Applied: odata.include-annotations="OData.Community.Display.V1.FormattedValue"  
Preference-Applied: odata.maxpagesize=4  
Content-Length: 2294  
  
{  
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#contacts(fullname,jobtitle,annualincome)",  
   "@odata.count":10,  
   "value":[  
      {  
         "@odata.etag":"W/\"620264\"",  
         "fullname":"Nancy Anderson (sample)",  
         "jobtitle":"Logistics Specialist",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$63,500.00",  
         "annualincome":63500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"cb48fdee-c143-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620266\"",  
         "fullname":"Scott Konersmann (sample)",  
         "jobtitle":"Accounts Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$38,000.00",  
         "annualincome":38000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"cf48fdee-c143-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620268\"",  
         "fullname":"Robert Lyon (sample)",  
         "jobtitle":"Senior Technician",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$78,000.00",  
         "annualincome":78000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"d348fdee-c143-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620270\"",  
         "fullname":"Paul Cannon (sample)",  
         "jobtitle":"Ski Instructor",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$68,500.00",  
         "annualincome":68500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"d748fdee-c143-e611-80d5-00155da84802"  
      }  
   ],  
   "@odata.nextLink":"http://[Organization URI]/api/data/v9.0/contacts?$select=fullname,jobtitle,annualincome&$filter=contains(fullname,'(sample)')&$count=true&$skiptoken=%3Ccookie%20pagenumber=%223%22%20pagingcookie=%22%253ccookie%2520page%253d%25222%2522%253e%253ccontactid%2520last%253d%2522%257bD748FDEE-C143-E611-80D5-00155DA84802%257d%2522%2520first%253d%2522%257bCB48FDEE-C143-E611-80D5-00155DA84802%257d%2522%2520%252f%253e%253c%252fcookie%253e%22%20istracking=%22False%22%20/%3E"  
}  
```  
  
 **コンソール出力**  
  
```  
Page 2 of 3:  
    1) Nancy Anderson (sample), Logistics Specialist, $63,500.00  
    2) Scott Konersmann (sample), Accounts Manager, $38,000.00  
    3) Robert Lyon (sample), Senior Technician, $78,000.00  
    4) Paul Cannon (sample), Ski Instructor, $68,500.00  
```  
  
<a name="bkmk_expandresults"></a>

## <a name="expanding-results"></a>結果の展開

関連付けられたエンティティの情報を取得するには、ナビゲーション プロパティの `$expand` クエリ オプションを使用します。 詳細: [ナビゲーション プロパティの拡張による関連エンティティの取得](query-data-web-api.md#bkmk_expandRelated)。  
  
### <a name="expand-on-single-valued-navigation-property"></a>単一値ナビゲーション プロパティの展開

単一値ナビゲーションのプロパティは多対一の関連付けを表します。 サンプル データでは、取引先企業は、`primarycontactid` 属性を介して取引先担当者と関連付けがあります。 この関連付けでは、取引先企業には 1 人の取引先責任者のみです。  <xref href="Microsoft.Dynamics.CRM.account?text=account EntityType" /> を使用して、取引先企業および取引先責任者の詳細な情報を取得するクエリを作成します。  
  
 **HTTP 要求**  
  
```  
GET http://[Organization URI]/api/data/v9.0/accounts(b2546951-c543-e611-80d5-00155da84802)?$select=name&$expand=primarycontactid($select=fullname,jobtitle,annualincome) HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Prefer: odata.maxpagesize=10, odata.include-annotations=OData.Community.Display.V1.FormattedValue  
```  
  
 **HTTP 応答**  
  
```  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Preference-Applied: odata.include-annotations="OData.Community.Display.V1.FormattedValue"  
Preference-Applied: odata.maxpagesize=10  
Content-Length: 700  
  
{  
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#accounts(name,primarycontactid,primarycontactid(fullname,jobtitle,annualincome))/$entity",  
   "@odata.etag":"W/\"620641\"",  
   "name":"Contoso, Ltd. (sample)",  
   "accountid":"b2546951-c543-e611-80d5-00155da84802",  
   "primarycontactid":{  
      "@odata.etag":"W/\"620534\"",  
      "fullname":"Yvonne McKay (sample)",  
      "jobtitle":"Coffee Master",  
      "annualincome@OData.Community.Display.V1.FormattedValue":"$45,000.00",  
      "annualincome":45000.0000,  
      "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
      "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
      "contactid":"b3546951-c543-e611-80d5-00155da84802"  
   }  
}  
```  
  
 **コンソール出力**  
  
```  
Account 'Contoso, Ltd. (sample)' has the following primary contact person:  
    Fullname: 'Yvonne McKay (sample)'   
    Jobtitle: 'Coffee Master'   
    Annualincome: '45000'  
```  
  
### <a name="expand-on-partner-property"></a>パートナー プロパティの展開

各ナビゲーション プロパティには対応する "パートナー" プロパティがあります。 この関連付けが構成されると、関連付けを通じて情報を取得できます。 使用する属性は、クエリに対する基本的なエンティティによって異なります。 たとえば、上記の操作では、<xref href="Microsoft.Dynamics.CRM.account?text=account EntityType" /> に対してクエリを作成し、取引先責任者に関する詳細な情報の取得を試みました。 `primarycontactid` 属性を介して、それを行いました。 [単一値ナビゲーション プロパティ](/dynamics365/customer-engagement/web-api/account?view=dynamics-ce-odata-9#Single-valued_navigation_properties) セクションで、<xref href="Microsoft.Dynamics.CRM.account?text=account EntityType" /> を検索する場合、`primarycontactid` に相当するパートナー プロパティは、<xref href="Microsoft.Dynamics.CRM.contact?text=contact EntityType" /> にある `account_primary_contact` コレクション値ナビゲーション プロパティです。  
  
取引先担当者に対してクエリを書くことにより、`account_primary_contact` 属性を展開して、この取引先担当者が取引先責任者であるという取引先企業に関する情報を取得できます。 サンプル データでは、`Yvonne McKay (sample)` が 1 つの取引先企業に対する取引先責任者です。 ただし、彼女は取引先責任者として他の取引先企業に割り当てられる可能性があります。 `account_primary_contact` プロパティは多対一の関連があるために、結果は取引先企業のエンティティの配列として返されます。  
  
 **HTTP 要求**  
  
```  
GET http://[Organization URI]/api/data/v9.0/contacts(b3546951-c543-e611-80d5-00155da84802)?$select=fullname,jobtitle,annualincome&$expand=account_primary_contact($select=name) HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Prefer: odata.maxpagesize=10, odata.include-annotations=OData.Community.Display.V1.FormattedValue  
```  
  
 **HTTP 応答**  
  
```  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Preference-Applied: odata.include-annotations="OData.Community.Display.V1.FormattedValue"  
Preference-Applied: odata.maxpagesize=10  
Content-Length: 737  
  
{  
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#contacts(fullname,jobtitle,annualincome,account_primary_contact,account_primary_contact(name))/$entity",  
   "@odata.etag":"W/\"620534\"",  
   "fullname":"Yvonne McKay (sample)",  
   "jobtitle":"Coffee Master",  
   "annualincome@OData.Community.Display.V1.FormattedValue":"$45,000.00",  
   "annualincome":45000.0000,  
   "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
   "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
   "contactid":"b3546951-c543-e611-80d5-00155da84802",  
   "account_primary_contact":[  
      {  
         "@odata.etag":"W/\"620919\"",  
         "name":"Contoso, Ltd. (sample)",  
         "accountid":"b2546951-c543-e611-80d5-00155da84802"  
      }  
   ]  
}  
```  
  
 **コンソール出力**  
  
```  
Contact 'Yvonne McKay (sample)' is the primary contact for the following accounts:  
    1) Contoso, Ltd. (sample)  
```  
  
### <a name="expand-on-collection-valued-navigation-property"></a>コレクション値ナビゲーション プロパティの展開

コレクション値のナビゲーション プロパティは 1 対多または多対多の関連付けをサポートします。 たとえば、サンプル データでは、取引先企業は、`contact_customer_accounts` 属性を介して多くの取引先担当者と関連付けがあります。  
  
<xref href="Microsoft.Dynamics.CRM.account?text=account EntityType" /> を使用して、取引先企業および取引先担当者の詳細な情報を取得するクエリを作成します。 このケースでは、`Contoso, Ltd. (sample)` は、`contact_customer_accounts` コレクション値のナビゲーション プロパティを介して、9 つの他の取引先担当者と関連付けられています。  
  
 **HTTP 要求**  
  
```  
GET http://[Organization URI]/api/data/v9.0/accounts(86546951-c543-e611-80d5-00155da84802)?$select=name&$expand=contact_customer_accounts($select=fullname,jobtitle,annualincome) HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Prefer: odata.maxpagesize=10, odata.include-annotations=OData.Community.Display.V1.FormattedValue  
```  
  
 **HTTP 応答**  
  
```  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Preference-Applied: odata.include-annotations="OData.Community.Display.V1.FormattedValue"  
Preference-Applied: odata.maxpagesize=10  
Content-Length: 4073  
  
{  
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#accounts(name,contact_customer_accounts,contact_customer_accounts(fullname,jobtitle,annualincome))/$entity",  
   "@odata.etag":"W/\"620921\"",  
   "name":"Contoso, Ltd. (sample)",  
   "accountid":"86546951-c543-e611-80d5-00155da84802",  
   "contact_customer_accounts":[  
      {  
         "@odata.etag":"W/\"620847\"",  
         "fullname":"Susanna Stubberod (sample)",  
         "jobtitle":"Senior Purchaser",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$52,000.00",  
         "annualincome":52000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"8e546951-c543-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620849\"",  
         "fullname":"Nancy Anderson (sample)",  
         "jobtitle":"Activities Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$55,500.00",  
         "annualincome":55500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"92546951-c543-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620851\"",  
         "fullname":"Maria Cambell (sample)",  
         "jobtitle":"Accounts Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$31,000.00",  
         "annualincome":31000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"96546951-c543-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620853\"",  
         "fullname":"Nancy Anderson (sample)",  
         "jobtitle":"Logistics Specialist",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$63,500.00",  
         "annualincome":63500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"9a546951-c543-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620855\"",  
         "fullname":"Scott Konersmann (sample)",  
         "jobtitle":"Accounts Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$38,000.00",  
         "annualincome":38000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"9e546951-c543-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620857\"",  
         "fullname":"Robert Lyon (sample)",  
         "jobtitle":"Senior Technician",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$78,000.00",  
         "annualincome":78000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"a2546951-c543-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620859\"",  
         "fullname":"Paul Cannon (sample)",  
         "jobtitle":"Ski Instructor",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$68,500.00",  
         "annualincome":68500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"a6546951-c543-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620861\"",  
         "fullname":"Rene Valdes (sample)",  
         "jobtitle":"Data Analyst III",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$86,000.00",  
         "annualincome":86000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"aa546951-c543-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620863\"",  
         "fullname":"Jim Glynn (sample)",  
         "jobtitle":"Senior International Sales Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$81,400.00",  
         "annualincome":81400.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"ae546951-c543-e611-80d5-00155da84802"  
      }  
   ]  
}  
```  
  
 **コンソール出力**  
  
```  
Account 'Contoso, Ltd. (sample)' has the following contact customers:  
    1) Susanna Stubberod (sample), Senior Purchaser, $52,000.00  
    2) Nancy Anderson (sample), Activities Manager, $55,500.00  
    3) Maria Cambell (sample), Accounts Manager, $31,000.00  
    4) Nancy Anderson (sample), Logistics Specialist, $63,500.00  
    5) Scott Konersmann (sample), Accounts Manager, $38,000.00  
    6) Robert Lyon (sample), Senior Technician, $78,000.00  
    7) Paul Cannon (sample), Ski Instructor, $68,500.00  
    8) Rene Valdes (sample), Data Analyst III, $86,000.00  
    9) Jim Glynn (sample), Senior International Sales Manager, $81,400.00  
```  
  
### <a name="expand-on-multiple-navigation-properties"></a>複数のナビゲーション プロパティを展開する

クエリが必要な数だけ、ナビゲーション プロパティを拡張できます。 しかし、`$expand` オプションは 1 レベル ディープだけ進むことができます。  
  
この例は、`primarycontactid`、`contact_customer_accounts`、および <xref href="Microsoft.Dynamics.CRM.account?text=account EntityType" /> の `Account_Tasks` ナビゲーション プロパティを拡張します。  このクエリは、取引先企業と、2 つのコレクション (取引先担当者のコレクションとタスクのコレクション) に関する情報を含む応答を返します。 サンプル コードでは、これらのコレクションを別々に処理します。  
  
 **HTTP 要求**  
  
```  
GET http://[Organization URI]/api/data/v9.0/accounts(86546951-c543-e611-80d5-00155da84802)?$select=name&$expand=primarycontactid($select=fullname,jobtitle,annualincome),contact_customer_accounts($select=fullname,jobtitle,annualincome),Account_Tasks($select=subject,description) HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Prefer: odata.maxpagesize=10, odata.include-annotations=OData.Community.Display.V1.FormattedValue  
```  
  
 **HTTP 応答**  
  
```  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Preference-Applied: odata.include-annotations="OData.Community.Display.V1.FormattedValue"  
Preference-Applied: odata.maxpagesize=10  
Content-Length: 5093  
  
{  
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#accounts(name,primarycontactid,contact_customer_accounts,Account_Tasks,primarycontactid(fullname,jobtitle,annualincome),contact_customer_accounts(fullname,jobtitle,annualincome),Account_Tasks(subject,description))/$entity",  
   "@odata.etag":"W/\"620921\"",  
   "name":"Contoso, Ltd. (sample)",  
   "accountid":"86546951-c543-e611-80d5-00155da84802",  
   "primarycontactid":{  
      "@odata.etag":"W/\"620726\"",  
      "fullname":"Yvonne McKay (sample)",  
      "jobtitle":"Coffee Master",  
      "annualincome@OData.Community.Display.V1.FormattedValue":"$45,000.00",  
      "annualincome":45000.0000,  
      "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
      "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
      "contactid":"87546951-c543-e611-80d5-00155da84802"  
   },  
   "contact_customer_accounts":[  
      {  
         "@odata.etag":"W/\"620847\"",  
         "fullname":"Susanna Stubberod (sample)",  
         "jobtitle":"Senior Purchaser",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$52,000.00",  
         "annualincome":52000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"8e546951-c543-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620849\"",  
         "fullname":"Nancy Anderson (sample)",  
         "jobtitle":"Activities Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$55,500.00",  
         "annualincome":55500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"92546951-c543-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620851\"",  
         "fullname":"Maria Cambell (sample)",  
         "jobtitle":"Accounts Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$31,000.00",  
         "annualincome":31000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"96546951-c543-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620853\"",  
         "fullname":"Nancy Anderson (sample)",  
         "jobtitle":"Logistics Specialist",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$63,500.00",  
         "annualincome":63500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"9a546951-c543-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620855\"",  
         "fullname":"Scott Konersmann (sample)",  
         "jobtitle":"Accounts Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$38,000.00",  
         "annualincome":38000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"9e546951-c543-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620857\"",  
         "fullname":"Robert Lyon (sample)",  
         "jobtitle":"Senior Technician",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$78,000.00",  
         "annualincome":78000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"a2546951-c543-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620859\"",  
         "fullname":"Paul Cannon (sample)",  
         "jobtitle":"Ski Instructor",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$68,500.00",  
         "annualincome":68500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"a6546951-c543-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620861\"",  
         "fullname":"Rene Valdes (sample)",  
         "jobtitle":"Data Analyst III",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$86,000.00",  
         "annualincome":86000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"aa546951-c543-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620863\"",  
         "fullname":"Jim Glynn (sample)",  
         "jobtitle":"Senior International Sales Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$81,400.00",  
         "annualincome":81400.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"ae546951-c543-e611-80d5-00155da84802"  
      }  
   ],  
   "Account_Tasks":[  
      {  
         "@odata.etag":"W/\"620840\"",  
         "subject":"Task 1",  
         "description":"Task 1 description",  
         "activityid":"8b546951-c543-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620842\"",  
         "subject":"Task 2",  
         "description":"Task 2 description",  
         "activityid":"8c546951-c543-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"620844\"",  
         "subject":"Task 3",  
         "description":"Task 3 description",  
         "activityid":"8d546951-c543-e611-80d5-00155da84802"  
      }  
   ]  
}  
```  
  
 **コンソール出力**  
  
```  
-- Expanding multiple property types in one request --   
Account 'Contoso, Ltd. (sample)' has the following primary contact person:  
    Fullname: 'Yvonne McKay (sample)'   
    Jobtitle: 'Coffee Master'   
    Annualincome: '45000'  
Account 'Contoso, Ltd. (sample)' has the following related contacts:  
    1) Susanna Stubberod (sample), Senior Purchaser, $52,000.00  
    2) Nancy Anderson (sample), Activities Manager, $55,500.00  
    3) Maria Cambell (sample), Accounts Manager, $31,000.00  
    4) Nancy Anderson (sample), Logistics Specialist, $63,500.00  
    5) Scott Konersmann (sample), Accounts Manager, $38,000.00  
    6) Robert Lyon (sample), Senior Technician, $78,000.00  
    7) Paul Cannon (sample), Ski Instructor, $68,500.00  
    8) Rene Valdes (sample), Data Analyst III, $86,000.00  
    9) Jim Glynn (sample), Senior International Sales Manager, $81,400.00  
Account 'Contoso, Ltd. (sample)' has the following tasks:  
    1) Task 1, Task 1 description  
    2) Task 2, Task 2 description  
    3) Task 3, Task 3 description  
```  
  
<a name="bkmk_fetchxml"></a>

## <a name="fetchxml-queries"></a>FetchXML クエリ

<!-- TODO:
Besides query filter operations, the Web API also supports FetchXML queries. FetchXml provides an alternative way to define queries and additional options to perform aggregations. More information:[Build queries with FetchXML](../org-service/build-queries-fetchxml.md)   -->
  
<!-- TODO: To use fetch xml you must compose a string representing the query. Make sure the query string conforms to the [FetchXML schema](../org-service/fetchxml-schema.md). Before you include the string in the URL you must URL encode the string.   -->
  
 `$select`、`$filter`、および `$orderby` などが通常定義するクエリ オプションはすべて XML 内で定義されるようになりました。 この操作では、`fullname` が `(sample)` に一致する取引先担当者をすべてクエリし、結果を `fullname` の降順で並び替えます。 これがこのクエリ用 XML です。  
  
```xml  
<fetch mapping="logical" output-format="xml-platform" version="1.0" distinct="false">  
  <entity name="contact">  
    <attribute name="fullname" />  
    <attribute name="jobtitle" />  
    <attribute name="annualincome" />  
    <order descending="true"  
           attribute="fullname" />  
    <filter type="and">  
      <condition value="%(sample)%"  
                 attribute="fullname"  
                 operator="like" />  
    </filter>  
  </entity>  
</fetch>  
```  
  
 **HTTP 要求**  
  
 要求クエリ文字列はエンコードされたフォームでサーバーに送信されます。 エンコードされたヘッダーはこのようになります。  
  
```  
GET http://[Organization URI]/api/data/v9.0/contacts?fetchXml=%253Cfetch%2520mapping%253D%2522logical%2522%2520output-format%253D%2522xml-platform%2522%2520version%253D%25221.0%2522%2520distinct%253D%2522false%2522%253E%2520%2520%2520%253Centity%2520name%253D%2522contact%2522%253E%2520%2520%2520%2520%2520%253Cattribute%2520name%253D%2522fullname%2522%2520%252F%253E%2520%2520%2520%2520%2520%253Cattribute%2520name%253D%2522jobtitle%2522%2520%252F%253E%2520%2520%2520%2520%2520%253Cattribute%2520name%253D%2522annualincome%2522%2520%252F%253E%2520%2520%2520%2520%2520%253Corder%2520descending%253D%2522true%2522%2520attribute%253D%2522fullname%2522%2520%252F%253E%2520%2520%2520%2520%2520%253Cfilter%2520type%253D%2522and%2522%253E%2520%2520%2520%2520%2520%2520%2520%253Ccondition%2520value%253D%2522%2525(sample)%2525%2522%2520attribute%253D%2522fullname%2522%2520operator%253D%2522like%2522%2520%252F%253E%2520%2520%2520%2520%2520%253C%252Ffilter%253E%2520%2520%2520%253C%252Fentity%253E%2520%253C%252Ffetch%253E%2520 HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Prefer: odata.maxpagesize=10, odata.include-annotations=OData.Community.Display.V1.FormattedValue  
```  
  
 **HTTP 応答**  
  
```  
HTTP/1.1 200 OK  
OData-Version: 4.0  
Preference-Applied: odata.include-annotations="OData.Community.Display.V1.FormattedValue"  
Content-Length: 4345  
  
{  
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#contacts(fullname,jobtitle,annualincome,_transactioncurrencyid_value,transactioncurrencyid,contactid)",  
   "value":[  
      {  
         "@odata.etag":"W/\"621502\"",  
         "fullname":"Yvonne McKay (sample)",  
         "jobtitle":"Coffee Master",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$45,000.00",  
         "annualincome":45000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"9255b257-c843-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"621627\"",  
         "fullname":"Susanna Stubberod (sample)",  
         "jobtitle":"Senior Purchaser",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$52,000.00",  
         "annualincome":52000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"9955b257-c843-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"621635\"",  
         "fullname":"Scott Konersmann (sample)",  
         "jobtitle":"Accounts Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$38,000.00",  
         "annualincome":38000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"a955b257-c843-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"621637\"",  
         "fullname":"Robert Lyon (sample)",  
         "jobtitle":"Senior Technician",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$78,000.00",  
         "annualincome":78000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"ad55b257-c843-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"621641\"",  
         "fullname":"Rene Valdes (sample)",  
         "jobtitle":"Data Analyst III",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$86,000.00",  
         "annualincome":86000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"b555b257-c843-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"621639\"",  
         "fullname":"Paul Cannon (sample)",  
         "jobtitle":"Ski Instructor",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$68,500.00",  
         "annualincome":68500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"b155b257-c843-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"621629\"",  
         "fullname":"Nancy Anderson (sample)",  
         "jobtitle":"Activities Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$55,500.00",  
         "annualincome":55500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"9d55b257-c843-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"621633\"",  
         "fullname":"Nancy Anderson (sample)",  
         "jobtitle":"Logistics Specialist",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$63,500.00",  
         "annualincome":63500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"a555b257-c843-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"621631\"",  
         "fullname":"Maria Cambell (sample)",  
         "jobtitle":"Accounts Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$31,000.00",  
         "annualincome":31000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"a155b257-c843-e611-80d5-00155da84802"  
      },  
      {  
         "@odata.etag":"W/\"621643\"",  
         "fullname":"Jim Glynn (sample)",  
         "jobtitle":"Senior International Sales Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$81,400.00",  
         "annualincome":81400.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"b955b257-c843-e611-80d5-00155da84802"  
      }  
   ]  
}  
```  
  
 **コンソール出力**  
  
```  
Contacts Fetched by fullname containing '(sample)':  
    1) Yvonne McKay (sample), Coffee Master, $45,000.00  
    2) Susanna Stubberod (sample), Senior Purchaser, $52,000.00  
    3) Scott Konersmann (sample), Accounts Manager, $38,000.00  
    4) Robert Lyon (sample), Senior Technician, $78,000.00  
    5) Rene Valdes (sample), Data Analyst III, $86,000.00  
    6) Paul Cannon (sample), Ski Instructor, $68,500.00  
    7) Nancy Anderson (sample), Activities Manager, $55,500.00  
    8) Nancy Anderson (sample), Logistics Specialist, $63,500.00  
    9) Maria Cambell (sample), Accounts Manager, $31,000.00  
    10) Jim Glynn (sample), Senior International Sales Manager, $81,400.00  
```  
  
### <a name="fetchxml-pagination"></a>FetchXML 改ページ

FetchXML がページングを扱う方法は、クエリ フィルターがページングを扱う方法とは異なります。 FetchXML では、ページごとに表示する結果数を示す `count` 属性を指定します。 同じ要求で、`page` 属性を使用して、必要なページ数を指定します。 この操作では、前の FetchXML 例から、3 ページ目を要求します。 サンプル データに基づくと、結果には 10 人の取引先担当者があることが必要です。 1 ページにつき 4 つのエンティティが表示されるように各ページを分けたので、3 ページあるはずです。 3 ページ目には、2 つのエンティティのみを含める必要があります。 次に 4 ページ目を要求した場合、システムは 0 の結果を返します。  
  
```xml  
<fetch mapping="logical"  
       output-format="xml-platform"  
       version="1.0"  
       distinct="false"  
       page="3"  
       count="4">  
  <entity name="contact">  
    <attribute name="fullname" />  
    <attribute name="jobtitle" />  
    <attribute name="annualincome" />  
    <order descending="true"  
           attribute="fullname" />  
    <filter type="and">  
      <condition value="%(sample)%"  
                 attribute="fullname"  
                 operator="like" />  
    </filter>  
  </entity>  
</fetch>  
```  
  
 **HTTP 要求**  
  
 要求クエリ文字列はエンコードされたフォームでサーバーに送信されます。 エンコードされたヘッダーはこのようになります。  
  
```  
GET http://[Organization URI]/api/data/v9.0/contacts?fetchXml=%253Cfetch%2520mapping%253D%2522logical%2522%2520output-format%253D%2522xml-platform%2522%2520version%253D%25221.0%2522%2520distinct%253D%2522false%2522%2520page%253D%25223%2522%2520count%253D%25224%2522%253E%2520%2520%2520%253Centity%2520name%253D%2522contact%2522%253E%2520%2520%2520%2520%2520%253Cattribute%2520name%253D%2522fullname%2522%2520%252F%253E%2520%2520%2520%2520%2520%253Cattribute%2520name%253D%2522jobtitle%2522%2520%252F%253E%2520%2520%2520%2520%2520%253Cattribute%2520name%253D%2522annualincome%2522%2520%252F%253E%2520%2520%2520%2520%2520%253Corder%2520descending%253D%2522true%2522%2520attribute%253D%2522fullname%2522%2520%252F%253E%2520%2520%2520%2520%2520%253Cfilter%2520type%253D%2522and%2522%253E%2520%2520%2520%2520%2520%2520%2520%253Ccondition%2520value%253D%2522%2525(sample)%2525%2522%2520attribute%253D%2522fullname%2522%2520operator%253D%2522like%2522%2520%252F%253E%2520%2520%2520%2520%2520%253C%252Ffilter%253E%2520%2520%2520%253C%252Fentity%253E%2520%253C%252Ffetch%253E%2520 HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Prefer: odata.maxpagesize=10, odata.include-annotations=OData.Community.Display.V1.FormattedValue  
  
```  
  
 **HTTP 応答**  
  
```  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Preference-Applied: odata.include-annotations="OData.Community.Display.V1.FormattedValue"  
Content-Length: 1037  
  
{   
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#contacts(fullname,jobtitle,annualincome,_transactioncurrencyid_value,transactioncurrencyid,contactid)",  
   "value":[   
      {   
         "@odata.etag":"W/\"621631\"",  
         "fullname":"Maria Cambell (sample)",  
         "jobtitle":"Accounts Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$31,000.00",  
         "annualincome":31000.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"a155b257-c843-e611-80d5-00155da84802"  
      },  
      {   
         "@odata.etag":"W/\"621643\"",  
         "fullname":"Jim Glynn (sample)",  
         "jobtitle":"Senior International Sales Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$81,400.00",  
         "annualincome":81400.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802",  
         "contactid":"b955b257-c843-e611-80d5-00155da84802"  
      }  
   ]  
}  
```  
  
 **コンソール出力**  
  
```  
Contacts Fetched by fullname containing '(sample)' - Page 3:  
    1) Maria Cambell (sample), Accounts Manager, $31,000.00  
    2) Jim Glynn (sample), Senior International Sales Manager, $81,400.00  
```  
  
<a name="bkmk_predefinedqueries"></a>
 
## <a name="predefined-queries"></a>定義済みクエリ

Web API を使用して定義済みクエリを実行できます。 詳細: [定義済みクエリの取得と実行](retrieve-and-execute-predefined-queries.md)。  
  
### <a name="saved-query"></a>保存済みクエリ

この操作では、**アクティブな取引先企業**という名前の保存済みクエリの `savedqueryid` GUID を要求します。 次にこの GUID と `savedQuery` パラメーターを使用して、すべてのアクティブな取引先企業をクエリします。  
  
 保存済みクエリの GUID を取得します。  
  
 **HTTP 要求**  
  
```  
GET http://[Organization URI]/api/data/v9.0/savedqueries?$select=name,savedqueryid&$filter=name%20eq%20'Active%20Accounts' HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Prefer: odata.maxpagesize=10, odata.include-annotations=OData.Community.Display.V1.FormattedValue  
Referer: http://localhost:1469/WebAPIQuery.html  
```  
  
 **HTTP 応答**  
  
```  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Content-Length: 251  
  
{   
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#savedqueries(name,savedqueryid)",  
   "value":[   
      {   
         "@odata.etag":"W/\"443067\"",  
         "name":"Active Accounts",  
         "savedqueryid":"00000000-0000-0000-00aa-000010001002"  
      }  
   ]  
}  
```  
  
 `savedQuery` パラメーターを使用して保存されたクエリの内容を取得  
  
 **HTTP 要求**  
  
```  
GET http://[Organization URI]/api/data/v9.0/accounts?savedQuery=00000000-0000-0000-00aa-000010001002 HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Prefer: odata.maxpagesize=10, odata.include-annotations=OData.Community.Display.V1.FormattedValue  
```  
  
 **HTTP 応答**  
  
```  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
REQ_ID: 2bc532c4-d445-44cd-adae-1909a616d6bc  
OData-Version: 4.0  
Preference-Applied: odata.include-annotations="OData.Community.Display.V1.FormattedValue"  
Content-Length: 446  
  
{   
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#accounts(name,_primarycontactid_value,primarycontactid,accountid)",  
   "value":[   
      {   
         "@odata.etag":"W/\"621613\"",  
         "name":"Contoso, Ltd. (sample)",  
         "_primarycontactid_value@OData.Community.Display.V1.FormattedValue":"Yvonne McKay (sample)",  
         "_primarycontactid_value":"9255b257-c843-e611-80d5-00155da84802",  
         "accountid":"9155b257-c843-e611-80d5-00155da84802"  
      }  
   ]  
}  
```  
  
 **コンソール出力**  
  
```  
-- Saved Query --   
Saved Query (Active Accounts):  
    1) Contoso, Ltd. (sample)  
```  
  
### <a name="user-query"></a>ユーザー クエリ

このサンプルでは、ユーザー クエリを作成および実行して、次にシステムから削除します。 このユーザー クエリは、`fullname` に `(sample)` が含まれ、`jobtitle` に `manager` が含まれ、さらに `annualincome` が `55000` 以上の取引先担当者を探します。 サンプル データには、このクエリに一致する 2 人の取引先担当者があります。  
  
 ユーザー クエリの GUID を取得します。  
  
 **HTTP 要求**  
  
```  
GET http://[Organization URI]/api/data/v9.0/userqueries?$select=name,userqueryid,&$filter=name%20eq%20'My%20User%20Query' HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Referer: http://localhost:1469/WebAPIQuery.html  
  
```  
  
 **HTTP 応答**  
  
```  
Pragma: no-cache  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Content-Length: 246  
  
{   
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#userqueries(name,userqueryid)",  
   "value":[   
      {   
         "@odata.etag":"W/\"621698\"",  
         "name":"My User Query",  
         "userqueryid":"7ec390ab-c943-e611-80d5-00155da84802"  
      }  
   ]  
}  
```  
  
 `userQuery` パラメーターの GUID 値を渡すユーザー クエリの内容を取得します。  
  
 **HTTP 要求**  
  
```  
GET http://[Organization URI]/api/data/v9.0/contacts?userQuery=7ec390ab-c943-e611-80d5-00155da84802 HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Content-Type: application/json; charset=utf-8  
Prefer: odata.maxpagesize=10, odata.include-annotations=OData.Community.Display.V1.FormattedValue  
  
```  
  
 **HTTP 応答**  
  
```  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
Content-Length: 1040  
  
{   
   "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#contacts(fullname,contactid,jobtitle,annualincome,_transactioncurrencyid_value,transactioncurrencyid)",  
   "value":[   
      {   
         "@odata.etag":"W/\"621643\"",  
         "fullname":"Jim Glynn (sample)",  
         "contactid":"b955b257-c843-e611-80d5-00155da84802",  
         "jobtitle":"Senior International Sales Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$81,400.00",  
         "annualincome":81400.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802"  
      },  
      {   
         "@odata.etag":"W/\"621629\"",  
         "fullname":"Nancy Anderson (sample)",  
         "contactid":"9d55b257-c843-e611-80d5-00155da84802",  
         "jobtitle":"Activities Manager",  
         "annualincome@OData.Community.Display.V1.FormattedValue":"$55,500.00",  
         "annualincome":55500.0000,  
         "_transactioncurrencyid_value@OData.Community.Display.V1.FormattedValue":"US Dollar",  
         "_transactioncurrencyid_value":"518c78c9-d3f6-e511-80d0-00155da84802"  
      }  
   ]  
}  
```  
  
 **コンソール出力**  
  
```  
-- User Query --   
Saved User Query:  
    1) Jim Glynn (sample), Senior International Sales Manager, $81,400.00  
    2) Nancy Anderson (sample), Activities Manager, $55,500.00  
```  
  
### <a name="see-also"></a>関連項目

[Common Data Service Web API の使用](overview.md)<br />
[Web API を使用したクエリ データ](query-data-web-api.md)<br />
[定義済みクエリの取得と実行](retrieve-and-execute-predefined-queries.md)<br />
[Web API クエリ データのサンプル (C#)](samples/query-data-csharp.md)<br />
[Web API クエリ データのサンプル (クライアント側の JavaScript)](samples/query-data-client-side-javascript.md)

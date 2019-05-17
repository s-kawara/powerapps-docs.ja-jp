---
title: Web API を使用したエンティティの取得 (Common Data Service) | Microsoft Docs
description: Common Data Service Web API を使用して GET 要求を作成する方法を調べて、一意の識別子を含むリソースとして指定されたエンティティのデータを取得する
ms.custom: ''
ms.date: 10/31/2018
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: abae4614-9e03-45e7-94fa-9e6e7225ece5
caps.latest.revision: 21
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

# <a name="retrieve-an-entity-using-the-web-api"></a>Web API を使用してエンティティを取得する

一意の識別子を含むリソースとして指定されたエンティティのデータを取得するには、`GET`要求を使用します。 エンティティの取得時に、さらに、特定のプロパティを要求して、関連エンティティからプロパティを戻すために、ナビゲーション プロパティを展開できます。  

> [!NOTE]
>  エンティティ メタデータの取得については、「[Web API を使用してメタデータをクエリする](query-metadata-web-api.md)」を参照してください。

<a name="bkmk_basicRetrieve"></a>

## <a name="basic-retrieve-example"></a>基本的な取得例

この例では、00000000-0000-0000-0000-000000000001 に等しい主キーの値を含む、取引先企業エンティティ インスタンスのデータを返します。

```http
GET [Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-0000-000000000001)
```

複数のエンティティを一度に取得するには、「[Web API を使用してデータをクエリする](query-data-web-api.md)」トピックの「[ベーシック クエリの例](query-data-web-api.md#bkmk_basicQuery)」を参照してください。

> [!CAUTION]
>  上の例では、データを取得するためのパフォーマンスのベスト プラクティスに対して、取引先企業レコードのすべてのプロパティが返されます。 この例は、Common Data Service のエンティティ インスタンスの基本取得ができる方法を単に図示していました。 すべてのプロパティは戻されたので、この例の要求に対する応答情報は含めていませんでした。
>
>  パフォーマンスのベスト プラクティスとして、データを取得する際に返されるプロパティを制限するためには、`$select` システム クエリ オプションを使用する必要があります。 これについては、次のセクション、**固有のプロパティの取得**を参照してください。
  
<a name="bkmk_requestProperties"></a>

## <a name="retrieve-specific-properties"></a>特定のプロパティの取得

プロパティ名のコンマ区切りリストを含めることにより返されるプロパティを制限するためには `$select` システム クエリ オプションを使用します。 これは重要なパフォーマンスのベスト プラクティスです。 プロパティが `$select` を使用して指定されない場合、すべてのプロパティが返されます。  

次の例では、00000000-0000-0000-0000-000000000001 に等しい主キーの値を含むアカウント エンティティの `name` および `revenue` プロパティを取得します。

**要求**
```http
GET [Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-0000-000000000001)?$select=name,revenue HTTP/1.1
Accept: application/json
Content-Type: application/json; charset=utf-8
OData-MaxVersion: 4.0
OData-Version: 4.0
```

**応答**
```http
HTTP/1.1 200 OK
Content-Type: application/json; odata.metadata=minimal
OData-Version: 4.0

{
"@odata.context": "[Organization URI]/api/data/v9.0/$metadata#accounts(name,revenue)/$entity",  
"@odata.etag": "W/\"502186\"",  
"name": "A. Datum Corporation (sample)",  
"revenue": 10000,  
"accountid": "00000000-0000-0000-0000-000000000001",  
"_transactioncurrencyid_value":"b2a6b689-9a39-e611-80d2-00155db44581"  
}  

```

特定の種類のプロパティを要求すると、さらに追加の読み取り専用プロパティが自動的に返されることを予期できます。

金額値を要求した場合、`_transactioncurrencyid_value` 検索プロパティが返されます。 このプロパティには取引通貨の GUID 値のみが含まれますので、この値を使用することにより <xref href="Microsoft.Dynamics.CRM.transactioncurrency?text=transactioncurrency EntityType" /> を使用して通貨に関する情報を取得できます。 または、コメントを要求することにより、同じ要求の追加データも取得できます。 詳細については、[検索プロパティに関するデータの取得](query-data-web-api.md#bkmk_lookupProperty)を参照してください。  

アドレスの複合属性の一部のプロパティを要求する場合は、複合プロパティも取得します。 たとえば、クエリ要求が、取引先担当者の `address1_line1` プロパティの場合は、`address1_composite` プロパティも返されます。 

<a name="BKMK_UsingAltKeys"></a>

## <a name="retrieve-using-an-alternate-key"></a>代替キーの使用の取得

エンティティで代替キーを定義している場合、さらに、代替キーを使用して、エンティティの一意の識別子ではないエンティティを取得することができます。 たとえば、`Contact` エンティティに、firstname と emailaddress1 のプロパティの両方を含む代替キーの定義がある場合、ここで示されているように、それらのキーに対して用意されているデータを含むクエリを使用して取引先担当者を取得できます。

```http
GET [Organization URI]/api/data/v9.0/contacts(firstname='Joe',emailaddress1='abc@example.com')
```

取得、更新、または削除するエンティティを一意に識別する必要のある場合には必ず、エンティティに対して構成された代替キーを使用できます。 既定では、エンティティに構成された代替キーがありません。 代替キーは、組織がそれらを追加する場合にのみ使用できます。

<a name="bkmk_retrieveSingleValue"></a>

## <a name="retrieve-a-single-property-value"></a>単一のプロパティ値の取得

エンティティの単一のプロパティ値を取得する必要がある場合、そのプロパティの値のみを返すために、エンティティの URI にプロパティの名前を付けることができます。 これは、応答で返されるものよりデータの必要が少ないために、パフォーマンスのベスト プラクティスです。

この例では、取引先企業エンティティの名前プロパティの値のみ返します。

**要求**
```http
GET [Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-0000-000000000001)/name HTTP/1.1
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
"@odata.context":"[Organization URI]/api/data/v9.0/$metadata#accounts(00000000-0000-0000-0000-000000000001)/name",
"value":"Adventure Works (sample)"
}
```

<a name="bkmk_retrieveNavigationPropertyValues"></a>

## <a name="retrieve-navigation-property-values"></a>ナビゲーション プロパティ値の取得

個々のプロパティ値が取得できることと同様に、個々のエンティティを参照する URI にナビゲーション プロパティ名を追加することによって、ナビゲーション プロパティ (検索フィールド) の値にもアクセスできます。

次の例では、`primarycontactid` 単一値ナビゲーション プロパティを使用して取引先企業の取引先責任者のフル ネームを返します。  

**要求**
 ```http
GET [Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-0000-000000000001)/primarycontactid?$select=fullname HTTP/1.1
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
"@odata.context": "[Organization URI]/api/data/v9.0/$metadata#contacts(fullname)/$entity",  
"@odata.etag": "W/\"500128\"",  
"fullname": "Rene Valdes (sample)",  
"contactid": "ff390c24-9c72-e511-80d4-00155d2a68d1"  
}

```

コレクション値ナビゲーション プロパティでは、関連するエンティティに対する参照だけまたは関連エンティティの数のみを返すオプションがあります。

次の例では、`/$ref`を要求に追加することによって、ちょうど特定の取引先企業に関連したタスクへの参照を返します。

**要求**
```http
GET [Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-0000-000000000001)/AccountTasks/$ref HTTP/1.1
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
"@odata.context": "[Organization URI]/api/data/v9.0/$metadata#Collection($ref)",  
"value": [  
{  
"@odata.id": "[Organization URI]/api/data/v9.0/tasks(6b5941dd-d175-e511-80d4-00155d2a68d1)"  
},  
{  
"@odata.id": "[Organization URI]/api/data/v9.0/tasks(fcbb60ed-d175-e511-80d4-00155d2a68d1)"  
}  
]  
}  
  
```
次の例では、`/$count` が追加された Account_Tasks コレクション値ナビゲーション プロパティを使用して、特定の取引先企業と関連するタスクの数を返します。  

 **要求**
```http
GET [Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-0000-000000000001)/Account_Tasks/$count HTTP/1.1  
Accept: application/json  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
  
```
**応答**
```http
ï»¿2
```
> [!NOTE]
> 戻る値には、これが UTF-8 ドキュメントであることを表す、UTF-8 バイトのオーダー マーク (BOM) 文字 (`ï»¿`) が含まれています。

<a name="bkmk_expandRelated"></a>

## <a name="retrieve-related-entities-for-an-entity-by-expanding-navigation-properties"></a>ナビゲーション プロパティの拡張によるエンティティに関連するエンティティの取得

`$expand` システム クエリ オプションを使用して、関連エンティティからどのデータが返されるかをコントロールします。 ナビゲーション プロパティには次の 2 種類があります。  

- *単一値* ナビゲーション プロパティは、多対 1 関係をサポートし、別のエンティティに対する参照が設定できるような検索属性に対応します。
- *コレクション値* ナビゲーション プロパティは 1 対多または多対多の関連付けに対応します。  

単にナビゲーション プロパティ名を含める場合、関連レコードのすべてのプロパティが表示されます。 ナビゲーション プロパティ名の後にかっこで示される、`$select` システム クエリ オプションを使用して、関連レコードに対して返されるプロパティを制限できます。 これは、単一値とコレクション値のナビゲーション プロパティの両方で使用します。

> [!NOTE]
> エンティティ セットの関連エンティティを取得するには、「[ナビゲーション プロパティの拡張による関連エンティティの取得](query-data-web-api.md#bkmk_expandRelated)」を参照してください。  

- **単一値ナビゲーション プロパティの拡張によるエンティティ インスタンスに対する関連エンティティの取得**: <br />以下の例は、取引先企業エンティティの取引先担当者を取得する方法を示します。 関連する取引先担当者レコードの場合、取引先担当者 ID およびフルネームのみを取得します。

  **要求**
  ```http
    GET [Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-0000-000000000001)?$select=name&$expand=primarycontactid($select=contactid,fullname) HTTP/1.1  
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
    "@odata.context":"[Organization URI]/api/data/v9.0/$metadata#accounts(name,primarycontactid,primarycontactid(contactid,fullname))/$entity",  
    "@odata.etag":"W/\"550616\"",  
    "name":"Adventure Works (sample)",  
    "accountid":"00000000-0000-0000-0000-000000000001",  
    "primarycontactid":{  
    "@odata.etag":"W/\"550626\"",  
    "contactid":"c59648c3-68f7-e511-80d3-00155db53318",  
    "fullname":"Nancy Anderson (sample)"  
    }  
    }  
  
  ```
  エンティティ インスタンスの関連エンティティを返す代わりに、`$ref` オプションを使用して単一値ナビゲーション プロパティを展開することにより、関連エンティティへの参照 (リンク) を返すこともできます。 次の例では、すべての取引先企業エンティティの取引先担当者レコードに対するリンクを返します。  

  **要求**
  ```http
    GET [Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-0000-000000000001)?$select=name&$expand=primarycontactid/$ref HTTP/1.1  
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
    "@odata.context":"[Organization URI]/api/data/v9.0/$metadata#accounts(name,primarycontactid)/$entity",  
    "@odata.etag":"W/\"550616\"",  
    "name":"Adventure Works (sample)",  
    "accountid":"00000000-0000-0000-0000-000000000001",  
    "_primarycontactid_value":"c59648c3-68f7-e511-80d3-00155db53318",  
    "primarycontactid":{  
    "@odata.id":"[Organization URI]/api/data/v9.0/contacts(c59648c3-68f7-e511-80d3-00155db53318)"  
    }  
    }
  ```
- **コレクション値ナビゲーション プロパティの拡張によるエンティティ インスタンスに対する関連エンティティの取得**:<br /> 以下の例は、取引先企業レコードに割り当てたすべてのタスクを取得する方法を示します。

  **要求**

  ```http
  GET [Organization URI]/api/data/v9.0/accounts(915e89f5-29fc-e511-80d2-00155db07c77)?$select=name&$expand=Account_Tasks($select=subject,scheduledstart)
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
  "@odata.context":"[Organization URI]/api/data/v9.0/$metadata#accounts(name,Account_Tasks,Account_Tasks(subject,scheduledstart))/$entity",  
    "@odata.etag":"W/\"514069\"","name":"Sample Child Account 1","accountid":"915e89f5-29fc-e511-80d2-00155db07c77",  
    "Account_Tasks":[  
    {  
    "@odata.etag":"W/\"514085\"",  
    "subject":"Sample Task 1",  
    "scheduledstart":"2016-04-11T15:00:00Z",  
    "activityid":"a983a612-3ffc-e511-80d2-00155db07c77"  
    },{  
    "@odata.etag":"W/\"514082\"",  
    "subject":"Sample Task 2",  
    "scheduledstart":"2016-04-13T15:00:00Z",  
    "activityid":"7bcc572f-3ffc-e511-80d2-00155db07c77"  
   }  
  ]  
  }
  ```
  
 > [!NOTE]
 > コレクション値ナビゲーション パラメーターを拡張して*エンティティ セット*の関連エンティティを取得すると、@odata.nextLink プロパティが関連エンティティの代わりに返されます。 必要なデータを返すには、新しい GET リクエストで、@odata.nextLink プロパティの値を 使用する必要があります。 詳細: [ナビゲーション プロパティの拡張による関連エンティティの取得](query-data-web-api.md#bkmk_expandRelated)

- **単一値およびコレクション値ナビゲーション プロパティ両方の拡張によるエンティティ インスタンスの関連エンティティの取得**: 以下の例は、単一およびコレクション値ナビゲーション プロパティの両方を使用して、エンティティ インスタンスの関連エンティティを拡張する方法を示します。  

  **要求**

  ```http 
    GET [Organization URI]/api/data/v9.0/accounts(99390c24-9c72-e511-80d4-00155d2a68d1)?$select=accountid&$expand=parentaccountid($select%20=%20createdon,%20name),Account_Tasks($select%20=%20subject,%20scheduledstart) HTTP/1.1  
    Accept: application/json  
    Content-Type: application/json; charset=utf-8  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0
  ```

  **応答**

  ```http
    HTTP/1.1 200 OK  
    Content-Type: application/json; odata.metadata=minimal  
    OData-Version: 4.0  

    {  
    "@odata.context":"[Organization URI]/api/data/v9.0/$metadata#accounts(accountid,parentaccountid,Account_Tasks,parentaccountid(createdon,name),Account_Tasks(subject,scheduledstart))/$entity","@odata.etag":"W/\"514069\"","accountid":"915e89f5-29fc-e511-80d2-00155db07c77",  
    "parentaccountid":{  
    "@odata.etag":"W/\"514074\"","createdon":"2016-04-06T00:29:04Z",  
    "name":"Adventure Works (sample)",  
    "accountid":"3adbf27c-8efb-e511-80d2-00155db07c77"  
    },"Account_Tasks":[  
    {  
    "@odata.etag":"W/\"514085\"",  
    "subject":"Sample Task 1",  
    "scheduledstart":"2016-04-11T15:00:00Z",  
    "activityid":"a983a612-3ffc-e511-80d2-00155db07c77"  
    },{  
    "@odata.etag":"W/\"514082\"",  
    "subject":"Sample Task 2",  
    "scheduledstart":"2016-04-13T15:00:00Z",  
    "activityid":"7bcc572f-3ffc-e511-80d2-00155db07c77"  
    }  
    ]  
    }
  ```

> [!NOTE]
> 関連するエンティティの URI のみ、または関連するエンティティの数のカウントを返すためには、`/$count` または `/$ref` パス セグメントを使用できません。

<a name="bkmk_optionsOnExpand"></a>

## <a name="options-to-apply-to-expanded-entities"></a>拡張されたエンティティに適用するためのオプション

 コレクション値ナビゲーション プロパティに対して返されるエンティティに特定のシステム クエリ オプションを適用することができます。 コレクション値ナビゲーション プロパティ名の後に、かっこで囲まれるシステム クエリ オプションのセミコロン区切りリストを使用します。 `$select`、`$filter`、`$orderby`、および `$top` を使用することができます。

 次の例では、取引先企業に関連するタスク エンティティの結果を、"1" で終わる件名を含むものにフィルター処理します。

```http
GET [Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-0000-000000000001)?$expand=Account_Tasks($filter=endswith(subject,'1');$select=subject)  
```

次の例では、関連タスクが `createdon` プロパティに基づいて昇順で返される必要のあることを指定します。

```http
GET [Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-0000-000000000001)?$expand=Account_Tasks($orderby=createdon asc;$select=subject,createdon)  
```

 次の例では、最初の関連するタスクのみ返します。

```http
GET [Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-0000-000000000001)?$expand=Account_Tasks($top=1;$select=subject)
```

> [!NOTE]
> これは、[OData バージョン 4.0 パート 1: プロトコル プラス Errata 02](http://docs.oasis-open.org/odata/odata/v4.0/errata02/os/complete/part1-protocol/odata-v4.0-errata02-os-part1-protocol-complete.html) の「11.2.4.2.1 展開オプション」セクションに記載のシステム クエリ オプションの一部です。 オプション `$skip`、`$count`、`$search`、`$expand`、および`$levels` は Web API ではサポートされていません。

<a name="bkmk_DetectIfChanged"></a>

## <a name="detect-if-an-entity-has-changed-since-it-was-retrieved"></a>エンティティが取得されてから変更されているかどうかの検出

パフォーマンスのベスト プラクティスとして、必要なデータのみを使用する必要があります。 以前にエンティティ レコードを取得した場合、以前に取得したレコードに関連する *ETag* を使用して、そのレコードを条件を付けて検索できます。  詳細については、「[条件付き検索](perform-conditional-operations-using-web-api.md#bkmk_DetectIfChanged)」を参照してください。  

<a name="bkmk_formattedValues"></a>

## <a name="retrieve-formatted-values"></a>書式設定された値の取得

個々のレコードの取得での書式設定された値の要求は、エンティティ セットへのクエリ時と同じ方法で行われます。 詳細: [書式設定値を含める](query-data-web-api.md#bkmk_includeFormattedValues)。

### <a name="see-also"></a>関連項目

[Web API 基本操作のサンプル (C#)](samples/basic-operations-csharp.md)<br />
[Web API 基本操作のサンプル (クライアント側の JavaScript)](samples/basic-operations-client-side-javascript.md)<br />
[Web API を使用して演算を実行する](perform-operations-web-api.md)<br />
[HTTP 要求の作成とエラーの処理](compose-http-requests-handle-errors.md)<br />
[Web API を使用したクエリ データ](query-data-web-api.md)<br />
[Web API を使用してエンティティを作成する](create-entity-web-api.md)<br />
[Web API を使用したエンティティの更新と削除](update-delete-entities-using-web-api.md)<br />
[Web API を使用したエンティティの関連付けと関連付け解除](associate-disassociate-entities-using-web-api.md)<br />
[Web API 関数の使用](use-web-api-functions.md)<br />
[Web API アクションの使用](use-web-api-actions.md)<br />
[Web API を使用してバッチ操作を実行する](execute-batch-operations-using-web-api.md)<br />
[Web API を使用して別のユーザーを偽装する](impersonate-another-user-web-api.md)<br />
[Web API を使用する条件付き演算を実行する](perform-conditional-operations-using-web-api.md)<br />

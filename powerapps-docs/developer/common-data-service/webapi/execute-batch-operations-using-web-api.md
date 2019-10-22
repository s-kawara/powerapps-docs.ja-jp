---
title: Web APIを使用したバッチ処理の実行 (Common Data Service)| Microsoft Docs
description: バッチ操作を使用すると、単一の HTTP 要求で複数のオペレーションをグループ化することができます。 Web API を使用してバッチ操作を実行する方法を読みます
ms.custom: ''
ms.date: 07/13/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 799b2346-bda1-4a26-a330-79d0927a7743
caps.latest.revision: 11
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
# <a name="execute-batch-operations-using-the-web-api"></a>Web API を使用してバッチ操作を実行する

バッチ操作を使用して複数の操作を 1 つの HTTP 要求にグループ化することができます。  
  
<a name="bkmk_Whentousebatchrequests"></a>

## <a name="when-to-use-batch-requests"></a>バッチ要求を使用する場合

バッチ要求が指定した値は、変更セットを含められるので、グループとして成功または失敗するいくつかの操作をまとめる手段を提供します。 Web API を使用して実行できる他の操作と比べ、HTTP プロトコルのより深い理解またはオブジェクトのシリアル化を含むいくつかのオブジェクト モデルなしに構成することは困難です。なぜなら要求本文は元来とても具体的な要件に一致する必要があるテキスト ドキュメントだからです。  
  
バッチ要求を使用するよりも簡単に、関連付けられたエンティティを 1 回の操作で作成できることに注意してください。 バッチ要求は、1 つのトランザクション操作ですべての操作を実行する必要がある場合に、相互に関連付けられていないエンティティに対して操作を実行するのに最も適しています。  
  
また、返された応答は、簡単に JSON に解析できるオブジェクトではなく、基本的にはテキスト ドキュメントです。 応答内のテキストを解析するか、応答内のデータにアクセスするためのヘルパー ライブラリを検索する必要があります。  
 
>[!NOTE]
>  バッチ要求には最大 100 個の別々要求を含めることができるが、他のバッチ要求を含めることはできません。  
  
<a name="bkmk_BatchRequests"></a> 

## <a name="batch-requests"></a>バッチ要求

POST 要求を使用して、複数の要求が含まれているバッチ操作を送信します。 バッチ要求には、GET 要求と変更セットを含めることができます。 バッチ要求のトランザクションの機能を使用するには、データを変更する操作のみ変更セット内に含められます。 GET 要求は変更セットに含まれていてはなりません。  
  
バッチが含まれている POST 要求には、マルチパート/混合に設定された値を持ち、このパターンを使用してバッチの識別子を組み込むように設定された境界を持つ、Content-Type ヘッダーが必要です。  
  
```  
--batch_<unique identifier>  
```  
  
一意の識別子は、GUID である必要はありませんが、一意である必要があります。 バッチ内の各項目の前に、次のようなコンテンツ タイプおよびコンテンツ転送エンコーディング ヘッダーを持つバッチ識別子が必要です。  
  
```  
--batch_WKQS9Yui9r  
Content-Type: application/http  
Content-Transfer-Encoding:binary  
```  
  
バッチの最後には、次のように、終端のインジケーターを含める必要があります。  
  
```  
--batch_WKQS9Yui9r--  
```   
  
<a name="bkmk_ChangeSets"></a>

## <a name="change-sets"></a>変更セット

変更セットに複数の操作が含まれる場合、すべての操作はアトミックと見なされます。これは、操作のいずれかが失敗した場合、完了した操作はロールバックされることを意味します。 バッチ要求のように、変更セットには、マルチパート/混合に設定された値を持ち、このパターンを使用して変更セットの識別子を組み込むように設定された境界を持つ、Content-Type ヘッダーが必要です。  
  
```  
--changeset_<unique identifier>  
```  
  
一意の識別子は、GUID である必要はありませんが、一意である必要があります。 変更セット内の各項目の前に、次のようなコンテンツ タイプおよびコンテンツ転送エンコーディング ヘッダーを持つ変更セット識別子が必要です。  
  
```  
--changeset_BBB456  
Content-Type: application/http  
Content-Transfer-Encoding:binary  
```  
  
また、変更セットには、一意の値を持つコンテンツ ID を含めることもできます。 この値は、接頭辞 `$` が付くと、その操作で作成された任意のエンティティの URI を格納する変数を表します。 たとえば、値 1 を設定すると、後から変更セット内で `$1` を使用してそのエンティティを参照できます。  
  
変更セットの最後には、次のように、終端のインジケーターを含める必要があります。  
  
```  
--changeset_BBB456--  
```  
  
<a name="bkmk_Example"></a>

## <a name="example"></a>例

次の例には、AAA123 という一意の識別子を持つバッチと、BBB456 という一意の識別子を持つ変更セットが含まれています。  
  
変更セット内で、2 つのタスクが POST を使用して作成され、accountid = 00000000-0000-0000-000000000001 の既存のアカウントに関連付けられています。  
  
最後に、バッチ要求で作成された 2 つのタスクを含めて、アカウントに関連付けられている 6 つのタスクすべてを取得するために、変更セットの外側に GET 要求が組み込まれます。  
  
 **要求**

```http 
POST[Organization URI]/api/data/v9.1/$batch HTTP/1.1  
Content-Type: multipart/mixed;boundary=batch_AAA123  
Accept: application/json  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
  
--batch_AAA123  
Content-Type: multipart/mixed;boundary=changeset_BBB456  
  
--changeset_BBB456  
Content-Type: application/http  
Content-Transfer-Encoding:binary  
Content-ID: 1  
  
POST[Organization URI]/api/data/v9.1/tasks HTTP/1.1  
Content-Type: application/json;type=entry  
  
{"subject":"Task 1 in batch","regardingobjectid_account_task@odata.bind":"[Organization URI]/api/data/v9.1/accounts(00000000-0000-0000-000000000001)"}  
--changeset_BBB456  
Content-Type: application/http  
Content-Transfer-Encoding:binary  
Content-ID: 2  
  
POST[Organization URI]/api/data/v9.1/tasks HTTP/1.1  
Content-Type: application/json;type=entry  
  
{"subject":"Task 2 in batch","regardingobjectid_account_task@odata.bind":"[Organization URI]/api/data/v9.1/accounts(00000000-0000-0000-000000000001)"}  
--changeset_BBB456--  
  
--batch_AAA123  
Content-Type: application/http  
Content-Transfer-Encoding:binary  
  
GET[Organization URI]/api/data/v9.1/accounts(00000000-0000-0000-000000000001)/Account_Tasks?$select=subject HTTP/1.1  
Accept: application/json  
  
--batch_AAA123--  
```  
  
 **応答**

```http 
--batchresponse_c1bd45c1-dd81-470d-b897-e965846aad2f  
Content-Type: multipart/mixed; boundary=changesetresponse_ff83b4f1-ab48-430c-b81c-926a2c596abc  
  
--changesetresponse_ff83b4f1-ab48-430c-b81c-926a2c596abc  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
Content-ID: 1  
  
HTTP/1.1 204 No Content  
OData-Version: 4.0  
Location:[Organization URI]/api/data/v9.1/tasks(a59c24f3-fafc-e411-80dd-00155d2a68cb)  
OData-EntityId:[Organization URI]/api/data/v9.1/tasks(a59c24f3-fafc-e411-80dd-00155d2a68cb)  
  
--changesetresponse_ff83b4f1-ab48-430c-b81c-926a2c596abc  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
Content-ID: 2  
  
HTTP/1.1 204 No Content  
OData-Version: 4.0  
Location:[Organization URI]/api/data/v9.1/tasks(a69c24f3-fafc-e411-80dd-00155d2a68cb)  
OData-EntityId:[Organization URI]/api/data/v9.1/tasks(a69c24f3-fafc-e411-80dd-00155d2a68cb)  
  
--changesetresponse_ff83b4f1-ab48-430c-b81c-926a2c596abc--  
--batchresponse_c1bd45c1-dd81-470d-b897-e965846aad2f  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
  
{  
  "@odata.context":"[Organization URI]/api/data/v9.1/$metadata#tasks(subject)","value":[  
    {  
      "@odata.etag":"W/\"474122\"","subject":"Task Created with Test Account","activityid":"919c24f3-fafc-e411-80dd-00155d2a68cb"  
    },{  
      "@odata.etag":"W/\"474125\"","subject":"Task 1","activityid":"a29c24f3-fafc-e411-80dd-00155d2a68cb"  
    },{  
      "@odata.etag":"W/\"474128\"","subject":"Task 2","activityid":"a39c24f3-fafc-e411-80dd-00155d2a68cb"  
    },{  
      "@odata.etag":"W/\"474131\"","subject":"Task 3","activityid":"a49c24f3-fafc-e411-80dd-00155d2a68cb"  
    },{  
      "@odata.etag":"W/\"474134\"","subject":"Task 1 in batch","activityid":"a59c24f3-fafc-e411-80dd-00155d2a68cb"  
    },{  
      "@odata.etag":"W/\"474137\"","subject":"Task 2 in batch","activityid":"a69c24f3-fafc-e411-80dd-00155d2a68cb"  
    }  
  ]  
}  
--batchresponse_c1bd45c1-dd81-470d-b897-e965846aad2f--  
```  
`GET` 要求を持つ `odata.include-annotations` 基本設定ヘッダーを含み、その値を "*" にセットしてプロパティに関連付けられたすべての注釈が戻されるように指定します。

```HTTP
--batch_AAA123  
Content-Type: application/http  
Content-Transfer-Encoding:binary  
  
GET[Organization URI]/api/data/v9.1/accounts(00000000-0000-0000-000000000001)?$select=name,telephone1,emailaddress1,shippingmethodcode,customersizecode,accountratingcode,followemail,donotemail,donotphone,statuscode HTTP/1.1  
Accept: application/json  
Prefer: odata.include-annotations="*"
  
--batch_AAA123-- 
```
基本設定ヘッダーの詳細については、 [ヘッダーの基本設定](http://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part1-protocol/odata-v4.0-errata03-os-part1-protocol-complete.html#_Toc453752234)を参照してください。

## <a name="reference-uris-in-an-operation"></a>運用における参照URI

`$1`、 `$2`などの `$parameter` を使用すると、バッチ要求に先行するチェンジセットで使用されていたURIを参照できます。 このセクションでは、 `$parameter` をバッチ操作の要求本体で使用してURIを参照する方法について、さまざまな例を示します。

### <a name="reference-uris-in-request-body"></a>要求本体のURI参照

以下の例では、2つのURI参照を1回の操作で使用する方法を示しています。

**要求**

```http
POST [Organization URI]/api/data/v9.1/$batch HTTP/1.1
Content-Type:  multipart/mixed;boundary=batch_AAA123
Accept:  application/json
OData-MaxVersion:  4.0
OData-Version:  4.0

--batch_AAA123
Content-Type: multipart/mixed; boundary=changeset_dd81ccab-11ce-4d57-b91d-12c4e25c3cab

--changeset_dd81ccab-11ce-4d57-b91d-12c4e25c3cab
Content-Type: application/http
Content-Transfer-Encoding: binary
Content-ID: 1

POST [Organization URI]/api/data/v9.1/leads HTTP/1.1
Content-Type: application/json

{
    "firstname":"aaa",
    "lastname":"bbb"
}

--changeset_dd81ccab-11ce-4d57-b91d-12c4e25c3cab
Content-Type: application/http
Content-Transfer-Encoding: binary
Content-ID: 2

POST [Organization URI]/api/data/v9.1/contacts HTTP/1.1
Content-Type: application/json

{"@odata.type":"Microsoft.Dynamics.CRM.contact","firstname":"Oncall Contact-1111"}

--changeset_dd81ccab-11ce-4d57-b91d-12c4e25c3cab
Content-Type: application/http
Content-Transfer-Encoding: binary
Content-ID: 3

POST [Organization URI]/api/data/v9.1/accounts HTTP/1.1
Content-Type: application/json

{
    "name":"IcM Account",
    "originatingleadid@odata.bind":"$1",
    "primarycontactid@odata.bind":"$2"
}

--changeset_dd81ccab-11ce-4d57-b91d-12c4e25c3cab--
--batch_AAA123--
```

**応答**

```http
200 OK

--batchresponse_3cace264-86ea-40fe-83d3-954b336c0f4a
Content-Type: multipart/mixed; boundary=changesetresponse_1a5db8a1-ec98-42c4-81f6-6bc6adcfa4bc

--changesetresponse_1a5db8a1-ec98-42c4-81f6-6bc6adcfa4bc
Content-Type: application/http
Content-Transfer-Encoding: binary
Content-ID: 1

HTTP/1.1 204 No Content
OData-Version: 4.0
Location: [Organization URI]/api/data/v9.1/leads(425195a4-7a75-e911-a97a-000d3a34a1bd)
OData-EntityId: [Organization URI]/api/data/v9.1/leads(425195a4-7a75-e911-a97a-000d3a34a1bd)

--changesetresponse_1a5db8a1-ec98-42c4-81f6-6bc6adcfa4bc
Content-Type: application/http
Content-Transfer-Encoding: binary
Content-ID: 2

HTTP/1.1 204 No Content
OData-Version: 4.0
Location: [Organization URI]/api/data/v9.1/contacts(495195a4-7a75-e911-a97a-000d3a34a1bd)
OData-EntityId: [Organization URI]/api/data/v9.1/contacts(495195a4-7a75-e911-a97a-000d3a34a1bd)

--changesetresponse_1a5db8a1-ec98-42c4-81f6-6bc6adcfa4bc
Content-Type: application/http
Content-Transfer-Encoding: binary
Content-ID: 3

HTTP/1.1 204 No Content
OData-Version: 4.0
Location: [Organization URI]/api/data/v9.1/accounts(4f5195a4-7a75-e911-a97a-000d3a34a1bd)
OData-EntityId: [Organization URI]/api/data/v9.1/accounts(4f5195a4-7a75-e911-a97a-000d3a34a1bd)

--changesetresponse_1a5db8a1-ec98-42c4-81f6-6bc6adcfa4bc--
--batchresponse_3cace264-86ea-40fe-83d3-954b336c0f4a--
```

### <a name="reference-uri-in-request-url"></a>要求URLのURI参照

以下の例は、この後に続く要求URLで `$1` を使用してURIを参照する方法を示しています。

**要求**

```http
POST [Organization URI]/api/data/v9.1/$batch HTTP/1.1
Content-Type:  multipart/mixed;boundary=batch_AAA123
Accept:  application/json
OData-MaxVersion:  4.0
OData-Version:  4.0

--batch_AAA123
Content-Type: multipart/mixed; boundary=changeset_dd81ccab-11ce-4d57-b91d-12c4e25c3cab

--changeset_dd81ccab-11ce-4d57-b91d-12c4e25c3cab
Content-Type: application/http
Content-Transfer-Encoding: binary
Content-ID: 1

POST [Organization URI]/api/data/v9.1/contacts HTTP/1.1
Content-Type: application/json

{
  "@odata.type":"Microsoft.Dynamics.CRM.contact",
  "firstname":"Contact",
  "lastname":"AAAAAA"
}

--changeset_dd81ccab-11ce-4d57-b91d-12c4e25c3cab
Content-Transfer-Encoding: binary
Content-Type: application/http
Content-ID: 2

PUT $1/lastname HTTP/1.1
Content-Type: application/json

{
  "value":"BBBBB"
}

--changeset_dd81ccab-11ce-4d57-b91d-12c4e25c3cab--
--batch_AAA123--
```

**応答**

```http
200 OK

--batchresponse_2cb48f48-39a8-41ea-aa52-132fa8ab3c2d
Content-Type: multipart/mixed; boundary=changesetresponse_d7528170-3ef3-41bd-be8e-eac971a8d9d4

--changesetresponse_d7528170-3ef3-41bd-be8e-eac971a8d9d4
Content-Type: application/http
Content-Transfer-Encoding: binary
Content-ID: 1

HTTP/1.1 204 No Content
OData-Version: 4.0
Location:[Organization URI]/api/data/v9.1/contacts(f8ea5d2c-8c75-e911-a97a-000d3a34a1bd)
OData-EntityId:[Organization URI]/api/data/v9.1/contacts(f8ea5d2c-8c75-e911-a97a-000d3a34a1bd)


--changesetresponse_d7528170-3ef3-41bd-be8e-eac971a8d9d4
Content-Type: application/http
Content-Transfer-Encoding: binary
Content-ID: 2

HTTP/1.1 204 No Content
OData-Version: 4.0


--changesetresponse_d7528170-3ef3-41bd-be8e-eac971a8d9d4--
--batchresponse_2cb48f48-39a8-41ea-aa52-132fa8ab3c2d--
```

### <a name="reference-uris-in-url-and-request-body-using-odataid"></a>URLの参照URIと @odata.idを使用する要求本体

以下の例では、取引先担当者 エンティティー レコードを、取引先企業 エンティティー レコードにリンクする方法を示しています。 取引先企業 エンティティー レコードのURIは `$1` として参照され、取引先担当者 エンティティー レコードのURIは `$2`として参照されます。

**要求**

```http
POST [Organization URI]/api/data/v9.1/$batch HTTP/1.1
Content-Type:multipart/mixed;boundary=batch_AAA123
Accept:application/json
OData-MaxVersion:4.0
OData-Version:4.0

--batch_AAA123
Content-Type: multipart/mixed; boundary=changeset_dd81ccab-11ce-4d57-b91d-12c4e25c3cab

--changeset_dd81ccab-11ce-4d57-b91d-12c4e25c3cab
Content-Type:application/http
Content-Transfer-Encoding:binary
Content-ID:1

POST [Organization URI]/api/data/v9.1/accounts HTTP/1.1
Content-Type: application/json

{"@odata.type":"Microsoft.Dynamics.CRM.account","name":"IcM Account"}

--changeset_dd81ccab-11ce-4d57-b91d-12c4e25c3cab
Content-Type:application/http
Content-Transfer-Encoding:binary
Content-ID:2

POST [Organization URI]/api/data/v9.1/contacts HTTP/1.1
Content-Type:application/json

{"@odata.type":"Microsoft.Dynamics.CRM.contact","firstname":"Oncall Contact"}

--changeset_dd81ccab-11ce-4d57-b91d-12c4e25c3cab
Content-Type:application/http
Content-Transfer-Encoding:binary
Content-ID:3

PUT $1/primarycontactid/$ref HTTP/1.1
Content-Type:application/json

{"@odata.id":"$2"}

--changeset_dd81ccab-11ce-4d57-b91d-12c4e25c3cab--
--batch_AAA123--
```

**応答**

```http
200 OK

--batchresponse_0740a25c-d8e1-41a5-9202-1b50a297864c
Content-Type: multipart/mixed; boundary=changesetresponse_19ca0da8-d8bb-4273-a3f7-fe0d0fadfe5f

--changesetresponse_19ca0da8-d8bb-4273-a3f7-fe0d0fadfe5f
Content-Type: application/http
Content-Transfer-Encoding: binary
Content-ID: 1

HTTP/1.1 204 No Content
OData-Version: 4.0
Location:[Organization URI]/api/data/v9.1/accounts(3dcf8c02-8c75-e911-a97a-000d3a34a1bd)
OData-EntityId:[Organization URI]/api/data/v9.1/accounts(3dcf8c02-8c75-e911-a97a-000d3a34a1bd)

--changesetresponse_19ca0da8-d8bb-4273-a3f7-fe0d0fadfe5f
Content-Type: application/http
Content-Transfer-Encoding: binary
Content-ID: 2

HTTP/1.1 204 No Content
OData-Version: 4.0
Location:[Organization URI]/api/data/v9.1/contacts(43cf8c02-8c75-e911-a97a-000d3a34a1bd)
OData-EntityId:[Organization URI]/api/data/v9.1/contacts(43cf8c02-8c75-e911-a97a-000d3a34a1bd)

--changesetresponse_19ca0da8-d8bb-4273-a3f7-fe0d0fadfe5f
Content-Type: application/http
Content-Transfer-Encoding: binary
Content-ID: 3

HTTP/1.1 204 No Content
OData-Version: 4.0

--changesetresponse_19ca0da8-d8bb-4273-a3f7-fe0d0fadfe5f--
--batchresponse_0740a25c-d8e1-41a5-9202-1b50a297864c--
```

### <a name="reference-uris-in-url-and-navigation-properties"></a>URL とナビゲーション プロパティの参照URI

次の例は、取引先担当者レコードの組織URIを使用し、 `primarycontactid` の単一値ナビゲーション プロパティを使用して取引先企業レコードにリンクする方法を示しています。 `PATCH` 要求では、取引先企業エンティティー レコードのURIは `$1` として参照され、取引先担当者エンティティー レコードのURIは `$2` として参照されます。

**要求**

```http
POST [Organization URI]/api/data/v9.1/$batch HTTP/1.1
Content-Type:multipart/mixed;boundary=batch_AAA123
Accept:application/json
OData-MaxVersion:4.0
OData-Version:4.0

--batch_AAA123
Content-Type: multipart/mixed; boundary=changeset_dd81ccab-11ce-4d57-b91d-12c4e25c3cab

--changeset_dd81ccab-11ce-4d57-b91d-12c4e25c3cab
Content-Type: application/http
Content-Transfer-Encoding: binary
Content-ID: 1

POST [Organization URI]/api/data/v9.1/accounts HTTP/1.1
Content-Type: application/json

{"@odata.type":"Microsoft.Dynamics.CRM.account","name":"IcM Account"}

--changeset_dd81ccab-11ce-4d57-b91d-12c4e25c3cab
Content-Type: application/http
Content-Transfer-Encoding: binary
Content-ID: 2

POST [Organization URI]/api/data/v9.1/contacts HTTP/1.1
Content-Type: application/json

{
  "@odata.type":"Microsoft.Dynamics.CRM.contact",
  "firstname":"Oncall Contact"
}

--changeset_dd81ccab-11ce-4d57-b91d-12c4e25c3cab
Content-Type: application/http
Content-Transfer-Encoding: binary
Content-ID: 3

PATCH $1 HTTP/1.1
Content-Type: application/json

{
  "primarycontactid@odata.bind":"$2"
}

--changeset_dd81ccab-11ce-4d57-b91d-12c4e25c3cab--
--batch_AAA123--
```
**応答**

```http
200 OK

--batchresponse_9595d3ae-48f6-414f-a3aa-a3a33559859e
Content-Type: multipart/mixed; boundary=changesetresponse_0c1567a5-ad0d-48fa-b81d-e6db05cad01c

--changesetresponse_0c1567a5-ad0d-48fa-b81d-e6db05cad01c
Content-Type: application/http
Content-Transfer-Encoding: binary
Content-ID: 1

HTTP/1.1 204 No Content
OData-Version: 4.0
Location: [Organization URI]/api/data/v9.1/accounts(6cd81853-7b75-e911-a97a-000d3a34a1bd)
OData-EntityId: [Organization URI]/api/data/v9.1/accounts(6cd81853-7b75-e911-a97a-000d3a34a1bd)

--changesetresponse_0c1567a5-ad0d-48fa-b81d-e6db05cad01c
Content-Type: application/http
Content-Transfer-Encoding: binary
Content-ID: 2

HTTP/1.1 204 No Content
OData-Version: 4.0
Location: [Organization URI]/api/data/v9.1/contacts(6ed81853-7b75-e911-a97a-000d3a34a1bd)
OData-EntityId: [Organization URI]/api/data/v9.1/contacts(6ed81853-7b75-e911-a97a-000d3a34a1bd)

--changesetresponse_0c1567a5-ad0d-48fa-b81d-e6db05cad01c
Content-Type: application/http
Content-Transfer-Encoding: binary
Content-ID: 3

HTTP/1.1 204 No Content
OData-Version: 4.0
Location: [Organization URI]/api/data/v9.1/accounts(6cd81853-7b75-e911-a97a-000d3a34a1bd)
OData-EntityId: [Organization URI]/api/data/v9.1/accounts(6cd81853-7b75-e911-a97a-000d3a34a1bd)

--changesetresponse_0c1567a5-ad0d-48fa-b81d-e6db05cad01c--
--batchresponse_9595d3ae-48f6-414f-a3aa-a3a33559859e--
```

> [!NOTE]
> 要求本体で宣言される前に Content-ID を参照すると、エラー **HTTP 400** Bad request が返されます。
>
> 以下の例では、このエラーの原因となり得る要求本体を示しています。
> 
> **要求本文**
> 
> ```http
> --batch_AAA123
> Content-Type: multipart/mixed; boundary=changeset_BBB456
> 
> --changeset_BBB456
> Content-Type: application/http
> Content-Transfer-Encoding:binary
> Content-ID: 2
> 
> POST [Organization URI]/api/data/v9.1/phonecalls HTTP/1.1
> Content-Type: application/json;type=entry
> 
> {
>     "phonenumber":"911",
>     "regardingobjectid_account_phonecall@odata.bind" : "$1"
> }
> 
> --changeset_BBB456
> Content-Type: application/http
> Content-Transfer-Encoding:binary
> Content-ID: 1
> 
> POST [Organization URI]/api/data/v9.1/accounts HTTP/1.1
> Content-Type: application/json;type=entry
> 
> {
>     "name":"QQQQ",
>     "revenue": 1.50
> }
> 
> --changeset_BBB456--
> --batch_AAA123--
> ```
>
> **応答**
> 
> ```http
> HTTP 400 Bad Request
> Content-ID Reference: '$1' does not exist in the batch context.
> ```

### <a name="see-also"></a>関連項目

[Web API を使用して演算を実行する](perform-operations-web-api.md)<br />
[HTTP 要求の作成とエラーの処理](compose-http-requests-handle-errors.md)<br />
[Web API を使用したクエリ データ](query-data-web-api.md)<br />
[Web API を使用してエンティティを作成する](create-entity-web-api.md)<br />
[Web API を使用してエンティティを取得する](retrieve-entity-using-web-api.md)<br />
[Web API を使用したエンティティの更新と削除](update-delete-entities-using-web-api.md)<br />
[Web API を使用したエンティティの関連付けと関連付け解除](associate-disassociate-entities-using-web-api.md)<br />
[Web API 関数の使用](use-web-api-functions.md)<br />
[Web API アクションの使用](use-web-api-actions.md)<br />
[Web API を使用して別のユーザーを偽装する](impersonate-another-user-web-api.md)<br />
[Web API を使用する条件付き演算を実行する](perform-conditional-operations-using-web-api.md)

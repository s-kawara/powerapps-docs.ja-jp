---
title: Web API (アプリ用 Common Data Service) を使用してバッチ操作を実行する | Microsoft Docs
description: バッチ操作を使用すると、単一の HTTP 要求で複数のオペレーションをグループ化することができます。 Web API を使用してバッチ操作を実行する方法を読みます
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 799b2346-bda1-4a26-a330-79d0927a7743
caps.latest.revision: 11
author: brandonsimons
ms.author: jdaly
manager: amyla
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
POST[Organization URI]/api/data/v9.0/$batch HTTP/1.1  
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
  
POST[Organization URI]/api/data/v9.0/tasks HTTP/1.1  
Content-Type: application/json;type=entry  
  
{"subject":"Task 1 in batch","regardingobjectid_account_task@odata.bind":"[Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-000000000001)"}  
--changeset_BBB456  
Content-Type: application/http  
Content-Transfer-Encoding:binary  
Content-ID: 2  
  
POST[Organization URI]/api/data/v9.0/tasks HTTP/1.1  
Content-Type: application/json;type=entry  
  
{"subject":"Task 2 in batch","regardingobjectid_account_task@odata.bind":"[Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-000000000001)"}  
--changeset_BBB456--  
  
--batch_AAA123  
Content-Type: application/http  
Content-Transfer-Encoding:binary  
  
GET[Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-000000000001)/Account_Tasks?$select=subject HTTP/1.1  
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
Location:[Organization URI]/api/data/v9.0/tasks(a59c24f3-fafc-e411-80dd-00155d2a68cb)  
OData-EntityId:[Organization URI]/api/data/v9.0/tasks(a59c24f3-fafc-e411-80dd-00155d2a68cb)  
  
--changesetresponse_ff83b4f1-ab48-430c-b81c-926a2c596abc  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
Content-ID: 2  
  
HTTP/1.1 204 No Content  
OData-Version: 4.0  
Location:[Organization URI]/api/data/v9.0/tasks(a69c24f3-fafc-e411-80dd-00155d2a68cb)  
OData-EntityId:[Organization URI]/api/data/v9.0/tasks(a69c24f3-fafc-e411-80dd-00155d2a68cb)  
  
--changesetresponse_ff83b4f1-ab48-430c-b81c-926a2c596abc--  
--batchresponse_c1bd45c1-dd81-470d-b897-e965846aad2f  
Content-Type: application/http  
Content-Transfer-Encoding: binary  
  
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0  
  
{  
  "@odata.context":"[Organization URI]/api/data/v9.0/$metadata#tasks(subject)","value":[  
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
  
GET[Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-000000000001)?$select=name,telephone1,emailaddress1,shippingmethodcode,customersizecode,accountratingcode,followemail,donotemail,donotphone,statuscode HTTP/1.1  
Accept: application/json  
Prefer: odata.include-annotations="*"
  
--batch_AAA123-- 
```
基本設定ヘッダーの詳細については、[ヘッダーの基本設定](http://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part1-protocol/odata-v4.0-errata03-os-part1-protocol-complete.html#_Toc453752234)を参照してください。

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

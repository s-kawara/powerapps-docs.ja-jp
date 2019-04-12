---
title: Web API 条件操作のサンプル (Common Data Service) | Microsoft Docs
description: このサンプル グループは、Common Data Service サーバーに含まれている、またはクライアントによって現在管理されているエンティティ レコードのバージョンに基づいて条件付きで操作を実行する方法を示します
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: f2e5d22b-93fe-43b7-af15-3e281f3b3084
caps.latest.revision: 13
author: brandonsimons
ms.author: jdaly
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="web-api-conditional-operations-sample"></a>Web API 条件付き演算サンプル

このサンプル グループは、Common Data Service サーバーに含まれている、またはクライアントによって現在管理されているエンティティ レコードのバージョンに基づいて条件付きで操作を実行する方法を示します。 詳細については、[Web API を使用する条件付き演算を実行](perform-conditional-operations-using-web-api.md) を参照してください。 このサンプルは次の言語に対する別個のプロジェクトとして実装されます。  
  
 [Web API 条件付き演算サンプル (C#)](samples/conditional-operations-csharp.md)  
 
 Common Data Service Web API は、[OData v4.0](http://www.odata.org/documentation/) プロトコルの規則に従います。それにより、[ETags](http://docs.oasis-open.org/odata/odata/v4.0/errata03/os/complete/part1-protocol/odata-v4.0-errata03-os-part1-protocol-complete.html#_Toc453752236) を使い、リソースのバージョン管理を実装します。 Web API の条件付き演算は、このバージョン管理メカニズムによって異なります。  
  
 このトピックは、より高度でニュートラル言語レベルの構造と内容の例を説明します。 適応可能な HTTP 要求と応答、また関連するプログラム出力について説明しています。 このトピックに説明されている操作を実行する方法に関する言語固有の実装および関連する詳細の取得については、上記のリンクされたサンプル トピックを確認してください。  
  
## <a name="demonstrates"></a>説明

 このサンプルでは、次の表に示す通り 3 つの主要なセクションに分かれています。   各セクションでは、トピック [Web API を使い条件付き演算を実行](perform-conditional-operations-using-web-api.md) の関連する概念的セクションで、より詳しく説明する一連の関連 Web API 操作を含みます。  
  
|コード セクション|関連する概念的なトピック|  
|------------------|----------------------------------|  
|[条件 GET](#bkmk_conditionalGet)|[条件付き検索](perform-conditional-operations-using-web-api.md#bkmk_DetectIfChanged)|  
|[削除および更新でのオプティミスティック同時実行](#bkmk_optimisiticConcurrency)|[オプティミスティック同時実行の適用](perform-conditional-operations-using-web-api.md#bkmk_Applyoptimisticconcurrency)|  
|[upsert 操作の制御](#bkmk_controllingUpsert)|[upsert 操作の制限](perform-conditional-operations-using-web-api.md#bkmk_limitUpsertOperations)|  
  
 次のセクションでは、Common Data Service Web API 操作の実行に関する簡単な説明、および各言語実装に共通の対応する HTTP メッセージおよび関連するコンソール出力が含まれています。 簡潔にするために、関連の少ない HTTP ヘッダーは省略されています。 レコードの URI は、基本の組織アドレスおよび Common Data Service サーバーが割り当てるレコードの ID によって異なります。  
  
<a name="bkmk_sampleData"></a>
   
## <a name="sample-data"></a>サンプル データ

 サンプルはプリンシパル コード セクションを実行する前に、次のレコードを作成します。  
  
|エンティティの種類|クライアントが割り当てたプロパティ|サーバーが割り当てたプロパティ|  
|-----------------|---------------------------------|---------------------------------|  
|<xref:Microsoft.Dynamics.CRM.account>|名前: `Contoso Ltd.` <br />売り上げ: `5000000`<br />電話: `555-0000`<br />説明: `Parent company of Contoso Pharmaceuticals, etc.`|ID: `14e151db-9b4f-e611-80e0-00155da84c08`<br />初期 Etag: `W/"628448"`|  
  
<a name="bkmk_conditionalGet"></a>

## <a name="conditional-get"></a>条件 GET

 このセクションのプログラムでは、クライアントに最新レコードの状態を維持したまま、ネットワーク帯域幅とサーバー処理を最適化するために条件付きの検索を実行する方法を説明します。 詳細: [条件付き検索](perform-conditional-operations-using-web-api.md#bkmk_DetectIfChanged)  
  
1.  アカウント レコードが作成された時に返された初期 ETag 値で識別されたアカウント `Contoso Ltd.` は、現在のバージョンと一致*しない*場合のみ、取得し直す必要があります。 この条件は、`If-None-Match` ヘッダーで表されます。  
  
 **要求**  
  
    ```http  
    GET http://[Organization URI]/api/data/v9.0/accounts(14e151db-9b4f-e611-80e0-00155da84c08)?$select=name,revenue,telephone1,description HTTP/1.1  
    If-None-Match: W/"628448"  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0  
    Accept: application/json  
  
    ```  
  
 **応答**  
  
    ```http  
    HTTP/1.1 304 Not Modified  
    ```  
  
 **コンソール出力**  
  
    ```  
    Instance retrieved using ETag: W/"628448"  
    Expected outcome: Entity was not modified so nothing was returned.  
    ```  
  
     応答値 `304 Not Modified` は、現在のレコードは最新のレコードを示しているので、サーバーでは応答本文に要求されたレコードが返され*ません*。  
  
2.  主な電話番号のプロパティを変更することで、取引先企業を更新します。  
  
 **要求**  
  
    ```http
    PUT http://[Organization URI]/api/data/v9.0/accounts(14e151db-9b4f-e611-80e0-00155da84c08)/telephone1 HTTP/1.1  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0  
    Accept: application/json  
    Content-Type: application/json  
    {  
      "value": "555-0001"  
    }  
    ```  
  
 **応答**  
  
    ```http
    HTTP/1.1 204 No Content  
    ```  
  
 **コンソール出力**  
  
    ```  
    Account telephone number updated.  
    ```  
  
3.  元の ETag 値を使用してもう一度、同じ条件 GET 操作をやり直してください。 今回の操作は、サーバー バージョンが要求で指定したバージョンとは異なる (および最新な) ため、要求されたデータを返します。 すべてのレコードを検索するために、応答には現在のバージョンを識別する ETag ヘッダーを含みます。  
  
 **要求**  
  
    ```http
    GET http://[Organization URI]/api/data/v9.0/accounts(14e151db-9b4f-e611-80e0-00155da84c08)?$select=name,revenue,telephone1,description HTTP/1.1  
    If-None-Match: W/"628448"  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0  
    Accept: application/json  
    ```  
  
 **応答**  
  
    ```http
    HTTP/1.1 200 OK  
    Content-Type: application/json; odata.metadata=minimal  
    ETag: W/"628460"  
    {  
      "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#accounts(name,revenue,telephone1,description)/$entity",  
      "@odata.etag":"W/\"628460\"",  
      "name":"Contoso Ltd",  
      "revenue":5000000.0000,  
      "telephone1":"555-0001",  
      "description":"Parent company of Contoso Pharmaceuticals, etc.",  
      "accountid":"14e151db-9b4f-e611-80e0-00155da84c08",  
      "_transactioncurrencyid_value":"0d4ed62e-95f7-e511-80d1-00155da84c03"  
    }  
    ```  
  
 **コンソール出力**  
  
    ```
    Instance retrieved using ETag: W/"628448"  
    {  
      "@odata.context": "http://[Organization URI]/api/data/v9.0/$metadata#accounts(name,revenue,telephone1,description)/$entity",  
      "@odata.etag": "W/\"628460\"",  
      "name": "Contoso Ltd",  
      "revenue": 5000000.0,  
      "telephone1": "555-0001",  
      "description": "Parent company of Contoso Pharmaceuticals, etc.",  
      "accountid": "14e151db-9b4f-e611-80e0-00155da84c08",  
      "_transactioncurrencyid_value": "0d4ed62e-95f7-e511-80d1-00155da84c03"  
    }  
  
    ```  
  
<a name="bkmk_optimisiticConcurrency"></a>
  
## <a name="optimistic-concurrency-on-delete-and-update"></a>削除および更新でのオプティミスティック同時実行
 
 このセクションのプログラムでは、条件付きの削除および更新処理の実行方法を示します。  このような操作の最も一般的な用途は、マルチユーザー環境のレコード処理に対処するオプティミスティック同時実行の実装をすることです。 詳細: [オプティミスティック同時実行の適用](perform-conditional-operations-using-web-api.md#bkmk_Applyoptimisticconcurrency)  
  
1.  元のバージョン (ETag 値) に一致する場合にのみ、元のアカウントを削除し直さなくてはいけません。  この条件は、`If-Match` ヘッダーで表されます。  アカウント レコードは前のセクションで更新され、この操作は失敗したので、その結果としてそのバージョンがサーバーで更新されました。  
  
 **要求**  
  
    ```http
    DELETE http://[Organization URI]/api/data/v9.0/accounts(14e151db-9b4f-e611-80e0-00155da84c08) HTTP/1.1  
    If-Match: W/"628448"  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0  
    Accept: application/json  
    ```  
  
 **応答**  
  
    ```http  
    HTTP/1.1 412 Precondition Failed  
    Content-Type: application/json; odata.metadata=minimal  
    OData-Version: 4.0  
    {  
      "error":{  
        "code":"","message":"The version of the existing record doesn't match the RowVersion property provided.", . . .  
        }  
    }  
    ```  
  
 **コンソール出力**  
  
    ```  
    Expected Error: The version of the existing record doesn't match the property provided.  
            Account not deleted using ETag 'W/"628448"', status code: '412'.  
    ```  
  
2.  元の ETag 値 に一致する場合にのみ、アカウントを更新し直さなくてはいけません。  もう一度、この条件は `If-Match` ヘッダーで表され、同じ理由で操作が失敗します。  
  
 **要求**  
  
    ```http  
    PATCH http://[Organization URI]/api/data/v9.0/accounts(14e151db-9b4f-e611-80e0-00155da84c08) HTTP/1.1  
    If-Match: W/"628448"  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0  
    Accept: application/json  
    Content-Type: application/json; charset=utf-8  
    {  
      "telephone1": "555-0002",  
      "revenue": 6000000  
    }    
    ```  
  
 **応答**  
  
    ```http  
    HTTP/1.1 412 Precondition Failed  
    Content-Type: application/json; odata.metadata=minimal  
    OData-Version: 4.0  
    {  
      "error":{  
        "code":"","message":"The version of the existing record doesn't match the RowVersion property provided.", . . .   
      }  
    }    
    ```  
  
 **コンソール出力**  
  
    ```  
    Expected Error: The version of the existing record doesn't match the property provided.  
            Account not updated using ETag 'W/"628448"', status code: '412'.  
    ```  
  
3.  更新し直さなくてはいけませんが、代わりに、前のセクションで検索した最後のレコードから取得した現在の ETag 値を使用します。  
  
 **要求**  
  
    ```http
    PATCH http://[Organization URI]/api/data/v9.0/accounts(14e151db-9b4f-e611-80e0-00155da84c08) HTTP/1.1  
    If-Match: W/"628460"  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0  
    Accept: application/json  
    {  
      "telephone1": "555-0003",  
      "revenue": 6000000  
    }  
    ```  
  
 **応答**  
  
    ```http
    HTTP/1.1 204 No Content  
    ```  
  
 **コンソール出力**  
  
    ```  
    Account successfully updated using ETag: W/"628460", status code: '204'.  
    ```  
  
4.  最新取引先企業の状態の取得と出力に成功した更新を確認します。  これには、基本的な GET 要求を使用します。  
  
 **要求**  
  
    ```http 
    GET http://[Organization URI]/api/data/v9.0/accounts(14e151db-9b4f-e611-80e0-00155da84c08)?$select=name,revenue,telephone1,description HTTP/1.1  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0  
    Accept: application/json  
    ```  
  
 **応答**  
  
    ```http
    HTTP/1.1 200 OK  
    Content-Type: application/json; odata.metadata=minimal  
    ETag: W/"628461"  
    OData-Version: 4.0  
    {  
      "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#accounts(name,revenue,telephone1,description)/$entity",  
      "@odata.etag":"W/\"628461\"",  
      "name":"Contoso Ltd",  
      "revenue":6000000.0000,  
      "telephone1":"555-0003",  
      "description":"Parent company of Contoso Pharmaceuticals, etc.",  
      "accountid":"14e151db-9b4f-e611-80e0-00155da84c08",  
      "_transactioncurrencyid_value":"0d4ed62e-95f7-e511-80d1-00155da84c03"  
    }  
    ```  
  
 **コンソール出力**  
  
    ```
    {  
      "@odata.context": "http://[Organization URI]/api/data/v9.0/$metadata#accounts(name,revenue,telephone1,description)/$entity",  
      "@odata.etag": "W/\"628461\"",  
      "name": "Contoso Ltd",  
      "revenue": 6000000.0,  
      "telephone1": "555-0003",  
      "description": "Parent company of Contoso Pharmaceuticals, etc.",  
      "accountid": "14e151db-9b4f-e611-80e0-00155da84c08",  
      "_transactioncurrencyid_value": "0d4ed62e-95f7-e511-80d1-00155da84c03"  
    }  
    ```  
  
<a name="bkmk_controllingUpsert"></a>

## <a name="controlling-upsert-operations"></a>upsert 操作の制御

 このセクションのプログラムでは、更新操作のみまたは挿入操作のみの制限付き upsert 操作を実行できる条件付き `PATCH` 操作の実行方法を示します。 詳細: [upsert 操作の制限](perform-conditional-operations-using-web-api.md#bkmk_limitUpsertOperations)  
  
1.  更新せずに、この取引先企業の主な電話番号と売り上げプロパティを挿入するようにしてください。 `*` を値に持つ `If-None-Match` ヘッダーは、この upsert 条件を表します。 この操作は、(同時に他のユーザーまたはプロセスによって削除されない限り) この取引先企業レコードがサーバーに存在しているため、失敗します。  
  
 **要求**  
  
    ```http
    PATCH http://[Organization URI]/api/data/v9.0/accounts(14e151db-9b4f-e611-80e0-00155da84c08) HTTP/1.1  
    If-None-Match: *  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0  
    Accept: application/json  
    Content-Type: application/json; charset=utf-8  
    {  
      "telephone1": "555-0004",  
      "revenue": 7500000  
    }  
    ```  
  
 **応答**  
  
    ```http
    HTTP/1.1 412 Precondition Failed  
    Content-Type: application/json; odata.metadata=minimal  
    OData-Version: 4.0  
    {  
      "error":{  
        "code":"","message":"A record with matching key values already exists.", . . .  
      }  
    }  
    ```  
  
 **コンソール出力**  
  
    ```   
    Expected Error: A record with matching key values already exists.  
            Account not updated using ETag 'W/"628448", status code: '412'.    
    ```  
  
2.  作成せずに同じ更新操作を実行します。 これを達成するためには、`*`を値に持つ条件 `If-Match` ヘッダーが使用されます。  この操作により、レコードがサーバー上に存在し、成功します。  
  
 **要求**  
  
    ```http
    PATCH http://[Organization URI]/api/data/v9.0/accounts(14e151db-9b4f-e611-80e0-00155da84c08) HTTP/1.1  
    If-Match: *  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0  
    Accept: application/json  
    Content-Type: application/json; charset=utf-8  
    {  
      "telephone1": "555-0005",  
      "revenue": 7500000  
    }  
    ```  
  
 **応答**  
  
    ```http
    HTTP/1.1 204 No Content  
    ```  
  
 **コンソール出力**  
  
    ```  
    Account updated using If-Match '*'  
    ```  
  
3.  基本の `GET` 要求と最新取引先企業の状態を取得して出力します。 取引先企業レコードの新しく更新したバージョンを反映するよう返された ETag 値が変更することに注意してください。  
  
 **要求**  
  
    ```http  
    GET http://[Organization URI]/api/data/v9.0/accounts(14e151db-9b4f-e611-80e0-00155da84c08)?$select=name,revenue,telephone1,description HTTP/1.1  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0  
    Accept: application/json    
    ```  
  
 **応答**  
  
    ```http  
    HTTP/1.1 200 OK  
    Content-Type: application/json; odata.metadata=minimal  
    ETag: W/"628463"  
    OData-Version: 4.0  
    {  
      "@odata.context":"http://[Organization URI]/api/data/v9.0/$metadata#accounts(name,revenue,telephone1,description)/$entity",  
      "@odata.etag":"W/\"628463\"",  
      "name":"Contoso Ltd","revenue":7500000.0000,  
      "telephone1":"555-0005",  
      "description":"Parent company of Contoso Pharmaceuticals, etc.",  
      "accountid":"14e151db-9b4f-e611-80e0-00155da84c08",  
      "_transactioncurrencyid_value":"0d4ed62e-95f7-e511-80d1-00155da84c03"  
    }    
    ```  
  
 **コンソール出力**  
  
    ```http    
    {  
      "@odata.context": "http://[Organization URI]/api/data/v9.0/$metadata#accounts(name,revenue,telephone1,description)/$entity",  
      "@odata.etag": "W/\"628463\"",  
      "name": "Contoso Ltd",  
      "revenue": 7500000.0,  
      "telephone1": "555-0005",  
      "description": "Parent company of Contoso Pharmaceuticals, etc.",  
      "accountid": "14e151db-9b4f-e611-80e0-00155da84c08",  
      "_transactioncurrencyid_value": "0d4ed62e-95f7-e511-80d1-00155da84c03"  
    }    
    ```  
  
4.  基本の `DELETE` と取引先企業を削除します。  
  
 **要求**  
  
    ```http    
    DELETE http://[Organization URI]/api/data/v9.0/accounts(14e151db-9b4f-e611-80e0-00155da84c08) HTTP/1.1  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0  
    Accept: application/json    
    ```  
  
 **応答**  
  
    ```http
    HTTP/1.1 204 No Content  
    ```  
  
 **コンソール出力**  
  
    ```  
    Account was deleted.  
    ```  
  
5.  手順 2 と同様に、存在する場合は取引先企業を更新してください。  もう一度、この条件は `*` を値に持つ `If-Match`ヘッダーで表されます。  この操作は、このレコードが削除されたので失敗します。 ただし、この `If-Match` ヘッダーが欠落した場合、実行する基本の upsert 操作で正常に新しいレコードを作成する必要があります。  
  
 **要求**  
  
    ```http  
    PATCH http://[Organization URI]/api/data/v9.0/accounts(14e151db-9b4f-e611-80e0-00155da84c08) HTTP/1.1  
    If-Match: *  
    OData-MaxVersion: 4.0  
    OData-Version: 4.0  
    Accept: application/json  
    Content-Type: application/json; charset=utf-8  
    {  
      "telephone1": "555-0006",  
      "revenue": 7500000  
    }    
    ```  
  
 **応答**  
  
    ```http    
    HTTP/1.1 404 Not Found  
    Content-Type: application/json; odata.metadata=minimal  
    OData-Version: 4.0  
    {  
      "error":{  
        "code":"","message":"account With Id = 14e151db-9b4f-e611-80e0-00155da84c08 Does Not Exist", . . .  
      }  
    }    
    ```  
  
 **コンソール出力**  
  
    ```    
    Expected Error: Account with Id = 14e151db-9b4f-e611-80e0-00155da84c08 does not exist.  
    Account not updated because it does not exist, status code: '404'.    
    ```  
  
 1 つの取引先企業レコードが 手順 4 で既に削除されたので、サンプル データをクリーンアップする必要はありません。  
  
### <a name="see-also"></a>関連項目

[Common Data Service Web API の使用](overview.md)<br />
[Web API を使用する条件付き演算を実行する](perform-conditional-operations-using-web-api.md)<br />
[Web API 条件付き演算サンプル (C#)](samples/conditional-operations-csharp.md)   

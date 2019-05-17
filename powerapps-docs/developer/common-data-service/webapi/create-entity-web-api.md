---
title: Web API を使用したエンティティの作成 (Common Data Service) | Microsoft Docs
description: データを送信する POST 要求の作成方法を読み取り、Web API を使用して Common Data Service 上でエンティティを作成する
ms.custom: ''
ms.date: 10/31/2018
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 244259ca-2fbc-4fd4-9a74-6166e6683355
caps.latest.revision: 51
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

# <a name="create-an-entity-using-the-web-api"></a>Web API を使用してエンティティを作成する

POST 要求を使用してエンティティを作成するデータを送信します。 "ディープ挿入" を使用して 1 回の操作で複数の関連するエンティティを作成できます。 また、@odata.bind 注釈を使用して既存のエンティティに新しいエンティティを関連付けるために値を設定する方法を知る必要があります。  

> [!NOTE]
> Web API を使用したエンティティ メタデータの作成および更新方法の詳細については、[Web APIを使用してエンティティ定義を作成および更新](create-update-entity-definitions-using-web-api.md)を参照してください。

<a name="bkmk_basicCreate"></a>

## <a name="basic-create"></a>基本的な作成

 この例では、新しい取引先企業エンティティを作成します。 応答 `OData-EntityId` ヘッダーには、作成したエンティティの URI が含まれています。

 **要求**

```http

POST [Organization URI]/api/data/v9.0/accounts HTTP/1.1
Content-Type: application/json; charset=utf-8
OData-MaxVersion: 4.0
OData-Version: 4.0
Accept: application/json

{
    "name": "Sample Account",
    "creditonhold": false,
    "address1_latitude": 47.639583,
    "description": "This is the description of the sample account",
    "revenue": 5000000,
    "accountcategorycode": 1
}
```

 **応答**

```http

HTTP/1.1 204 No Content
OData-Version: 4.0
OData-EntityId: [Organization URI]/api/data/v9.0/accounts(7eb682f1-ca75-e511-80d4-00155d2a68d1)

```

新しいエンティティを作成するには、有効なプロパティの名前と型を識別する必要があります。 すべてのシステム エンティティと属性の詳細については、[エンティティの参照について](../reference/about-entity-reference.md) にある、そのエンティティのトピックでこの情報を見つけることができます。 ユーザー定義エンティティまたは属性については、[CSDL $metadata ドキュメント](web-api-types-operations.md#csdl-metadata-document) にあるそのエンティティの定義を参照してください。 詳細: [エンティティの種類](web-api-types-operations.md#entity-types)

<a name="bkmk_CreateRelated"></a>

## <a name="create-related-entities-in-one-operation"></a>1 回の操作で関連するエンティティを作成する

 ナビゲーション プロパティの値として定義することで、相互に関連するエンティティを作成することができます。 これを*ディープ挿入*と言います。

 基本的な作製と同様に、応答 `OData-EntityId` ヘッダーには、作製したエンティティの URI が含まれています。 作成された関連するエンティティの URI は返されません。

 たとえば、`Account` エンティティ セットに投稿された次の要求本文は、アカウントの作成のコンテキストで合計 4 つの新しいエンティティを作成します。

- 取引先担当者が作成されます。これは、取引先担当者が単一値のナビゲーション プロパティ `primarycontactid` のオブジェクト プロパティとして定義されているためです。

- 営業案件が作成されます。これは、営業案件が、コレクション値を持つナビゲーション プロパティ `opportunity_customer_accounts` の値に設定された配列内のオブジェクトとして定義されているためです。

- タスクが作成されます。これは、タスクが、コレクション値を持つナビゲーション プロパティ `Opportunity_Tasks` の値に設定された配列内のオブジェクトとして定義されているためです。

**要求**

```http
POST [Organization URI]/api/data/v9.0/accounts HTTP/1.1
Content-Type: application/json; charset=utf-8
OData-MaxVersion: 4.0
OData-Version: 4.0
Accept: application/json

{
 "name": "Sample Account",
 "primarycontactid":
 {
     "firstname": "John",
     "lastname": "Smith"
 },
 "opportunity_customer_accounts":
 [
  {
      "name": "Opportunity associated to Sample Account",
      "Opportunity_Tasks":
      [
       { "subject": "Task associated to opportunity" }
      ]
  }
 ]
}

```

**応答**

 ```http

HTTP/1.1 204 No Content
OData-Version: 4.0
OData-EntityId: [Organization URI]/api/data/v9.0/accounts(3c6e4b5f-86f6-e411-80dd-00155d2a68cb)

```

<a name="bkmk_associateOnCreate"></a>

## <a name="associate-entities-on-create"></a>作成時にエンティティを関連付ける

 新しいエンティティを作成するときに、新しいエンティティを既存のエンティティに関連付けるには、`@odata.bind` 注釈を使用して、単一値ナビゲーション プロパティの値を設定する必要があります。

 取引先企業エンティティ セットに投稿された次の要求本文は、00000000-0000-0000-0000-000000000001 の値を持つ `contactid` を使用して、既存の取引先担当者に関連付けられた新しい取引先企業を作成します。

**要求**

```http

POST [Organization URI]/api/data/v9.0/accounts HTTP/1.1
Content-Type: application/json; charset=utf-8
OData-MaxVersion: 4.0
OData-Version: 4.0
Accept: application/json

{
"name":"Sample Account",
"primarycontactid@odata.bind":"/contacts(00000000-0000-0000-0000-000000000001)"
}

```

**応答**

```http

HTTP/1.1 204 No Content
OData-Version: 4.0
OData-EntityId: [Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-0000-000000000002)

```

> [!NOTE]
> コレクション値を持つナビゲーション プロパティを使用してこの方法でエンティティを関連付けることは、Web API ではサポートされていません。

<a name="bkmk_SuppressDuplicateDetection"></a>

## <a name="check-for-duplicate-records"></a>重複レコードの確認


既定では、Web API を使用したレコードの作成時には重複データ検出が実行されません。 重複データ検出を有効にするには、POST 要求に `MSCRM.SuppressDuplicateDetection: false` ヘッダを含める必要があります。 重複データ検出は、組織が重複データ検出を有効にし、エンティティが重複データ検出に対応しており、アクティブな重複データ検出ルールが適用されている場合にのみ適用されます。 詳細: [コードを使用した重複データの検出](../detect-duplicate-data-with-code.md)

作成操作中に重複データを検出する方法の詳細については、「[Web API を使用した重複データの検出](manage-duplicate-detection-create-update.md#bkmk_create)」を参照してください。

<a name="bkmk_initializefrom"></a>

## <a name="create-a-new-entity-from-another-entity"></a>別のエンティティから新しいエンティティを作成する

`InitializeFrom function` を使用して、レコードが属するエンティティ間にマッピングが存在する既存のレコードのコンテキスト内にレコードを新規作成します。 

次の例は、c65127ed-2097-e711-80eb-00155db75426 と等しい値の `accountid` を持つ取引先企業エンティティの既存のレコードの属性値を使用して、取引先企業レコードを作成する方法を示します。

**要求**

```http
GET [Organization URI]/api/data/v9.0/InitializeFrom(EntityMoniker=@p1,TargetEntityName=@p2,TargetFieldType=@p3)?@p1={'@odata.id':'accounts(c65127ed-2097-e711-80eb-00155db75426)'}&@p2='account'&@p3=Microsoft.Dynamics.CRM.TargetFieldType'ValidForCreate' HTTP/1.1
If-None-Match: null
OData-Version: 4.0
OData-MaxVersion: 4.0
Content-Type: application/json
Accept: application/json
```

**応答**

```json
{
        "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#accounts/$entity",
        "@odata.type": "#Microsoft.Dynamics.CRM.account",
        "parentaccountid@odata.bind": "accounts(c65127ed-2097-e711-80eb-00155db75426)",
        "transactioncurrencyid@odata.bind": "transactioncurrencies(732e87e1-1d96-e711-80e4-00155db75426)",
        "address1_line1":"123 Maple St.",
        "address1_city":"Seattle",
        "address1_country":"United States of America"
}
```

InitializeFrom 要求から受け取った反応は、ソース エンティティとターゲット エンティティ間でマッピングされた属性値と親レコードの GUID で構成されます。 エンティティの関連付けを持つエンティティ間の属性マッピングは、違うエンティティ セットでは異なりカスタマイズ可能であるため、InitializeFrom 関数要求からの応答は違うエンティティおよび組織では異なる可能性があります。 この応答が新しいレコードの作成要求のボディに渡されるとき、これらの属性値は新しいレコードで複製されます。 カスタム マッピングした属性の値も、プロセス中に新しいレコード内のセットを取得します。

> [!NOTE]
> 二つのエンティティをマッピング可能かどうか判断するには、このクエリを使用します。  
GET [組織 URI]/api/data/v9.0/entitymaps?$select=sourceentityname,targetentityname&$orderby=sourceentityname

また、以下の例に示すように、他の属性値を JSON 要求のボディ内に追加することにより、新しいレコードのために他の属性値をセットしたり修正したりすることができます。

```http
POST [Organization URI]/api/data/v9.0/accounts HTTP/1.1
Content-Type: application/json; charset=utf-8
OData-MaxVersion: 4.0
OData-Version: 4.0
Accept: application/json

    {
        "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#accounts/$entity",
        "@odata.type": "#Microsoft.Dynamics.CRM.account",
        "parentaccountid@odata.bind": "accounts(c65127ed-2097-e711-80eb-00155db75426)",
        "transactioncurrencyid@odata.bind": "transactioncurrencies(732e87e1-1d96-e711-80e4-00155db75426)",
        "name":"Contoso Ltd",
        "numberofemployees":"200",
        "address1_line1":"100 Maple St.",
        "address1_city":"Seattle",
        "address1_country":"United States of America",
        "fax":"73737"
    }
}
```

<a name="bkmk_createWithDataReturned"></a>

## <a name="create-with-data-returned"></a>返されるデータで作成する

作成されたレコードからのデータを 201 (作成済み) の状態で戻すように、POST 要求を構成することができます。  結果を取得するには、要求のヘッダーで `return=representation` の基本設定を使用する必要があります。

どのプロパティが返されるかを制御するには、`$select` クエリ オプションを URL に、そしてエンティティ セットに追加します。  `$expand` クエリ オプションは、使用すると無視されます。

エンティティがこのように作成されると、作成されたレコードへの URL を含む `OData-EntityId` ヘッダーは返されません。

この例では、新しい取引先企業エンティティを作成し、応答で必要なデータを返します。

**要求**

 ```http

POST [Organization URI]/api/data/v9.0/accounts?$select=name,creditonhold,address1_latitude,description,revenue,accountcategorycode,createdon HTTP/1.1
OData-MaxVersion: 4.0
OData-Version: 4.0
Accept: application/json
Content-Type: application/json; charset=utf-8
Prefer: return=representation

{
    "name": "Sample Account",
    "creditonhold": false,
    "address1_latitude": 47.639583,
    "description": "This is the description of the sample account",
    "revenue": 5000000,
    "accountcategorycode": 1
}

```

**応答**

```http

HTTP/1.1 201 Created
Content-Type: application/json; odata.metadata=minimal
Preference-Applied: return=representation
OData-Version: 4.0

{
    "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#accounts/$entity",
    "@odata.etag": "W/\"536530\"",
    "accountid": "d6f193fc-ce85-e611-80d8-00155d2a68de",
    "accountcategorycode": 1,
    "description": "This is the description of the sample account",
    "address1_latitude": 47.63958,
    "creditonhold": false,
    "name": "Sample Account",
    "createdon": "2016-09-28T22:57:53Z",
    "revenue": 5000000.0000,
    "_transactioncurrencyid_value": "048dddaa-6f7f-e611-80d3-00155db5e0b6"
}

```

### <a name="see-also"></a>関連項目

[Web API 基本操作のサンプル (C#)](samples/basic-operations-csharp.md)<br />
[Web API 基本操作のサンプル (クライアント側の JavaScript)](samples/basic-operations-client-side-javascript.md)<br />
<xref href="Microsoft.Dynamics.CRM.InitializeFrom?text=InitializeFrom Function" />  
[Web API を使用して演算を実行する](perform-operations-web-api.md)<br />
[HTTP 要求の作成とエラーの処理](compose-http-requests-handle-errors.md)<br />
[Web API を使用したクエリ データ](query-data-web-api.md)<br />
[Web API を使用してエンティティを取得する](retrieve-entity-using-web-api.md)<br />
[Web API を使用したエンティティの更新と削除](update-delete-entities-using-web-api.md)<br />
[Web API を使用したエンティティの関連付けと関連付け解除](associate-disassociate-entities-using-web-api.md)<br />
[Web API 関数の使用](use-web-api-functions.md)<br />
[Web API アクションの使用](use-web-api-actions.md)<br />
[Web API を使用してバッチ操作を実行する](execute-batch-operations-using-web-api.md)<br />
[Web API を使用して別のユーザーを偽装する](impersonate-another-user-web-api.md)<br />
[Web API を使用する条件付き演算を実行する](perform-conditional-operations-using-web-api.md)<br />

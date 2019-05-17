---
title: Web API を使用した重複データの検出 (Common Data Service) | Microsoft Docs
description: MSCRM.SuppressDuplicateDetection ヘッダーおよび Common Data Service Web API を使用して重複データを検出する方法の説明
ms.custom: ''
ms.date: 10/31/2018
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: AE107774-4545-44B4-94C8-A0271EFA7876
caps.latest.revision: 11
author: susikka
ms.author: susikka
manager: shujoshi
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="detect-duplicate-data-using-the-web-api"></a>Web API を使用した重複データの検出

Common Data Service Web API を使用すると、データの整合性を維持するために、既存のレコードの重複レコードを検出できます。 コードを使用した重複データの検出の詳細については、[コードを使用した重複データの検出](../detect-duplicate-data-with-code.md) を参照してください。 

## <a name="detect-duplicates-during-create-operation"></a>作成操作中に重複データを検出する

`POST` 要求中に `MSCRM.SuppressDuplicateDetection` ヘッダーを使用して、既存のレコードの重複レコードの作成を検出します。 `MSCRM.SuppressDuplicateDetection` ヘッダーに割り当てられる値は、作成または更新操作を完了できるかどうかを決定します。

- `true` – 重複データが検出された場合にレコードを作成または更新します。
- `false` – 重複データが検出された場合にレコードを作成または更新しません。

> [!NOTE]
> `CalculateMatchCodeSynchronously` オプション パラメーターを渡す必要はありません。 重複の検出に使用される一致コードは、このパラメーターに渡される値に関係なく同期的に計算されます。

基本設定ヘッダー `MSCRM.SuppressDuplicateDetection` を使用して、 Web API 要求でその値を `false` に設定します。


> [!NOTE]
> 適切な重複データ検出ルールが存在することを確認します。 Common Data Service には、取引先企業、取引先担当者、および潜在顧客のための既定の重複データ検出ルールが含まれますが、他のレコードの種類のための既定のルールは含まれません。 システムが他のレコードの種類の重複データを検出するようにするには、新しいルールを作成する必要があります。 <br/>- UI を使用して重複データの検出ルールを作成する方法については、[データを整理するための重複データ検出ルールの設定](/dynamics365/customer-engagement/admin/set-up-duplicate-detection-rules-keep-data-clean) を参照してください。<br/>- コードを使用して重複データ検出ルールを作成する方法の詳細については、[重複ルール エンティティを参照します](../duplicaterule-entities.md) 



<a name="bkmk_create"></a>

###  <a name="example-detect-duplicates-during-create-operation-using-the-web-api"></a>例: Web API を使用した、作成操作中の重複データ検出

次の例は、Web API 要求で `MSCRM.SuppressDuplicateDetection` ヘッダーを使用して、`Create` および `Update` 操作中に重複データを検出する方法を示しています。

**要求**
```http
POST [Organization URI]/org1/api/data/v9.0/leads HTTP/1.1
If-None-Match: null
OData-Version: 4.0
OData-MaxVersion: 4.0
Content-Type: application/json
Accept: application/json
MSCRM.SuppressDuplicateDetection: false

{
    "firstname":"Monte",
    "lastname":"Orton",
    "emailaddress1":"monteorton@example.com"
}
```
同じ `emailaddress1` 属性を持つ潜在顧客レコードが既に存在する場合、次の応答が返されます。

**応答**
```json
HTTP/1.1 500 Internal Server Error  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0

{
    "error": {
        "code": "0x80040333",
        "message": "A record was not created or updated because a duplicate of the current record already exists.",
        "innererror": {
            "message": "A record was not created or updated because a duplicate of the current record already exists.",
            "type": "Microsoft.Crm.CrmException",
            [ Stack Trace and internal exception details ommitted for brevity]
        }
    }
}
```
`MSCRM.SuppressDuplicateDetection` ヘッダーに値 `true` を割り当てて、重複レコードの作成を許可します。

<a name="bkmk_update"></a>

## <a name="detect-duplicates-during-update-operation"></a>更新操作中に重複データを検出する

`PATCH` 要求で `MSCRM.SuppressDuplicateDetection` ヘッダーの値を `false` に設定して、更新操作中の重複レコードの作成を回避します。 既定では、Web API を使用したレコードの更新時には重複データ検出が実行されません。

###  <a name="example-detect-duplicates-during-update-operation-using-the-web-api"></a>例: Web API を使用した、更新プログラム操作中の重複データ検出

次に示す例では、既存のレコードと同じ `emailaddress1` 属性値を含む潜在顧客のエンティティ レコードを更新しようとします。

**要求**
```http
PATCH [Organization URI]/api/data/v9.0/leads(c4567bb6-47a3-e711-811b-e0071b6ac1b1) HTTP/1.1
If-None-Match: null
OData-Version: 4.0
OData-MaxVersion: 4.0
Content-Type: application/json
Accept: application/json
MSCRM.SuppressDuplicateDetection: false

{
    "firstname":"Monte",
    "lastname":"Orton",
    "emailaddress1":"monteorton@example.com"
}
```  

**応答**
```json  
HTTP/1.1 500 Internal Server Error  
Content-Type: application/json; odata.metadata=minimal  
OData-Version: 4.0

{
    "error": {
        "code": "0x80040333",
        "message": "A record was not created or updated because a duplicate of the current record already exists.",
        "innererror": {
            "message": "A record was not created or updated because a duplicate of the current record already exists.",
            "type": "Microsoft.Crm.CrmException",
            [ Stack Trace and internal exception details ommitted for brevity]
        }
    }
}
```

### <a name="see-also"></a>関連項目

[組織サービスを使用して重複データを検出する](../org-service/detect-duplicate-data.md)
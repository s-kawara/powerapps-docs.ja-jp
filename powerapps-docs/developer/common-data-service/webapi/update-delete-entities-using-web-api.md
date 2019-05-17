---
title: Web API を用いたエンティティの更新および削除 (Common Data Service) | Microsoft Docs
description: Web API を使用したエンティティの更新と削除の各操作を実行する方法を説明します。
ms.custom: ''
ms.date: 10/31/2018
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 694889fd-2b85-43a0-97bc-1e760695db31
caps.latest.revision: 17
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
# <a name="update-and-delete-entities-using-the-web-api"></a>Web API を使用したエンティティの更新と削除

データを変更する操作は Web API のコア部分です。 単純な更新と削除に加えて、単一の属性に対して操作を実行して、エンティティの有無に基づいてそのエンティティを更新または挿入する *upsert* 要求を作成できます。  
  
> [!NOTE]
>  エンティティを定義するメタデータは別の形式で更新されます。 詳細:[Web API を使用したモデル エンティティの作成および更新](create-update-entity-definitions-using-web-api.md)  
  
<a name="bkmk_update"></a>

## <a name="basic-update"></a>基本的な更新

更新操作には HTTP 動詞 `PATCH` を使用します。 更新するプロパティが含まれる JSON オブジェクトを、エンティティを表す URI に渡します。 更新が成功した場合、状態 204 の応答が返されます。  
  
 この例は、`accountid` 値 00000000-0000-0000-0000-000000000001 で既存の取引先企業レコードを更新します。  
  
> [!IMPORTANT]
>  エンティティを更新するとき、要求本文には変更するプロパティのみを含めます。 先に取得したエンティティのプロパティを単純に更新して、その JSON を要求に含めることにより、値が同じであっても、各プロパティが更新されます。 これにより、値が変化したことを予期するビジネス ロジックをトリガーすることができる、システム イベントを発生させます。 これにより、プロパティが実際に変更されなかったとき、監査データではプロパティが更新されたように見えます。

> [!NOTE] 
> 属性のメタデータはプロパティ `RequiredLevel` を含みます。 これが `SystemRequired` に設定された場合、これらの属性を null 値に設定することはできません。 詳細: [属性の入力要求レベル](../entity-attribute-metadata.md#attribute-requirement-level)
  
 **要求**

```http
PATCH [Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-0000-000000000001) HTTP/1.1  
Content-Type: application/json  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
  
{  
    "name": "Updated Sample Account ",  
    "creditonhold": true,  
    "address1_latitude": 47.639583,  
    "description": "This is the updated description of the sample account",  
    "revenue": 6000000,  
    "accountcategorycode": 2  
}  
```  
  
 **応答**

```http
HTTP/1.1 204 No Content  
OData-Version: 4.0  
  
```  
  
> [!NOTE]
>  更新時のエンティティの関連付けの詳細については、「[更新時にエンティティを関連付ける](associate-disassociate-entities-using-web-api.md#bkmk_Associateentitiesonupdate)」を参照してください。  
  
<a name="bkmk_updateWithDataReturned"></a>

## <a name="update-with-data-returned"></a>返されるデータでの更新
  
更新するエンティティからデータを取得するには、作成されたレコードからのデータを 200 (OK) の状態で返すよう `PATCH` 要求を作成します。  この結果を取得するには、要求のヘッダーで `return=representation` の基本設定を使用する必要があります。  
  
 どのプロパティが返されるかを制御するには、`$select` クエリ オプションを URL に、そしてエンティティ セットに追加します。  `$expand` クエリ オプションは、使用すると無視されます。  
  
 この例では、取引先企業エンティティを更新し、応答で必要なデータを返します。  
  
 **要求**

```http
PATCH [Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-0000-000000000001)?$select=name,creditonhold,address1_latitude,description,revenue,accountcategorycode,createdon HTTP/1.1  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
Accept: application/json  
Content-Type: application/json; charset=utf-8  
Prefer: return=representation  
  
{"name":"Updated Sample Account"}  
```  
  
 **応答** 
 
```http
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
Preference-Applied: return=representation  
OData-Version: 4.0  
  
{  
    "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#accounts/$entity",  
    "@odata.etag": "W/\"536537\"",  
    "accountid": "00000000-0000-0000-0000-000000000001",  
    "accountcategorycode": 1,  
    "description": "This is the description of the sample account",  
    "address1_latitude": 47.63958,  
    "creditonhold": false,  
    "name": "Updated Sample Account",  
    "createdon": "2016-09-28T23:14:00Z",  
    "revenue": 5000000.0000,  
    "_transactioncurrencyid_value": "048dddaa-6f7f-e611-80d3-00155db5e0b6"  
}  
  
```  
  
<a name="bkmk_updateSingleProperty"></a> 
  
## <a name="update-a-single-property-value"></a>単一のプロパティ値の更新  

単一のプロパティ値のみを更新するときは、エンティティの Uri にプロパティ名が付加された PUT 要求を使用します。  
  
 次の例は、`accountid` 値 00000000-0000-0000-0000-000000000001 で既存の取引先企業エンティティの名前 プロパティを更新します。  
  
 **要求**  

```http
PUT [Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-0000-000000000001)/name HTTP/1.1  
Content-Type: application/json  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
  
{"value": "Updated Sample Account Name"}  
```  
  
 **応答**

```http
HTTP/1.1 204 No Content  
OData-Version: 4.0  
  
```  
  
<a name="bkmk_deleteSingleProperty"></a>

## <a name="delete-a-single-property-value"></a>単一のプロパティ値の削除

単一のプロパティ値を削除するには、エンティティの Uri にプロパティ名が付加された DELETE 要求を使用します。  
  
次の例は、`accountid` 値 00000000-0000-0000-0000-000000000001 で取引先企業エンティティの `description` プロパティの値を削除します。  
  
 **要求**

```http
DELETE [Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-0000-000000000001)/description HTTP/1.1  
Content-Type: application/json  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
```  
  
 **応答**

```http
HTTP/1.1 204 No Content  
OData-Version: 4.0  
  
```  
  
> [!NOTE]
>  これを単一値のナビゲーション プロパティに対して使用して、2 つのエンティティの関連付けを解除することはできません。 代替の方法については、「[エンティティへの参照の削除](associate-disassociate-entities-using-web-api.md#bkmk_Removeareferencetoanentity)」を参照してください。  
  
<a name="bkmk_upsert"></a>

## <a name="upsert-an-entity"></a>エンティティの Upsert

*upsert* 操作は更新とよく似ています。 この操作では `PATCH` 要求が使用され、URI を使用して特定のエンティティが参照されます。 違いは、エンティティが存在しない場合にエンティティが作成されることです。 すでに存在する場合は、そのエンティティが更新されます。 通常、新しいエンティティの作成時に、システムが一意の識別子を割り当てるようにすることができます。 これがベスト プラクティスです。 特定の `id` 値でレコードを作成する必要がある場合は、`upsert` がこれを行う方法を提供します。 これは、異なるシステムのデータを同期している状態で有益なことがあります。  
  
`upsert` を操作する場合もありますが、既定である可能性のあるアクションである、作成または更新のいずれかを止める方がいいでしょう。      `If-Match` または `If-None-Match` の追加によってこれを実行できます。 詳細については、「[upsert 操作の制限](perform-conditional-operations-using-web-api.md#bkmk_limitUpsertOperations)」を参照してください。  
  
<a name="bkmk_delete"></a>
  
## <a name="basic-delete"></a>基本的な削除

削除操作は非常に単純です。 削除するエンティティの URI に対して、DELETE 動詞を使用します。 この例のメッセージは、主キーの `accountid` 値が00000000-0000-0000-0000-000000000001 に等しい取引先企業エンティティを削除します。  
  
 **要求**

```http
DELETE [Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-0000-000000000001) HTTP/1.1  
Content-Type: application/json  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
```  
  
 **応答**

 このエンティティが存在する場合は、削除に成功したことを示す状態が 204 の通常応答を受け取ります。 エンティティが存在しなかった場合は、状態が 404 の応答を受け取ります。  
  
```http
HTTP/1.1 204 No Content  
OData-Version: 4.0  
```  

<a name="bkmk_duplicate"></a>

## <a name="check-for-duplicate-records"></a>重複レコードの確認

<!-- TODO:
By default, duplicate detection is suppressed when you are updating records using the Web API. You must include the `MSCRM.SuppressDuplicateDetection: false` header with your PATCH request to enable duplicate detection . Duplicate detection only applies when the organization has enabled duplicate detection, the entity is enabled for duplicate detection, and there are active duplicate detection rules being applied. For more information, see [Detect duplicate data for developers](../detect-duplicate-data-for-developers.md). -->

更新操作中に重複データを検出する方法の詳細については、「[Web API を使用した、更新操作中の重複データ検出](manage-duplicate-detection-create-update.md#bkmk_update)」を参照してください。

### <a name="see-also"></a>関連項目

[Web API 基本操作のサンプル (C#)](samples/basic-operations-csharp.md)<br />
[Web API 基本操作のサンプル (クライアント側の JavaScript)](samples/basic-operations-client-side-javascript.md)<br />
[Web API を使用して演算を実行する](perform-operations-web-api.md)<br />
[HTTP 要求の作成とエラーの処理](compose-http-requests-handle-errors.md)<br />
[Web API を使用したクエリ データ](query-data-web-api.md)<br />
[Web API を使用してエンティティを作成する](create-entity-web-api.md)<br />
[Web API を使用してエンティティを取得する](retrieve-entity-using-web-api.md)<br />
[Web API を使用したエンティティの関連付けと関連付け解除](associate-disassociate-entities-using-web-api.md)<br />
[Web API 関数の使用](use-web-api-functions.md)<br />
[Web API アクションの使用](use-web-api-actions.md)<br />
[Web API を使用してバッチ操作を実行する](execute-batch-operations-using-web-api.md)<br />
[Web API を使用して別のユーザーを偽装する](impersonate-another-user-web-api.md)<br />
[Web API を使用する条件付き演算を実行する](perform-conditional-operations-using-web-api.md)

---
title: Web API (Common Data Service) を使用して別のユーザーを偽装する | Microsoft Docs
description: 偽装は、別の Common Data Service ユーザーに代わってビジネス ロジック (コード) を実行し、偽装されるユーザーの適切なロール ベースとオブジェクトベースのセキュリティを使用して任意の機能やサービスを提供するために使用されます。 Web API を使用して別の Common Data Service ユーザーを偽装する方法について説明します。
ms.custom: ''
ms.date: 03/18/2019
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 74d07683-63ff-4d05-a434-dcfd44cd634d
caps.latest.revision: 9
author: brandonsimons
ms.author: jdaly
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

<!-- TOD0: The higher level topic [Impersonate another user](../impersonate-another-user.md) should include all generic concepts.
This topic should only cover the Web API specific details -->


# <a name="impersonate-another-user-using-the-web-api"></a>Web API を使用して別のユーザーを偽装する

コードで別のユーザーに代わって操作を実行する必要がある場合もあります。 コードを実行しているシステム アカウントに必要な権限がある場合は、他のユーザーに代わって操作を実行できます。  
  
<a name="bkmk_Requirementsforimpersonation"></a>

## <a name="requirements-for-impersonation"></a>偽装の要件

偽装は、別の Common Data Service ユーザーに代わってビジネス ロジック (コード) を実行し、偽装されるユーザーの適切なロール ベースとオブジェクトベースのセキュリティを使用して任意の機能やサービスを提供するために使用されます。 偽装が必要なのは、ワークフローやユーザー定義の ISV ソリューションなどで、Common Data Service ユーザーに代わってさまざまなクライアントやサービスによって Common Data Service Web サービスを呼び出すことができるためです。 偽装には 2 つの異なるユーザー アカウントが含まれ、1つのユーザー アカウント (A) が、もう一方のユーザー アカウント (B) に代わって何らかのタスクを行うコードの実行時に使用されます。  
  
ユーザー アカウント (A) は、代理人セキュリティ ロールに含まれる `prvActOnBehalfOfAnotherUser` 特権を必要とします。 データ変更に使用される実際の特権のセットは、代理人の役割のユーザーが所有する特権と、偽装されたユーザーが所有する特権との共通部分です。 つまり、ユーザー (A) と偽装されたユーザー (B) が操作に必要な特権を持つ場合にのみ、ユーザー (A) は何かを実行できます。  
  
<a name="bkmk_Howtoimpersonateauser"></a>

## <a name="how-to-impersonate-a-user"></a>ユーザーを偽装する方法

ユーザーを偽装することができる 2 つの方法がありますが、両方とも関連するユーザー ID でヘッダーを渡すことにより可能になります。

 1. **希望する方法:** Azure Active Directory (AAD) オブジェクト ID に基づき、その値を `CallerObjectId` ヘッダーと共に渡すことにより、ユーザーを偽装します。
2. **従来:** システム ユーザー ID に基づきユーザーを偽装するには、関連するグリッド値と共に `MSCRMCallerID` を活用することができます。

 この例では、Azure Active Directory オブジェクト ID `e39c5d16-675b-48d1-8e67-667427e9c084` を持つユーザのために新しい取引先企業エンティティが作成されます。   
  
 **要求**  
```http 
POST [Organization URI]/api/data/v9.0/accounts HTTP/1.1  
CallerObjectId: e39c5d16-675b-48d1-8e67-667427e9c084  
Accept: application/json  
Content-Type: application/json; charset=utf-8  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
  
{"name":"Sample Account created using impersonation"}  
```  
  
 **応答**  
```http 
HTTP/1.1 204 No Content  
OData-Version: 4.0  
OData-EntityId: [Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-000000000003)  
```  
  
<a name="bkmk_Determinetheactualuser"></a>

## <a name="determine-the-actual-user"></a>実際のユーザーを確認する

偽装を使用してエンティティの作成などの操作を実行する場合、`createdonbehalfby` という単一値ナビゲーション プロパティを含むレコードを照会することによって、実際に操作を実行したユーザーを見つけることができます。 エンティティを更新する操作には、対応する modifiedonbehalfby 単一値ナビゲーション プロパティを使用できます。  
  
 **要求**

```http 
GET [Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-000000000003)?$select=name&$expand=createdby($select=fullname),createdonbehalfby($select=fullname),owninguser($select=fullname) HTTP/1.1   
Accept: application/json  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
```  
  
 **応答**  
```http 
HTTP/1.1 200 OK  
Content-Type: application/json; odata.metadata=minimal  
ETag: W/"506868"  
  
{
  "@odata.context": "[Organization URI]/api/data/v9.0/$metadata#accounts(name,createdby(fullname,azureactivedirectoryobjectid),createdonbehalfby(fullname,azureactivedirectoryobjectid),owninguser(fullname,azureactivedirectoryobjectid))/$entity",
  "@odata.etag": "W/\"2751197\"",
  "name": "Sample Account created using impersonation",
  "accountid": "00000000-0000-0000-000000000003",
  "createdby": {
    "@odata.etag": "W/\"2632435\"",
    "fullname": "Impersonated User",
    "azureactivedirectoryobjectid": "e39c5d16-675b-48d1-8e67-667427e9c084",
    "systemuserid": "75df116d-d9da-e711-a94b-000d3a34ed47",
    "ownerid": "75df116d-d9da-e711-a94b-000d3a34ed47"
  },
  "createdonbehalfby": {
    "@odata.etag": "W/\"2632445\"",
    "fullname": "Actual User",
    "azureactivedirectoryobjectid": "3d8bed3e-79a3-47c8-80cf-269869b2e9f0",
    "systemuserid": "278742b0-1e61-4fb5-84ef-c7de308c19e2",
    "ownerid": "278742b0-1e61-4fb5-84ef-c7de308c19e2"
  },
  "owninguser": {
    "@odata.etag": "W/\"2632435\"",
    "fullname": "Impersonated User",
    "azureactivedirectoryobjectid": "e39c5d16-675b-48d1-8e67-667427e9c084",
    "systemuserid": "75df116d-d9da-e711-a94b-000d3a34ed47",
    "ownerid": "75df116d-d9da-e711-a94b-000d3a34ed47"
  }
}
```  
  
### <a name="see-also"></a>関連項目

[もう一方のユーザーの偽装](../impersonate-another-user.md)<br />
[組織サービスを使用して別のユーザーを偽装する](../impersonate-another-user.md#impersonate-another-user-using-the-organization-service)<br />
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
[Web API を使用する条件付き演算を実行する](perform-conditional-operations-using-web-api.md)

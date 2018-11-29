---
title: Web API 使用したエンティティの関連付けと関連付け解除 (アプリ用 Common Data Service) | Microsoft Docs
description: Web API を使用してコレクション値のナビゲーション プロパティへ参照を追加、参照を削除、既存の参照を変更する方法について説明します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: ad4e4eac-117a-4958-9df0-b7353305b0c7
caps.latest.revision: 13
author: brandonsimons
ms.author: jdaly
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="associate-and-disassociate-entities-using-the-web-api"></a>Web API を使用したエンティティの関連付けと関連付け解除

エンティティの関連付けと関連付け解除に使用できる方法はいくつかあります。 どの方法を適用するかは、エンティティを作成または更新するかどうか、参照先エンティティまたは参照元エンティティのコンテキストのいずれで動作しているかにより異なります。  

<a name="bkmk_Addareferencetoacollection"></a>

## <a name="add-a-reference-to-a-collection-valued-navigation-property"></a>コレクション値ナビゲーション プロパティへの参照の追加

 次の例は、`00000000-0000-0000-0000-000000000002` という `accountid` 値を含むアカウント エンティティのコレクション値 `opportunity_customer_accounts` ナビゲーション プロパティに、`00000000-0000-0000-0000-000000000001` という `opportunityid` 値と既存の営業案件エンティティを関連付ける方法を示しています。 これは、1:N の関連付けですが、N:N の関連付けに対しては同じ操作を行うことができます。  
  
**要求**  
```http  
POST [Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-0000-000000000002)/opportunity_customer_accounts/$ref HTTP/1.1   
Content-Type: application/json   
Accept: application/json   
OData-MaxVersion: 4.0   
OData-Version: 4.0  
  
{  
"@odata.id":"[Organization URI]/api/data/v9.0/opportunities(00000000-0000-0000-0000-000000000001)"  
}  
```  
  
**応答**  
```http 
HTTP/1.1 204 No Content  
OData-Version: 4.0  
```  
  
<a name="bkmk_Removeareferencetoanentity"></a>

## <a name="remove-a-reference-to-an-entity"></a>エンティティへの参照の削除

 削除要求を使用して、エンティティへの参照を削除します。 それを行う方法は、コレクション値ナビゲーション プロパティまたは単一値ナビゲーション プロパティに参照しているかどうかによって異なります。  
  
 **要求**  
 コレクション値ナビゲーション プロパティについては、以下を使用します。  
  
```http  
DELETE [Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-0000-000000000002)/opportunity_customer_accounts/$ref?$id=[Organization URI]/api/data/v9.0/opportunities(00000000-0000-0000-0000-000000000001) HTTP/1.1  
Accept: application/json  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
```  
  
 または、これを使用します。  
  
```http 
DELETE [Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-0000-000000000002)/opportunity_customer_accounts(00000000-0000-0000-0000-000000000001)/$ref HTTP/1.1  
Accept: application/json  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
```  
  
 **要求**  
 単一値ナビゲーション プロパティでは、`$id`クエリ文字列パラメーターを削除します。  
  
```http 
DELETE [Organization URI]/api/data/v9.0/opportunities(00000000-0000-0000-0000-000000000001)/customerid_account/$ref HTTP/1.1  
Accept: application/json  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
```  
  
 **応答**  
 いずれの場合でも、正常な応答にはステータス 204 があります。  
  
```http 
HTTP/1.1 204 No Content  
OData-Version: 4.0  
```  
  
<a name="bkmk_Changethereferenceinasingle"></a>
 
## <a name="change-the-reference-in-a-single-valued-navigation-property"></a>単一値ナビゲーション プロパティでの参照の変更

 PUT 要求を使用して単一値ナビゲーション プロパティの値を設定することによってエンティティを以下のパターンに関連付けることができます。  
  
 **要求**

```http 
PUT [Organization URI]/api/data/v9.0/opportunities(00000000-0000-0000-0000-000000000001)/customerid_account/$ref HTTP/1.1  
Content-Type: application/json  
Accept: application/json  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
  
{  
 "@odata.id":"[Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-0000-000000000002)"  
}  
```  
  
 **応答**  

```http 
HTTP/1.1 204 No Content  
OData-Version: 4.0  
```  
  
<a name="bkmk_Associateentitiesoncreate"></a>

## <a name="associate-entities-on-create"></a>作成時にエンティティを関連付ける

 [1 回の操作で関連するエンティティを作成する](create-entity-web-api.md#bkmk_CreateRelated) に説明されているように、新しいエンティティは、*ディープ挿入* を使用した関連付けによって作成できます。  
  
<a name="bkmk_Associateentitiesonupdate"></a>

## <a name="associate-entities-on-update-using-single-valued-navigation-property"></a>単一値のナビゲーション プロパティを使用して更新プログラムのエンティティを関連付け

 [基本的な更新](update-delete-entities-using-web-api.md#bkmk_update) で記載された同じメッセージを使用して更新時のエンティティを関連付けることができますが、@odata.bind 注釈を使用して単一値ナビゲーション プロパティの値を設定する使用する必要があります。 次の例では、`customerid_account` 単一値ナビゲーション プロパティを使用して営業案件に関連付けられた取引先企業を変更します。  
  
 **要求**

```http 
PATCH [Organization URI]/api/data/v9.0/opportunities(00000000-0000-0000-0000-000000000001) HTTP/1.1  
Content-Type: application/json  
Accept: application/json  
OData-MaxVersion: 4.0  
OData-Version: 4.0  
  
{  
 "customerid_account@odata.bind":"[Organization URI]/api/data/v9.0/accounts(00000000-0000-0000-0000-000000000002)"  
}  
```  
  
 **応答**  

```http 
HTTP/1.1 204 No Content  
OData-Version: 4.0  
```  
<a name="bkmk_Associateentitiesonupdate_multi"></a>

## <a name="associate-entities-on-update-using-collection-valued-navigation-property"></a>コレクション値のナビゲーション プロパティを使用して更新プログラムのエンティティを関連付け

次の例は、コレクション値のナビゲーションプロパティ `email_activity_parties` を使用して、複数の既存の [ActivityParty](../reference/entities/activityparty.md) エンティティを [電子メール](../reference/entities/email.md) エンティティと関連付ける方法を示します。

> [!NOTE]
> 複数のエンティティを更新プログラムのエンティティに関連付けることは、<xref href="Microsoft.Dynamics.CRM.activityparty?text=activityparty EntityType" /> でのみ可能な特別なシナリオです。

**要求**

```HTTP
PUT [Organization URI]/api/data/v9.0/emails(2479d20d-3a39-e711-8145-e0071b6a2001)/email_activity_parties
Content-Type: application/json  
Accept: application/json  
OData-MaxVersion: 4.0  
OData-Version: 4.0

{
    "value": [
        {
            "partyid_contact@odata.bind":"contacts(a30d4045-fc46-e711-8115-e0071b66df51)",
            "participationtypemask":3
            
        },
        {
            "partyid_contact@odata.bind":"contacts(1dcdda07-3a39-e711-8145-e0071b6a2001)",
            "participationtypemask":2
            
        }
        ]
}
```

**応答**

```HTTP
HTTP/1.1 204 No Content  
OData-Version: 4.0 
```

### <a name="see-also"></a>関連項目

 [Web API 基本操作のサンプル (C#)](samples/basic-operations-csharp.md)   
 [Web API 基本操作のサンプル (クライアント側の JavaScript)](samples/basic-operations-client-side-javascript.md)   
 [Web API を使用して演算を実行する](perform-operations-web-api.md)   
 [HTTP 要求の作成とエラーの処理](compose-http-requests-handle-errors.md)   
 [Web API を使用したクエリ データ](query-data-web-api.md)   
 [Web API を使用してエンティティを作成する](create-entity-web-api.md)   
 [Web API を使用してエンティティを取得する](retrieve-entity-using-web-api.md)   
 [Web API を使用したエンティティの更新と削除](update-delete-entities-using-web-api.md)   
 [Web API 関数の使用](use-web-api-functions.md)   
 [Web API アクションの使用](use-web-api-actions.md)   
 [Web API を使用してバッチ操作を実行する](execute-batch-operations-using-web-api.md)   
 [Web API を使用して別のユーザーを偽装する](impersonate-another-user-web-api.md)   
 [Web API を使用する条件付き演算を実行する](perform-conditional-operations-using-web-api.md)

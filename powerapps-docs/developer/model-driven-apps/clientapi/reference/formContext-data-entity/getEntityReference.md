---
title: モデル駆動型アプリの getEntityReference (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 1a66f93d-a47c-4316-91f1-dcf5d09f9d19
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getentityreference-client-api-reference"></a>getEntityReference (クライアント API 参照)



[!INCLUDE[./includes/getEntityReference-description.md](./includes/getEntityReference-description.md)]

## <a name="syntax"></a>構文

`formContext.data.entity.getEntityReference();`

## <a name="return-value"></a>戻り値

**種類**: 検索オブジェクト。

**説明**: 返されたオブジェクトには、次の 3 つの属性があります。

- **entityType**: 文字列。 エンティティ レコードの論理名。 たとえば、「account」。
- **id**: 文字列。 エンティティ レコードの GUID 値。
- **name**: (任意) 文字列。 エンティティ レコードの名前。 




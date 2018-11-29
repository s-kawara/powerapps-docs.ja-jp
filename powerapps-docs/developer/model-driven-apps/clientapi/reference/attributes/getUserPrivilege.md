---
title: getUserPrivilege (クライアント API 参照)| MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 0a3f0349-af9a-418a-b99d-5085999884eb
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getuserprivilege-client-api-reference"></a>getUserPrivilege (クライアント API 参照)



ユーザーが属性のデータ値を作成、読み取り、または更新することができるか示す特権に対応する、3 つのブール値のプロパティを持つオブジェクトを返します。 この機能は、フィールド レベル セキュリティにより、ユーザーの特定の属性に対する特権が変更されるときに使用することを目的としています 

## <a name="attribute-types-supported"></a>サポートされる属性の種類

すべて

## <a name="syntax"></a>構文

`formContext.getAttribute(arg).getUserPrivilege()`

## <a name="return-value"></a>戻り値

**種類**: オブジェクト。 

**説明**: オブジェクトには次の 3 つのブール値プロパティがあります。
- canRead
- canUpdate
- canCreate


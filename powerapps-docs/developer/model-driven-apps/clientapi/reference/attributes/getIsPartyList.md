---
title: getIsPartyList (クライアント API 参照)| MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 487d0923-9675-4308-b88e-fdbf91853a98
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getispartylist-client-api-reference"></a>getIsPartyList (クライアント API 参照)



検索が関係者リスト検索かどうかを示すブール値を返します。 関係者リスト検索を使用すると、電子メール エンティティ レコードの**宛先:** フィールドなど、複数のレコードを設定できます。

## <a name="attribute-types-supported"></a>サポートされる属性の種類

検索

## <a name="syntax"></a>構文

`formContext.getAttribute(arg).getIsPartyList()`

## <a name="return-value"></a>戻り値

**種類**: ブール値。 

**説明**: 検索属性が関係者リストの場合は true、それ以外の場合は false。


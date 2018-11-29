---
title: getAttribute (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 9ef1c886-a0b8-4ba9-bb9f-e6ecfa9d6dff
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getattribute-client-api-reference"></a>getAttribute (クライアント API 参照)



属性の種類を表す文字列値を返します。 

## <a name="attribute-types-supported"></a>サポートされる属性の種類

すべて

## <a name="syntax"></a>構文

`formContext.getAttribute(arg).getAttributeType()`

## <a name="return-value"></a>戻り値

このメソッドは、次の**文字列**値のいずれかを返します。

- boolean
- datetime
- 小数
- double
- integer
- lookup
- memo
- 金額
- multioptionset
- optionset
- 文字列
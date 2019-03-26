---
title: getAttributeType (クライアント API リファレンス)| MicrosoftDocs
ms.date: 02/13/2019
ms.service: powerapps
ms.topic: reference
ms.assetid: 9ef1c886-a0b8-4ba9-bb9f-e6ecfa9d6dff
author: KumarVivek
ms.author: kvivek
manager: annbe
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getattributetype-client-api-reference"></a>getAttributeType (クライアント API リファレンス)



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
- multiselectoptionset
- optionset
- 文字列

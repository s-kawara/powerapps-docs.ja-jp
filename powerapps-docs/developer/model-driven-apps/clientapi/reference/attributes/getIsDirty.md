---
title: getIsDirty (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 5f75ecae-a946-47a0-b748-96525b556f31
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getisdirty-client-api-reference"></a>getIsDirty (クライアント API 参照)



属性値に対する変更内容が保存されていないことを示すブール値を返します。 

## <a name="attribute-types-supported"></a>サポートされる属性の種類

すべて

## <a name="syntax"></a>構文

`formContext.getAttribute(arg).getIsDirty()`

## <a name="return-value"></a>戻り値

**種類**: ブール値。 

**説明**: 保存されていない変更がある場合は true、それ以外の場合は false。
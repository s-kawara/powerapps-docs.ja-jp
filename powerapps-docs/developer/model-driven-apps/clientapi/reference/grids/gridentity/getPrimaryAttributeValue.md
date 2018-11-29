---
title: モデル駆動型アプリの getPrimaryAttributeValue (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 4bd76f0c-5905-4bc2-a423-7d74a267a464
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getprimaryattributevalue-client-api-reference"></a>getPrimaryAttributeValue (クライアント API 参照)



[!INCLUDE[./includes/getPrimaryAttributeValue-description.md](./includes/getPrimaryAttributeValue-description.md)]

## <a name="grid-types-supported"></a>サポートされるグリッドの種類

読み取り専用グリッド

## <a name="syntax"></a>構文

`gridEntity.getPrimaryAttributeValue();`

## <a name="return-value"></a>戻り値

**種類**: 文字列

**説明**: 行内のレコードの主属性値です。

## <a name="remarks"></a>備考

`gridEntity` オブジェクトを取得するには、「[GridEntity](../gridentity.md)」を参照してください。 


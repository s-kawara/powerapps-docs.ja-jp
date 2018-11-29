---
title: モデル駆動型アプリの getEntityName (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 20f9127f-c90a-4ea9-aab3-6ef1f0347a48
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getentityname-client-api-reference"></a>getEntityName (クライアント API 参照)



[!INCLUDE[./includes/getEntityName-description.md](./includes/getEntityName-description.md)]

## <a name="grid-types-supported"></a>サポートされるグリッドの種類

読み取り専用および編集可能なグリッド

## <a name="syntax"></a>構文

`gridEntity.getEntityName();`

## <a name="return-value"></a>戻り値

**種類**: 文字列

**説明**: 行内のレコードの論理名です。

## <a name="remarks"></a>備考

`gridEntity` オブジェクトを取得するには、「[GridEntity](../gridentity.md)」を参照してください。 


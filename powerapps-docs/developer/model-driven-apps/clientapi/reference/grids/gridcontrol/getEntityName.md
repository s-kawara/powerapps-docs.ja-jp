---
title: モデル駆動型アプリの getEntityName (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 1ead9dc0-7511-4b41-bd7d-23b8bb3b4e43
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

`gridContext.getEntityName();`

## <a name="return-value"></a>戻り値

**種類**: 文字列

**説明**: グリッドに表示されるエンティティ データの論理名。

## <a name="remarks"></a>備考

`gridContext` を取得するには、「[グリッド コンテキストの取得](../../grids.md#bkmk_gridcontext)」を参照してください。 



---
title: モデル駆動型アプリの getGrid (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 4d025f92-db16-440c-9f82-e40d71e09862
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getgrid-client-api-reference"></a>getGrid (クライアント API 参照)



[!INCLUDE[./includes/getGrid-description.md](./includes/getGrid-description.md)]

## <a name="grid-types-supported"></a>サポートされるグリッドの種類

読み取り専用および編集可能なグリッド

## <a name="syntax"></a>構文

`var grid = gridContext.getGrid();`

## <a name="return-value"></a>戻り値

**種類**: [グリッド](../grid.md)

**説明**: **グリッド**オブジェクト。

## <a name="remarks"></a>備考

`gridContext` を取得するには、「[グリッド コンテキストの取得](../../grids.md#bkmk_gridcontext)」を参照してください。 



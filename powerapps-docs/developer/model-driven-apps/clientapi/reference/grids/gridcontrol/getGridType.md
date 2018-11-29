---
title: モデル駆動型アプリの getGridType (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: a441c08c-df32-433e-b666-4253f2cf878c
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getgridtype-client-api-reference"></a>getGridType (クライアント API 参照)



[!INCLUDE[./includes/getGridType-description.md](./includes/getGridType-description.md)]

## <a name="grid-types-supported"></a>サポートされるグリッドの種類

読み取り専用および編集可能なグリッド

## <a name="syntax"></a>構文

`var gridType = gridContext.getGridType();`

## <a name="return-value"></a>戻り値

**種類**: 数値

**説明**: 次のいずれかの値を返します。

|Value |内容 |
|--|--|
|1|HomePageGrid|
|2|サブグリッド|

## <a name="remarks"></a>備考

`gridContext` を取得するには、「[グリッド コンテキストの取得](../../grids.md#bkmk_gridcontext)」を参照してください。 



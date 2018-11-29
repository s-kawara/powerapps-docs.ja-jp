---
title: モデル駆動型アプリの getSelectedRows (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 49f39f0f-33ef-41d1-9ab3-14966ae075b5
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getselectedrows-client-api-reference"></a>getSelectedRows (クライアント API 参照)



[!INCLUDE[./includes/getSelectedRows-description.md](./includes/getSelectedRows-description.md)]

## <a name="grid-types-supported"></a>サポートされるグリッドの種類

読み取り専用および編集可能なグリッド

## <a name="syntax"></a>構文

`var allSelectedRows = gridContext.getGrid().getSelectedRows();`

## <a name="return-value"></a>戻り値

**種類:** コレクション

**説明**: グリッド内で選択した行のコレクション。

## <a name="remarks"></a>備考

`gridContext` を取得するには、「[グリッド コンテキストの取得](../../grids.md#bkmk_gridcontext)」を参照してください。

コレクション内のデータにアクセスするために使用できるメソッドの詳細については、「[コレクション (クライアント API 参照)](../../collections.md)」を参照してください。


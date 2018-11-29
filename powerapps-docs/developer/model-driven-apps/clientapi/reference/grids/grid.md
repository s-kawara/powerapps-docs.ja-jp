---
title: モデル駆動型アプリにおけるグリッド (Client API リファレンス) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 02fef0b4-b895-4277-b604-3f525c29dca3
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="grid-client-api-reference"></a>グリッド (クライアント API 参照)



グリッドは **gridContext**.[getGrid](gridcontrol/getGrid.md) メソッドによって返されます。 グリッド メソッドを使用して、グリッドのデータに関する情報にアクセスします。

`var myGrid = gridContext.getGrid();`

## <a name="methods"></a>メソッド

|Name|内容|以下に使用できます|
|--|--|--|
|[getRows](grid/getRows.md)|[!INCLUDE[grid/includes/getRows-description.md](grid/includes/getRows-description.md)]|読み取り専用および編集可能なグリッド|
|[getSelectedRows](grid/getSelectedRows.md)|[!INCLUDE[grid/includes/getSelectedRows-description.md](grid/includes/getSelectedRows-description.md)]|読み取り専用および編集可能なグリッド|
|[getTotalRecordCount](grid/getTotalRecordCount.md)|[!INCLUDE[grid/includes/getTotalRecordCount-description.md](grid/includes/getTotalRecordCount-description.md)]|読み取り専用および編集可能なグリッド|

### <a name="related-topics"></a>関連トピック

[GridRow](gridrow.md)

[モデル駆動型アプリにおけるグリッドおよびサブグリッド](../grids.md)

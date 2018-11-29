---
title: モデル駆動型アプリにおける GridRow (Client API リファレンス) | Microsoft Docs
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
# <a name="gridrow-client-api-reference"></a>GridRow (クライアント API 参照)



[Grid](grid.md).[getRows](grid/getRows.md) および [Grid](grid.md).[getSelectedRows](grid/getSelectedRows.md)  メソッドによって、GridRow コレクションが返されます。

```JavaScript
var myRows = gridContext.getGrid().getRows();
var gridRow = myRows.get(arg);
```

## <a name="properties"></a>プロパティ​​

|Name|内容|以下に使用できます|
|--|--|--|
|data|GridRow の [GridRowData](gridrowdata.md) を含むコレクション。 コレクション内のデータにアクセスするために使用できるメソッドの詳細については、「[コレクション (クライアント API 参照)](../collections.md)」を参照してください。|読み取り専用および編集可能なグリッド|


## <a name="methods"></a>メソッド

|Name|内容|以下に使用できます|
|--|--|--|
|[getData](gridrow/getData.md)|[!INCLUDE[gridrow/includes/getData-description.md](gridrow/includes/getData-description.md)]|読み取り専用および編集可能なグリッド|

### <a name="related-topics"></a>関連トピック

[GridRowData](gridrowdata.md)

[モデル駆動型アプリにおけるグリッドおよびサブグリッド](../grids.md)



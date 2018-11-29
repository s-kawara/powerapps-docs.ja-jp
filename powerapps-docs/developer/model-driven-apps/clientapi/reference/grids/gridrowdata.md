---
title: モデル駆動型アプリにおける GridRowData (Client API リファレンス) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 8139c622-e4d9-478f-9510-414d140e5556
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="gridrowdata-client-api-reference"></a>GridRowData (クライアント API 参照)



GridRowData は、[GridRow](gridrow.md).[getData](gridrow/getData.md) メソッドによって返されます。

また、GridRowData では、行に含まれるすべての属性のコレクションを含む、編集可能なグリッドの行に表示されるレコードに固有の情報を取得するメソッドも提供します。 属性データは編集可能なグリッドで表示される列に制限されています。 コレクション内のデータにアクセスするために使用できるメソッドの詳細については、「[コレクション (クライアント API 参照)](../collections.md)」を参照してください。

```JavaScript
var myRows = gridContext.getGrid().getRows();
var myRow = myRows.get(arg);
var gridRowData = myRow.getData();
```

## <a name="properties"></a>プロパティ​​

|Name|内容|以下に使用できます|
|--|--|--|
|エンティティ|GridRowData の [GridEntity](gridentity.md) を返します。|読み取り専用および編集可能なグリッド|


## <a name="methods"></a>メソッド

|Name|内容|以下に使用できます|
|--|--|--|
|[getEntity](gridrowdata/getEntity.md)|[!INCLUDE[gridrowdata/includes/getEntity-description.md](gridrowdata/includes/getEntity-description.md)]|読み取り専用および編集可能なグリッド|



---
title: モデル駆動型アプリにおける GridEntity (Client API リファレンス) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: cc2b7eca-61f4-4949-8398-52c9fc36721c
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="gridentity-client-api-reference"></a>GridEntity (クライアント API 参照)



GridEntity は、[GridRowData](gridrowdata.md).[getEntity](gridrowdata/getEntity.md) メソッドによって、または [GridRowData](gridrowdata.md).**entity** オブジェクトに直接アクセスすることによって返されます。 GridEntity メソッドを使用して、行内の特定のレコードに関するデータにアクセスします。

```JavaScript
var myRows = gridContext.getGrid().getRows();
var myRow = myRows.get(arg);
var gridEntity = myRow.getData().getEntity();
```

また、GridEntity は、編集可能なグリッド内のエンティティの属性のコレクションを操作するメソッドを提供する**属性**コレクションもサポートします。 各属性 ([GridAttribute](gridattribute.md)) は編集可能なグリッドのセルのデータを表します。各属性には、属性に関連付けられているすべてのセルへの参照が含まれています。 コレクション内のデータにアクセスするために使用できるメソッドの詳細については、「[コレクション (クライアント API 参照)](../collections.md)」を参照してください。

## <a name="methods"></a>メソッド

|Name|内容|以下に使用できます|
|--|--|--|
|[getEntityName](gridentity/getEntityName.md)|[!INCLUDE[gridentity/includes/getEntityName-description.md](gridentity/includes/getEntityName-description.md)]|読み取り専用および編集可能なグリッド|
|[getEntityReference](gridentity/getEntityReference.md)|[!INCLUDE[gridentity/includes/getEntityReference-description.md](gridentity/includes/getEntityReference-description.md)]|読み取り専用および編集可能なグリッド|
|[getId](gridentity/getId.md)|[!INCLUDE[gridentity/includes/getId-description.md](gridentity/includes/getId-description.md)]|読み取り専用および編集可能なグリッド|
|[getPrimaryAttributeValue](gridentity/getPrimaryAttributeValue.md)|[!INCLUDE[gridentity/includes/getPrimaryAttributeValue-description.md](gridentity/includes/getPrimaryAttributeValue-description.md)]|読み取り専用グリッド|

### <a name="related-topics"></a>関連トピック

[GridAttribute](gridattribute.md)

[モデル駆動型アプリにおけるグリッドおよびサブグリッド](../grids.md)

[属性](../attributes.md)



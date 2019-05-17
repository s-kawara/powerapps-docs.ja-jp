---
title: 種類 | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d9fb178c-6cc6-48cc-99c0-9972e37dec3e
---

# <a name="type"></a>種類

[!INCLUDE [type-description](includes/type-description.md)]

## <a name="parent-elements"></a>親要素

|Element|説明|
|--|--|
|[種類のグループ](type-group.md)|[!INCLUDE [type-group-description](includes/type-group-description.md)]|

## <a name="value-element"></a>値要素

この要素は以下の値のひとつの `string` を含みます:

[!INCLUDE [type-table](includes/type-table.md)]

### <a name="example"></a>例

```XML
<type-group name="numbers">
      <type>Whole.None</type>
      <type>Currency</type>
      <type>FP</type>
      <type>Decimal</type>
    </type-group>
```

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークのマニフェスト スキーマ リファレンス](index.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../overview.md)
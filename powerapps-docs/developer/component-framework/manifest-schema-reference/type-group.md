---
title: 種類グループの要素 | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ec7c1ad4-b834-4755-8a04-2c8940f75674
---

# <a name="type-group-element"></a>種類グループの要素

[!INCLUDE [type-group-description](includes/type-group-description.md)]

## <a name="attributes"></a>属性

|Name|説明|型|必須出席者|
|--|--|--|--|
|`name`|データの種類名|`string`|あり|

## <a name="parent-elements"></a>親要素

|Element|説明|
|--|--|
|[コントロール](control.md)|[!INCLUDE [control-description](includes/control-description.md)]|


## <a name="child-elements"></a>下位要素

|Element|説明|発生回数|
|--|--|--|
|[タイプ](type.md)|[!INCLUDE [type-description](includes/type-description.md)]|1 以上|

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
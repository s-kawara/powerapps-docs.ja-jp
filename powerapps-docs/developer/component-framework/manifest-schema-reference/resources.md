---
title: リソース要素 | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 66599c2f-6651-4b27-92da-a38897acdfb5
---

# <a name="resources-element"></a>リソース要素

[!INCLUDE [resources-description](includes/resources-description.md)]

## <a name="parent-elements"></a>親要素

|Element|説明|
|--|--|
|[コントロール](control.md)|[!INCLUDE [control-description](includes/control-description.md)]|

## <a name="child-elements"></a>下位要素

|Element|説明|発生回数|
|--|--|--|
|[コード](code.md)|[!INCLUDE [code-description](includes/code-description.md)]|1 以上|
|[css](css.md)|[!INCLUDE [css-description](includes/css-description.md)]|0 以上|
|[img](img.md)|[!INCLUDE [img-description](includes/img-description.md)]|0 以上|
|[HTML](html.md)|[!INCLUDE [html-description](includes/html-description.md)]|0 以上|
|[resx](resx.md)|[!INCLUDE [resx-description](includes/resx-description.md)]|0 以上|

## <a name="example"></a>例

```xml
<resources>
  <code path="JS_HelloWorldControl.js" order="1" />
<css path="css/JS_HelloWorldControl.css" order="1" />
        </resources>
```

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークのマニフェスト スキーマ リファレンス](index.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../overview.md)
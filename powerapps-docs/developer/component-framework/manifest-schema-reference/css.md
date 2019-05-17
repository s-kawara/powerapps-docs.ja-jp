---
title: CSS 要素 | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
ms.assetid: b6119424-c0a4-4412-b25c-8239da6cbe36
---

# <a name="css-element"></a>CSS 要素

[!INCLUDE [css-description](includes/css-description.md)]

## <a name="attributes"></a>属性

|Name|説明|型|必須出席者|
|--|--|--|--|
|`path`|CSS ファイルが置かれている w.r.t のマニフェストの相対パス|`string`|あり|
|`order`|ファイルを読み込む必要がある順序|`Positive integer`|[任意出席者]|

## <a name="parent-elements"></a>親要素

|Element|説明|
|--|--|
|[リソース](resources.md)|[!INCLUDE [resources-description](includes/resources-description.md)]|

## <a name="example"></a>例

```xml
<css path="css/JS_HelloWorldControl.css" order="1" />
```

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークのマニフェスト スキーマ リファレンス](index.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../overview.md)

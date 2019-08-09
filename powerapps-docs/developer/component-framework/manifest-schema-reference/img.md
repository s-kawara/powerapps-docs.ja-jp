---
title: 画像要素 | Microsoft Docs
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
ms.assetid: 0e776647-a4a2-42c9-85e8-62718154052f
---

# <a name="img-element"></a>画像要素

[!INCLUDE[cc-beta-prerelease-disclaimer](../../../includes/cc-beta-prerelease-disclaimer.md)]

[!INCLUDE [img-description](includes/img-description.md)]

## <a name="attributes"></a>属性

|Name|説明|型|必須出席者|
|--|--|--|--|
|`path`|画像ファイルが置かれている w.r.t のマニフェストの相対パス|`string`|あり|

## <a name="parent-elements"></a>親要素

|Element|説明|
|--|--|
|[リソース](resources.md)|[!INCLUDE [resources-description](includes/resources-description.md)]|


### <a name="example"></a>例

```XML
<img path="img/default.png" />
```

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークのマニフェスト スキーマ リファレンス](index.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../overview.md)
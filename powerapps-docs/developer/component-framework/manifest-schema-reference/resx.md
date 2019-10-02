---
title: Resx 要素 | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
author: Nkrb
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 38acfda3-4adc-4aa2-bb8b-f29ba572a6e5
---

# <a name="resx-element"></a>resx 要素

[!INCLUDE[cc-beta-prerelease-disclaimer](../../../includes/cc-beta-prerelease-disclaimer.md)]

[!INCLUDE [resx-description](includes/resx-description.md)]

## <a name="attributes"></a>属性

|Name|説明|型|必須出席者|
|--|--|--|--|
|`path`|Resx ファイルが置かれている w.r.t のマニフェストの相対パス|`string`|あり|
|`version`|resx ファイルの現在のバージョン|`string`|あり|

## <a name="parent-elements"></a>親要素

|Element|説明|
|--|--|
|[リソース](resources.md)|[!INCLUDE [resources-description](includes/resources-description.md)]|

## <a name="example"></a>例

```xml
<resources>
      <code path="TS_LocalizationAPI.js" order="1" />
        <css path="css/TS_LocalizationAPI.css" order="1" />
      <resx path="strings/TSLocalizationAPI.1033.resx" version="1.0.0" />
      <resx path="strings/TSLocalizationAPI.1035.resx" version="1.0.0" />
      <resx path="strings/TSLocalizationAPI.3082.resx" version="1.0.0" />
    </resources>
```

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークのマニフェスト スキーマ リファレンス](index.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../overview.md)

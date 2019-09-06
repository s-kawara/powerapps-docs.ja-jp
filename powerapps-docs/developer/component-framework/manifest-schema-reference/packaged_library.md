---
title: パッケージ化されたライブラリ要素 | Microsoft Docs
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
ms.assetid: 41c50db2-3096-4990-ac2b-e702c161bf4f
---

# <a name="packaged_library-element"></a>パッケージ化されたライブラリ要素

[!INCLUDE[cc-beta-prerelease-disclaimer](../../../includes/cc-beta-prerelease-disclaimer.md)]

[!INCLUDE [packaged_library-description](includes/packaged_library-description.md)]

## <a name="attributes"></a>属性

|Name|説明|型|必須出席者|
|--|--|--|--|
|`path`|パッケージ化されたライブラリ ファイルのある場所|`string`|あり|
|`version`|パッケージ化されたライブラリの現在のバージョン|`string`|あり|

## <a name="parent-elements"></a>親要素

|Element|説明|
|--|--|
|[ライブラリ](library.md)|[!INCLUDE [library-description](includes/library-description.md)]|

## <a name="example"></a>例

```xml
<resources>
    <library name="AngularJSCore" version=">=1" order="1">
    <packaged_library path="libs/angular.min.js" version="1.5.8" />
    </library>
```

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークのマニフェスト スキーマ リファレンス](index.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../overview.md)

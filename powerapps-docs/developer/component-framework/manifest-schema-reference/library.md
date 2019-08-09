---
title: ライブラリ要素 | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 90f2b4c9-7396-4ab9-bc9f-810189dc18b7
---

# <a name="library-element"></a>ライブラリ要素

[!INCLUDE[cc-beta-prerelease-disclaimer](../../../includes/cc-beta-prerelease-disclaimer.md)]

[!INCLUDE [library-description](includes/library-description.md)]

## <a name="attributes"></a>属性

|Name|説明|型|必須出席者|
|--|--|--|--|
|`name`|ライブラリ名|`string`|あり|
|`version`|現在のライブラリ バージョン|正の整数|あり|
|`order`|ライブラリ ファイルを読み込む必要がある順序|正の整数|あり|

## <a name="parent-elements"></a>親要素

|Element|説明|
|--|--|
|[リソース](resources.md)|[!INCLUDE [resources-description](includes/resources-description.md)]|

## <a name="child-elements"></a>下位要素

|Element|説明|発生回数|
|--|--|--|
|[パッケージ化されたライブラリ]||0 以上|

## <a name="example"></a>例

```xml
<resources>
<library name="AngularJSCore" version=">=1" order="1">
<packaged_library path="libs/angular.min.js" version="1.5.8" />
</library>
  </resources>
```

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークのマニフェスト スキーマ リファレンス](index.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../overview.md)
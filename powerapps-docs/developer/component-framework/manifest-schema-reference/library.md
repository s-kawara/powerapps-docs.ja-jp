---
title: Library 要素 |Microsoft Docs
description: ''
keywords: ''
ms.author: nabuthuk
author: Nkrb
manager: kvivek
ms.date: 10/01/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 90f2b4c9-7396-4ab9-bc9f-810189dc18b7
ms.openlocfilehash: bd766864e6ef971b5245afad7d49af54b9369087
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72346304"
---
# <a name="library-element"></a>library 要素

[!INCLUDE [library-description](includes/library-description.md)]

## <a name="attributes"></a>属性

|名前|Description|種類|必須|
|--|--|--|--|
|`name`|ライブラリの名前|`string`|はい|
|`version`|現在のライブラリのバージョン|正の整数|はい|
|`order`|ライブラリファイルの読み込み順序|正の整数|はい|

## <a name="parent-elements"></a>親要素

|要素|Description|
|--|--|
|[リソース](resources.md)|[!INCLUDE [resources-description](includes/resources-description.md)]|

## <a name="child-elements"></a>子要素

|要素|Description|連続|
|--|--|--|
|[packaged_library]||0以上|

## <a name="example"></a>例

```xml
<resources>
<library name="AngularJSCore" version=">=1" order="1">
<packaged_library path="libs/angular.min.js" version="1.5.8" />
</library>
  </resources>
```

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネントフレームワークマニフェストスキーマリファレンス](index.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../overview.md)
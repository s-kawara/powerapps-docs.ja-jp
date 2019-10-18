---
title: パッケージライブラリ要素 |Microsoft Docs
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
ms.assetid: 41c50db2-3096-4990-ac2b-e702c161bf4f
ms.openlocfilehash: 011aa2ab527cc2bd16fc99842e2388a3a6b0918e
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72346189"
---
# <a name="packaged_library-element"></a>packaged_library 要素

[!INCLUDE [packaged_library-description](includes/packaged_library-description.md)]

## <a name="available-for"></a>利用可能な対象

モデル駆動型アプリ

## <a name="attributes"></a>属性

|名前|Description|種類|必須|利用可能な対象|
|--|--|--|--|-------|
|`path`|パッケージライブラリファイルが配置されている場所|`string`|はい|モデル駆動型アプリ|
|`version`|パッケージライブラリの現在のバージョン|`string`|はい|モデル駆動型アプリ|

## <a name="parent-elements"></a>親要素

|要素|Description|
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

[PowerApps コンポーネントフレームワークマニフェストスキーマリファレンス](index.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../overview.md)

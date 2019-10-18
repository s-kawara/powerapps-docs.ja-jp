---
title: Resources 要素 |Microsoft Docs
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
ms.assetid: 66599c2f-6651-4b27-92da-a38897acdfb5
ms.openlocfilehash: a7df2dde98667fd0de8489943094ad6f4ff210f0
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72346074"
---
# <a name="resources-element"></a>resources 要素

[!INCLUDE [resources-description](includes/resources-description.md)]

## <a name="available-for"></a>利用可能な対象

モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー)

## <a name="parent-elements"></a>親要素

|要素|Description|
|--|--|
|[コントロール](control.md)|[!INCLUDE [control-description](includes/control-description.md)]|

## <a name="child-elements"></a>子要素

|要素|Description|連続|
|--|--|--|
|[コード](code.md)|[!INCLUDE [code-description](includes/code-description.md)]|1|
|[css](css.md)|[!INCLUDE [css-description](includes/css-description.md)]|0以上|
|[img](img.md)|[!INCLUDE [img-description](includes/img-description.md)]|0以上|
|[html](html.md)|[!INCLUDE [html-description](includes/html-description.md)]|0以上|
|[resx](resx.md)|[!INCLUDE [resx-description](includes/resx-description.md)]|0以上|

## <a name="example"></a>例

```xml
<resources>
  <code path="JS_HelloWorldControl.js" order="1" />
<css path="css/JS_HelloWorldControl.css" order="1" />
        </resources>
```

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネントフレームワークマニフェストスキーマリファレンス](index.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../overview.md)
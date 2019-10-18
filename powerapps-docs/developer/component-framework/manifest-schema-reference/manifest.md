---
title: Manifest 要素 |Microsoft Docs
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
ms.assetid: a48831c6-133a-4747-99fa-7cc1df4558d0
ms.openlocfilehash: d62b72c43a9c77a41c0a434a723d330ffa4b890a
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72346258"
---
# <a name="manifest-element"></a>Manifest 要素

[!INCLUDE [manifest-description](includes/manifest-description.md)]

## <a name="available-for"></a>利用可能な対象

モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー)

## <a name="child-elements"></a>子要素

|要素|Description|連続|利用可能な対象|
|--|--|--|-------|
|[コントロール](control.md)|[!INCLUDE [control-description](includes/control-description.md)]|1以上|モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー) (試験的なプレビュー)|
|[type-group](type-group.md)|[!INCLUDE [type-group-description](includes/type-group-description.md)]|0以上|モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー) (試験的なプレビュー)|
|[プロパティ](property.md)|[!INCLUDE [property-description](includes/property-description.md)]|0以上|モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー) (試験的なプレビュー)|
|[data-set](data-set.md)|[!INCLUDE [data-set-description](includes/data-set-description.md)]|0以上|モデル駆動型アプリ|
|[センター](resources.md)|[!INCLUDE [resource-description](includes/resources-description.md)]|1以上|モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー) (試験的なプレビュー)|

## <a name="example"></a>例

```xml
<?xml version="1.0" encoding="utf-8" ?>
<manifest>
    <control namespace="MyNameSpace" constructor="JSHelloWorldControl" version="1.0.0" display-name-key="JS_HelloWorldControl_Display_Key" description-key="JS_HelloWorldControl_Desc_Key" control-type="standard">
        <property name="myFirstProperty" display-name-key="myFirstProperty_Display_Key" description-key="myFirstProperty_Desc_Key" of-type="SingleLine.Text" usage="bound" required="true" />
        <resources>
            <code path="JS_HelloWorldControl.js" order="1" />
            <css path="css/JS_HelloWorldControl.css" order="1" />
        </resources>
    </control>
</manifest>
```

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネントフレームワークマニフェストスキーマリファレンス](index.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../overview.md)

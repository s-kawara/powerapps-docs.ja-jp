---
title: モード | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
---

# <a name="manifest-element"></a>マニフェスト要素

[!INCLUDE [mode-description](includes/mode-description.md)]

## <a name="child-elements"></a>下位要素

|Element|説明|発生回数|
|--|--|--|
|[読み込み](read.md)|[!INCLUDE [read-description](includes/read-description.md)]|1 以上|
|[編集](edit.md)|[!INCLUDE [edit-description](includes/edit-description.md)]|0 以上|
|[コンテナ](container.md)|[!INCLUDE [property-description](includes/container-description.md)]|0 以上|
|[データセット](data-set.md)|[!INCLUDE [data-set-description](includes/data-set-description.md)]|0 以上|
|[リソース](resources.md)|[!INCLUDE [resource-description](includes/resources-description.md)]|1 以上|

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

[PowerApps コンポーネント フレームワークのマニフェスト スキーマ リファレンス](index.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../overview.md)

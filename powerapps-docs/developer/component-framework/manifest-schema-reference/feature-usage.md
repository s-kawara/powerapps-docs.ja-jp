---
title: feature-usage | Microsoft Docs
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
ms.assetid: 87f5e921-4114-4710-a362-db741426a69b
---

# <a name="feature-usage-element"></a>feature-usage の要素

feature-usage 要素は `uses-feature` 要素のラッパーとして機能します。この要素によって開発者は、コンポーネントが使用する機能を宣言することができます。 uses-feature の要素が定義されていない場合は、この要素は必要ありません。

## <a name="child-elements"></a>下位要素

|Element|説明|
|--|--|
|[uses-feature](uses-feature.md)|コンポーネントが使用する機能を示します。|


## <a name="example"></a>例

```XML
<feature-usage>
    <uses-feature name="Device.captureAudio" required="true" />
    <uses-feature name="Device.captureImage" required="true" />
    <uses-feature name="Device.captureVideo" required="true" />
    <uses-feature name="Device.getBarcodeValue" required="true" />
    <uses-feature name="Device.getCurrentPosition" required="true" />
    <uses-feature name="Device.pickFile" required="true" />
    <uses-feature name="Utility" required="true" />
    <uses-feature name="WebAPI" required="true" />
 </feature-usage>
```

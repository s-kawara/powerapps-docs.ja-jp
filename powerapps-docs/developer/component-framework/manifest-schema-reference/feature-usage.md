---
title: 機能の使用 |Microsoft Docs
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
ms.assetid: 87f5e921-4114-4710-a362-db741426a69b
ms.openlocfilehash: 21e76a2a17910fe36967364f063ff2fc9b25e153
ms.sourcegitcommit: 63ea15e2f861d43333aacda19230cd8922d7bdfd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/01/2019
ms.locfileid: "72339634"
---
# <a name="feature-usage-element"></a>機能の使用法要素

機能使用量要素は `uses-feature` 要素のラッパーとして機能します。これにより、開発者は、コンポーネントが使用する機能を宣言できます。 使用する機能の要素が定義されていない場合、機能の使用に関する要素は必要ありません。

## <a name="available-for"></a>利用可能な対象

モデル駆動型アプリ

## <a name="child-elements"></a>子要素

|要素|Description|利用可能な対象|
|--|--|-----|
|[使用-機能](uses-feature.md)|コンポーネントが使用する機能を示します。|モデル駆動型アプリ|


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

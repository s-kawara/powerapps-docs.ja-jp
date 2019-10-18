---
title: Image 要素 |Microsoft Docs
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
applies_to:
- Dynamics 365 (online)
- Dynamics 365 Version 9.x
ms.assetid: 0e776647-a4a2-42c9-85e8-62718154052f
ms.openlocfilehash: f3abd4f6a4061161a86d270f1bb4d0037632880c
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72346511"
---
# <a name="img-element"></a>img 要素

[!INCLUDE [img-description](includes/img-description.md)]

## <a name="available-for"></a>利用可能な対象

モデル駆動型アプリ

## <a name="attributes"></a>属性

|名前|Description|種類|必須|利用可能な対象|
|--|--|--|--|-------|
|`path`|イメージファイルが配置されている相対パス (w.x.y.z)|`string`|はい|モデル駆動型アプリ|

## <a name="parent-elements"></a>親要素

|要素|Description|
|--|--|
|[リソース](resources.md)|[!INCLUDE [resources-description](includes/resources-description.md)]|


### <a name="example"></a>例

```XML
<img path="img/default.png" />
```

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネントフレームワークマニフェストスキーマリファレンス](index.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../overview.md)
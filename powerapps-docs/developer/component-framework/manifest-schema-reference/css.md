---
title: CSS 要素 |Microsoft Docs
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
ms.assetid: b6119424-c0a4-4412-b25c-8239da6cbe36
ms.openlocfilehash: b7c96ba2bbb3e5d6d20df92e58ef0bc4005e7d37
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72346580"
---
# <a name="css-element"></a>css 要素

[!INCLUDE [css-description](includes/css-description.md)]

## <a name="available-for"></a>利用可能な対象

モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー)

## <a name="attributes"></a>属性

|名前|Description|種類|必須|利用可能な対象|
|--|--|--|--|-----|
|`path`|CSS ファイルが配置される相対パス w.x.y.z マニフェスト|`string`|はい|モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー) (試験的なプレビュー)|
|`order`|CSS ファイルの読み込み順序|`Positive integer`|Optional|モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー) (試験的なプレビュー)|

## <a name="parent-elements"></a>親要素

|要素|Description|
|--|--|
|[リソース](resources.md)|[!INCLUDE [resources-description](includes/resources-description.md)]|

## <a name="example"></a>例

```xml
<css path="css/JS_HelloWorldControl.css" order="1" />
```

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネントフレームワークマニフェストスキーマリファレンス](index.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../overview.md)

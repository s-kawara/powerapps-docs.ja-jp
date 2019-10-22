---
title: Code 要素 |Microsoft Docs
description: ''
keywords: ''
ms.author: nabuthuk
author: Nkrb
manager: kvivek
ms.date: 06/4/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Dynamics 365 (online)
- Dynamics 365 Version 9.x
ms.assetid: 44d9fcfb-0cd8-48cc-aace-dd589099dd79
ms.openlocfilehash: 2caf89a73dba006240c5bb6e8c874dfdd795d8c2
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72346649"
---
# <a name="code-element"></a>code 要素

[!INCLUDE [code-description](includes/code-description.md)]

## <a name="available-for"></a>利用可能な対象

モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー)

## <a name="attributes"></a>属性

|名前|Description|種類|必須|利用可能な対象|
|--|--|--|--|-----|
|`path`|リソースファイルが配置されている場所|`String`|はい|モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー) (試験的なプレビュー)|
|`order`|リソースファイルを読み込む順序|`Positive integer`|はい|モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー) (試験的なプレビュー)|

## <a name="parent-elements"></a>親要素

|要素|Description|
|--|--|
|[リソース](resources.md)|[!INCLUDE [resources-description](includes/resources-description.md)]|

### <a name="example"></a>例

```XML
<code path="TS_IncrementControl.js" order="1" />
        <css path="css/TS_IncrementControl.css" order="1" />
      <resx path="strings/TSIncrementControl.1033.resx" version="1.0.0" />
```

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネントフレームワークマニフェストスキーマリファレンス](index.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../overview.md)
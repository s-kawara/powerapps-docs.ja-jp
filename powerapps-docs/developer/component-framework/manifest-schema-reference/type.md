---
title: Type |Microsoft Docs
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
ms.assetid: d9fb178c-6cc6-48cc-99c0-9972e37dec3e
ms.openlocfilehash: 960f3aee9007c1bc8391ee7cf85a961234bbf3ae
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72345959"
---
# <a name="type"></a>type

[!INCLUDE [type-description](includes/type-description.md)]

## <a name="available-for"></a>利用可能な対象

モデル駆動型アプリ

## <a name="parent-elements"></a>親要素

|要素|Description|
|--|--|
|[type-group](type-group.md)|[!INCLUDE [type-group-description](includes/type-group-description.md)]|

## <a name="value-element"></a>Value 要素

この要素には、次のいずれかの値を持つ `string` が含まれます。

[!INCLUDE [type-table](includes/type-table.md)]

### <a name="example"></a>例

```XML
<type-group name="numbers">
      <type>Whole.None</type>
      <type>Currency</type>
      <type>FP</type>
      <type>Decimal</type>
    </type-group>
```

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネントフレームワークマニフェストスキーマリファレンス](index.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../overview.md)
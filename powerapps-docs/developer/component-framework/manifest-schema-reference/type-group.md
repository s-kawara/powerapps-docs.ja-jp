---
title: Type Group 要素 |Microsoft Docs
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
ms.assetid: ec7c1ad4-b834-4755-8a04-2c8940f75674
ms.openlocfilehash: 7b09fad6097bb837c19116d59bb90afbde4d46b2
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72345982"
---
# <a name="type-group-element"></a>type-group 要素

[!INCLUDE [type-group-description](includes/type-group-description.md)]

## <a name="available-for"></a>利用可能な対象

モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー)

## <a name="attributes"></a>属性

|名前|Description|種類|必須|
|--|--|--|--|
|`name`|データ型の名前|`string`|はい|

## <a name="parent-elements"></a>親要素

|要素|Description|
|--|--|
|[コントロール](control.md)|[!INCLUDE [control-description](includes/control-description.md)]|


## <a name="child-elements"></a>子要素

|要素|Description|連続|
|--|--|--|
|[各種](type.md)|[!INCLUDE [type-description](includes/type-description.md)]|1以上|


この実験的なプレビューでは、種類グループのキャンバスアプリに対するサポートが制限されています。 コンポーネントをインポートしようとすると、次の問題が発生します。

1. 型グループに示されているすべての型が互換性のある javascript 型である場合、開発者は、一覧表示されている最も汎用的なオプションを選択しようとします。 互換性があると見なされる型は次のとおりです。
   - 文字列: Regexoptions.singleline、Multiple、Regexoptions.singleline、Regexoptions.singleline、Regexoptions.singleline、Regexoptions.singleline、regexoptions.singleline。この2つの文字列を入力します。
   - 数値:10 進数、浮動小数点、全体。なし、通貨。
   - 日付: dateandtime。 dateandtime、DateAndTime。 DateOnly。

2. グループに示されている型が互換性がないと見なされた場合、パラメーターは、型グループに一覧表示されている最初の型として扱われます。

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
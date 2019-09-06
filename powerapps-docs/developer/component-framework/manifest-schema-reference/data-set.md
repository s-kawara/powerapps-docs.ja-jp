---
title: データセット要素 | Microsoft Docs
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
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
ms.assetid: 9ffe8930-b290-4252-98d4-a1195b00205f
---

# <a name="data-set-element"></a>データセット要素

[!INCLUDE[cc-beta-prerelease-disclaimer](../../../includes/cc-beta-prerelease-disclaimer.md)]

[!INCLUDE [data-set-description](includes/data-set-description.md)]

## <a name="attributes"></a>属性

|Name|説明|型|必須出席者|
|--|--|--|--|
|`description-key`|プロパティの説明を説明するローカライズされた文字列としてカスタマイズ画面で使用します。|`string`|[任意出席者]|
|`display-name-key`|プロパティ名を説明するローカライズされた文字列としてカスタマイズ画面で使用します。|`string`|あり|
|`name`|グリッド名|`string`|あり|
|`cds-data-set-options`|trueと設定されている場合は、Commandbar、 ViewSelector、 QuickFindSearch を表示します |`boolean`|あり|

## <a name="parent-elements"></a>親要素

|Element|説明|
|--|--|
|[コントロール](control.md)|[!INCLUDE [control-description](includes/control-description.md)]|

## <a name="example"></a>例

```xml
 <data-set name="dataSetGrid" display-name-key="DataSetGridProperty" cds-data-set-options="displayCommandBar:true;displayViewSelector:true;displayQuickFindSearch:true">
 </data-set>
```

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークのマニフェスト スキーマ リファレンス](index.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../overview.md)
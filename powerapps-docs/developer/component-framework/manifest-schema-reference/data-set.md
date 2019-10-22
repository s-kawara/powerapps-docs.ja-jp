---
title: DataSet 要素 |Microsoft Docs
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
ms.assetid: 9ffe8930-b290-4252-98d4-a1195b00205f
ms.openlocfilehash: adf672b036d1f49619cbc4a5ef72661fbeebf013
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72346557"
---
# <a name="data-set-element"></a>データセット要素

[!INCLUDE [data-set-description](includes/data-set-description.md)]

## <a name="attributes"></a>属性

|名前|Description|種類|必須|利用可能な対象|
|--|--|--|--|-------|
|`description-key`|プロパティの説明を定義します。|`string`|Optional|
|`display-name-key`|プロパティの名前を定義します。|`string`|はい|
|`name`|グリッドの名前|`string`|はい|
|`cds-data-set-options`|True に設定されている場合は、Commandbar、ViewSelector、QuickFindSearch を表示します |`boolean`|はい|

## <a name="parent-elements"></a>親要素

|要素|Description|
|--|--|
|[コントロール](control.md)|[!INCLUDE [control-description](includes/control-description.md)]|

## <a name="example"></a>例

```xml
 <data-set name="dataSetGrid" display-name-key="DataSetGridProperty" cds-data-set-options="displayCommandBar:true;displayViewSelector:true;displayQuickFindSearch:true">
 </data-set>
```

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネントフレームワークマニフェストスキーマリファレンス](index.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../overview.md)
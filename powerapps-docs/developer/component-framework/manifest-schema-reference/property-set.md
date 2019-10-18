---
title: Property Set 要素 |Microsoft Docs
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
ms.assetid: 996f10e5-8057-40ea-9680-555e4cd682ff
ms.openlocfilehash: 98e0bcf7588e72f001e45471c87f0050dd0846ba
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72346235"
---
# <a name="property-set-element"></a>プロパティセット要素

[!INCLUDE [property-set-description](includes/property-set-description.md)]

## <a name="available-for"></a>利用可能な対象

モデル駆動型アプリ

## <a name="attributes"></a>属性

|名前|Description|種類|必須|
|--|--|--|--|
|`name`|フィールドの名前|`string`|はい|
|`display-name-key`|カスタマイズ画面で、プロパティの名前を記述するローカライズされた文字列として使用されます。|`string`|はい|
|`description-key`|カスタマイズ画面で、プロパティの説明を記述するローカライズされた文字列として使用されます。|`string`|Optional|
|`of-type`|プロパティのデータ型を定義します。|「[解説](#remarks)」を参照|Optional|
|`required`|プロパティが必須かどうかを示します。|`boolean`|Optional|
|`of-type-group`|マニフェストで定義されている型グループの名前|`string`|Optional|
|`usage`|Usage 属性は、プロパティが、コンポーネントが変更 (バインド) または読み取り専用の値 (入力) できるエンティティ属性を表すものかどうかを識別します。|`bound` または `input`|はい|

## <a name="parent-elements"></a>親要素

|要素|Description|
|--|--|
|[data-set](data-set.md)|[!INCLUDE [data-set-description](includes/data-set-description.md)]|

## <a name="child-elements"></a>子要素

|要素|Description|連続|
|--|--|--|
|[な](types.md)||0以上|

### <a name="remarks"></a>」

@No__t_0 属性値には、次のいずれかを指定する必要があります。

[!INCLUDE [type-table](includes/type-table.md)]

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネントフレームワークマニフェストスキーマリファレンス](index.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../overview.md)
---
title: プロパティ設定の要素 | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 996f10e5-8057-40ea-9680-555e4cd682ff
---

# <a name="property-set-element"></a>プロパティ設定の要素

[!INCLUDE[cc-beta-prerelease-disclaimer](../../../includes/cc-beta-prerelease-disclaimer.md)]

[!INCLUDE [property-set-description](includes/property-set-description.md)]

## <a name="attributes"></a>属性

|Name|説明|型|必須出席者|
|--|--|--|--|
|`name`|フィールド名|`string`|あり|
|`display-name-key`|プロパティ名を説明するローカライズされた文字列としてカスタマイズ画面で使用します|`string`|あり|
|`description-key`|プロパティの説明を説明するローカライズされた文字列としてカスタマイズ画面で使用します|`string`|[任意出席者]|
|`of-type`|プロパティのデータの種類を定義します|[備考](#remarks) を参照してください|[任意出席者]|
|`required`|プロパティが必須かどうか|`boolean`|[任意出席者]|
|`of-type-group`|マニフェストで定義された種類グループ名|`string`|[任意出席者]|

## <a name="parent-elements"></a>親要素

|Element|説明|
|--|--|
|[データセット](data-set.md)|[!INCLUDE [data-set-description](includes/data-set-description.md)]|

## <a name="child-elements"></a>下位要素

|Element|説明|発生回数|
|--|--|--|
|[種類](types.md)||0 以上|

### <a name="remarks"></a>備考

`of-type` 属性値は以下のひとつである必要があります:

[!INCLUDE [type-table](includes/type-table.md)]

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークのマニフェスト スキーマ リファレンス](index.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../overview.md)
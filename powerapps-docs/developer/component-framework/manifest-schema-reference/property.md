---
title: プロパティ要素 | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 45f4872d-c1d2-4c5a-8721-251b96ede370
---

# <a name="property-element"></a>プロパティ要素

[!INCLUDE[cc-beta-prerelease-disclaimer](../../../includes/cc-beta-prerelease-disclaimer.md)]

[!INCLUDE [property-description](includes/property-description.md)]

## <a name="attributes"></a>属性

|Name|説明|型|必須出席者|
|--|--|--|--|
|`name`|プロパティ名|`string`|あり|
|`display-name-key`|プロパティ名を説明するローカライズされた文字列としてカスタマイズ画面で使用します。|`string`|あり|
|`of-type`|プロパティのデータの種類を定義します|[備考](#remarks) を参照してください|[任意出席者]|
|`usage`|使用方法属性はプロパティが、コンポーネントが値を変更 (バインド) または読み取り専用値 (入力) にできるエンティティ属性を表すことを意図しているか識別します。|`bound` または `input`|[任意出席者]|
|`required`|プロパティが必須かどうか|`boolean`|[任意出席者]|
|`of-type-group`|マニフェストで定義された種類グループ名|`string`|[任意出席者]|
|`description-key`|プロパティの説明を説明するローカライズされた文字列としてカスタマイズ画面で使用します。|`string`|[任意出席者]|

### <a name="remarks"></a>備考

`of-type` 属性値は以下のひとつである必要があります:

[!INCLUDE [type-table](includes/type-table.md)]

## <a name="parent-elements"></a>親要素

|Element|説明|
|--|--|
|[マニフェスト](manifest.md)|[!INCLUDE [manifest-description](includes/manifest-description.md)]|


## <a name="example"></a>例

```xml
<property name="myFirstProperty" display-name-key="myFirstProperty_Display_Key" 
description-key="myFirstProperty_Desc_Key" of-type="SingleLine.Text" usage="bound" required="true" />
```

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークのマニフェスト スキーマ リファレンス](index.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../overview.md)

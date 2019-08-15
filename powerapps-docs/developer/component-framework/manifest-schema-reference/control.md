---
title: コントロール要素 | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
ms.assetid: 4dacd337-c9df-458e-86f3-bfb3ab543ea7
---

# <a name="control-element"></a>コントロール要素

[!INCLUDE[cc-beta-prerelease-disclaimer](../../../includes/cc-beta-prerelease-disclaimer.md)]

[!INCLUDE [control-description](includes/control-description.md)]

## <a name="attributes"></a>属性

|Name|説明|型|必須出席者|
|--|--|--|--|
|`namespace`|コンポーネントのオブジェクト プロトタイプを定義します|[!INCLUDE [alphanumerictype-description](includes/alphanumerictype-description.md)]|はい|
|`constructor`|オブジェクトを初期化するメソッド|[!INCLUDE [alphanumerictype-description](includes/alphanumerictype-description.md)]|はい|
|`control-type`|標準|[!INCLUDE [controltype-description](includes/controltype-description.md)]|いいえ|
|`description-key`|プロパティの説明を説明するローカライズされた文字列としてカスタマイズ画面で使用します。|`string`|いいえ|
|`display-name-key`|プロパティ名を説明するローカライズされた文字列としてカスタマイズ画面で使用します。|`string`|はい|
|`preview-image`|コンポーネントのプレビューをカスタマイザーに表示する、カスタマイズ画面で使用される画像|`string`|いいえ|
|`version`|[セマンティック バージョン](https://semver.org) で定義されたコンポーネントのバージョンを定義します。|`string`|はい|
|`hidden`|コンポーネントを非表示にするか定義します|[!INCLUDE [booleantype-description](includes/booleantype-description.md)]| いいえ|

## <a name="parent-elements"></a>親要素

|Element|説明|
|--|--|
|[マニフェスト](manifest.md)|[!INCLUDE [manifest-description](includes/manifest-description.md)]|

## <a name="child-elements"></a>下位要素

|Element|説明|発生回数|
|--|--|--|
|[データセット](data-set.md)|[!INCLUDE [data-set-description](includes/data-set-description.md)]|0 以上|
|[プロパティ](property.md)|[!INCLUDE [property-description](includes/property-description.md)]|0 以上|
|[リソース](resources.md)|[!INCLUDE [resources-description](includes/resources-description.md)]|1|
|[種類のグループ](type-group.md)|[!INCLUDE [type-group-description](includes/type-group-description.md)]|0 以上|

## <a name="example"></a>例

```xml
<control namespace="MyNameSpace" constructor="JSHelloWorldControl" version="1.0.0"
 display-name-key="JS_HelloWorldControl_Display_Key" description-key="JS_HelloWorldControl_Desc_Key"
 control-type="standard" preview-image="img/preview.png">
</control>
  ```

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークのマニフェスト スキーマ リファレンス](index.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../overview.md)
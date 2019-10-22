---
title: Control 要素 |Microsoft Docs
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
ms.assetid: 4dacd337-c9df-458e-86f3-bfb3ab543ea7
ms.openlocfilehash: aa02b89ce1e032a3cf2fdedca8f0fdf79cb84045
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72346626"
---
# <a name="control-element"></a>control 要素

[!INCLUDE [control-description](includes/control-description.md)]

## <a name="available-for"></a>利用可能な対象

モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー)

## <a name="attributes"></a>属性

|名前|Description|種類|必須|利用可能な対象|
|--|--|--|--|--------|
|`namespace`|コンポーネントのオブジェクトプロトタイプを定義します。|[!INCLUDE [alphanumerictype-description](includes/alphanumerictype-description.md)]|はい|モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー) (試験的なプレビュー)|
|`constructor`|オブジェクトを初期化するためのメソッド|[!INCLUDE [alphanumerictype-description](includes/alphanumerictype-description.md)]|はい|モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー) (試験的なプレビュー)|
|`control-type`|規格|[!INCLUDE [controltype-description](includes/controltype-description.md)]|いいえ|モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー) (試験的なプレビュー)|
|`description-key`|UI に表示されるコンポーネントの説明を定義します。|`string`|いいえ|モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー) (試験的なプレビュー)|
|`display-name-key`|UI に表示されるコントロールの名前を定義します。|`string`|はい|モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー) (試験的なプレビュー)|
|`preview-image`|コンポーネントのプレビューを表示するためにカスタマイズ画面で使用されるイメージです。|`string`|いいえ|モデル駆動型アプリ|
|`version`|[セマンティックバージョン管理](https://semver.org)で定義されているコンポーネントのバージョンを定義します|`string`|はい|モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー) (試験的なプレビュー)|
<!--|`hidden`|コンポーネントを非表示にするかどうかを定義します|[!INCLUDE [booleantype-description](includes/booleantype-description.md)]| いいえ|モデル駆動型アプリ|-->

## <a name="parent-elements"></a>親要素

|要素|Description|
|--|--|
|[マニフェスト](manifest.md)|[!INCLUDE [manifest-description](includes/manifest-description.md)]|

## <a name="child-elements"></a>子要素

|要素|Description|連続|
|--|--|--|
|[data-set](data-set.md)|[!INCLUDE [data-set-description](includes/data-set-description.md)]|0以上|
|[プロパティ](property.md)|[!INCLUDE [property-description](includes/property-description.md)]|0以上|
|[リソース](resources.md)|[!INCLUDE [resources-description](includes/resources-description.md)]|1|
|[type-group](type-group.md)|[!INCLUDE [type-group-description](includes/type-group-description.md)]|0以上|

## <a name="example"></a>例

```xml
<control namespace="MyNameSpace" constructor="JSHelloWorldControl" version="1.0.0"
 display-name-key="JS_HelloWorldControl_Display_Key" description-key="JS_HelloWorldControl_Desc_Key"
 control-type="standard" preview-image="img/preview.png">
</control>
  ```

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネントフレームワークマニフェストスキーマリファレンス](index.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../overview.md)
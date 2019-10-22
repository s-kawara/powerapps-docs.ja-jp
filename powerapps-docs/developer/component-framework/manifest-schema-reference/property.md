---
title: Property 要素 |Microsoft Docs
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
ms.assetid: 45f4872d-c1d2-4c5a-8721-251b96ede370
ms.openlocfilehash: ee4e0b0259d5978f3e84757d4023827ada45f01e
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72346143"
---
# <a name="property-element"></a>property 要素

[!INCLUDE [property-description](includes/property-description.md)]

## <a name="available-for"></a>利用可能な対象

モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー)

## <a name="attributes"></a>属性

|名前|Description|種類|必須|
|--|--|--|--|
|`name`|プロパティの名前|`string`|はい|
|`display-name-key`|カスタマイズ画面で、プロパティの名前を記述するローカライズされた文字列として使用されます。|`string`|はい|
|`of-type`|プロパティのデータ型を定義します。|「[解説](#remarks)」を参照|Optional|
|`usage`|Usage 属性は、プロパティが、コンポーネントが変更 (バインド) または読み取り専用の値 (入力) できるエンティティ属性を表すものかどうかを識別します。|`bound` または `input`|Optional|
|`required`|プロパティが必須かどうか|`boolean`|Optional|
|`of-type-group`|マニフェストで定義されている型グループの名前|`string`|Optional|
|`description-key`|カスタマイズ画面で、プロパティの説明を記述するローカライズされた文字列として使用されます。|`string`|Optional|
|`default-value`|コンポーネントに提供される既定の構成値。 モデル駆動型アプリでは、バインドされたパラメーターにはフィールドが関連付けられていると想定されているため、この属性は入力でのみ使用できます。|`string`|Optional|

### <a name="remarks"></a>」

@No__t_0 属性値には、次のいずれかを指定する必要があります。

[!INCLUDE [type-table](includes/type-table.md)]

## <a name="parent-elements"></a>親要素

|要素|Description|
|--|--|
|[マニフェスト](manifest.md)|[!INCLUDE [manifest-description](includes/manifest-description.md)]|


## <a name="example"></a>例

```xml
<property name="myFirstProperty" display-name-key="myFirstProperty_Display_Key" 
description-key="myFirstProperty_Desc_Key" of-type="SingleLine.Text" usage="bound" required="true" />
```

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネントフレームワークマニフェストスキーマリファレンス](index.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../overview.md)

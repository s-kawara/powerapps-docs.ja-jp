---
title: ポップアップ | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: b0af1803-ae3a-41c2-a8a5-b15970bd6f96
---

# <a name="popup"></a>ポップアップ

[!INCLUDE [popup-description](includes/popup-description.md)]

## <a name="closeonoutsideclick"></a>closeOnOutsideClick

範囲外のマウス クリックでポップアップを閉じるかを示します。

**種類**: `boolean`

## <a name="content"></a>内容

挿入される静的 DOM 要素

**種類**: [HTMLElement](https://developer.mozilla.org/docs/Web/API/HTMLElement)

## <a name="id"></a>id

アンカー コンポーネントがある場合に設定される ID。

**種類**: `string`

## <a name="name"></a>名前

ポップアップの名前。 ポップアップ を開く参照のように使用されます。

**種類**: `string`

## <a name="popuptoopen"></a>popupToOpen

開く必要があるポップアップ名。

**種類**: `string`

### <a name="remarks"></a>備考

ルート ポップアップでのみ定義されます。 入れ子になったポップアップを開くには `rootName.nestedName.[allOtherNestedNames]` のように文字列を指定します。 ポップアップを閉じるには、空文字列を指定します。 このプロパティは自動的に子に伝播されます。

## <a name="type"></a>種類

ポップアップの種類

**種類**: `enum`

`type` 値は以下の値を取り得る列挙値です。

|Value|メンバー|
|--|--|
|1|ルート|
|2|入れ子|

### <a name="remarks"></a>備考

ポップアップの各セットに対して `Root` ポップアップはひとつだけである必要があります。

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークの API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../overview.md)
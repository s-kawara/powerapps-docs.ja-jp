---
title: Popup | Microsoft Docs
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
ms.assetid: b0af1803-ae3a-41c2-a8a5-b15970bd6f96
ms.openlocfilehash: bb28a979ac721eded06025a56588023c211ea6f9
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72342210"
---
# <a name="popup"></a>Popup

[!INCLUDE [popup-description](includes/popup-description.md)]

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリ

## <a name="properties"></a>プロパティ

### <a name="closeonoutsideclick"></a>closeOnOutsideClick

マウスの外側をクリックしたときにポップアップを閉じるかどうかを示します。 @No__t_0 に設定すると、マウスの外側をクリックしてもポップアップは閉じられません。

**種類**: `boolean`

### <a name="content"></a>情報

挿入される静的な DOM 要素。

**型**:[では htmlelement](https://developer.mozilla.org/docs/Web/API/HTMLElement)

### <a name="id"></a>id

アンカーコンポーネントに設定される id (存在する場合)。

**種類**: `string`

### <a name="name"></a>指定

ポップアップの名前。 ポップアップを開くための参照として使用されます。

**種類**: `string`

### <a name="popuptoopen"></a>popupToOpen

開くポップアップの名前。

**種類**: `string`

### <a name="remarks"></a>」

ルートポップアップでのみ定義されている必要があります。 入れ子になったポップアップを開くには、`rootName.nestedName.[allOtherNestedNames]` のような文字列を指定する必要があります。 ポップアップを閉じるには、空の文字列を指定する必要があります。 このプロパティは、自動的に子に反映されます。

## <a name="type"></a>type

ポップアップの種類。列挙型の PopupType で説明されています。 ポップアップの各セットには、`root` ポップアップが1つだけ存在する必要があります。

**種類**: `enum`

@No__t_0 値は列挙型であり、次の値を使用できます。

|Value|Member|
|--|--|
|1|ルート|
|2|複合|

### <a name="remarks"></a>」

ポップアップの各セットの `Root` ポップアップは1つだけにする必要があります。

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネントフレームワーク API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../overview.md)
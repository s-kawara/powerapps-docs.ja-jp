---
title: コンテキスト | Microsoft Docs
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
ms.assetid: 6e066350-9d22-4078-b497-26be7d2fa374
ms.openlocfilehash: 4bb6c5cce36be1512ab10cdd2536a2b05fea3725
ms.sourcegitcommit: b8148ec3324b7ffed9fa5a28ea1f4df7e444a081
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/15/2019
ms.locfileid: "72347385"
---
# <a name="context"></a>関連

[!INCLUDE [context-description](includes/context-description.md)]

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー)

### <a name="client"></a>client

[!INCLUDE [client-description](includes/client-description.md)]
**種類**:[クライアント](client.md)

### <a name="device"></a>ドライブ

[!INCLUDE [device-description](includes/device-description.md)]

**種類**:[デバイス](device.md)

### <a name="factory"></a>factory

[!INCLUDE [factory-description](includes/factory-description.md)]

**種類**:[ファクトリ](factory.md)

### <a name="formatting"></a>書式設定

[!INCLUDE [formatting-description](includes/formatting-description.md)]

**種類**:[書式設定](formatting.md)

### <a name="mode"></a>Mode

[!INCLUDE [mode-description](includes/mode-description.md)]

**種類**:[モード](mode.md)

### <a name="navigation"></a>領域

[!INCLUDE [navigation-description](includes/navigation-description.md)]

**種類**:[ナビゲーション](navigation.md)

### <a name="parameters"></a>パラメータ

コンポーネントに提供されるデータ。 パラメーターおよびデータセットノードに対応する、コンポーネントのマニフェストで定義されている構造体。

**種類**: `TInputs`

### <a name="resources"></a>resources

`context.resource` のリソース インターフェイス

[!INCLUDE [resource-description](includes/resources-description.md)]

### <a name="updatedproperties"></a>updatedProperties

文字列の配列は、このコンポーネントに最後に渡されたとき以降にコンテキストオブジェクトでどの値が変更されたかを示します。

**種類**: `string[]`

### <a name="usersettings"></a>userSettings

[!INCLUDE [usersettings-description](includes/usersettings-description.md)]

**型**: [UserSettings](usersettings.md)

### <a name="utils"></a>utils

[!INCLUDE [utility-description](includes/utility-description.md)]

**型**: [Utility](utility.md)

### <a name="webapi"></a>webAPI

[!INCLUDE [webapi-description](includes/webapi-description.md)]

**型**: [WebApi](webapi.md)

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネントフレームワーク API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../overview.md)
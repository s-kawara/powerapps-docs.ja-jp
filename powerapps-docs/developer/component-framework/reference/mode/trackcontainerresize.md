---
title: TrackContainerResize |Microsoft Docs
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
ms.assetid: c5f482c2-dde2-460b-89a7-39e0efcc5704
ms.openlocfilehash: 8f9bc1ef17bdcb762e992d9f77dcdcd7ba1e8c50
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72342555"
---
# <a name="trackcontainerresize"></a>trackContainerResize

[!INCLUDE [trackcontainerresize-description](includes/trackcontainerresize-description.md)]。

コンポーネントをホストしている親コンテキストがモデル駆動型アプリの高さの制限を提供する場合、同じが子コンポーネントに適切に適用されます。 ただし、ほとんどのシナリオでは、親コンテキストによってコンポーネントの高さが制限されることはないため、"-1" を受け取り、さらに大きくなる可能性があることを示します。

キャンバスアプリでは、親コンテキストは、ドラッグアンドドロップエディターの性質によって、常にコンポーネントの高さと幅を提供します。

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリ

## <a name="syntax"></a>構文

`context.mode.trackContainerResize(value)`

## <a name="parameters"></a>パラメーター

| パラメーター名|種類|必須|Description|
| ------------- |----|--------|-----------|
|値|`Boolean`|はい|`True` コントロールがコンテナーのサイズを追跡する必要がある場合、コンポーネントは allocatedWidth または allocatedHeight を取得します。|


### <a name="related-topics"></a>関連トピック

[モード](../mode.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../../overview.md)

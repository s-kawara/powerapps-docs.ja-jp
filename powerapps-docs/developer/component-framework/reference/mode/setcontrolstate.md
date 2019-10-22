---
title: setControlState |Microsoft Docs
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
ms.assetid: 1052db82-7002-44ca-ad1f-9d3d4c311817
ms.openlocfilehash: 56c2221916781db646d27b131dfc00e61e742be3
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72342670"
---
# <a name="setcontrolstate"></a>setControlState

[!INCLUDE [setcontrolstate-description](includes/setcontrolstate-description.md)]

## <a name="syntax"></a>構文

`context.mode.setControlState(state);`

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー) 

## <a name="parameters"></a>パラメーター

| パラメーター名|種類|必須|Description|
| ------------- |----|--------|-----------|
|状態|`Dictionary`|はい|1人のユーザーに対して1つのセッションに保持されるデータ。|

## <a name="return-value"></a>戻り値

種類: `boolean`


### <a name="related-topics"></a>関連トピック

[モード](../mode.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../../overview.md)
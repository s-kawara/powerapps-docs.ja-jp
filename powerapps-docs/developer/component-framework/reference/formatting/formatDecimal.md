---
title: formatDecimal |Microsoft Docs
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
ms.assetid: 05c1c54d-14b5-4dad-9cd8-eec07e750c00
ms.openlocfilehash: 02f31ce76df0300fae517bbf4699c6d559b04591
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72343498"
---
# <a name="formatdecimal"></a>formatDecimal

[!INCLUDE [formatdecimal-description](includes/formatdecimal-description.md)]

## <a name="syntax"></a>構文

`context.formatting.formatDecimal(value, precision);`

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー)

## <a name="parameters"></a>パラメーター

| パラメーター名|種類|必須|Description|
| ------------- |----|--------|-----------|
|値|`number`|はい|書式設定する日付。|
|精度|`number`|はい|小数点の後の桁数。|

## <a name="return-value"></a>戻り値

種類: `string`


### <a name="related-topics"></a>関連トピック

[形式](../formatting.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../../overview.md)
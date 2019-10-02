---
title: openUrl | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 590078f3-c604-4bd0-ac74-9cf6d8806802
---

# <a name="openurl"></a>openUrl

[!INCLUDE [openurl-description](includes/openurl-description.md)]

## <a name="syntax"></a>構文

`openUrl(url, options)`

## <a name="parameters"></a>パラメーター

| パラメーター名|型|必須出席者|説明|
| ------------- |----|--------|-----------|
|url|`string`|はい|開く URL。|
|オプション|`OpenUrlOptions`|はい|URL のウィンドウ オプション。 OpenUrlOptions には以下のパラメータがあります: <br/>- **高さ**: `number`。 結果ページに表示されるウィンドウの高さです (単位はピクセル)。<br/>- **幅**: `number`。 結果ページに表示されるウィンドウの幅です (単位はピクセル)。|


### <a name="related-topics"></a>関連トピック

[ナビゲーション](../navigation.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../../overview.md)
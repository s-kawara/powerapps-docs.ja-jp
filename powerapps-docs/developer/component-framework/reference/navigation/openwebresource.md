---
title: openWebResource | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
author: Nkrb
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 27a1e54c-71fe-450f-8f84-b4cc125970bf
---

# <a name="openwebresource"></a>openWebResource

[!INCLUDE [openwebresource-description](includes/openwebresource-description.md)]

## <a name="syntax"></a>構文

`openWebResource(name, options, data)`

## <a name="parameters"></a>パラメーター

| パラメーター名|型|必須出席者|説明|
| ------------- |----|--------|-----------|
|名前|`string`|はい|開くところの HTML Web リソースの名前。|
|オプション|`OpenWebResourceOptions`|はい|Web リソースのウィンドウ オプション。 OpenWebResourceOptions は以下の属性を持ちます:<br/>- **高さ**: `number`。 結果ページに表示されるウィンドウの高さです (単位はピクセル)。<br/>- **幅**: `number`。 結果ページに表示されるウィンドウの幅です (単位はピクセル)。<br/>- **openInNewWindow**: `boolean`。 Web リソースを新しいウィンドウで開くか。|
|data|`string`|いいえ|データ パラメーターに渡されるデータ。


### <a name="related-topics"></a>関連トピック

[ナビゲーション](../navigation.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../../overview.md)
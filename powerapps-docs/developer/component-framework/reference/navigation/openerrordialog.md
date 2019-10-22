---
title: openErrorDialog |Microsoft Docs
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
ms.assetid: 10c154b9-45a0-44ee-a621-73d6a9009c6d
ms.openlocfilehash: c3371b7c3ea8bde869acc261ab7d4fc8f28ba7da
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72342440"
---
# <a name="openerrordialog"></a>openErrorDialog

[!INCLUDE [openerrordialog-description](includes/openerrordialog-description.md)]

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリ

## <a name="syntax"></a>構文

`context.navigation.openErrorDialog(options)`

## <a name="parameters"></a>パラメーター

| パラメーター名|種類|必須|Description|
| ------------- |----|--------|-----------|
|オプション|`ErrorDialogOptions`|はい|エラーダイアログオプション。 ErrorDialogOptions には次の属性があります。 <br/>-  の**詳細**: `String`。 エラーの詳細。 これを指定すると、 **[ログファイルのダウンロード]** ボタンがエラーメッセージに表示されます。このボタンをクリックすると、ユーザーはこの属性で指定されたコンテンツを含むテキストファイルをダウンロードできます。<br/>- **errorCode**: `Number`。 エラーコード。 ErrorCode を設定した場合は、エラーコードのメッセージがサーバーから自動的に取得され、エラーダイアログに表示されます。 **ErrorCode**値を指定すると、既定のエラーメッセージを含むエラーダイアログが表示されます。<br/>- **メッセージ**: `String`。 エラーダイアログに表示されるメッセージ。 **ErrorCode**または**message**属性を設定する必要があります。|

## <a name="return-value"></a>戻り値

種類: `Promise`

## <a name="remarks"></a>」

[Promise](https://developer.mozilla.org/docs/Web/JavaScript/reference/Global_Objects/Promise)と[ファイル](https://developer.mozilla.org/docs/Web/API/File)を参照


### <a name="related-topics"></a>関連トピック

[ナビゲーション](../navigation.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../../overview.md)
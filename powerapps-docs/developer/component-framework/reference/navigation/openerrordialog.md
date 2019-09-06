---
title: openErrorDialog | Microsoft Docs
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
ms.assetid: 10c154b9-45a0-44ee-a621-73d6a9009c6d
---
# <a name="openerrordialog"></a>openErrorDialog

[!INCLUDE [openerrordialog-description](includes/openerrordialog-description.md)]

## <a name="syntax"></a>構文

`openErrorDialog(options)`

## <a name="parameters"></a>パラメーター

| パラメーター名|型|必須出席者|説明|
| ------------- |----|--------|-----------|
|オプション|`ErrorDialogOptions`|はい|エラー ダイアログのオプション ErrorDialogOptions は以下の属性を持ちます: <br/>- **詳細**: `string`。 エラーに関する詳細。 これを指定すると、ログ ファイルのダウンロードボタンがエラー メッセージで使用できるようになり、それをクリックすると、ユーザーはこの属性に指定されたコンテンツを含むテキスト ファイルをダウンロードできます。<br/>- **errorCode**: `number`。 errorCode のみを設定した場合、エラー コードのメッセージがサーバーから自動的に取得され、エラー ダイアログに表示されます。 errorCode 値を指定すると、既定のエラー メッセージでエラー ダイアログが表示されます。<br/>- **message**: `string`。 エラー ダイアログに表示するメッセージ。|

## <a name="return-value"></a>戻り値

種類: `Promise`

## <a name="remarks"></a>備考

[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise) と [ファイル](https://developer.mozilla.org/docs/Web/API/File) を参照してください。


### <a name="related-topics"></a>関連トピック

[ナビゲーション](../navigation.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../../overview.md)
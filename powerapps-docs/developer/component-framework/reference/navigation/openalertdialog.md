---
title: openAlertDialog | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4acd3f17-74c0-4de1-9326-3778ff413f1e
---

# <a name="openalertdialog"></a>openAlertDialog

[!INCLUDE [openalertdialog-description](includes/openalertdialog-description.md)]

## <a name="syntax"></a>構文

`openAlertDialog(alertStrings, options)`

## <a name="parameters"></a>パラメーター

| パラメーター名|型|必須出席者|説明|
| ------------- |----|--------|-----------|
|alertStrings|`AlertDialogStrings`|はい|警告ダイアログで使用される文字列。 AlertDialogStrings は以下の属性を持ちます:<br/>- **テキスト**: `string`。 警告ダイアログに表示するメッセージ。 <br/>- **confirmButtonLabel**: `string`. 確認ボタン ラベルです。 ボタン ラベルを指定しない場合、ボタンのラベルとして (ユーザーの設定言語で) OK が使用されます。|
|オプション|`AlertDialogOptions`|はい|ダイアログのオプション。 AlertDialogOptions は以下の属性を持ちます:<br/>- **高さ**: `number`。 警告ダイアログのピクセル単位の高さ。 <br/>- **幅**: `number`。 警告ダイアログのピクセル単位の幅。|

## <a name="return-value"></a>戻り値

種類: `Promise`

## <a name="remarks"></a>備考

[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise) と [ファイル](https://developer.mozilla.org/docs/Web/API/File) を参照してください。

### <a name="related-topics"></a>関連トピック

[ナビゲーション](../navigation.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../../overview.md)
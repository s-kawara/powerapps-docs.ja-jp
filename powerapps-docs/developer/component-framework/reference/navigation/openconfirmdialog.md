---
title: openConfirmDialog | Microsoft Docs
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
ms.assetid: 83f2c208-696c-48b1-b65c-2ba7374d6cfc
---

# <a name="openconfirmdialog"></a>openConfirmDialog

[!INCLUDE [openconfirmdialog-description](includes/openconfirmdialog-description.md)]

## <a name="syntax"></a>構文

`openConfirmDialog(confirmStrings, options)`

## <a name="parameters"></a>パラメーター

| パラメーター名|型|必須出席者|説明|
| ------------- |----|--------|-----------|
|confirmStrings|`ConfirmDialogStrings`|はい|ダイアログで使用される文字列。 ConfirmDialogStrings は以下の属性を持ちます:<br/>- **タイトル**: `string`。 ダイアログのタイトルを確認します。 <br/>- **サブタイトル**: `string`。 ダイアログのサブタイトルを確認します。<br/>- **テキスト**: `string`。 ダイアログのテキスト / メッセージを確認します。<br/>- **confirmButtonLabel**: `string`. 確認ボタン ラベルです。 ボタン ラベルを指定しない場合、ボタンのラベルとして (ユーザーの設定言語で) OK が使用されます。|
|オプション|`ConfirmDialogOptions`|はい|ダイアログのオプション ConfirmDialogOptions は以下の属性を持ちます:<br/>- **高さ**: `number`。 確認ダイアログのピクセル単位の高さ。 <br/>- **幅**:`number`。 確認ダイアログのピクセル単位の幅|

## <a name="return-value"></a>戻り値

種類: `Promise<ConfirmDialogResponse>`

ダイアログをクローズするために確認ボタンがクリックされたかどうかを示す 確認済 (ブール値) 属性を持つオブジェクトが返されます。

## <a name="remarks"></a>備考

[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise) と [ファイル](https://developer.mozilla.org/docs/Web/API/File) を参照してください。


### <a name="related-topics"></a>関連トピック

[ナビゲーション](../navigation.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../../overview.md)
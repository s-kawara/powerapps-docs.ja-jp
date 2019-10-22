---
title: openConfirmDialog |Microsoft Docs
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
ms.assetid: 83f2c208-696c-48b1-b65c-2ba7374d6cfc
ms.openlocfilehash: 8b7bda89b9c8d83614a4a95281853676db9cf568
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72342486"
---
# <a name="openconfirmdialog"></a>openConfirmDialog

[!INCLUDE [openconfirmdialog-description](includes/openconfirmdialog-description.md)]

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリ

## <a name="syntax"></a>構文

`context.navigation.openConfirmDialog(confirmStrings, options)`

## <a name="parameters"></a>パラメーター

| パラメーター名|種類|必須|Description|
| ------------- |----|--------|-----------|
|confirmStrings|`ConfirmDialogStrings`|はい|ダイアログで使用される文字列。 Confirmの文字列には、次の属性があります。<br/>- **title**: `String`。 確認ダイアログに表示されるタイトル。 <br/>- **サブタイトル**: `String`。 確認ダイアログに表示されるサブタイトル。<br/>- **テキスト**: `String`。 確認ダイアログに表示されるメッセージ。<br/>- **Confirmbuttonlabel**: `String`。 [確認] ボタンのラベル。 ボタンのラベルを指定しない場合は、ボタンラベルとして **[OK]** (ユーザーの優先言語) が使用されます。<br/>- **Cancelbuttonlabel**: [キャンセル] ボタンのラベル `String` ます。 [キャンセル] ボタンのラベルを指定しなかった場合は、 **[キャンセル**] がボタンのラベルとして使用されます。|
|オプション|`ConfirmDialogOptions`|いいえ|ダイアログのオプション。 ConfirmDialogOptions には、次の属性があります。<br/>-  の**高さ**: `Number` します。 確認ダイアログの高さ (ピクセル単位)。 <br/>- **幅**: `Number`。 確認ダイアログの幅 (ピクセル単位)|

## <a name="return-value"></a>戻り値

種類: `Promise<ConfirmDialogResponse>`

説明: ダイアログを閉じるために [確認] ボタンがクリックされたかどうかを示す、確認済み (ブール値) の属性を持つオブジェクトを返します。

## <a name="remarks"></a>」

[Promise](https://developer.mozilla.org/docs/Web/JavaScript/reference/Global_Objects/Promise)を見る 


### <a name="related-topics"></a>関連トピック

[ナビゲーション](../navigation.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../../overview.md)
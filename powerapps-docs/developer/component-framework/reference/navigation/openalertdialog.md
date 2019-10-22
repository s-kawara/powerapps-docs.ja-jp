---
title: openAlertDialog |Microsoft Docs
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
ms.assetid: 4acd3f17-74c0-4de1-9326-3778ff413f1e
ms.openlocfilehash: f1f5a2a78faf3dd9c6a1d6d197fab61772969084
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72342509"
---
# <a name="openalertdialog"></a>openAlertDialog

[!INCLUDE [openalertdialog-description](includes/openalertdialog-description.md)]

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリ

## <a name="syntax"></a>構文

`context.navigation.openAlertDialog(alertStrings, options)`

## <a name="parameters"></a>パラメーター

| パラメーター名|種類|必須|Description|
| ------------- |----|--------|-----------|
|alertStrings|`AlertDialogStrings`|はい|警告ダイアログで使用する文字列。 Alertの文字列には、次の属性があります。<br/>- **テキスト**: `string`。 警告ダイアログに表示されるメッセージ。 <br/>- **Confirmbuttonlabel**: `string`。 [確認] ボタンのラベル。 ボタンのラベルを指定しない場合は、ボタンラベルとして **[OK]** (ユーザーの優先言語) が使用されます。|
|オプション|`AlertDialogOptions`|はい|ダイアログオプション。 Alertのオプションには、次の属性があります。<br/>-  の**高さ**: `number` します。 警告ダイアログの高さ (ピクセル単位)。 <br/>- **幅**: `number`。 警告ダイアログの幅 (ピクセル単位)|

## <a name="return-value"></a>戻り値

種類: `Promise`

## <a name="remarks"></a>」

[Promise](https://developer.mozilla.org/docs/Web/JavaScript/reference/Global_Objects/Promise)と[ファイル](https://developer.mozilla.org/docs/Web/API/File)を参照

## <a name="example"></a>例 

```TypeScript
context.navigation.openAlertDialog({text:"This is an alert.", confirmButtonLabel : "Yes",}).then(
        function success()
        {
            document.getElementById("openAlertDialogButton")!.innerHTML = "Alert dialog closed";
        },
        function()
        {
            document.getElementById("openAlertDialogButton")!.innerHTML = "Error in Alert Dialog";
        }
    );
```

### <a name="related-topics"></a>関連トピック

[ナビゲーション](../navigation.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../../overview.md)
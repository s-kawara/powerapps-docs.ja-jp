---
title: モデル駆動型アプリにおける openConfirmDialog (Client API リファレンス) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 9c82028d-cbc9-4d40-9987-6ce1ea01fde2
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="openconfirmdialog-client-api-reference"></a>openConfirmDialog (クライアント API 参照)



[!INCLUDE[./includes/openConfirmDialog-description.md](./includes/openConfirmDialog-description.md)]

## <a name="syntax"></a>構文

`Xrm.Navigation.openConfirmDialog(confirmStrings,confirmOptions).then(successCallback,errorCallback);`

## <a name="parameters"></a>パラメーター

|Name |種類​​ |必須出席者 |内容 |
|---|---|---|---|
|confirmStrings|オブジェクト|あり|確認ダイアログで使用される文字列。 オブジェクトには、次の属性が含まれています。<br/>- **cancelButtonLabel**: (任意) 文字列。 キャンセル ボタン ラベルです。 キャンセル ボタン ラベルを指定しない場合、ボタンのラベルとして**キャンセル**が使用されます。<br/>- **confirmButtonLabel**: (任意) 文字列。 確認ボタン ラベルです。 確認ボタン ラベルを指定しない場合、ボタンのラベルとして **OK** が使用されます。<br/>- **subtitle**: (任意) 文字列。 確認ダイアログに表示するサブタイトル。<br/>- **text**: 文字列。 確認ダイアログに表示されるメッセージ。<br/>- **title**: (任意) 文字列。 確認ダイアログに表示されるタイトル。|
|confirmOptions|オブジェクト|いいえ|確認ダイアログの高さと幅のオプション。 オブジェクトには、次の属性が含まれています。<br/>- **height**: (任意) 数値。 確認ダイアログのピクセル単位の高さ。<br/>- **width**: (任意) 数値。 確認ダイアログのピクセル単位の幅。|
|successCallback|関数|No|ダイアログの右上隅にある確認、キャンセル、または **X** をクリックすることで確認ダイアログがクローズされるときに実行する関数。 ダイアログをクローズするために確認ボタンがクリックされたかどうかを示す **confirmed** (ブール値) 属性を持つオブジェクトが渡されます。|
|errorCallback|関数|No|処理が失敗したときに実行する関数。|

## <a name="example"></a>例

次のコード サンプルは、確認ダイアログ ボックスを表示します。 ダイアログを閉じるために確認またはキャンセル/**X** がクリックされたかどうかに応じて、適切なメッセージがコンソールに記録されます。

```JavaScript
var confirmStrings = { text:"This is a confirmation.", title:"Confirmation Dialog" };
var confirmOptions = { height: 200, width: 450 };
Xrm.Navigation.openConfirmDialog(confirmStrings, confirmOptions).then(
function (success) {    
    if (success.confirmed)
        console.log("Dialog closed using OK button.");
    else
        console.log("Dialog closed using Cancel button or X.");
});

```

### <a name="related-topics"></a>関連トピック

[Xrm.Navigation](../xrm-navigation.md)


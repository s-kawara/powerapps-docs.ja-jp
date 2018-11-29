---
title: モデル駆動型アプリにおける openAlertDialog (Client API リファレンス) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 8615a284-41b4-479c-81bd-577b3b7c79ad
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="openalertdialog-client-api-reference"></a>openAlertDialog (クライアント API 参照)



[!INCLUDE[./includes/openAlertDialog-description.md](./includes/openAlertDialog-description.md)]

## <a name="syntax"></a>構文

`Xrm.Navigation.openAlertDialog(alertStrings,alertOptions).then(closeCallback,errorCallback);`

## <a name="parameters"></a>パラメーター

|Name |種類​​ |必須出席者 |内容 |
|---|---|---|---|
|alertStrings|オブジェクト|あり|警告ダイアログで使用される文字列。 オブジェクトには、次の属性が含まれています。<br/>- **confirmButtonLabel**: (任意) 文字列。 確認ボタン ラベルです。 ボタンのラベルを指定しない場合、ボタンのラベルとして **OK** が使用されます。<br/>- **text**: 文字列。 警告ダイアログに表示するメッセージ。|
|alertOptions|オブジェクト|No|警告ダイアログの高さと幅のオプション。 オブジェクトには、次の属性が含まれています。<br/>- **height**: (任意) 数値。 警告ダイアログのピクセル単位の高さ。<br/>- **width**: (任意) 数値。 警告ダイアログのピクセル単位の幅。|
|successCallback|関数|No|警告ダイアログが、確認ボタンをクリックしてクローズされるか、Esc キーを押してキャンセルされるときに実行される関数です。|
|errorCallback|関数|No|処理が失敗したときに実行する関数。|


## <a name="example"></a>例

次のサンプル コードは、警告ダイアログを表示します。 警告ダイアログの**はい**をクリックするか、または Esc キーを押して警告ダイアログをキャンセルすると、`close` 関数が呼び出されます。

```JavaScript
var alertStrings = { confirmButtonLabel: "Yes", text: "This is an alert." };
var alertOptions = { height: 120, width: 260 };
Xrm.Navigation.openAlertDialog(alertStrings, alertOptions).then(
    function success(result) {
        console.log("Alert dialog closed");
    },
    function (error) {
        console.log(error.message);
    }
);
```

### <a name="related-topics"></a>関連トピック

[Xrm.navigation](../xrm-navigation.md)


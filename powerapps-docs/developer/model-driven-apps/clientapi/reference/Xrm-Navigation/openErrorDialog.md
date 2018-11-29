---
title: モデル駆動型アプリにおける openErrorDialog (Client API リファレンス) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 9749143d-c159-4833-aff9-d8bc2c3395f3
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="openerrordialog-client-api-reference"></a>openErrorDialog (クライアント API 参照)



[!INCLUDE[./includes/openErrorDialog-description.md](./includes/openErrorDialog-description.md)]

## <a name="syntax"></a>構文

`Xrm.Navigation.openErrorDialog(errorOptions).then(successCallback,errorCallback);`

## <a name="parameters"></a>パラメーター

|Name |種類​​ |必須出席者 |内容 |
|---|---|---|---|
|errorOptions|オブジェクト|あり|エラー ダイアログのオプションを指定するオブジェクト。 オブジェクトには、次の属性が含まれています。<br/>- **details**: (任意) 文字列。 エラーに関する詳細。 これを指定すると、**ログ ファイルのダウンロード**ボタンがエラー メッセージで使用できるようになり、それをクリックすると、ユーザーはこの属性に指定されたコンテンツを含むテキスト ファイルをダウンロードできます。<br/>- **errorCode**: (任意) 数値。 エラー コード。 **errorCode** のみを設定した場合、エラー コードのメッセージがサーバーから自動的に取得され、エラー ダイアログに表示されます。 無効な **errorCode** 値を指定すると、既定のエラー メッセージでエラー ダイアログが表示されます。<br/>- **message**: (任意) 文字列。 エラー ダイアログに表示するメッセージ。<br/><br/>**errorCode** または **message** 属性のいずれかを設定する必要があります。 |
|successCallback|関数|No|エラー ダイアログがクローズされると実行される関数です。|
|errorCallback|関数|No|処理が失敗したときに実行する関数。|

## <a name="example"></a>例

次のコード サンプルは、正しくない errorCode (1234) を渡して、既定のメッセージでエラー ダイアログを表示します。

```JavaScript
Xrm.Navigation.openErrorDialog({ errorCode:1234 }).then(
    function (success) {
        console.log(success);        
    },
    function (error) {
        console.log(error);
    });
```

これにより、既定のメッセージでエラー ダイアログが表示されます。

![既定のメッセージを含むエラー ダイアログ](../../../media//clientapi_sampleerrordialog.png)

### <a name="related-topics"></a>関連トピック

[Xrm.Navigation](../xrm-navigation.md)


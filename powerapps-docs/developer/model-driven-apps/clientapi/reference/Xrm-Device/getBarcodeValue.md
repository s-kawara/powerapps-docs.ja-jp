---
title: getBarcodeValue| MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 0218b96c-2809-4f2d-9f9f-d8ee8f8e3b7b
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getbarcodevalue-client-api-reference"></a>getBarcodeValue (クライアント API 参照)



[!INCLUDE[./includes/getBarcodeValue-description.md](./includes/getBarcodeValue-description.md)]


## <a name="syntax"></a>構文

`Xrm.Device.getBarcodeValue().then(successCallback, errorCallback)`

## <a name="parameters"></a>パラメーター

| パラメーター名        | 種類​​           | 必須出席者  |内容  |
| ------------- |-------------| -----|-----|
|successCallback |関数 | あり|バーコード値が文字列として返される場合に呼び出す関数。|
|errorCallback |関数 | あり|処理が失敗したときに呼び出す関数。 エラーの詳細を記述した **message** プロパティ (文字列) を持つエラー オブジェクトが渡されます。|
 

## <a name="return-value"></a>戻り値
成功時に、スキャンされたバーコード値を含む文字列を返します。

## <a name="remarks"></a>備考
このメソッドは、モバイルクライアントでのみサポートされます。

## <a name="example"></a>例

```JavaScript
Xrm.Device.getBarcodeValue().then(
    function success(result) {
        Xrm.Navigation.openAlertDialog({ text: "Barcode value: " + result });
    },
    function (error) {
        Xrm.Navigation.openAlertDialog( {text: error.message} );
    }
);
``` 

### <a name="related-topics"></a>関連トピック
[Xrm.Device](../xrm-device.md)


---
title: getCurrentPosition| MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 062a52d8-170c-4e98-b48a-ac99ec759f83
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getcurrentposition-client-api-reference"></a>getCurrentPosition (クライアント API 参照)



[!INCLUDE[./includes/getCurrentPosition-description.md](./includes/getCurrentPosition-description.md)]


## <a name="syntax"></a>構文

`Xrm.Device.getCurrentPosition().then(successCallback, errorCallback)`

## <a name="parameters"></a>パラメーター

| パラメーター名        | 種類​​           | 必須出席者  |内容  |
| ------------- |-------------| -----|-----|
|successCallback |関数 | あり|現在の物理的場所情報が返される場合に呼び出す関数。 次の属性の物理的場所オブジェクトは関数に渡されます。<br/>- **coords**: 関連する精度を伴った地理座標のセットだけでなく、高度および速度などその他の任意の属性のセットが含まれます。 <br/>- **timestamp**: オブジェクトを取得した時間が DOMTimeStamp として表されます。|
|errorCallback |機能 | あり|処理が失敗したときに呼び出す関数。 次のプロパティを持つオブジェクトが渡されます。 <br/>- **code**: エラー コード。 番号。 <br/>- **message**: エラーの詳細を記述するローカライズされたメッセージ。 文字列。<br/><br/>ユーザーの場所設定がモバイル デバイスで有効ではない場合、エラー メッセージが表示されます。 モデル駆動型アプリ モバイル クライアントの以前のバージョンを使用している場合、または物理的場所機能がモバイル デバイス上で使用できない場合、エラー コールバックに null が渡されます。|
 

## <a name="return-value"></a>戻り値
成功時に、**successCallback** 関数で指定済みの属性を持つ geolocation オブジェクトを返します。

## <a name="remarks"></a>備考
**getCurrentPosition** メソッドが機能するには、物理的場所機能がモバイル デバイスで有効になっている必要があり、モデル駆動型アプリ モバイル クライアントは、既定で有効になっていないデバイスの場所へのアクセス許可が必要です。

このメソッドは、モバイルクライアントでのみサポートされます。

## <a name="example"></a>例

```JavaScript
Xrm.Device.getCurrentPosition().then(
    function success(location) {
        Xrm.Navigation.openAlertDialog({
            text: "Latitude: " + location.coords.latitude +
            ", Longitude: " + location.coords.longitude
        });
    },
    function (error) {
        Xrm.Navigation.openAlertDialog({ text: error.message });
    }
);
```

### <a name="related-topics"></a>関連トピック
[Xrm.Device](../xrm-device.md)


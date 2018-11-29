---
title: captureImage | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 1b24e8b2-20af-4e75-8c00-1aa393c07aef
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="captureimage-client-api-reference"></a>captureImage (クライアントAPI参照)



[!INCLUDE[./includes/captureImage-description.md](./includes/captureImage-description.md)]


## <a name="syntax"></a>構文

`Xrm.Device.captureImage(imageOptions).then(successCallback, errorCallback)`

## <a name="parameters"></a>パラメーター

| パラメーター名        | 種類           | 必須出席者  |内容  |
| ------------- |-------------| -----|-----|
|imageOptions |オブジェクト | No|次の属性があるオブジェクト:<br/>- **allowEdit**: 保存する前に画像を編集するかどうかを指定します。 ブール値。<br/>- **高さ**: 取り込むイメージの高さ。 番号。<br/>- **preferFrontCamera**: デバイスの前部カメラを使用して画像を取り込むかどうかを指定します。 ブール値。<br/>- **品質**: パーセント値で表した画像ファイルの品質。 番号。<br/>- **幅**: 取り込むイメージの幅。 数値..|
|successCallback |関数 | あり|画像が返される場合に呼び出す関数。 次の属性のBase64でエンコードされた画像オブジェクトは関数に渡されます:<br/>- **fileContent**: 画像ファイルの内容です。 String <br/>- **fileName**: 画像ファイルのファイル名です。 文字列。<br/>- **fileSize**: 画像ファイルのサイズ(KB)です。 番号。<br/>- **mimeType**: 画像ファイルのMIMEタイプです。 文字列。|
|errorCallback |関数 | あり|処理が失敗したときに呼び出す関数。 |
 

## <a name="return-value"></a>戻り値
成功時に、先に指定した属性を使用して、Base64 でエンコードされたイメージ オブジェクトを返します。

## <a name="remarks"></a>備考
このメソッドは、モバイルクライアントでのみサポートされます。

### <a name="related-topics"></a>関連トピック
[Xrm.Device](../xrm-device.md)


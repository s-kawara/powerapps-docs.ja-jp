---
title: captureAudio | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: fa39d18e-4b82-423a-84a0-e54450b7964e
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="captureaudio-client-api-reference"></a>captureAudio (クライアントAPI参照)



[!INCLUDE[./includes/captureAudio-description.md](./includes/captureAudio-description.md)]


## <a name="syntax"></a>構文

`Xrm.Device.captureAudio().then(successCallback, errorCallback)`

## <a name="parameters"></a>パラメーター

| パラメーター名        | 種類           | 必須出席者  |内容  |
| ------------- |-------------| -----|-----|
|successCallback |関数 | あり|音声が返される場合に呼び出す関数。 次の属性のBase64でエンコードされたオーディオオブジェクトは関数に渡されます:<br/>- **fileContent**: 音声ファイルの内容です。 String <br/>- **fileName**: 音声ファイルのファイル名です。 文字列。<br/>- **fileSize**: 音声ファイルのサイズ(KB)です。 番号。<br/>- **mimeType**: 音声ファイルのMIMEタイプです。 文字列。|
|errorCallback |関数 | あり|処理が失敗したときに呼び出す関数。 |
 

## <a name="return-value"></a>戻り値
成功時に、先に指定した属性を使用して、Base64 でエンコードされた音声オブジェクトを返します。

## <a name="remarks"></a>備考
このメソッドは、モバイルクライアントでのみサポートされます。

### <a name="related-topics"></a>関連トピック
[Xrm.Device](../xrm-device.md)


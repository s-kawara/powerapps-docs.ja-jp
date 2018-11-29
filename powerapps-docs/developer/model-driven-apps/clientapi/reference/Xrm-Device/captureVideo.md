---
title: captureVideo | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 9580d05a-a91f-4126-b94b-4d1068da35fa
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="capturevideo-client-api-reference"></a>captureVideo (クライアントAPI参照)



[!INCLUDE[./includes/captureVideo-description.md](./includes/captureVideo-description.md)]


## <a name="syntax"></a>構文

`Xrm.Device.captureVideo().then(successCallback, errorCallback)`

## <a name="parameters"></a>パラメーター

| パラメーター名        | 種類           | 必須出席者  |内容  |
| ------------- |-------------| -----|-----|
|successCallback |関数 | あり|動画が返される場合に呼び出す関数。 次の属性のBase64でエンコードされた動画オブジェクトは関数に渡されます:<br/>- **fileContent**: 動画ファイルの内容です。 String <br/>- **fileName**: 動画ファイルのファイル名です。 文字列。<br/>- **fileSize**: 動画ファイルのサイズ(KB)です。 番号。<br/>- **mimeType**: 動画ファイルのMIMEタイプです。 文字列。|
|errorCallback |関数 | あり|処理が失敗したときに呼び出す関数。 |
 

## <a name="return-value"></a>戻り値
成功時に、先に指定した属性を使用して、Base64 でエンコードされたビデオ オブジェクトを返します。

## <a name="remarks"></a>備考
このメソッドは、モバイルクライアントでのみサポートされます。

### <a name="related-topics"></a>関連トピック
[Xrm.Device](../xrm-device.md)


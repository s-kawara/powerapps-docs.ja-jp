---
title: pickFile| MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: c777a0b8-2b07-458b-8a4f-8938f7a2e696
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="pickfile-client-api-reference"></a>pickFile (クライアント API 参照)



[!INCLUDE[./includes/pickFile-description.md](./includes/pickFile-description.md)]


## <a name="syntax"></a>構文

`Xrm.Device.pickFile(pickFileOptions).then(successCallback, errorCallback)`

## <a name="parameters"></a>パラメーター

| パラメーター名        | 種類​​           | 必須出席者  |内容  |
| ------------- |-------------| -----|-----|
|pickFileOptions |オブジェクト | No|次の属性があるオブジェクト:<br/>- **accept**: 選択するイメージ ファイルの種類。 有効な値は、"audio"、"video"、または "image" です。 ストリング。<br/>- **allowMultipleFiles**: 複数のファイルを選択できるようにするかどうかを示します。 ブール値。<br/>- **maximumAllowedFileSize**: 選択するファイルの最大サイズ。 番号。|
|successCallback |関数 | あり|選択したファイルが返されるときに呼び出す関数。 *各* オブジェクトが以下の属性を持つオブジェクトの配列が関数に渡されます。<br/>- **fileContent**: ファイルの内容です。 String <br/>- **fileName**: ファイルの名前です。 ストリング。<br/>- **fileSize**: ファイルのサイズ (KB) です。 番号。<br/>- **mimeType**: ファイルの MIME タイプです。 ストリング。|
|errorCallback |関数 | あり|処理が失敗したときに呼び出す関数。 |
 

## <a name="return-value"></a>戻り値
成功時には、**successCallback** 関数に以前に指定されたオブジェクトの配列がある Promise を返します。

### <a name="related-topics"></a>関連トピック
[Xrm.Device](../xrm-device.md)


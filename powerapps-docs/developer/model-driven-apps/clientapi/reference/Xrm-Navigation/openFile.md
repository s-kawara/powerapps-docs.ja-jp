---
title: モデル駆動型アプリの openFile (Client API reference)| MicrosoftDocs
ms.date: 01/25/2019
ms.service: powerapps
ms.topic: reference
ms.assetid: 6a2497fe-08ad-4953-b3ff-44c72bc25082
author: KumarVivek
ms.author: kvivek
manager: annbe
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="openfile-client-api-reference"></a>openFile (クライアント API 参照)

[!INCLUDE[./includes/openFile-description.md](./includes/openFile-description.md)]

## <a name="syntax"></a>構文

`Xrm.Navigation.openFile(file,openFileOptions)`

## <a name="parameters"></a>パラメーター

| パラメーター名        | 種類​​           | 必須出席者  |内容  |
| ------------- |-------------| -----|-----|
|ファイル |オブジェクト | あり|開くファイルを説明するオブジェクト。 オブジェクトには次の属性があります。<br/>- **fileContent**: 文字列。 ファイルの内容です。  <br/>- **fileName**: 文字列。 ファイルの名前。<br/>- **fileSize**: 数値。 ファイルのサイズ (KB) です。<br/>- **mimeType**: 文字列。 ファイルの MIME の種類です。|
|openFileOptions |オブジェクト | なし|ファイルを開くか、保存するかを記述するオブジェクトです。 オブジェクトには、次の属性があります。<br/>- **openMode**: `1` (開く) `2` を指定して保存します。 <br/>このパラメーターを指定しない場合、既定で `1` (開く) が渡されます。<br/>このパラメーターは、統一インターフェイス上でのみサポートされます。|

### <a name="related-topics"></a>関連トピック

[Xrm.Navigation](../xrm-navigation.md)

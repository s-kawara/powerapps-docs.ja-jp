---
title: モデル駆動型アプリの openFile (Client API reference)| MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 6a2497fe-08ad-4953-b3ff-44c72bc25082
author: KumarVivek
ms.author: kvivek
manager: amyla
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
|openFileOptions |数値 | No|ファイルを開くか、保存するかを指定します。<br/> `1:Open`<br/> `2:Save`<br/>このパラメーターを指定しない場合、既定で **1** (開く) が渡されます。|

### <a name="related-topics"></a>関連トピック

[Xrm.Navigation](../xrm-navigation.md)

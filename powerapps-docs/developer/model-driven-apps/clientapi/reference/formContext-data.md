---
title: モデル駆動型アプリの formContext.data (クライアント API 参照) | Microsoft Docs
description: クライアント API を使用したモデル駆動型アプリのプロセスの作業の詳細
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 32e8d1d0-4093-4588-a517-2930eec34dce
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="formcontextdata-client-api-reference"></a>formContext.data (クライアント API 参照)



フォーム上のデータを操作するプロパティとメソッドを提供します。

![formContext データ オブジェクト モデル](../../media/ClientAPI-formContext-data-Model.png)

## <a name="properties"></a>プロパティ​​

|Name|内容|
|--|--|
|属性|フォーム上のエンティティ以外のデータの収集。 このコレクションのアイテムは、attributes コレクションと同じ種類ですが、フォーム エンティティの属性ではありません。 <br/>詳細: [コレクション](collections.md)|
|エンティティ|ページに表示されるレコードに固有の情報を取得するメソッド、save メソッド、およびフォーム上に含まれるすべての属性のコレクションを提供します。 属性データは、フォーム上のフィールドによって表される属性に制限されています。 <br/>詳細: [formContext.data.entity](formContext-data-entity.md)|
|プロセス|フォームの業務プロセス フローのデータを操作するためのオブジェクトおよびメソッドを提供します。<br/>詳細: [formContext.data.process](formContext-data-process.md)|


## <a name="methods"></a>メソッド 

|Name|内容|
|--|--|
|[addOnLoad](formContext-data/addOnload.md)|[!INCLUDE[formContext-data/includes/addOnLoad-description.md](formContext-data/includes/addOnLoad-description.md)]|
|[getIsDirty](formContext-data/getIsDirty.md)|[!INCLUDE[formContext-data/includes/getIsDirty-description.md](formContext-data/includes/getIsDirty-description.md)]|
|[isValid](formContext-data/isValid.md)|[!INCLUDE[formContext-data/includes/isValid-description.md](formContext-data/includes/isValid-description.md)]|
|[最新の情報に更新](formContext-data/refresh.md)|[!INCLUDE[formContext-data/includes/refresh-description.md](formContext-data/includes/refresh-description.md)]|
|[removeOnLoad](formContext-data/removeOnLoad.md)|[!INCLUDE[formContext-data/includes/removeOnLoad-description.md](formContext-data/includes/removeOnLoad-description.md)]|
|[save](formContext-data/save.md)|[!INCLUDE[formContext-data/includes/save-description.md](formContext-data/includes/save-description.md)]|


### <a name="related-topics"></a>関連トピック

[formContext.data.entity](formContext-data-entity.md)

[formContext.data.process](formContext-data-process.md)





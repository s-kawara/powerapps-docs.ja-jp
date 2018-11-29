---
title: モデル駆動型アプリにおける refresh (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 03e970ee-7ed3-4df2-9670-222d76a479fd
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="refresh-client-api-reference"></a>refresh (クライアント API 参照)



[!INCLUDE[./includes/refresh-description.md](./includes/refresh-description.md)]

## <a name="syntax"></a>構文

`formContext.data.refresh(save).then(successCallback, errorCallback);`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|上書き保存​​|Boolean|No|データを更新後に保存する場合は true、それ例外の場合は false。|
|successCallback|関数|No|処理が成功したときに呼び出す関数。|
|errorCallback|関数|No|処理が失敗したときに呼び出す関数。|

### <a name="related-topics"></a>関連トピック

[formContext](../../clientapi-form-context.md)


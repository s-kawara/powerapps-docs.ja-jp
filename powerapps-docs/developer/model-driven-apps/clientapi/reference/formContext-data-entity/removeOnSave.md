---
title: モデル駆動型アプリにおける removeOnSave (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 14a92f7c-f4c0-475d-8797-dcbb283db37a
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="removeonsave-client-api-reference"></a>removeOnSave (クライアント API 参照)



[!INCLUDE[./includes/removeOnSave-description.md](./includes/removeOnSave-description.md)]

## <a name="syntax"></a>構文

`formContext.data.entity.removeOnSave(myFunction)`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|myFunction|関数リファレンス|あり|**OnSave** イベントの削除する関数。

### <a name="related-topics"></a>関連トピック

[addOnSave](addOnSave.md)

[フォーム OnSave イベント](../events/form-onsave.md)


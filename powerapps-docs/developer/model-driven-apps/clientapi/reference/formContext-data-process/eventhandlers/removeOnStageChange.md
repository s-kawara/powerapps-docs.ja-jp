---
title: モデル駆動型アプリにおける removeOnStageChange (Client API リファレンス) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 649fe7b0-016d-409f-ba3c-b14e0f1953e0
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="removeonstagechange-client-api-reference"></a>removeOnStageChange (クライアント API 参照)

[!INCLUDE[./includes/removeOnStageChange-description.md](./includes/removeOnStageChange-description.md)]

## <a name="syntax"></a>構文

`formContext.data.process.removeOnStageChange(myFunction);`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|myFunction|関数リファレンス|あり|[OnStageChange](../../events/onstagechange.md) イベントから削除する関数。|

### <a name="related-topics"></a>関連トピック

[addOnStageChange](addOnStageChange.md)
 
[formContext.data.process](../../formContext-data-process.md)
 



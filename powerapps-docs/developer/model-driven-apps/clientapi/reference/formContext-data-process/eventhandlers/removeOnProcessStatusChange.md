---
title: モデル駆動型アプリにおける removeOnProcessStatusChange (Client API リファレンス) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 5e41f59e-ddb3-4d47-b45b-454aa9e04439
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="removeonprocessstatuschange-client-api-reference"></a>removeOnProcessStatusChange (クライアント API 参照)



[!INCLUDE[./includes/removeOnProcessStatusChange-description.md](./includes/removeOnProcessStatusChange-description.md)]

## <a name="syntax"></a>構文

`formContext.data.process.removeOnProcessStatusChange(myFunction);`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|myFunction|関数リファレンス|あり|[OnProcessStatusChange](../../events/onprocessstatuschange.md) イベントから削除する関数。|

### <a name="related-topics"></a>関連トピック

[addOnProcessStatusChange](addOnProcessStatusChange.md)
 
[formContext.data.process](../../formContext-data-process.md)
 



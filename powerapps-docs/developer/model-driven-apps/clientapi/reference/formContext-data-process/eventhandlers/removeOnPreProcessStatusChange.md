---
title: Dynamics 365 for Customer Engagement の removeOnPreProcessStatusChange (クライアント API 参照) | MicrosoftDocs
ms.date: 06/30/2019
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 for Customer Engagement (online)
ms.assetid: null
author: MSFTMan
ms.author: Deonhe
manager: KVivek
search.audienceType:
  - developer
search.app:
  - D365CE
---
# <a name="removeonpreprocessstatuschange-client-api-reference"></a>removeOnPreProcessStatusChange (クライアント API 参照)

[!INCLUDE[](../../../../../../includes/cc_applies_to_update_9_0_0.md)]

[!INCLUDE[./includes/removeOnPreProcessStatusChange-description.md](./includes/removeOnPreProcessStatusChange-description.md)]

## <a name="syntax"></a>構文

`formContext.data.process.removeOnPreProcessStatusChange(myFunction);`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|myFunction|関数リファレンス|あり|[OnPreProcessStatusChange](../../events/onpreprocessstatuschange.md) イベントから削除される関数。|

### <a name="related-topics"></a>関連トピック

[addOnProcessStatusChange](addOnProcessStatusChange.md)
 
[formContext.data.process](../../formContext-data-process.md)
 



---
title: モデル駆動型アプリにおける removeOnPreStageChange (Client API リファレンス) | Microsoft Docs
ms.date: 08/05/2019
ms.service: powerapps
ms.topic: reference
applies_to: Dynamics 365 (online)
author: MsftMan
ms.author: DeonHe
manager: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="removeonprestagechange-client-api-reference"></a>removeOnPreStageChange (クライアント API 参照)

[!INCLUDE[./includes/removeOnPreStageChange-description.md](./includes/removeOnPreStageChange-description.md)]

## <a name="syntax"></a>構文

`formContext.data.process.removeOnPreStageChange(myFunction);`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|myFunction|関数リファレンス|あり|[OnPreStageChange](../../events/onprestagechange.md) イベントから削除される関数。|

### <a name="related-topics"></a>関連トピック

[addOnPreStageChange](addOnPreStageChange.md)
 
[formContext.data.process](../../formContext-data-process.md)
 



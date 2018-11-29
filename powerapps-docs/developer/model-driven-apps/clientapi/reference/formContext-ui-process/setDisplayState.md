---
title: モデル駆動型アプリの setDisplayState (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 21368fac-d4bc-4f75-8a9c-cce098fa0b45
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="setdisplaystate-client-api-reference"></a>setDisplayState (クライアント API 参照)



[!INCLUDE[./includes/setDisplayState-description.md](./includes/setDisplayState-description.md)]

## <a name="syntax"></a>構文

`formContext.ui.process.setDisplayState(state);`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|状態|String|あり|"展開"、"折りたたみ"、または "フローティング" を指定します。 "フローティング" 値は Web クライアントではサポートされていません。|

### <a name="related-topics"></a>関連トピック

[getDisplayState](getDisplayState.md)

[formContext.ui.process](../formContext-ui-process.md)




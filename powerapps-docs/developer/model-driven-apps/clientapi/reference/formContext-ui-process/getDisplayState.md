---
title: モデル駆動型アプリの getDisplayState (クライアント API 参照)| MicrosoftDocs
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
# <a name="getdisplaystate-client-api-reference"></a>getDisplayState (クライアント API 参照)



[!INCLUDE[./includes/getDisplayState-description.md](./includes/getDisplayState-description.md)]

## <a name="syntax"></a>構文

`formContext.ui.process.getDisplayState();`

## <a name="return-value"></a>戻り値

**種類**: 文字列。

**説明**: Web クライアントでは "展開" または "折りたたみ" を返します。統一インターフェイスでは "展開"、"折りたたみ"、または "フローティング" を返します。

### <a name="related-topics"></a>関連トピック

[setDisplayState](setDisplayState.md)

[formContext.ui.process](../formContext-ui-process.md)




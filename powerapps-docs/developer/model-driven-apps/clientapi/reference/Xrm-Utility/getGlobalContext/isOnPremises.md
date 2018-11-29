---
title: モデル駆動型アプリにおける isOnPremise (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 855767c5-c48f-47a2-8f99-52423221d974
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="isonpremise-client-api-reference"></a>isOnPremise (クライアント API 参照)



モデル駆動型アプリ インスタンスが設置型またはオンラインでホストされているかどうかを示すブール値を返します。 

## <a name="syntax"></a>構文

```JavaScript
var globalContext = Xrm.Utility.getGlobalContext();
globalContext.isOnPremises();
```

## <a name="return-value"></a>戻り値

**種類** :ブール値

**Description**: モデル駆動型アプリのインスタンスが設置型の場合は **true**、それ以外の場合は **false**。

### <a name="related-topics"></a>関連トピック

[Xrm.Utility.getGlobalContext](../getGlobalContext.md)




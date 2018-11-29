---
title: モデル駆動型アプリにおける isDefaultPrevented (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 9a8802ad-80aa-4386-a192-573280587546
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="isdefaultprevented-client-api-reference"></a>isDefaultPrevented (クライアント API 参照)



[!INCLUDE[./includes/isDefaultPrevented-description.md](./includes/isDefaultPrevented-description.md)]

## <a name="syntax"></a>構文

`executionContext.getEventArgs().isDefaultPrevented();`

## <a name="return-value"></a>戻り値

**種類**: ブール値

**説明**: preventDefault メソッドが使用されたため、この保存イベントが取り消された場合は **true**、それ以外の場合は **false** です。


### <a name="related-topics"></a>関連トピック

[getSaveMode](getSaveMode.md)

[preventDefault](preventDefault.md)


---
title: モデル駆動型アプリの getVersion (クライアント API 参照)| MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 2fd5c43e-5a01-431d-ac2c-abefdb8d06ac
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getversion-client-api-reference"></a>getVersion (クライアント API 参照)



モデル駆動型アプリ インスタンスのバージョン番号を返します。

## <a name="syntax"></a>構文

```JavaScript
var globalContext = Xrm.Utility.getGlobalContext();
globalContext.getVersion();
``` 
## <a name="return-value"></a>戻り値

**種類**: 文字列

**説明**: モデル駆動型アプリ インスタンスのバージョンです。 たとえば、次のようになります。

`"9.0.0.1103"`

### <a name="related-topics"></a>関連トピック

[Xrm.Utility.getGlobalContext](../getGlobalContext.md)

---
title: getCurrentAppUrl (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: powerapps
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 89123cde-7c66-4c7d-94e4-e287285019f8
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getcurrentappurl-client-api-reference"></a>getCurrentAppUrl (クライアント API 参照)



モデル駆動型アプリで現在のビジネス アプリの URL を返します。

## <a name="syntax"></a>構文

```JavaScript
var globalContext = Xrm.Utility.getGlobalContext();
globalContext.getCurrentAppUrl();
``` 

## <a name="return-value"></a>戻り値

**種類**: 文字列

**説明**: 現在のビジネス アプリの URL。 可能な戻り値:

|Value |クライアント |
|---|---|
|https://[org].crm.dynamics.com/main.aspx?appid=[GUID]|モデル駆動型アプリ (オンライン)|
|https://[server]/[org]/main.aspx?appid=[GUID]|モデル駆動型アプリ (設置型)|

### <a name="related-topics"></a>関連トピック

[コードを使用してモデル駆動型アプリを作成、管理、公開する](../../../../create-manage-model-driven-apps-using-code.md)

[Xrm.Utility.getGlobalContext](../getGlobalContext.md) 




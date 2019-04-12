---
title: モデル駆動型アプリの getClientUrl (クライアント API 参照) | MicrosoftDocs
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
# <a name="getclienturl-client-api-reference"></a>getClientUrl (クライアント API 参照)



アプリケーションへのアクセスに使用された基本 URL を返します。

## <a name="syntax"></a>構文

```JavaScript
var globalContext = Xrm.Utility.getGlobalContext();
globalContext.getClientUrl();
``` 

## <a name="return-value"></a>戻り値

**種類**: 文字列

**説明**: 返された値は、次の表に示されているようなものになります。

|Value |クライアント |
|---|---|
|https://[org].crm.dynamics.com|モデル駆動型アプリ (オンライン)|
|http(s)://[server]/[org]|モデル駆動型アプリ (設置型)|
|http://localhost:2525|オフライン時にオフライン アクセス対応 Outlook 用モデル駆動型アプリ|

### <a name="related-topics"></a>関連トピック

[Xrm.Utility.getGlobalContext](../getGlobalContext.md)






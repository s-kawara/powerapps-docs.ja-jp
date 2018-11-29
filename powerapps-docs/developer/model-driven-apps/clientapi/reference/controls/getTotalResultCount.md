---
title: モデル駆動型アプリの getTotalResultCount (クライアント API 参照)| MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 1f9169ce-cba3-4bb6-af20-f86140139cfe
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="gettotalresultcount-client-api-reference"></a>getTotalResultCount (クライアント API 参照)



検索コントロールで見つけられる結果の数を取得します。 

## <a name="control-types-supported"></a>サポートされているコントロールの種類

サポート情報検索コントロール

## <a name="syntax"></a>構文

```
var kbSearchControl = formContext.getControl("<name>");
var searchCount = kbSearchControl.getTotalResultCount();
```

## <a name="return-value"></a>戻り値

**種類**: 数値

**説明**: 検索結果の数。
---
title: モデル駆動型アプリの getSearchQuery (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 4d025f92-db16-440c-9f82-e40d71e09862
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getsearchquery-client-api-reference"></a>getSearchQuery (クライアント API 参照)



サポート情報管理のコントロールの検索条件として使用するテキストを取得します。 

## <a name="control-types-supported"></a>サポートされているコントロールの種類

サポート情報検索コントロール

## <a name="syntax"></a>構文

```
var kbSearchControl = formContext.getControl("<name>");
var searchQuery = kbSearchControl.getSearchQuery();
```

## <a name="return-value"></a>戻り値

**種類**: 文字列

**説明**: 検索クエリのテキスト。

### <a name="related-topics"></a>関連トピック

[setSearchQuery](setSearchQuery.md)


---
title: モデル駆動型アプリにおける setSearchQuery (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 99e82b80-b6c3-4ee8-83cc-637b13ed8498
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="setsearchquery-client-api-reference"></a>setSearchQuery (クライアント API 参照)



サポート情報検索コントロールの検索条件として使用するテキストを設定します。

## <a name="control-types-supported"></a>サポートされているコントロールの種類

サポート情報検索コントロール

## <a name="syntax"></a>構文

```
var kbSearchControl = formContext.getControl("<name>");
kbSearchControl.setSearchQuery(searchString);
```

## <a name="parameters"></a>パラメーター

|Name | 種類​​ | 必須出席者 | 内容|
|--|--|--|--|
|searchString |String |あり|検索クエリ用テキスト。| 

### <a name="related-topics"></a>関連トピック

[getSearchQuery](getSearchQuery.md)



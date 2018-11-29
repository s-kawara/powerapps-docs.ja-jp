---
title: モデル駆動型アプリにおける addOnPostSearch (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 9d000628-5dbe-45bd-9c47-e19187ffdae7
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="addonpostsearch-client-api-reference"></a>addOnPostSearch (クライアント API 参照)



[PostSearch](../events/postsearch.md) イベントにイベント ハンドラーを追加します。 

## <a name="control-types-supported"></a>サポートされているコントロールの種類

サポート情報検索コントロール

## <a name="syntax"></a>構文

```
var kbSearchControl = formContext.getControl("<name>";
kbSearchControl.addOnPostSearch(myFunction);
```

## <a name="parameters"></a>パラメーター

|Name | 種類​​ | 必須出席者 | 内容|
|--|--|--|--|
|myFunction |関数 |あり|**PostSearch** イベントに追加する関数。 [実行コンテキスト](../../clientapi-execution-context.md)は、この関数に最初のパラメーターとして自動的に渡されます。| 

### <a name="related-topics"></a>関連トピック

[PostSearch イベント](../events/postsearch.md)

[removeOnPostSearch](removeOnPostSearch.md)
---
title: モデル駆動型アプリにおける addOnPostSearch (Client API リファレンス) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: c398dbca-0ead-487a-8a92-35b1f2953bf6
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="removeonpostsearch-client-api-reference"></a>removeOnPostSearch (クライアント API 参照)



[PostSearch](../events/postsearch.md) イベントからイベント ハンドラーを削除します。 

## <a name="control-types-supported"></a>サポートされているコントロールの種類

サポート情報検索コントロール

## <a name="syntax"></a>構文

```
var kbSearchControl = formContext.getControl("<name>";
kbSearchControl.removeOnPostSearch(myFunction);
```

## <a name="parameters"></a>パラメーター

|Name | 種類​​ | 必須出席者 | 内容|
|--|--|--|--|
|myFunction |関数 |あり|**PostSearch** イベントから削除する関数。| 

### <a name="related-topics"></a>関連トピック

[PostSearch イベント](../events/postsearch.md)

[addOnPostSearch](addOnPostSearch.md) 



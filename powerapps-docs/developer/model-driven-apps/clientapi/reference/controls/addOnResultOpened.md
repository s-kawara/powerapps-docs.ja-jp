---
title: モデル駆動型アプリにおける addOnResultOpened (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 5f0eabe1-985a-4e89-b23a-72657208ae7e
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="addonresultopened-client-api-reference"></a>addOnResultOpened (クライアント API 参照)



[OnResultOpened](../events/onresultopened.md) イベントにイベント ハンドラーを追加します。 

## <a name="control-types-supported"></a>サポートされているコントロールの種類

サポート情報検索コントロール

## <a name="syntax"></a>構文

```
var kbSearchControl = formContext.getControl("<name>");
kbSearchControl.addOnResultOpened(myFunction);
```

## <a name="parameters"></a>パラメーター

|Name | 種類​​ | 必須出席者 | 内容|
|--|--|--|--|
|myFunction |関数 |あり|**OnResultOpened** イベントに追加する関数。 [実行コンテキスト](../../clientapi-execution-context.md)は、この関数に最初のパラメーターとして自動的に渡されます。|

### <a name="related-topics"></a>関連トピック

[OnResultOpened イベント](../events/onresultopened.md)

[removeOnResultOpened](removeOnResultOpened.md)

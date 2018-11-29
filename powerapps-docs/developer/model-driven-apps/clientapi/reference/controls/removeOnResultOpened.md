---
title: モデル駆動型アプリにおける removeOnResultOpened (クライアント API 参照) | MicrosoftDocs
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
# <a name="removeonresultopened-client-api-reference"></a>removeOnResultOpened (クライアント API 参照)



[OnResultOpened](../events/onresultopened.md) イベントからイベント ハンドラーを削除します。 

## <a name="control-types-supported"></a>サポートされているコントロールの種類

サポート情報検索コントロール

## <a name="syntax"></a>構文

```
var kbSearchControl = formContext.getControl("<name>");
kbSearchControl.removeOnResultOpened(myFunction);
```

## <a name="parameters"></a>パラメーター

|Name | 種類​​ | 必須出席者 | 内容|
|--|--|--|--|
|myFunction |関数 |あり|**OnResultOpened** イベントから削除する関数。|

### <a name="related-topics"></a>関連トピック

[OnResultOpened イベント](../events/onresultopened.md)

[addOnResultOpened](addOnResultOpened.md) 



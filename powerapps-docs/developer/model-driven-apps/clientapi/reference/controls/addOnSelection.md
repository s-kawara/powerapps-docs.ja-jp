---
title: モデル駆動型アプリにおける addOnSelection (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 66cfb2ff-4d78-4bb9-8dc0-e214ae1d2880
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="addonselection-client-api-reference"></a>addOnSelection (クライアント API 参照)



[OnSelection](../events/onselection.md) イベントにイベント ハンドラーを追加します。 

## <a name="control-types-supported"></a>サポートされているコントロールの種類

サポート情報検索コントロール

## <a name="syntax"></a>構文

```
var kbSearchControl = formContext.getControl("<name>");
kbSearchControl.addOnSelection(myFunction);
```

## <a name="parameters"></a>パラメーター

|Name | 種類​​ | 必須出席者 | 内容|
|--|--|--|--|
|myFunction |関数 |あり|**OnSelection** イベントに追加する関数。 [実行コンテキスト](../../clientapi-execution-context.md)は、この関数に最初のパラメーターとして自動的に渡されます。|

### <a name="related-topics"></a>関連トピック

[addOnSelection イベント](../events/onselection.md)

[removeOnSelection](removeOnSelection.md)
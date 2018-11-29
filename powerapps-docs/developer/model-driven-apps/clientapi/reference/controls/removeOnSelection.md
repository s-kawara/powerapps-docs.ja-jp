---
title: モデル駆動型アプリにおける removeOnSelection (Client API リファレンス) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 3ca41e3e-af2b-4aa8-8233-64a8c276d0ef
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="removeonselection-client-api-reference"></a>removeOnSelection (クライアント API 参照)



[OnSelection](../events/onselection.md) イベントからイベント ハンドラーを削除します。 

## <a name="control-types-supported"></a>サポートされているコントロールの種類

サポート情報検索コントロール

## <a name="syntax"></a>構文

```
var kbSearchControl = formContext.getControl("<name>");
kbSearchControl.removeOnSelection(myFunction);
```

## <a name="parameters"></a>パラメーター

|Name | 種類​​ | 必須出席者 | 内容|
|--|--|--|--|
|myFunction |関数 |あり|**OnSelection** イベントから削除する関数。| 

### <a name="related-topics"></a>関連トピック

[addOnSelection](addOnSelection.md)



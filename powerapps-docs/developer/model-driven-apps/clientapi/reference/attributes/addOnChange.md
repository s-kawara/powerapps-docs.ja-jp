---
title: モデル駆動型アプリにおける addOnChange (クライアント API 参照) | Microsoft Docs
description: 属性値が変更されたときに呼び出される関数を設定するための、addOnchange メソッドについて説明します。
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 9f3b2fed-fde5-46e4-8c59-43aa51aa82df
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="addonchange-client-api-reference"></a>addOnChange (クライアント API 参照)



**OnChange** イベントの発生時に呼び出されるように関数を設定します。

## <a name="attribute-types-supported"></a>サポートされる属性の種類

すべて

## <a name="syntax"></a>構文

`formContext.getAttribute(arg).addOnChange(myFunction)`

## <a name="parameters"></a>パラメーター

| パラメーター名| 種類​​| 内容  |
| --------|-----------| -----|
|myFunction| 関数リファレンス| 属性 **OnChange** イベントから削除する関数を指定します。 [実行コンテキスト](../../clientapi-execution-context.md)は、この関数に最初のパラメーターとして自動的に渡されます。|


### <a name="related-topics"></a>関連トピック

[removeOnChange](removeOnChange.md)

[属性 OnChange イベント](../events/attribute-onchange.md)






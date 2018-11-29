---
title: モデル駆動型アプリの removePreSearch (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 2451c4ac-527c-4487-8f52-bde1690c5bde
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="removepresearch-client-api-reference"></a>removePreSearch (クライアント API 参照)



このメソッドを使用して、[PreSearch](../events/PreSearch.md) イベントに設定済みのイベント ハンドラー関数を削除します。

## <a name="control-types-supported"></a>サポートされているコントロールの種類

検索

## <a name="syntax"></a>構文

`formContext.getControl(arg).removePreSearch(myFunction)`

## <a name="parameters"></a>パラメーター

|Name | 種類​​ | 必須出席者 | 内容|
|--|--|--|--|
|myFunction |関数 |あり| 取り外す関数。 [実行コンテキスト](../../clientapi-execution-context.md)は、この関数に最初のパラメーターとして自動的に渡されます。|

### <a name="related-topics"></a>関連トピック

[PreSearch イベント](../events/PreSearch.md)

[addPreSearch](addPreSearch.md) 



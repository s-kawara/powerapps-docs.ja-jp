---
title: モデル駆動型アプリにおける addPreSearch (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: d69a432a-1d74-4782-bedd-f9f30d3d7d9c
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="addpresearch-client-api-reference"></a>addPreSearch (クライアント API 参照)



ユーザーが検索結果を表示しようとするときの値に基づき、検索に変更を適用します。

## <a name="control-types-supported"></a>サポートされているコントロールの種類

検索

## <a name="syntax"></a>構文

`formContext.getControl(arg).addPreSearch(myFunction)`

## <a name="parameters"></a>パラメーター

|Name | 種類​​ | 必須出席者 | 内容|
|--|--|--|--|
|myFunction |関数 |あり| 検索発生時に検索が結果を提供する直前に実行される関数です。 この関数を使用してその他の検索コントロールのいずれかを呼び出すことができ、検索に表示される結果を改善できます。 [実行コンテキスト](../../clientapi-execution-context.md)は、この関数に最初のパラメーターとして自動的に渡されます。|

### <a name="related-topics"></a>関連トピック

[PreSearch イベント](../events/PreSearch.md)

[removePreSearch](removePreSearch.md) 



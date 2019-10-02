---
title: ConditionExpression | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bd90b3fd-a4b4-4999-8b53-d2a5dce4966b
---

# <a name="conditionexpression"></a>ConditionExpression

[!INCLUDE [conditionexpression-description](includes/conditionexpression-description.md)]

## <a name="attributename"></a>attributeName

フィルターを適用するデータセット列の名前。

**種類**: `string`

## <a name="conditionoperator"></a>conditionOperator

条件の評価に使用される演算子。

**種類**: `enum`

`conditionOperator` の値は以下の可能な値を含む列挙値です

|Value|メンバー|
|--|--|
|-1|なし|
|0|等号|
|1|NotEqual|
|2|GreaterThan|
|3|LessThan|
|4|GreaterEqual|
|5|LessEqual|
|6|いいね!|
|8|に含まれる|
|12|Null|
|14|昨日|
|15|Today|
|16|[明日]|
|17|Last7Days|
|18|Next7Days|
|19|LastWeek|
|20|ThisWeek|
|22|LastMonth|
|23|ThisMonth|
|25|オン|
|26|OnOrBefore|
|27|OnOrAfter|
|28|LastYear|
|29|ThisYear|
|33|LastXDays|
|34|NextXDays|
|37|LastXMonths|
|38|NextXMonths|
|49|が次の内容を含む|
|70|InFiscalPeriodAndYear|
|75|Above|
|76|未満|
|77|NotUnder|
|78|AboveOrEqual|
|79|UnderOrEqual|
|87|ContainValues|

## <a name="entityaliasname"></a>entityAliasName

リンクされたエンティティでフィルター処理を使用できるようにするエンティティのエイリアス名

**種類**: `string`

## <a name="value"></a>値

条件で評価された値。

**種類**: `string | string[]`


### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークの API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../overview.md)
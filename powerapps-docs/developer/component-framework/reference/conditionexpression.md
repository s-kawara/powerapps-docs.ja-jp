---
title: ConditionExpression | Microsoft Docs
description: ''
keywords: ''
ms.author: nabuthuk
author: Nkrb
manager: kvivek
ms.date: 10/01/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bd90b3fd-a4b4-4999-8b53-d2a5dce4966b
ms.openlocfilehash: 10f7275643c0df4c2a4099a80b490fb5e27ce318
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72345545"
---
# <a name="conditionexpression"></a>ConditionExpression

[!INCLUDE [conditionexpression-description](includes/conditionexpression-description.md)]

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリ

## <a name="properties"></a>プロパティ

### <a name="attributename"></a>attributeName

フィルターを適用するデータセット列の名前。

**種類**: `string`

### <a name="conditionoperator"></a>conditionOperator

条件を評価するために使用される演算子。

**種類**: `enum`

@No__t_0 値は列挙型であり、次の値を使用できます。

|Value|Member|
|--|--|
|1-1|存在|
|0|つの|
|1|NotEqual|
|2|GreaterThan|
|3|LessThan|
|4|は|
|5|LessEqual|
|6|という感じで|
|8|In|
|12|空白|
|14|昨日|
|15|Today|
|まで|明日|
|a3|Last7Days|
|18|Next7Days|
|21|LastWeek|
|20@@|終了|
|×|LastMonth|
|23|今月|
|ほど|代わっ|
|35|OnOrBefore|
|27|OnOrAfter|
|桁|LastYear|
|複素数|ThisYear|
|33|LastXDays|
|34|NextXDays|
|37|LastXMonths|
|38|NextXMonths|
|49|は|
|70|InFiscalPeriodAndYear|
|75|上図|
|76|下位|
|77|NotUnder|
|78|AboveOrEqual|
|79|過小一致|
|87|値の指定|

### <a name="entityaliasname"></a>entityAliasName

エンティティの別名は、リンクされたエンティティに対してフィルター処理を使用できるようにするための名前です。

**種類**: `string`

### <a name="value"></a>値

条件によって評価される値。

**種類**: `string | string[]`

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネントフレームワーク API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../overview.md)
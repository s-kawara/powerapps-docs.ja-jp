---
title: FilterExpression | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
author: Nkrb
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 19ad54b8-e044-4f07-a18e-b00d26b75832
---

# <a name="filterexpression"></a>FilterExpression

[!INCLUDE[cc-beta-prerelease-disclaimer](../../../includes/cc-beta-prerelease-disclaimer.md)]

[!INCLUDE [filterexpression-description](includes/filterexpression-description.md)]

## <a name="properties"></a>プロパティ

## <a name="conditions"></a>条件

このフィルタに関連付けられた一連の条件。

**種類**: [ConditionExpression](conditionexpression.md)[]

## <a name="filteroperator"></a>filterOperator

このフィルターで条件を統合するために使用されるオペレーター。

**種類**: `enum`

`filterOperator` の値は以下の可能な値を含む列挙値です

|Value|メンバー|
|--|--|
|0|And|
|1|Or|

## <a name="filters"></a>フィルター

このフィルタを評価した後で評価する必要がある子フィルター。

**種類**: [FilterExpression](filterexpression.md)[]<br />

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークの API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../overview.md)
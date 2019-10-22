---
title: FilterExpression |Microsoft Docs
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
ms.assetid: 19ad54b8-e044-4f07-a18e-b00d26b75832
ms.openlocfilehash: 7b613238f28987b688d4f2299506fa91b72a99a7
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72343981"
---
# <a name="filterexpression"></a>FilterExpression

[!INCLUDE [filterexpression-description](includes/filterexpression-description.md)]

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリ

## <a name="properties"></a>プロパティ

### <a name="conditions"></a>照明

このフィルターに関連付けられている条件のセット。

**型**: [conditionexpression](conditionexpression.md)[]

### <a name="filteroperator"></a>filterOperator

このフィルターの条件を結合するために使用される演算子。

**種類**: `enum`

@No__t_0 値は列挙型であり、次の値を使用できます。

|Value|Member|
|--|--|
|0|And|
|1|Or|

### <a name="filters"></a>仕分け

このフィルターを評価した後に評価する必要がある子フィルター。

**型**: [filterexpression](filterexpression.md)[]<br />

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネントフレームワーク API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../overview.md)
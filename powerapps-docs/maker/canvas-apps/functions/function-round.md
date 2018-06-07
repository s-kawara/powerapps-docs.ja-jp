---
title: Round、RoundDown、および RoundUp 関数 | Microsoft Docs
description: 構文を含む PowerApps の Round、RoundDown、および RoundUp 関数の参照情報
documentationcenter: na
author: gregli-msft
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: reference
ms.component: canvas
ms.date: 11/07/2015
ms.author: gregli
ms.openlocfilehash: 07771027ea728d65bfb35d79fb67bdef1ac80f1a
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "31825788"
---
# <a name="round-rounddown-and-roundup-functions-in-powerapps"></a>PowerApps の Round、RoundDown、および RoundUp 関数
数値を丸めます。

## <a name="description"></a>説明
**Round**、**RoundDown**、**RoundUp** 関数は、指定した小数点以下桁数まで数値を丸めます。

* **Round** は、次の桁の数値が 5 以上の場合に切り上げます。 それ以外の場合、この関数では切り捨てます。
* **RoundDown** は、常に前の小さい数値になるように切り捨てます。
* **RoundUp** は、常に次の大きい数値になるように切り上げます。

数値を 1 つだけ渡した場合、丸められた数値が戻り値として返されます。  数値を含む単一列[テーブル](../working-with-tables.md)を渡すと、丸められた数値の単一列テーブルが戻り値として返されます。 複数列テーブルがある場合は、[テーブルの使用](../working-with-tables.md)に関するページの説明に従って、そのテーブルを単一列テーブルにすることができます。

## <a name="syntax"></a>構文
**Round**( *Number*, *DecimalPlaces* )<br>**RoundDown**( *Number*, *DecimalPlaces* )<br>**RoundUp**( *Number*, *DecimalPlaces* )

* *Number* - 必須。 丸める対象となる数値。
* *DecimalPlaces* - 必須。  丸める範囲を示す小数点以下の桁数。  整数に丸めるには、0 を使用します。  


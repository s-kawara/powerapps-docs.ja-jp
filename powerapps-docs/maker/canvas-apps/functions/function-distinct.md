---
title: Distinct 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Distinct 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 11/07/2015
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 17a2f2cfca16c5589f74ac434b36326037146b16
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61551217"
---
# <a name="distinct-function-in-powerapps"></a>PowerApps の Distinct 関数
重複を削除して、[テーブル](../working-with-tables.md)の[レコード](../working-with-tables.md#records)を要約します。

## <a name="description"></a>説明
**Distinct** 関数は、テーブルの各レコードで数式を評価します。 **Distinct** は、重複する値が削除された結果を含む 1 列のテーブルを返します。  

[!INCLUDE [record-scope](../../../includes/record-scope.md)]

## <a name="syntax"></a>構文
**Distinct**( *Table*, *Formula* )

* *Table* - 必須。  全体を評価するテーブル。
* *Formula* - 必須。  各レコードについて評価する数式。

## <a name="example"></a>例
**Department** 列が含まれている **Employees** テーブルがある場合、この関数はこの列内の各部署名を一覧表示します。この列で各名前が何回か出現していても、一覧では重複しないように表示されます。

**Distinct(Employees, Department)**


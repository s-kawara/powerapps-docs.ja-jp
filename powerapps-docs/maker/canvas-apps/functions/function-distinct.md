---
title: Distinct 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Distinct 関数の参照情報
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
ms.openlocfilehash: 101c28f2b4ac8135a9b4def9421f886f373105bf
ms.sourcegitcommit: 91a102426f1bc37504142cc756884f3670da5110
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/26/2018
ms.locfileid: "31825581"
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


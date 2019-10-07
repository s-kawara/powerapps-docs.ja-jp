---
title: First、FirstN、Last、および LastN 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の First、FirstN、Last、および LastN 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 11/07/2015
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 48e8311d5da00b02cbefbf6f47661c89adcc80a5
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "71992724"
---
# <a name="first-firstn-last-and-lastn-functions-in-powerapps"></a>PowerApps の First、FirstN、Last、および LastN 関数
テーブルの最初または最後の[レコード](../working-with-tables.md#records) セットを返します。

## <a name="description"></a>説明
**First** 関数は、[テーブル](../working-with-tables.md)の最初のレコードを返します。

**FirstN** 関数は、テーブルの最初のレコード セットを返します。2 番目の引数で、返されるレコードの数を指定します。

**Last** 関数は、テーブルの最後のレコードを返します。

**LastN** 関数は、テーブルの最後のレコード セットを返します。2 番目の引数で、返されるレコードの数を指定します。

**First** および **Last** は 1 つのレコードを返します。  **FirstN** および **LastN** は、1 つのレコードのみを指定した場合でも、テーブルを返します。

[!INCLUDE [delegation-no](../../../includes/delegation-no.md)]

## <a name="syntax"></a>構文
**First**( *Table* )<br>**Last**( *Table* )

* *Table* - 必須。 操作の対象となるテーブル。

**FirstN**( *Table* [, *NumberOfRecords* ] )<br>**LastN**( *Table* [, *NumberOfRecords* ] )

* *Table* - 必須。 操作の対象となるテーブル。
* *NumberOfRecords* - 省略可能。  返されるレコードの数。 この引数を指定しない場合は、1 つのレコードが返されます。

## <a name="examples"></a>例
この数式では、**Employees** というテーブルから最初のレコードが返されます。<br>
**First(Employees)**

この数式では、**Employees** というテーブルから最後の 15 件のレコードが返されます。<br>
**LastN(Employees, 15)**


---
title: Shuffle 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Shuffle 関数の参照情報
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
ms.openlocfilehash: 181ef038a90c9bfc7e3fe72af9514a34afce9776
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/07/2019
ms.locfileid: "71983945"
---
# <a name="shuffle-function-in-powerapps"></a>PowerApps の Shuffle 関数
[テーブル](../working-with-tables.md)の[レコード](../working-with-tables.md#records)をランダムに並べ替えます。

## <a name="description"></a>説明
**Shuffle** 関数は、テーブルのレコードを並べ替えます。

**Shuffle** は、引数と同じ[列](../working-with-tables.md#columns)と行数を持つテーブルを返します。

## <a name="syntax"></a>構文
**Shuffle**( *Table* )

* *Table* - 必須。  シャッフルするテーブル。

## <a name="example"></a>例
**Deck** という名前の[コレクション](../working-with-data-sources.md#collections)にトランプの詳細情報を格納していた場合、この数式は、ランダムにシャッフルされたそのコレクションのコピーを返します。

**Shuffle(Deck)**


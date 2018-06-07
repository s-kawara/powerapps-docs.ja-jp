---
title: Shuffle 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Shuffle 関数の参照情報
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
ms.openlocfilehash: 6d981c410b22dd9db52cdf077a00e6eaae83be75
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "31827369"
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


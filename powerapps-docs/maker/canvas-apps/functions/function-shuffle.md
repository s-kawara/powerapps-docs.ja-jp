---
title: Shuffle 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Shuffle 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 11/07/2015
ms.author: gregli
ms.openlocfilehash: 39307e9c7b3de7bfae151709827c409fcc7087ad
ms.sourcegitcommit: dfa0e1a7981814e15e6ca4720e2a5f930e859db1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2018
ms.locfileid: "39014238"
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


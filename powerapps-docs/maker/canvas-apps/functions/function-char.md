---
title: Char 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Char 関数の参照情報
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
ms.openlocfilehash: b5d63b26498b94943f5340d9f57f3255390c7c94
ms.sourcegitcommit: 79b8842fb0f766a0476dae9a537a342c8d81d3b3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2018
ms.locfileid: "37895985"
---
# <a name="char-function-in-powerapps"></a>PowerApps の Char 関数
文字コードを文字列に変換します。

## <a name="description"></a>説明
**Char** 関数は、プラットフォームの適切な ASCII 文字を含む文字列を返します。

## <a name="syntax"></a>構文
**Char**( *CharacterCode* )

* *CharacterCode* - 必須。 変換する ASCII 文字コード。

## <a name="examples"></a>例

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Char( 65 )** |ASCII コード 65 に対応する文字を返します。 |A |
| **Char( 105 )** |ASCII コード 105 に対応する文字を返します。 |i |
| **Char( 35 )** |ASCII コード 35 に対応する文字を返します。 |# |


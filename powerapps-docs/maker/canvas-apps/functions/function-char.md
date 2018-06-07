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
ms.openlocfilehash: 2e8281f401088f43aa7785ac5dcf7b2f07bb6f96
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "31826214"
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


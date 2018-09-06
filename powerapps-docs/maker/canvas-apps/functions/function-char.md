---
title: Char 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Char 関数の参照情報
dauthor: gregli-msft
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
ms.openlocfilehash: aec27b788fff8434cfdc4e0e130487f718a42aa6
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "42826367"
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


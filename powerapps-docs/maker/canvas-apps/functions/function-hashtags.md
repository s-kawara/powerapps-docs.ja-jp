---
title: HashTags 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の HashTags 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 11/07/2015
ms.author: gregli
ms.openlocfilehash: 66fad5a1afd9086bf07da88a93ac68b756dfb3d6
ms.sourcegitcommit: 521a7b8e6ae72a211045b54d153a8a8c8f59172e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2018
ms.locfileid: "40021320"
---
# <a name="hashtags-function-in-powerapps"></a>PowerApps の HashTags 関数
テキストの文字列からハッシュタグ (#文字列) を抽出します。

## <a name="description"></a>説明
**HashTags** 関数はハッシュタグの文字列をスキャンします。 ハッシュタグはシャープ記号 (#) で始まり、その後に次の組み合わせでできた文字列が続きます。

* 大文字と小文字
* 数字
* アンダースコア
* 通貨記号 ($ など)

**HashTags** は、文字列内のハッシュタグが含まれた 1 列の[テーブル](../working-with-tables.md)を返します。  文字列にハッシュタグがない場合、この関数は 1 列の[空](function-isblank-isempty.md)のテーブルを返します。

## <a name="syntax"></a>構文
**HashTags**( *String* )

* *String* - 必須。  ハッシュタグをスキャンする文字列。

## <a name="examples"></a>例
### <a name="step-by-step"></a>ステップ バイ ステップ
1. **[テキスト入力](../controls/control-text-input.md)** コントロールを追加し、**Tweet** という名前を付けて、そこに次の文を入力します。
   
    **This #app is #AMAZING and can #coUnt123 or #123abc but not #1-23 or #$\*(#\@")**
2. 垂直カスタム ギャラリーを追加し、**[Items](../controls/properties-core.md)** プロパティを次の関数に設定します。
   
    **HashTags(Tweet.Text)**
3. ギャラリー テンプレートに**[ラベル](../controls/control-text-box.md)** を追加します。
   
    次のハッシュタグがギャラリーに表示されます。
   
   * **\#app**
   * **\#AMAZING**
   * **\#coUnt123**
   * **\#123abc**
   * **\#1**


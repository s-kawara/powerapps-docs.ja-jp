---
title: Char 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Char 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 03/01/2019
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 1b598cc863ec01bcb2a66a9510cb48ec5203e679
ms.sourcegitcommit: f84095d964fe1fe5cc5290e5edbee284bd768e1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "59042632"
---
# <a name="char-function-in-powerapps"></a>PowerApps の Char 関数

文字コードを文字列に変換します。

## <a name="description"></a>説明

**Char**関数に対応する ASCII 文字の文字列に数値を変換します。

## <a name="syntax"></a>構文

**Char**( *CharacterCode* )

- *CharacterCode* - 必須。 変換する ASCII 文字コード。

## <a name="examples"></a>例

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Char( 65 )** |ASCII コード 65 に対応する文字を返します。 |"A" |
| **Char( 105 )** |ASCII コード 105 に対応する文字を返します。 |"i" |
| **Char( 35 )** |ASCII コード 35 に対応する文字を返します。 |"#" |

### <a name="display-a-character-map"></a>文字マップを表示します。

1. タブレット アプリで空の画面を追加、 [**ギャラリー** ](../controls/control-gallery.md)コントロールを**空白水平**レイアウトし、これらのプロパティを設定。

    - **項目**: `[0,1,2,3,4,5,6,7]`
    - **幅**:800
    - **高さ**:500
    - **TemplateSize**:100
    - **TemplatePadding**:0

1. 、そのギャラリー内に追加、**ギャラリー**コントロールを、**空白垂直**レイアウトし、これらのプロパティを設定。

    - **項目**: `ForAll( [0,2,3,4,5,6,7,8,9,10,11,12,13,14,15], Value + ThisItem.Value * 16 )`
    - **幅**:100
    - **高さ**:500
    - **TemplateSize**:30
    - **TemplatePadding**:0

    値、**項目**プロパティの値列によって提供される、列番号の 16 を乗算し、**項目**最初のギャラリーからのプロパティ (0 ~ 7 で`ThisItem.Value`)。 数式から結果が追加されます、行番号のいずれかに 2 つ目のギャラリーから (0 ~ 15 レコードのスコープを[ **ForAll** ](function-forall.md)関数を提供します)。

1. 2 つ目の (垂直) ギャラリー内に追加、**ラベル**を制御して、これらのプロパティを設定します。

    - **テキスト**: `ThisItem.Value`
    - **幅**:50

1. 2 つ目の (垂直) ギャラリー内でもう 1 つの追加**ラベル**を制御して、これらのプロパティを設定します。

    - **テキスト**: `Char( ThisItem.Value )`
    - **幅**:50
    - **X**:50

最初の 128 個の ASCII 文字のグラフを作成しました。 小さな四角形を印刷できないように表示される文字。

![最初の 128 の ASCII 文字](media/function-char/chart-lower.png)

拡張 ASCII 文字を表示するには、設定、**項目**に次の式では、各文字の値を 128 を追加します。 2 番目のギャラリーのプロパティ。

`ForAll( [0,2,3,4,5,6,7,8,9,10,11,12,13,14,15], Value + ThisItem.Value * 16 + 128)`

![拡張 ASCII 文字](media/function-char/chart-higher.png)

別のフォントで文字を表示するには、設定、**フォント**などの値を 2 番目のラベルのプロパティ **' ダンス Script'** します。

![スクリプトのダンス](media/function-char/chart-higher-dancing-script.png)

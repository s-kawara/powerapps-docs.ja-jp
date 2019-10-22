---
title: 関数 |Microsoft Docs
description: 構文を含む PowerApps の With 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 08/15/2019
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: c8d793fcfd2992a781f92d529002e22a34a9df5a
ms.sourcegitcommit: 742a5a21e73a811e9cea353d8275f09c22366afc
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2019
ms.locfileid: "70130344"
---
# <a name="with-function-in-powerapps"></a>PowerApps の With 関数
値を計算し、名前付きの値のインラインレコードを含む1つの[レコード](../working-with-tables.md#records)に対してアクションを実行します。

## <a name="description"></a>説明

**With**関数は、1つのレコードに対して数式を評価します。  数式は、値を計算したり、操作 (データの変更や接続の操作など) を実行したりできます。  レコードのテーブル内のすべてのレコードの数式を評価するには、 [ **ForAll**関数](function-forall.md)を使用します。

[!INCLUDE [record-scope](../../../includes/record-scope.md)]

**と共**に使用すると、複雑な数式をより小さな名前のサブ式に分割することにより、読みやすさを向上させることができます。  これらの名前付きの値は、のスコープに限定され**た**単純なローカル変数のように動作します。  [ **Updatecontext**関数](function-updatecontext.md)で使用されるのと同じインラインレコード構文は、と共に使用できます。  を**と共に**使用することをお勧めします。コンテキスト変数またはグローバル変数は、自己完結し、わかりやすく、任意の宣言型の数式コンテキストで使用できます。  

[**Patch**](function-patch.md)や[**Match**](function-ismatch.md)などの関数によって返されるレコードのフィールドにアクセスするには、**と共**にを使用します。  **で**は、これらの関数からの値を保持し、さらに多くの計算やアクションで使用できるようにします。  

**の** *レコード*引数がエラーの場合、関数によってそのエラーが返され、*式*は評価されません。

## <a name="syntax"></a>構文
**で**(*レコード*、*式*)

* *Record* –必須。 操作するレコード。  名前の値には、インライン構文を使用します。`{ name1: value1, name2: value2, ... }`
* *Formula* –必須。  *レコード*に対して評価する数式。  この数式では、レコードのフィールドをレコードスコープとして直接参照できます。

## <a name="examples"></a>使用例

### <a name="simple-named-values"></a>単純な名前付きの値

```powerapps-dot
With( { radius: 10, 
        height: 15 },
    Pi() * (radius*radius) * height
)
// Result: 4712.38898038 (as shown in a label control)
```

この例では、名前付きの値のレコードを使用して、円柱のボリュームを計算します。  を使用する**と**、すべての入力値が一緒にキャプチャされるため、計算自体から簡単に区切ることができます。  

### <a name="nested-with"></a>入れ子になった

![With 関数を使用した対象計算](media/function-with/interest-calculator.gif)

```powerapps-dot
With( { AnnualRate: RateSlider/8/100,        // slider moves in 1/8th increments and convert to decimal
        Amount: AmountSlider*10000,          // slider moves by 10,000 increment
        Years: YearsSlider,                  // slider moves in single year increments, no adjustment required
        AnnualPayments: 12 },                // number of payments per year
      With( { r: AnnualRate/AnnualPayments,  // interest rate
              P: Amount,                     // loan amount
              n: Years*AnnualPayments },     // number of payments
            r*P / (1 - (1+r)^-n)             // standard interest calculation
      )
)  
```

この例では、関数**を使用して**、[月額ローン返済](https://en.wikipedia.org/wiki/Mortgage_calculator#Monthly_payment_formula)の2層計算を作成しています。  競合がない限り、外側のすべての名前付きの値は、の内部で使用できます。

スライダーコントロールは1ずつずつ移動できるので、スライダーを分割または乗算して、カスタムインクリメントを効果的に作成します。  利率がの場合、 **RateSlider**の Max プロパティは**48**に設定されています。この**値**は、1/8 のパーセンテージで割った値を8で割って100で割った値から、0.125% から 6% の範囲である10進数に変換します。  ローンの金額の場合、 **AmountSlider**の**Max**プロパティは**60**に設定され、1万が乗算されます。これは1万から60万までの範囲です。

スライダーが移動し、新しいローンの支払いが表示されると、 **With**が自動的に再計算されます。  変数は使用されず、スライダーコントロールの**OnChange**プロパティを使用する必要はありません。

このアプリを作成するための詳細な手順は次のとおりです。
1. 新しいアプリを作成します。
2. [**スライダー**コントロール](../controls/control-slider.md)を追加し、 **RateSlider**という名前を指定します。  **Max**プロパティを48に設定します。
3. スライダーコントロールの左側に[**ラベル**コントロール](../controls/control-text-box.md)を追加します。  **Text**プロパティを **"利率:"** に設定します。
3. スライダーコントロールの右側に**ラベル**コントロールを追加します。  **Text**プロパティを数式**RateSlider/8 & "&nbsp;%"** に設定します。
3. 別の**スライダー**コントロールを追加し、 **AmountSlider**という名前を指定します。  **Max**プロパティを60に設定します。
3. このスライダーコントロールの左側に**ラベル**コントロールを追加します。  **Text**プロパティを **"Loan Amount:"** に設定します。 
3. このスライダーコントロールの右側に**ラベル**コントロールを追加します。  **Text**プロパティを数式**AmountSlider/8 * 1万**に設定します。
4. 別の**スライダー**コントロールを追加し、 **YearsSlider**という名前を指定します。  **Max**プロパティを40に設定します。
3. このスライダーコントロールの左側に**ラベル**コントロールを追加します。  **Text**プロパティを **"Years of Years:"** に設定します。 
3. このスライダーコントロールの右側に**ラベル**コントロールを追加します。  **Text**プロパティを数式**YearsSlider**に設定します。
5. **ラベル**コントロールを追加し、その**Text**プロパティを、上に示した数式に設定します。
3. 最後のラベルコントロールの左側に**ラベル**コントロールを追加します。  **Text**プロパティを **"定期的な月額支払い:"** に設定します。  

### <a name="primary-key-returned-from-patch"></a>修正プログラムからプライマリキーが返されました

```powerapps-dot
With( Patch( Orders, Defaults( Orders ), { OrderStatus: "New" } ),
      ForAll( NewOrderDetails, 
              Patch( OrderDetails, Defaults( OrderDetails ), 
                     { Order: OrderID,          // from With's first argument, primary key of Patch result
                       Quantity: Quantity,      // from ForAll's NewOrderDetails table
                       ProductID: ProductID }   // from ForAll's NewOrderDetails table
              )
      )
)
```

この例では、SQL Server の**Order**テーブルにレコードを追加します。  次に、返された主キーを**OrderID**フィールドの**Patch**関数によって返される注文に使用して、 **OrderDetails**テーブルに関連レコードを作成します。  

### <a name="extracted-values-with-a-regular-expression"></a>正規表現を使用して抽出された値

```powerapps-dot
With( 
    Match( "PT2H1M39S", "PT(?:<hours>\d+)H)?(?:(?<minutes>\d+)M)?(?:(?<seconds>\d+)S)?" ),
    Time( Value( hours ), Value( minutes ), Value( seconds ) )
)
// Result: 2:01 AM (as shown in a label control, use the Text function to see the seconds)
```

この例では、ISO 8601 duration 値から時間、分、および秒を抽出し、これらのサブマッチを使用して日付/時刻値を作成します。 

サブマッチには数値が含まれていますが、まだテキスト文字列に含まれていることに注意してください。  数値演算を実行する前に、[**値**](function-value.md)関数を使用して数値に変換します。  


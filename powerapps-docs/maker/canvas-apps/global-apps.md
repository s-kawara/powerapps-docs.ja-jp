---
title: キャンバス アプリにグローバル サポートを組み込む | Microsoft Docs
description: PowerApps を使用し、世界中で使用されるアプリを作成します。
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 10/25/2016
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 4aae487a0b2efe50e3ac6bd42c90d26de23fed60
ms.sourcegitcommit: ead27300a1b7371136edee1842829ed87ca77a72
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/14/2019
ms.locfileid: "57892278"
---
# <a name="build-global-support-into-canvas-apps"></a>キャンバス アプリにグローバル サポートを組み込む
PowerApps はグローバル製品です。 さまざまな言語や地域でキャンバス アプリをビルドし、使用できます。

アプリのビルド中および実行中、PowerApps によって表示されるテキストはさまざまな言語に翻訳されています。  メニュー項目、ダイアログ ボックス、リボンのタブなどのテキストがお使いの言語で表示されます。  日付や数字の入力と表示にも、お使いの言語とリージョンが適用されています。  一部の地域の世界の使用など、**します。** (ドットまたはピリオド) として、小数点区切り文字を使用しながら、 **、** (コンマ)。  

作成したアプリをグローバル対応にすることもできます。  **[Language](functions/function-language.md)**、**[Text](functions/function-text.md)**、**[Value](functions/function-value.md)**、**[DateValue](functions/function-datevalue-timevalue.md)** やその他の関数を使用して、さまざまな言語で何が表示され、入力として使用されるかを適用します。   

## <a name="language-settings"></a>言語の設定
ネイティブのスタジオまたはネイティブのプレーヤーを使用している場合は、使用する言語がホスト オペレーティング システムによって提供されます。  Windows の場合、これは "すべての設定"、次に "時間と言語" の設定で制御できます。  さらに Windows では、言語設定をオーバーライドして、小数点区切り文字として使用する文字を指定できます。  

Web の使用が発生しているときに使用される言語は、ブラウザーによって提供されます。  多くのブラウザーでは、既定でホスト オペレーティング システムの設定が使用されますが、一部のブラウザーでは手動で言語を設定することもできます。

## <a name="authoring-environment"></a>オーサリング環境
オーサリング環境は、作成者の言語設定に適応します。  さまざまな言語を使用する作成者たちが同じアプリを編集できるように、アプリ自体は言語に依存しない方法で格納されます。

### <a name="names-in-formulas"></a>数式での名前
数式のほとんどの要素は常に英語です。

* 関数名:**場合**、**移動**、**収集**、.
* コントロールのプロパティ名:**Screen.Fill**、 **Button.OnSelect**、 **Textbox.Font**、.
* 列挙名:**Color.Aqua**, **DataSourceInfo.MaxValue**, **FontWeight.Bold**...
* 信号レコード:**Compass.Heading**、**場所。Latitude**、**App.ActiveScreen**、…
* 演算子:**親**、**で**、 **exactIn**、.

オーサリング環境がローカライズされることにともない、コントロールやその他のオブジェクト名が作成者のネイティブ言語で表示されます。  スペイン語の場合、一部のコントロールは次のように表示されます。

![](media/global-apps/insert-controls-es.png)

アプリに次のいずれかを挿入すると、その名前は既定で英語になります。  これは、コントロールのプロパティ名と、数式の残りの部分との一貫性を保つために行われます。  たとえば、上記で一覧表示されている **Casilla** を **Checkbox1** として挿入します。  

コントロールの挿入後に、好きな名前に変更できます。  選択した状態では、"コンテンツ" リボンの左側にコントロールの名前が表示されます。  この名前を選択すると、名前を編集できるテキスト ボックスが現れます。

![](media/global-apps/control-rename.png)

必要に応じて、コントロールの名前を **Casilla1** に変更できます。  (ここではブラウザーによって) 赤い波線が表示されるのは、この名前がスペイン語ではないためであり、問題はありません。

以下のものについて、好きな名前を付けることができます。

* コントロール名
* コレクション名
* コンテキストの変数名

### <a name="formula-separators-and-chaining-operator"></a>数式の区切り記号とチェーン演算子
いくつかの[区切り記号と演算子](functions/operators.md)は、作成者の言語の小数点に基づいて変更されます。

| 作成者の言語の小数点 | PowerApps 小数点 | PowerApps リストの区切り記号 | PowerApps チェーン演算子 |
| --- | --- | --- | --- |
| **.** (ドットまたはピリオド) |**.** (ドットまたはピリオド) |**,** (コンマ) |**;** (セミコロン) |
| **,** (コンマ) |**,** (コンマ) |**;** (セミコロン) |**;;** (二重セミコロン) |

PowerApps リスト区切り記号の変更は、Excel リスト区切り記号の変更と一致します。  これにより、次のものが影響を受けます。

* 関数呼び出しの引数
* [レコード](working-with-tables.md#elements-of-a-table)のフィールド
* [値テーブル](working-with-tables.md#inline-syntax)のレコード

たとえば、次の数式言語および日本など、英国、小数点としてドットまたはピリオドを使用している地域で表現を考えてみます。

![PowerApps の数式オープンかっこ slider1 ドット値のコンマの 12 ドット 59 より大きい場合に通知オープンかっこ付きの"Valid!" コンマ成功閉じるかっこオープンかっこ閉じるかっこなし"NextScreen"コンマ、セミコロンで Navigate コンマ オープンの通知かっこ付きのかっこで囲まれた"無効な場合は、もう一度やり直してください"コンマ エラー閉じるかっこ閉じる](media/global-apps/operators-dot.png)

この同次数式を表示の言語と地域の 10 進区切り記号のフランスやスペインなどのコンマが使用されているようになりました。

![PowerApps の数式にオープンかっこ slider1 ドット値 12 コンマ セミコロンが 59 より大きい場合は、オープンを通知かっこ付きの"Valid!" セミコロンで成功を閉じるかっこ開く Navigate かっこ"NextScreen"セミコロンの閉じかっこなし二重セミコロン セミコロン オープンの通知かっこ付きのかっこで囲まれた"無効な場合は、もう一度やり直してください"セミコロン エラー閉じるかっこ閉じる](media/global-apps/operators-comma.png)

強調表示は、2 つのバージョンを変更する演算子を示します。  プロパティ選択演算子に注意してください **。** (ドットまたはピリオド) で**Slider1.Value**は常に、小数点区切り文字にかかわらず同じです。

内部的には数式は変更されず、変更されるのは表示方法と作成者による編集方法のみです。  2 つの異なる言語を使用する 2 人の作成者が、それぞれの言語に応じた区切り文字と演算子を見ながら同じ数式を編集することができます。

## <a name="creating-a-global-app"></a>グローバルなアプリの作成
作成したアプリは、さまざまな言語に適応し、世界中のユーザーに優れたユーザー エクスペリエンスを提供することができます。

### <a name="language-function"></a>Language 関数
**[Language](functions/function-language.md)** 関数は、現在のユーザーの言語タグを返します。  たとえば、この関数は英国のユーザーには **"en-GB"** を、ドイツのユーザーには **"de-DE"** を返します。  

特に、**Language** を使用すると、ユーザー向けに翻訳されたテキストを表示できます。  アプリには、アプリの翻訳済みの値のテーブルを含めることができます。

![](media/global-apps/loc-table.png)

その後、次のような数式を使用して、テーブルから翻訳された文字列をプルします。

**LookUp( Table1, TextID = "Hello" && (LanguageTag = Left( Language(), 2 ) || IsBlank( LanguageTag ))).LocalizedText**  

その他の言語に翻訳された文字列は、お使いの言語での文字列よりもはるかに長くなる可能性があることに注意してください。  多くの場合、ユーザー インターフェイスでこれらの文字列を表示するラベルやその他の要素を、大きくして適応させる必要があります。

詳細については、**[Language](functions/function-language.md)** 関数のドキュメントを参照してください。

### <a name="formatting-numbers-dates-and-times"></a>数値、日付、および時刻の書式設定
世界各地で、数値、日付、および時刻はさまざまな形式で表記されています。  コンマの意味、小数点以下桁数、および月、日、年の順序は場所によって異なります。   

**[Text](functions/function-text.md)** 関数は、ユーザーの言語設定を使用して数値および日付を書式設定します。

**Text** には、数値や日付をどのように書式設定するかを把握するために、書式設定文字列が必要です。  この書式設定文字列は、以下の 2 つの書式のいずれかである可能性があります。

* **グローバル対応列挙体。**  たとえば、**Text( Now(), DateTimeFormat.LongDate )** のようになります。  この数式は、言語に適切な形式で現在の日付の書式を設定します。  これは、書式設定文字列を指定する場合にお勧めします。
* **カスタム書式設定文字列。**  たとえば、**Text( Now(), "[$-en-US]dddd, mmmm dd, yyyy" )** とすると、言語 "en-US" で使用される場合の列挙と同様のテキストが表示されます。  カスタム書式設定文字列の利点は、特定の項目を指定できることです。

カスタム書式設定文字列の前にある "[$-en-US]" は、その言語でカスタム書式設定文字列を解釈するのかを **Text** に指示しています。  これが挿入され、既定でユーザーのオーサリング言語になります。  通常、これを変更する必要はありません。  これは、さまざまな言語を使用する作成者が同じアプリを編集するときに便利です。

**Text** に対する 3 つ目の引数は、関数の結果にどの言語を使用するかを指定します。  既定では、現在のユーザーの言語設定です。

詳細については、**[Text](functions/function-text.md)** 関数のドキュメントを参照してください。      

### <a name="reading-numbers-dates-and-times"></a>数値、日付、および時刻の読み取り
数値、日付、および、ユーザーが指定した時刻を読み取るための 4 つの関数があります。

* **[値](functions/function-value.md)**:テキスト文字列内の番号を数値に変換します。
* **[DateValue](functions/function-datevalue-timevalue.md)**:テキスト文字列の日付値を日付/時刻値に変換します。  テキスト文字列で指定された時刻は無視されます。
* **[TimeValue](functions/function-datevalue-timevalue.md)**:テキスト文字列の時刻値を日付/時刻値に変換します。  テキスト文字列で指定された日付は無視されます。
* **[DateTimeValue](functions/function-datevalue-timevalue.md)**:文字列の日付と時刻の値を日付/時刻値に変換します。  

Excel を使用したことがある場合、これらの関数はすべて単一の **Value** 関数にまとめられています。  PowerApps には日付/時刻および数字に個別の型がありるため、ここでは分割されます。

これらすべての関数には、同じ引数があります。

* *必要な文字列*:ユーザーからの文字列。 これには、**テキスト入力**コントロールに入力され、**Text** プロパティによってこのコントロールから読み取られる文字列などがあります。
* *言語の省略可能な*:解釈する言語、*文字列*します。  既定では、ユーザーの言語設定です。

例:

* **Value( "12,345.678", "en-US" )** または **Value( "12,345.678" )** の場合、"en-US" がユーザーの言語であり、計算に使用できる数字 **12345.678** を返します。
* **DateValue( "1/2/01", "es-ES" )** または **DateValue( "1/2/01" )** の場合、"es-ES" がユーザーの言語であり、日付/時刻の値 **2001 年 2 月 1 日深夜**を返します。
* **TimeValue( "11:43:02", "fr-FR" )** または **DateValue( "11:43:02" )** の場合、"fr-FR" がユーザーの言語であり、日付/時刻の値 **1970 年 1 月 1 日 11:43:02** を返します。
* **TimeDateValue( "11:43:02 1/2/01", "de-DE" )** または **DateValue( "11:43:02" )** の場合、"de-DE" がユーザーの言語であり、日付/時刻の値 **2001 年 2 月 1 日 11:43:02** を返します。

詳細については、**[Value 関数](functions/function-value.md)** および **[DateValue 関数、TimeValue 関数、DateTimeValue 関数](functions/function-datevalue-timevalue.md)** に関するドキュメント、および[日付と時刻の処理](show-text-dates-times.md)を参照してください。

### <a name="calendar-and-clock-information"></a>カレンダーと時計の情報
**[Calendar](functions/function-clock-calendar.md)** 関数および **[Clock](functions/function-clock-calendar.md)** 関数は、ユーザーの現在の言語でのカレンダーと時計の情報を提供します。  

特に、これらの関数を使用すると、選択肢が一覧表示された**ドロップダウン**コントロールが提供されます。  

詳細については、**[Calendar](functions/function-clock-calendar.md)** 関数および **[Clock](functions/function-clock-calendar.md)** 関数のドキュメントを参照してください。

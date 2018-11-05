---
title: 関数、シグナル、列挙型 | Microsoft Docs
description: PowerApps の関数、シグナル、および列挙体に関する参照情報。
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 06/05/2018
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 752bb630c1ecd1e86f37a1a063bcc5ee192431f0
ms.sourcegitcommit: 3aeb9381fbeb66cf08355d9a3d0f00ce2737e256
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/29/2018
ms.locfileid: "43163639"
---
# <a name="formula-reference-for-powerapps"></a>PowerApps の数式のリファレンス
数式では、多くの要素を組み合わせて使用します。  使用できる要素は、次のとおりです。

* **関数**: パラメーターを受け取り、演算を実行し、値を返します。 たとえば、**Sqrt(25)** は **5** を返します。 関数は、Microsoft Excel 関数をモデルにしています。  関数の中には、副作用を生じるものがあります。たとえば、**SubmitForm** 関数は、**Button.OnSelect** のような[動作の数式](working-with-formulas-in-depth.md)でのみ正しく機能します。
* **シグナル**: 環境に関する情報を返します。 たとえば、**[Location](functions/signals.md)** は、デバイスの現在の GPS 座標を返します。 シグナルは、パラメーターを受け取らず、副作用もありません。
* **列挙型**: 事前定義された定数値を返します。 たとえば、**[Color](functions/function-colors.md)** は、**Color.Red** や **Color.Blue** などの事前定義された値を持つ列挙型です。  一般的な列挙体がこのページに記載されています。関数に固有の列挙型は、関数と併せて説明しています。
* **[ThisItem](functions/operators.md#thisitem-operator)** や **[Parent](functions/operators.md#parent-operator)** などの**名前付き演算子**を使用すると、コンテナー内から情報にアクセスできます。

上記の他にも、次のような要素を使用できます。

* [すべての演算子](functions/operators.md)
* [コントロールとそのプロパティ](reference-properties.md)

## <a name="a"></a>A
**[Abs](functions/function-numericals.md)** – 数値の絶対値を返します。  

**[Acceleration](functions/signals.md)** – デバイス内の加速度センサーを読み取ります。

**[Acos](functions/function-trig.md)** – 数値のアークコサインをラジアン単位で返します。

**[Acot](functions/function-trig.md)** – 数値のアークコタンジェントをラジアン単位で返します。

**[AddColumns](functions/function-table-shaping.md)** – [列](working-with-tables.md#columns)が追加されたテーブルを返します。

**[And](functions/function-logicals.md)** – ブール論理の AND です。  すべての引数が **true** の場合に **true** を返します。  [**&&** 演算子](functions/operators.md)を使用することもできます。

**[App](functions/signals.md)** – どの画面が表示されているかなど、現在実行されているアプリに関する情報を返します。

**[Asin](functions/function-trig.md)** – 数値のアークサインをラジアン単位で返します。

**[Atan](functions/function-trig.md)** – 数値のアークタンジェントをラジアン単位で返します。

**[Atan2](functions/function-trig.md)** – (*x*,*y*) 座標に基づいてアークタンジェントをラジアン単位で返します。

**[Average](functions/function-aggregates.md)** – テーブル式または引数セットの平均を計算します。

## <a name="b"></a>B
**[Back](functions/function-navigate.md)** – 前の画面を表示します。  

**[Blank](functions/function-isblank-isempty.md)** – "*空白*" の値を返します。データ ソースに NULL 値を挿入するために使用できます。

## <a name="c"></a>C
**[Calendar](functions/function-clock-calendar.md)** – 現在のロケールのカレンダーに関する情報を取得します。

**[Char](functions/function-char.md)** – 文字コードを文字列に変換します。

**[Choices](functions/function-choices.md)** – ルックアップ列で使用可能な値のテーブルを返します。

**[Clear](functions/function-clear-collect-clearcollect.md)** – [コレクション](working-with-data-sources.md#collections)からすべてのデータを削除します。

**[ClearCollect](functions/function-clear-collect-clearcollect.md)** – コレクションからすべてのデータを削除し、[レコード](working-with-tables.md#records)のセットを追加します。

**[Clock](functions/function-clock-calendar.md)** – 現在のロケールの時計に関する情報を取得します。

**[Coalesce](functions/function-isblank-isempty.md)** – *空*以外の値は変更せずに、*空*の値を置き換えます。

**[Collect](functions/function-clear-collect-clearcollect.md)** – コレクションを作成するか、データ ソースにデータを追加します。

**[Color](functions/function-colors.md)** – 組み込みの色の値をプロパティに設定します。

**[ColorFade](functions/function-colors.md)** – 色の値をフェードします。

**[ColorValue](functions/function-colors.md)** – CSS 色名または 16 進コードを色の値に変換します。  

**[Compass](functions/signals.md)** – コンパスの方位を返します。

**[Concat](functions/function-concatenate.md)** – データ ソース内の文字列を連結します。  

**[Concatenate](functions/function-concatenate.md)** – 文字列を連結します。

**[Concurrent](functions/function-concurrent.md)** – 複数の数式を相互に同時に評価します。 

**[Connection](functions/signals.md)** – ネットワーク接続に関する情報を返します。

**[Count](functions/function-table-counts.md)** – 数値が格納されたテーブル レコードをカウントします。

**[Cos](functions/function-trig.md)** – ラジアン単位で指定された角度のコサインを返します。

**[Cot](functions/function-trig.md)** – ラジアン単位で指定された角度のコタンジェントを返します。

**[CountA](functions/function-table-counts.md)** – [空](functions/function-isblank-isempty.md)ではないテーブル レコードをカウントします。

**[CountIf](functions/function-table-counts.md)** – 条件に一致するテーブル レコードをカウントします。  

**[CountRows](functions/function-table-counts.md)** – テーブル レコードをカウントします。   

## <a name="d"></a>D
**[DataSourceInfo](functions/function-datasourceinfo.md)** – データ ソースに関する情報を返します。

**[Date](functions/function-date-time.md)** – **Year**、**Month**、および **Day** の値に基づいて、日付/時刻値を返します。  

**[DateAdd](functions/function-dateadd-datediff.md)** – 日数、月数、四半期数、または年数を日付/時刻値に加算します。

**[DateDiff](functions/function-dateadd-datediff.md)** – 2 つの日付値の差を、日数、月数、四半期数、または年数で返します。

**[DateTimeValue](functions/function-datevalue-timevalue.md)** – 日付と時刻の文字列を日付/時刻値に変換します。

**[DateValue](functions/function-datevalue-timevalue.md)** – 日付のみの文字列を日付/時刻値に変換します。

**[Day](functions/function-datetime-parts.md)** – 日付/時刻値の日付部分を取得します。  

**[Defaults](functions/function-defaults.md)** – データ ソースの既定値を返します。

**[Degrees](functions/function-trig.md)** - ラジアンを度数法で示した角度に変換します。

**[Disable](functions/function-enable-disable.md)** – GPS を読み取るための **[Location](functions/signals.md)** などのシグナルを無効にします。

**[Distinct](functions/function-distinct.md)** – 重複を削除してテーブルのレコードを集約します。  

**[Download](functions/function-param.md)** – Web からローカル デバイスにファイルをダウンロードします。

**[DropColumns](functions/function-table-shaping.md)** – 1 つ以上の列を削除してテーブルを返します。

## <a name="e"></a>E
**[EditForm](functions/function-form.md)** – 項目を編集するためのフォーム コントロールをリセットします。

**[Enable](functions/function-enable-disable.md)** – GPS を読み取るための **[Location](functions/signals.md)** などのシグナルを有効にします。

**[EndsWith](functions/function-startswith.md)** – あるテキスト文字列が別のテキスト文字列で終わるかどうかを調べます。

**[Errors](functions/function-errors.md)** – データ ソースに対する以前の変更のエラー情報を提供します。

**[EncodeUrl](functions/function-encode-decode.md)** – URL エンコードを使用して特殊文字をエンコードします。

**[Exit](functions/function-exit.md)** – 現在実行中のアプリを終了します。

**[Exp](functions/function-numericals.md)** - *e* の累乗を返します。

## <a name="f"></a>F
**[Filter](functions/function-filter-lookup.md)** – 1 つ以上の条件に基づいてフィルター処理されたテーブルを返します。

**[Find](functions/function-find.md)** – ある文字列が別の文字列内にあるかどうかを調べて、その位置を返します。

**[First](functions/function-first-last.md)** – テーブルの最初のレコードを返します。

**[FirstN](functions/function-first-last.md)** – テーブルの最初のレコード セット (N 個のレコード) を返します。

**[ForAll](functions/function-forall.md)** – 値を計算し、テーブルのすべてのレコードに対して操作を実行します。

## <a name="g"></a>G
**[GroupBy](functions/function-groupby.md)** – レコードをグループ化したテーブルを返します。

**[GUID](functions/function-guid.md)** – GUID 文字列を GUID 値に変換するか、新しい GUID 値を作成します。

## <a name="h"></a>H
**[HashTags](functions/function-hashtags.md)** – 文字列からハッシュタグ (#文字列) を抽出します。

**[Hour](functions/function-datetime-parts.md)** – 日付/時刻値の時間の部分を取得します。

## <a name="i"></a>I
**[If](functions/function-if.md)** – 条件が true の場合とそうでない場合とで異なる値を返します。 

**[IfError](functions/function-iferror.md)** – エラーを検出し、代替値を提供するか、操作を実行します。 

**[IsBlank](functions/function-isblank-isempty.md)** – [空白](functions/function-isblank-isempty.md)の値がないかを調べます。

**[IsEmpty](functions/function-isblank-isempty.md)** – 空のテーブルがないかを調べます。

**[IsMatch](functions/function-ismatch.md)** – 文字列をパターンと照合します。  正規表現を使用できます。

**[IsNumeric](functions/function-isnumeric.md)** – 数値がないかを調べます。

**[IsToday](functions/function-now-today-istoday.md)** – 日付/時刻値が今日に当たるかどうかを調べます。

## <a name="l"></a>L
**[Language](functions/function-language.md)** – 現在のユーザーの言語タグを返します。

**[Last](functions/function-first-last.md)** – テーブルの最後のレコードを返します。

**[LastN](functions/function-first-last.md)** – テーブルの最後のレコード セット (N 個のレコード) を返します。

**[Launch](functions/function-param.md)** – Web アドレスまたはアプリを起動します。

**[Left](functions/function-left-mid-right.md)** – 文字列の左端部分の文字を返します。

**[Len](functions/function-len.md)** – 文字列の長さを返します。

**[Ln](functions/function-numericals.md)** – 自然対数を返します。

**[LoadData](functions/function-savedata-loaddata.md)** – PowerApps プライベート ストレージからコレクションを読み込みます。

**[Location](functions/signals.md)** – GPS (Global Positioning System) などの情報を使用して現在地を地図座標として返します。

**[LookUp](functions/function-filter-lookup.md)** – 1 つ以上の条件に基づいてテーブル内の 1 つのレコードを検索します。

**[Lower](functions/function-lower-upper-proper.md)** – テキストの文字列内の文字をすべて小文字に変換します。

## <a name="m"></a>M
**[Max](functions/function-aggregates.md)** – テーブル式または引数セットの最大値を返します。

**[Mid](functions/function-left-mid-right.md)** – 文字列の中間部分の文字を返します。

**[Min](functions/function-aggregates.md)** – テーブル式または引数セットの最小値を返します。

**[Minute](functions/function-datetime-parts.md)** – 日付/時刻値の分の部分を取得します。  

**[Mod](functions/function-mod.md)** – 被除数を除数で除算した後に、その剰余を返します。

**[Month](functions/function-datetime-parts.md)** – 日付/時刻値の月の部分を取得します。

## <a name="n"></a>N
**[Navigate](functions/function-navigate.md)** – 表示する画面を変更します。

**[NewForm](functions/function-form.md)** – 項目を作成するためのフォーム コントロールをリセットします。

**[Not](functions/function-logicals.md)** – ブール論理の NOT です。  引数が **false** の場合は **true** を、**true** の場合は **false** を返します。  [**!** 演算子](functions/operators.md)を使用することもできます。

**[Notify](functions/function-showerror.md)** – バナー メッセージをユーザーに表示します。

**[Now](functions/function-now-today-istoday.md)** – 現在の日付/時刻値を取得します。

## <a name="o"></a>O
**[Or](functions/function-logicals.md)** – ブール論理の OR です。  引数のいずれかが **true** の場合に **true** を返します。  [**||** 演算子](functions/operators.md)を使用することもできます。

## <a name="p"></a>P
**[Param](functions/function-param.md)** – ユーザーがアプリを開いたときに渡されるパラメーターを取得します。

**[Parent](functions/operators.md#parent-operator)** – コンテナー コントロールのプロパティを取得します。

**[Patch](functions/function-patch.md)** – データ ソース内のレコードを変更または作成するか、データ ソースの外部でレコードをマージします。

**[Pi](functions/function-trig.md)** – 数値 &pi; を返します。

**[PlainText](functions/function-encode-decode.md)** – 文字列から HTML タグと XML タグを削除します。

**[Power](functions/function-numericals.md)** – 数値の累乗を返します。  [**^** 演算子](functions/operators.md)を使用することもできます。

**[Proper](functions/function-lower-upper-proper.md)** – 文字列内の各単語の最初の文字を大文字に変換し、残りを小文字に変換します。

## <a name="r"></a>R
**[Radians](functions/function-trig.md)** - 度数法を使った角度をラジアン値に変換します。

**[Rand](functions/function-rand.md)** – 疑似乱数を返します。

**[Refresh](functions/function-refresh.md)** – データ ソースのレコードを更新します。

**[Remove](functions/function-remove-removeif.md)** – データ ソースから特定のレコードを削除します。

**[RemoveIf](functions/function-remove-removeif.md)** – 条件に基づいてデータ ソースからレコードを削除します。

**[RenameColumns](functions/function-table-shaping.md)** – テーブルの列の名前を変更します。

**[Replace](functions/function-replace-substitute.md)** – 文字列の一部を別の文字列に置き換えます。対象の文字列の開始位置を指定します。

**[Reset](functions/function-reset.md)** – ユーザーによる変更を破棄して、入力コントロールを既定値にリセットします。

**[ResetForm](functions/function-form.md)** – 既存の項目を編集するためのフォーム コントロールをリセットします。

**[Revert](functions/function-revert.md)** – データ ソースのレコードを更新し、エラーをクリアします。

**[RGBA](functions/function-colors.md)** – 赤、緑、青、アルファのコンポーネント セットの色の値を返します。

**[Right](functions/function-left-mid-right.md)** – 文字列の右端部分の文字を返します。

**[Round](functions/function-round.md)** – 最も近い数値に丸めます。

**[RoundDown](functions/function-round.md)** – 元の数値以下の最大値になるように切り捨てます。

**[RoundUp](functions/function-round.md)** – 元の数値以上の最小値になるように切り上げます。

## <a name="s"></a>S
**[SaveData](functions/function-savedata-loaddata.md)** – PowerApps プライベート ストレージにコレクションを保存します。

**[Search](functions/function-filter-lookup.md)** – テーブル内で、いずれかの列に文字列が含まれているレコードを検索します。  

**[Second](functions/function-datetime-parts.md)** – 日付/時刻値の秒の部分を取得します。

**[Select](functions/function-select.md)** – コントロールでの選択アクションをシミュレートし、**OnSelect** 式の評価を実行させます。

**[Set](functions/function-set.md)** – グローバル変数の値を設定します。

**[ShowColumns](functions/function-table-shaping.md)** – 選択した列のみが含まれたテーブルを返します。

**[Shuffle](functions/function-shuffle.md)** – テーブルのレコードをランダムに並べ替えます。

**[Sin](functions/function-trig.md)** – ラジアン単位で指定された角度のサインを返します。

**[Sort](functions/function-sort.md)** – 数式に基づいて並べ替えられたテーブルを返します。

**[SortByColumns](functions/function-sort.md)** – 1 つ以上の列に基づいて並べ替えられたテーブルを返します。

**[Split](functions/function-split.md)** - テキスト文字列を部分文字列のテーブルに分割します。

**[Sqrt](functions/function-numericals.md)** – 数値の平方根を返します。

**[StartsWith](functions/function-startswith.md)** – あるテキスト文字列が別のテキスト文字列の先頭にあるかどうかを調べます。

**[StdevP](functions/function-aggregates.md)** – 引数の標準偏差を返します。  

**[Substitute](functions/function-replace-substitute.md)** – 文字列を照合して、文字列の一部を別の文字列に置き換えます。

**[SubmitForm](functions/function-form.md)** – フォーム コントロール内の項目をデータ ソースに保存します。

**[Sum](functions/function-aggregates.md)** – テーブル式または引数セットの合計を計算します。  

**[Switch](functions/function-if.md)** – 値のセットと一致した後、対応する数式を評価します。

## <a name="t"></a>T
**[Table](functions/function-table.md)** – 一時テーブルを作成します。  

**[Tan](functions/function-trig.md)** - ラジアン単位で指定された角度のタンジェントを返します。

**[Text](functions/function-text.md)** – 数値が文字列として表示されるように書式を設定します。

**[ThisItem](functions/operators.md#thisitem-operator)** – ギャラリーまたはフォーム内で、コンテナーから現在の項目のデータを返します。

**[Time](functions/function-date-time.md)** – **Hour**、**Minute**、および **Second** の値に基づいて、日付/時刻値を返します。  

**[TimeValue](functions/function-datevalue-timevalue.md)** – 時刻のみの文字列を日付/時刻値に変換します。

**[TimeZoneOffset](functions/function-dateadd-datediff.md)** – UTC とユーザーのローカル時刻の差を分の単位で返します。

**[Today](functions/function-now-today-istoday.md)** – 現在の日付/時刻値を取得します。

**[Trim](functions/function-trim.md)** – テキストの文字列の末尾や内部から余分なスペースを削除します。

**[TrimEnds](functions/function-trim.md)** – テキストの文字列の末尾のみから余分なスペースを削除します。

## <a name="u"></a>U
**[Ungroup](functions/function-groupby.md)** – グループを削除します。

**[Update](functions/function-update-updateif.md)** – データ ソースのレコードを置き換えます。

**[UpdateContext](functions/function-updatecontext.md)** – 現在の画面にある、1 つまたは複数の[コンテキスト変数](working-with-variables.md#create-a-context-variable)の値を設定します。

**[UpdateIf](functions/function-update-updateif.md)** – 条件に基づいてデータ ソース内のレコードのセットを変更します。

**[Upper](functions/function-lower-upper-proper.md)** – テキストの文字列内の文字をすべて大文字に変換します。

**[User](functions/function-user.md)** – 現在のユーザーに関する情報を返します。

## <a name="v"></a>V
**[Validate](functions/function-validate.md)** – データ ソースの単一の列またはレコード全体の値が有効であるかどうかを調べます。

**[Value](functions/function-value.md)** – 文字列を数値に変換します。

**[VarP](functions/function-aggregates.md)** – 引数の分散を返します。  

**[ViewForm](functions/function-form.md)** – 既存の項目を表示するためのフォーム コントロールをリセットします。

## <a name="w"></a>W
**[Weekday](functions/function-datetime-parts.md)** – 日付/時刻値の曜日の部分を取得します。

## <a name="y"></a>Y
**[Year](functions/function-datetime-parts.md)** – 日付/時刻値の年の部分を取得します。  


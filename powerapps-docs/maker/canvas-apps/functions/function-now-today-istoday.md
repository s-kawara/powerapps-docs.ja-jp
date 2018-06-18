---
title: Now、Today、および IsToday 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の Now、Today、および IsToday 関数の参照情報
author: gregli-msft
ms.service: powerapps
ms.topic: reference
ms.component: canvas
ms.date: 06/09/2018
ms.author: gregli
ms.openlocfilehash: 690144a8d5aef2d7608f0e4104661620840b02ad
ms.sourcegitcommit: 6bfb002180148a3f22a4d1d8d750fc442489ebe4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/11/2018
ms.locfileid: "35291699"
---
# <a name="now-today-and-istoday-functions-in-powerapps"></a>PowerApps の Now、Today、および IsToday 関数
現在の日付と時刻を返し、日付/時刻値が今日のものかどうかをテストします。

## <a name="description"></a>説明
**Now** 関数は、現在の日付と時刻を日付/時刻値として返します。

**Today** 関数は、現在の日付を日付/時刻値として返します。 時刻部分は、午前 0 時です。 **Today** は、1 日 (今日の午前 0 時から翌日の午前 0 時まで) を通して同じ値を保持します。

**IsToday** 関数は、日付/時刻値が今日の午前 0 時から翌日の午前 0 時の間の値になっているかどうかをテストします。 この関数は、ブール値 (**true** または **false**) を返します。

これらの関数はすべて、現在のユーザーのローカル時刻を使用します。

詳細については、[日付と時刻の操作](../show-text-dates-times.md)に関するページを参照してください。

## <a name="volatile-functions"></a>揮発性関数
**Now** と **Today** は揮発性の関数です。  これらの関数はいずれも、評価されるたびに異なる値を返します。  

データ フロー式で使うと、揮発性関数は、それが出現する数式が再評価された場合にのみ、異なる値を返します。  数式で何も変更されていない場合、アプリの実行全体を通じて同じ値を返します。

たとえば、**Label1.Text = Now()** であるラベル コントロールは、アプリがアクティブな間は変化しません。  アプリをいったん閉じて再び開いた場合にのみ、新しい値が返ります。

関数は、何かが変更された数式の一部である場合に再評価されます。  たとえば、**Label1.Text = DateAdd( Now(), Slider1.Value, Minutes )** であるスライダー コントロールを含むように例を変更した場合、スライダー コントロールの値が変化するたびにラベルのテキスト プロパティが再評価されて、現在の時刻が取得されます。

[動作の数式](../working-with-formulas-in-depth.md)で使うと、動作の数式が評価されるたびに、揮発性関数が評価されます。  例については、以下を参照してください。

## <a name="syntax"></a>構文
**Now**()

**Today**()

**IsToday**( *DateTime* )

* *DateTime* - 必須。  テストする日付/時刻値。

## <a name="examples"></a>例
このセクションの例では、現在の時刻が **2015 年 2 月 12 日**の**午前 3 時 59 分**、言語が **en-us** です。

| 数式 | 説明 | 結果 |
| --- | --- | --- |
| **Text( Now(), "mm/dd/yyyy hh:mm:ss" )** |現在の日付と時刻を取得し、文字列として表示します。 |"02/12/2015 03:59:00" |
| **Text( Today(), "mm/dd/yyyy hh:mm:ss" )** |現在の日付のみを取得し、時刻は午前 0 時としたまま、これを文字列として表示します。 |"02/12/2015 00:00:00" |
| **IsToday( Now() )** |現在の日付と時刻が、今日の午前 0 時から翌日の午前 0 時の間であるかどうかをテストします。 |**true** |
| **IsToday( Today() )** |現在の日付が、今日の午前 0 時から翌日の午前 0 時の間であるかどうかをテストします。 |**true** |
| **Text( DateAdd( Now(), 12 ), "mm/dd/yyyy hh:mm:ss" )** |現在の日付と時刻を取得し、その結果に 12 日を加算して、文字列として表示します。 |"02/24/2015 03:59:00" |
| **Text( DateAdd( Today(), 12 ), "mm/dd/yyyy hh:mm:ss" )** |現在の日付を取得し、その結果に 12 日を加算して、文字列として表示します。 |"02/24/2015 00:00:00" |
| **IsToday( DateAdd( Now(), 12 ) )** |現在の日付と時刻に 12 日を加算した日時が今日の午前 0 時から翌日の午前 0 時の間であるかどうかをテストします。 |**false** |
| **IsToday( DateAdd( Today(), 12 ) )** |現在の日付に 12 日を加算した日付が今日の午前 0 時から翌日の午前 0 時の間であるかどうかをテストします。 |**false** |

#### <a name="display-a-clock-that-updates-in-real-time"></a>リアルタイムで更新される時計を表示する

1. **[Timer](../controls/control-timer.md)** コントロールを追加し、その **Duration** プロパティを **1000** に設定し、**Repeat** プロパティを **true** に設定します。

    タイマーは 1 秒間実行して自動的に最初からやり直すパターンを続けます。 

1. コントロールの **OnTimerEnd** プロパティを次の式に設定します。

    **Set( CurrentTime, Now() )**

    タイマーが (1 秒ごとに) 最初から再開するたびに、この式は **CurrentTime** グローバル変数に **Now** 関数の現在の値を設定します。

    ![式 OnTimerEnd = Set(CurrentTime, Now()) であるタイマー コントロールを含む画面](media/function-now-today-istoday/now-set-currenttime.png)

1. **[Label](../controls/control-text-box.md)** コントロールを追加し、その **Text** プロパティを次の数式に設定します。

    **Text( CurrentTime, LongTime24 )**

    **[Text](function-text.md)** 関数を使って日付と時刻の書式を設定するか、またはこのプロパティに **CurrentTime** を設定して秒を除いた時と分だけを表示します。

    ![Text プロパティが Text( CurrentTime, LongTime24) に設定されたラベル コントロールを含む画面](media/function-now-today-istoday/now-use-currenttime.png)

1. F5 キーを押してアプリをプレビューした後、クリックまたはタップしてタイマーを開始します。

    ラベルは、秒の単位まで現在時刻を示し続けます。

    ![4 つの時刻値 (13:50:22、13:50:45、13:51:03、13:51:25) を示す 4 つの画面](media/function-now-today-istoday/now-four-times.png)

1. タイマーの **AutoStart** プロパティを **true** に設定し、**Visible** プロパティを **false** に設定します。

    タイマーは表示されず、自動的に開始されます。

1. 次の例のように、画面の **[OnStart](../controls/control-screen.md)** プロパティを、**CurrentTime** 変数が有効な値になるように設定します。

    **Set(CurrentTime, Now())**

    アプリが起動するとすぐに (タイマーがまるまる 1 秒動く前に)、ラベルが表示されます。

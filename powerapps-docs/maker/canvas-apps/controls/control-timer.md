---
title: 'タイマー コントロール: リファレンス | Microsoft Docs'
description: 各種プロパティとサンプルを含むタイマー コントロールに関する情報
author: fikaradz
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 10/25/2016
ms.author: fikaradz
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 5d20e2324f2efb4f866ed4fc183f289733c10a41
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61560469"
---
# <a name="timer-control-in-powerapps"></a>PowerApps のタイマー コントロール
一定の時間が経過した後のアプリの反応を決定できるコントロールです。

## <a name="description"></a>説明
タイマーは、たとえば、コントロールが表示される時間の長さを決定したり、一定の時間が経過した後にコントロールの他のプロパティを変更したりできます。

> [!NOTE]
> PowerApps Studio では、タイマーは、プレビュー モードでのみ実行します。


## <a name="key-properties"></a>主要なプロパティ
**Duration** - タイマーを実行する時間の長さを、ミリ秒単位で指定します。  最大値はありません。

**OnTimerEnd** – タイマーが実行を完了した場合のアプリの反応を指定します。

**Repeat** – タイマーが実行を完了したときに自動的に再開されるかどうかを指定します。

## <a name="additional-properties"></a>その他のプロパティ
**[Align](properties-text.md)** – コントロールの水平方向の中心に対するテキストの位置です。

**AutoPause** – ユーザーが別の画面に移動した場合、タイマー コントロールを自動的に一時停止するかどうかを指定します。

**AutoStart** – ユーザーがタイマー コントロールを含む画面に移動したときに、自動的に再生を開始するかどうかを指定します。

**[BorderColor](properties-color-border.md)** – コントロールの境界線の色です。

**[BorderStyle](properties-color-border.md)** – コントロールの境界線を **Solid** (実線)、**Dashed** (破線)、**Dotted** (点線)、**None** (なし) のいずれに指定します。

**[BorderThickness](properties-color-border.md)** – コントロールの境界線の太さです。

**[Color](properties-color-border.md)** – コントロールのテキストの色です。

**[DisplayMode](properties-core.md)** – コントロールで、ユーザー入力を許可するか (**Edit**)、データの表示のみを許可するか (**View**)、許可しないか (**Disabled**) を設定します。

**[DisabledBorderColor](properties-color-border.md)** – コントロールの **[DisplayMode](properties-core.md)** プロパティが **Disabled** に設定されている場合のコントロールの境界線の色です。

**[DisabledColor](properties-color-border.md)** – コントロールの **[DisplayMode](properties-core.md)** プロパティが **Disabled** に設定されている場合のコントロール内のテキストの色です。

**[DisabledFill](properties-color-border.md)** – コントロールの **[DisplayMode](properties-core.md)** プロパティが **Disabled** に設定されている場合のコントロールの背景色です。

**[Fill](properties-color-border.md)** – コントロールの背景色です。

**[FocusedBorderColor](properties-color-border.md)** – コントロールにフォーカスがあるときのコントロールの境界線の色です。

**[FocusedBorderThickness](properties-color-border.md)** – コントロールにフォーカスがあるときのコントロールの境界線の太さです。

**[Font](properties-text.md)** – テキストを表記するフォントのファミリー名です。

**[FontWeight](properties-text.md)** – コントロール内のテキストの太さ。**太字**、 **Semibold**、 **標準**、または **明るい** します。

**[Height](properties-size-location.md)** – コントロールの上端と下端の距離です。

**[HoverBorderColor](properties-color-border.md)** – コントロール上にユーザーがマウス ポインターを重ねているときのコントロールの境界線の色です。

**[HoverColor](properties-color-border.md)** – コントロールにユーザーがマウス ポインターを重ねているときのコントロール内のテキストの色です。

**[HoverFill](properties-color-border.md)** – コントロールにユーザーがマウス ポインターを重ねているときのコントロールの背景色です。

**[Italic](properties-text.md)** – コントロール内のテキストを斜体にするかどうかを指定します。

**[OnSelect](properties-core.md)** – ユーザーがコントロールをタップまたはクリックした場合のアプリの反応を指定します。

**OnTimerStart** – タイマーが実行を開始した場合のアプリの反応を指定します。

**[PressedBorderColor](properties-color-border.md)** – コントロールをユーザーがタップまたはクリックしたときのコントロールの境界線の色です。

**[PressedColor](properties-color-border.md)** – コントロールをユーザーがタップまたはクリックしたときのコントロール内のテキストの色です。

**[PressedFill](properties-color-border.md)** – コントロールをユーザーがタップまたはクリックしたときのコントロールの背景色です。

**[Reset](properties-core.md)** – コントロールを既定値に戻すかどうかを指定します。

**[Size](properties-text.md)** – コントロールに表示されるテキストのフォント サイズです。

**Start** – タイマーが開始するかどうか。

**[Strikethrough](properties-text.md)** – コントロールに表示されるテキストに取り消し線を付けるかどうかを指定します。

**[TabIndex](properties-accessibility.md)** – 他のコントロールに関連するキーボード ナビゲーションの順序です。

**[Text](properties-core.md)** – コントロールに表示されるテキスト、またはコントロールにユーザーが入力するテキストです。

**[Tooltip](properties-core.md)** – ポインターをコントロールに合わせたときに表示される説明テキストです。

**[Underline](properties-text.md)** – コントロールに表示されるテキストの下に線を引くかどうかを指定します。

**[Visible](properties-core.md)** – コントロールを表示するか非表示にするかを指定します。

**[Width](properties-size-location.md)** – コントロールの左端と右端の間の距離です。

**[X](properties-size-location.md)** – コントロールの左端とその親コンテナー (親コンテナーがない場合は画面) の左端間の距離です。

**[Y](properties-size-location.md)** – コントロールの上端とその親コンテナー (親コンテナーがない場合は画面) の上端間の距離です。

## <a name="related-functions"></a>関連する関数
[**Refresh**( *DataSource* )](../functions/function-refresh.md)

## <a name="examples"></a>例
### <a name="show-a-countdown"></a>カウントダウンの表示
1. タイマーを追加して **Countdown** という名前を付けます。

    [コントロールの追加、命名、構成についてはこちらをご覧ください](../add-configure-controls.md)。
2. タイマーの **Duration** プロパティを **10000** に、その **Repeat** および **Autostart** プロパティを **true** に設定します。
3. (オプション) **[Height](properties-size-location.md)** プロパティを **160** に、**[Width](properties-size-location.md)** プロパティを **600** に、**[Size](properties-text.md)** プロパティを **60** に設定して、タイマーを読み取りやすくします。
4. ラベルを追加し、その **[Text](properties-core.md)** プロパティを次の数式に設定します。
   <br>**"残りの秒数: " & RoundUp(10-Countdown.Value/1000, 0)**

    **[RoundUp](../functions/function-round.md)** 関数または[その他の関数](../formula-reference.md)については各関連記事を参照してください。

    ラベルには、タイマーが再開されるまでの秒数が表示されます。

### <a name="animate-a-control"></a>コントロールのアニメーション
1. タイマーを追加して **FadeIn** という名前を付けます。

    [コントロールの追加、命名、構成についてはこちらをご覧ください](../add-configure-controls.md)。
2. タイマーの **Duration** プロパティを **5000** に、**Repeat** プロパティを **true** に、**[Text](properties-core.md)** プロパティを**アニメーションの切り替え**に設定します。
3. (オプション) **[Height](properties-size-location.md)** プロパティを **160** に、**[Width](properties-size-location.md)** プロパティを **600** に、**[Size](properties-text.md)** プロパティを **60** に設定して、タイマーを読み取りやすくします。
4. ラベルを追加し、その **[Text](properties-core.md)** プロパティを設定して "**ようこそ!**" を表示し、 その **[Color](properties-color-border.md)** プロパティを次の数式に設定します。
   <br>**ColorFade(Color.BlueViolet, FadeIn.Value/5000)**

    **[ColorFade](../functions/function-colors.md)** 関数または[その他の関数](../formula-reference.md)については各関連記事を参照してください。

5. アニメーションを開始または停止するには、タイマー ボタンを選択します。 ラベル内のテキストが白色にフェードした後、最大輝度に戻り、このプロセスが繰り返されます。

## <a name="accessibility-guidelines"></a>アクセシビリティのガイドライン
同じガイドライン、 **[ボタン](control-button.md)** にコントロールを適用、**タイマー**ユーザーが操作できる場合は、制御します。

### <a name="background-timers"></a>バック グラウンド タイマー
バック グラウンド タイマーは、自動的に実行され、非表示します。 使用脇役をユーザーにはほとんど興味の経過時間があります。 たとえば、1 分ごとにデータを更新したり、一定の時間に対してのみ、通知メッセージを表示できます。

バック グラウンド タイマーがあります、 **[Visible](properties-core.md)** すべてのユーザーからに隠れているように、プロパティが false に設定します。

### <a name="timing-considerations"></a>タイミングに関する考慮事項
場合、**タイマー**の実行が自動的に、ユーザーに読み取りのコンテンツを使用するには、十分な時間があるかどうかを検討します。 キーボードとスクリーン リーダー ユーザーは、多くの時間、時間指定イベントに応答する必要があります。

これらの方法のいずれかで十分です。
* 時間指定イベントをキャンセルできるようにします。
* 開始前に、制限時間を調整できるようにします。
* 期限が切れる前に、20 秒間警告し、制限を拡張する簡単な方法を提供します。

一部のシナリオでは、これらの要件は除外されます。 詳細については、[時間制限に関する WCAG 2.0 ガイドライン](https://www.w3.org/TR/WCAG20/#time-limits)を参照してください。

### <a name="screen-reader-support"></a>スクリーン リーダーのサポート
* タイマーが現在の画面上の変更をトリガーする場合は、使用、[ライブ領域](../accessible-apps-live-regions.md)への変更内容をスクリーン リーダー ユーザーに通知します。

    > [!NOTE]
    > スクリーン リーダー、タイマーが表示され、実行中の場合は、経過時間が 5 秒ごとに通知されます。

* 使用しないでください、 **[テキスト](properties-core.md)** 時間を区別して重要な情報については、コントロールのプロパティ。 スクリーン リーダーへの変更が通知されません**[テキスト](properties-core.md)** します。
* 対話型のタイマー。
    * **[Text](properties-core.md)** を指定する必要があります。
    * 追加を検討する、 **[ラベル](control-text-box.md)** 経過時間を表示するコントロール。 使用して、タイマーの**[テキスト](properties-core.md)** プロパティを開始またはタイマーを停止するように指示します。

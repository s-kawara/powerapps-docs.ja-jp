---
title: 'シェイプ コントロールとアイコン コントロール: リファレンス | Microsoft Docs'
description: 各種プロパティとサンプルを含むシェイプ コントロールとアイコン コントロールに関する情報
author: fikaradz
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 10/25/2016
ms.author: fikaradz
ms.openlocfilehash: 12865bf432ed31f0964add63fa024182680fb7aa
ms.sourcegitcommit: dfa0e1a7981814e15e6ca4720e2a5f930e859db1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2018
ms.locfileid: "39022403"
---
# <a name="shape-controls-and-icon-controls-in-powerapps"></a>PowerApps のシェイプ コントロールとアイコン コントロール
見た目と動作のプロパティが構成できるグラフィックスです。

## <a name="description"></a>説明
これらのコントロールには、矢印、幾何学的図形、アクション アイコン、記号などがあり、塗りつぶし、サイズ、位置などのプロパティを構成できます。 また、**[OnSelect](properties-core.md)** プロパティを構成すると、ユーザーがコントロールをクリックまたはタップした場合にアプリが反応するようにできます。

## <a name="key-properties"></a>主要なプロパティ
**[Fill](properties-color-border.md)** – コントロールの背景色です。

**[OnSelect](properties-core.md)** – ユーザーがコントロールをタップまたはクリックした場合のアプリの反応を指定します。

## <a name="additional-properties"></a>その他のプロパティ
**[AccessibleLabel](properties-accessibility.md)** – スクリーン リーダー用のラベルです。

**[DisplayMode](properties-core.md)** – コントロールで、ユーザー入力を許可するか (**Edit**)、データの表示のみを許可するか (**View**)、許可しないか (**Disabled**) を設定します。

**[FocusedBorderColor](properties-color-border.md)** – コントロールにフォーカスがあるときのコントロールの境界線の色です。

**[FocusedBorderThickness](properties-color-border.md)** – コントロールにフォーカスがあるときのコントロールの境界線の太さです。

**[Height](properties-size-location.md)** – コントロールの上端と下端の距離です。

**[HoverFill](properties-color-border.md)** – コントロールにユーザーがマウス ポインターを重ねているときのコントロールの背景色です。

**[PressedBorderColor](properties-color-border.md)** – コントロールをユーザーがタップまたはクリックしたときのコントロールの境界線の色です。

**[PressedFill](properties-color-border.md)** – コントロールをユーザーがタップまたはクリックしたときのコントロールの背景色です。

**[TabIndex](properties-accessibility.md)** – 他のコントロールに関連するキーボード ナビゲーションの順序です。

**[Visible](properties-core.md)** – コントロールを表示するか非表示にするかを指定します。

**[Width](properties-size-location.md)** – コントロールの左端と右端の間の距離です。

**[X](properties-size-location.md)** – コントロールの左端とその親コンテナー (親コンテナーがない場合は画面) の左端間の距離です。

**[Y](properties-size-location.md)** – コントロールの上端とその親コンテナー (親コンテナーがない場合は画面) の上端間の距離です。

## <a name="related-functions"></a>関連する関数

[**Navigate**( *ScreenName*, *ScreenTransition* )](../functions/function-navigate.md)

## <a name="example"></a>例

1. 既定の**[スクリーン](control-screen.md)** コントロールに **Target** という名前を付け、**[ラベル](control-text-box.md)** コントロールを追加して **Target** を表示するように **[Text](properties-core.md)** プロパティを設定します。

    [コントロールの追加および構成](../add-configure-controls.md)についてはこちらをご覧ください。

2. **[スクリーン](control-screen.md)** コントロールを追加し、**Source** という名前を付けます。
3. **Source** に **シェイプ** コントロールを追加し、**[OnSelect](properties-core.md)** プロパティに次の式を設定します。<br>**Navigate(Target, ScreenTransition.Fade)**
4. F5 キーを押してから、**シェイプ** コントロールをクリックまたはタップします。

    **[Target]\(ターゲット)** 画面が表示されます。

5. (省略可能) Esc キーを押して既定のワークスペースに戻り、**Target** に**シェイプ** コントロールを追加して、**シェイプ** コントロールの **[OnSelect](properties-core.md)** プロパティに次の式を設定します。
   <br>**Navigate(Source, ScreenTransition.Fade)**


## <a name="accessibility-guidelines"></a>アクセシビリティのガイドライン

### <a name="color-contrast"></a>色のコントラスト

以下は、ボタンとして使用されるグラフィックまたは単なる装飾用ではないグラフィックにのみ適用されます。

アイコンの場合:
* **[Color](properties-color-border.md)** と **[Fill](properties-color-border.md)**
* その他の[標準の色のコントラスト要件](../accessible-apps-color.md)が適用されます (ボタンとして使用される場合)

境界線のある図形の場合:
* **[BorderColor](properties-color-border.md)** およびコントロールの外部の色
* **[FocusedBorderColor](properties-color-border.md)** およびコントロールの外部の色 (ボタンとして使用される場合)

境界線のない図形の場合:
* **[Fill](properties-color-border.md)** およびコントロールの外部の色
* **[PressedFill](properties-color-border.md)** およびコントロールの外部の色 (ボタンとして使用される場合)
* **[HoverFill](properties-color-border.md)** およびコントロールの外部の色 (ボタンとして使用される場合)

### <a name="screen-reader-support"></a>スクリーン リーダーのサポート
* グラフィックがボタンとして使用されるか、単なる装飾用ではない場合は、**[AccessibleLabel](properties-accessibility.md)** が存在する必要があります。
* グラフィックが純粋に装飾用である場合は、**[AccessibleLabel](properties-accessibility.md)** を空または空の文字列 **""** にする必要があります。 それにより、スクリーン リーダーでグラフィックが無視されます。
* グラフィックが冗長な情報を提供する場合は、**[AccessibleLabel](properties-accessibility.md)** を空または空の文字列 **""** にすることができます。

    たとえば、**[AccessibleLabel](properties-accessibility.md)** が**設定**に設定された **[設定]** アイコンがあるとします。 このアイコンは、ボタンとしては使用されません。 同じく **[設定]** と表示される**[ラベル](control-text-box.md)** の横にあります。 スクリーン リーダーは、アイコンを**設定**と読み上げ、ラベルをもう一度**設定**と読み上げます。 これは不必要に冗長です。 この場合、アイコンに **[AccessibleLabel](properties-accessibility.md)** は必要ありません。

    > [!IMPORTANT]
    > スクリーン リーダーは、**[AccessibleLabel](properties-accessibility.md)** が空の場合でも、**[TabIndex](properties-accessibility.md)** が 0 以上のアイコンまたは図形を常に読み上げます。 これらはボタンとしてレンダリングされるためです。 **[AccessibleLabel](properties-accessibility.md)** が指定されていない場合、スクリーン リーダーは単純にグラフィックを**ボタン**として読み上げます。

### <a name="keyboard-support"></a>キーボードのサポート
* グラフィックをボタンとして使用する場合は、**[TabIndex](properties-accessibility.md)** を 0 以上にする必要があります。 こうすることで、キーボード ユーザーがそこに移動できるようになります。
* グラフィックをボタンとして使用する場合は、フォーカス インジケーターを明確に表示する必要があります。 これを実現するには **[FocusedBorderColor](properties-color-border.md)** と **[FocusedBorderThickness](properties-color-border.md)** を使用します。

    > [!NOTE]
  > **[TabIndex](properties-accessibility.md)** が 0 以上の場合、アイコンまたは図形はボタンとしてレンダリングされます。 視覚的な外観は変わりませんが、スクリーン リーダーはイメージをボタンとして正しく識別します。 **[TabIndex](properties-accessibility.md)** が 0 未満の場合、アイコンまたは図形はイメージとして識別されます。

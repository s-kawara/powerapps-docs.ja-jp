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
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 88e0a74d2c25d1d2f5f571f4d1850417d1aab9ca
ms.sourcegitcommit: 4ed29d83e90a2ecbb2f5e9ec5578e47a293a55ab
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "63318430"
---
# <a name="shape-controls-and-icon-controls-in-powerapps"></a>PowerApps のシェイプ コントロールとアイコン コントロール
見た目と動作のプロパティが構成できるグラフィックスです。

## <a name="description"></a>説明
これらのコントロールには、矢印、幾何学的図形、アクション アイコン、記号などがあり、塗りつぶし、サイズ、位置などのプロパティを構成できます。 構成することも、 **[OnSelect](properties-core.md)** プロパティ、ユーザーがコントロールを選択するかどうかのアプリの応答できるようにします。

## <a name="key-properties-icons-and-shapes"></a>キー プロパティ (アイコンとシェイプ)
**[Fill](properties-color-border.md)** – コントロールの背景色です。

**[OnSelect](properties-core.md)**  – ユーザーがコントロールを選択したとき、アプリの応答方法。

## <a name="key-properties-icons-only"></a>キー プロパティ (アイコンのみ)

**アイコン**-表示するアイコンの種類 (たとえば、 **ArrowDown**または**ShoppingCart**)。 

**回転**-アイコンを回転する角度の数。 

**色**-名前または RGBA 値でアイコンの色。

## <a name="additional-properties"></a>その他のプロパティ
**[AccessibleLabel](properties-accessibility.md)** – スクリーン リーダー用のラベルです。

**[DisplayMode](properties-core.md)** – コントロールで、ユーザー入力を許可するか (**Edit**)、データの表示のみを許可するか (**View**)、許可しないか (**Disabled**) を設定します。

**[FocusedBorderColor](properties-color-border.md)** – コントロールにフォーカスがあるときのコントロールの境界線の色です。

**[FocusedBorderThickness](properties-color-border.md)** – コントロールにフォーカスがあるときのコントロールの境界線の太さです。

**[Height](properties-size-location.md)** – コントロールの上端と下端の距離です。

**[HoverFill](properties-color-border.md)** – コントロールにユーザーがマウス ポインターを重ねているときのコントロールの背景色です。

**[PressedBorderColor](properties-color-border.md)**  – ユーザーがそのコントロールを選択すると、コントロールの境界線の色。

**[PressedFill](properties-color-border.md)**  – ユーザーがそのコントロールを選択するときのコントロールの背景色。

**[TabIndex](properties-accessibility.md)** – 他のコントロールに関連するキーボード ナビゲーションの順序です。

**[Visible](properties-core.md)** – コントロールを表示するか非表示にするかを指定します。

**[Width](properties-size-location.md)** – コントロールの左端と右端の間の距離です。

**[X](properties-size-location.md)** – コントロールの左端とその親コンテナー (親コンテナーがない場合は画面) の左端間の距離です。

**[Y](properties-size-location.md)** – コントロールの上端とその親コンテナー (親コンテナーがない場合は画面) の上端間の距離です。

## <a name="related-functions"></a>関連する関数

[**Navigate**( *ScreenName*, *ScreenTransition* )](../functions/function-navigate.md)

## <a name="example"></a>例

1. 既定の **[スクリーン](control-screen.md)** コントロールに **Target** という名前を付け、 **[ラベル](control-text-box.md)** コントロールを追加して **Target** を表示するように **[Text](properties-core.md)** プロパティを設定します。

    [コントロールの追加および構成](../add-configure-controls.md)についてはこちらをご覧ください。

1. **[スクリーン](control-screen.md)** コントロールを追加し、**Source** という名前を付けます。

1. **Source** に **シェイプ** コントロールを追加し、 **[OnSelect](properties-core.md)** プロパティに次の式を設定します。

  `Navigate(Target, ScreenTransition.Fade)`
  
1. F5 キーを押すし、選択、**図形**コントロール。

    **[Target]\(ターゲット)** 画面が表示されます。

1. (省略可能) Esc キーを押して既定のワークスペースに戻り、**Target** に**シェイプ** コントロールを追加して、**シェイプ** コントロールの **[OnSelect](properties-core.md)** プロパティに次の式を設定します。

  `Navigate(Source, ScreenTransition.Fade)`

## <a name="accessibility-guidelines"></a>アクセシビリティのガイドライン

### <a name="color-contrast"></a>色のコントラスト

以下は、ボタンとして使用されるグラフィックまたは単なる装飾用ではないグラフィックにのみ適用されます。

アイコンの場合:
- **[Color](properties-color-border.md)** と **[Fill](properties-color-border.md)**
- その他の[標準の色のコントラスト要件](../accessible-apps-color.md)が適用されます (ボタンとして使用される場合)

境界線のある図形の場合:
- **[BorderColor](properties-color-border.md)** およびコントロールの外部の色
- **[FocusedBorderColor](properties-color-border.md)** およびコントロールの外部の色 (ボタンとして使用される場合)

境界線のない図形の場合:
- **[Fill](properties-color-border.md)** およびコントロールの外部の色
- **[PressedFill](properties-color-border.md)** およびコントロールの外部の色 (ボタンとして使用される場合)
- **[HoverFill](properties-color-border.md)** およびコントロールの外部の色 (ボタンとして使用される場合)

### <a name="screen-reader-support"></a>スクリーン リーダーのサポート
- **[AccessibleLabel](properties-accessibility.md)** グラフィックがボタンとして使用または装飾用だけでなくそれ以外の場合は、空でない文字列に設定する必要があります。

- **[AccessibleLabel](properties-accessibility.md)** 空または空の文字列にする必要があります **""** グラフィックが冗長な情報を提供します。 または、純粋に装飾用である場合。 この値は、スクリーン リーダーでグラフィックが無視するとします。

たとえば、設定することがあります、 **[AccessibleLabel](properties-accessibility.md)** のプロパティを**設定**アイコン**設定**します。 このアイコンは、ボタンとして使用されません。 横に、 **[ラベル](control-text-box.md)** もという**設定**します。 アイコンとラベルとしての両方にスクリーン リーダーは読み取り**設定**、不必要に冗長であります。 この場合、アイコンが不要、  **[AccessibleLabel](properties-accessibility.md)** します。

> [!IMPORTANT]
> スクリーン リーダーは読み取りアイコンまたは図形として**ボタン**場合その **[AccessibleLabel](properties-accessibility.md)** が空の文字列に設定し、その **[TabIndex](properties-accessibility.md)** 0 以上に設定します。 このようなアイコンまたは図形は、ボタンとしてレンダリングされます。 

### <a name="keyboard-support"></a>キーボードのサポート
- **[TabIndex](properties-accessibility.md)**  0 にする必要があります以上グラフィックがボタンとして使用される場合。 アイコンまたは図形には、この値を設定する場合は、キーボード ユーザーに移動できます。

- フォーカス インジケーターは、グラフィックがボタンとして使用される場合は、わかりやすく表示する必要があります。 使用 **[FocusedBorderColor](properties-color-border.md)** と **[FocusedBorderThickness](properties-color-border.md)** この結果を実現するためにします。

    > [!NOTE]
    > **[TabIndex](properties-accessibility.md)** が 0 以上の場合、アイコンまたは図形はボタンとしてレンダリングされます。 外観は変更されませんが、スクリーン リーダーはイメージをボタンとして正しく識別します。 **[TabIndex](properties-accessibility.md)** が 0 未満の場合、アイコンまたは図形はイメージとして識別されます。

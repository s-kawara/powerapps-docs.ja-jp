---
title: 'スクリーン コントロール: リファレンス | Microsoft Docs'
description: 各種プロパティとサンプルを含む画面コントロールに関する情報
author: emcoope-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 09/14/2019
ms.author: emcoope
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: dceb9eee8eb5a0ed11a4b44fb2df6d63ba5e9cae
ms.sourcegitcommit: 5899d37e38ed7111d5a9d9f3561449782702a5e9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/17/2019
ms.locfileid: "71038250"
---
# <a name="screen-control-in-powerapps"></a>PowerApps の画面コントロール

アプリ内で 1 つまたは複数の他のコントロールを含む UI 要素。

## <a name="description"></a>説明

ほとんどのアプリには、 **[ラベル](control-text-box.md)** コントロールや **[ボタン](control-button.md)** コントロールのほか、データを表示したりナビゲーションをサポートしたりするその他のコントロールを含む複数の **画面**コントロールがあります。 画面を追加する方法、画面の順序を変更する方法、およびナビゲーションを構成する方法の詳細については、「[画面の追加](../add-screen-context-variables.md)」を参照してください。

## <a name="key-properties"></a>主要なプロパティ

**[BackgroundImage](properties-visual.md)** – 画面の背景に表示される画像ファイルの名前です。

**[Fill](properties-color-border.md)** – コントロールの背景色です。

## <a name="additional-properties"></a>その他のプロパティ

**Height** -画面の高さ。 アプリの応答**性が高く**、アプリが実行されているデバイスがこのプロパティより短い場合は、画面を垂直[**方向にスクロール**](../set-aspect-ratio-portrait-landscape.md#change-screen-size-and-orientation)できます。

**[ImagePosition](properties-visual.md)** – 画面またはコントロールのサイズが画像と異なる場合の、画面またはコントロール内の画像の位置です (**Fill** (フィル)、**Fit** (サイズに合わせる)、**Stretch** (伸ばす)、**Tile** (タイル表示)、または **Center** (中央に表示))。

**[名前]** -画面の名前。

**OnHidden** – ユーザーがある画面から離れたときのアプリの動作。

**OnVisible** – ユーザーが画面に移動したときのアプリの動作。  このプロパティを使用して、画面で使用される変数およびプリロードデータを設定します。  アプリの起動時に1回設定する場合は、 [**app.config**](../functions/object-app.md#onstart-property)プロパティを使用します。

**Orientation** -画面の向き。 **幅**が**高さ**よりも大きい場合、向きはレイアウトになり**ます。横方向**;それ以外の場合は、 **Layout. Vertical**となります。

**Size** -画面のサイズを分類する正の整数。 分類を決定するには、画面の **[幅]** プロパティを "[**アプリのサイズ**](../functions/signals.md)" プロパティの値と比較します。 **ScreenSize**型は、1 ~ 4 の整数に対応する4つの値 (**Small**、 **Medium**、 **Large**、 **ExtraLarge**) で構成されます。

**Width** -画面の幅。 アプリの応答**性が高く**、アプリが実行されているデバイスがこのプロパティよりも狭い場合は、画面を水平[**方向にスクロール**](../set-aspect-ratio-portrait-landscape.md#change-screen-size-and-orientation)できます。

## <a name="related-functions"></a>関連する関数

[**Distinct**( *DataSource*, *ColumnName* )](../functions/function-distinct.md)

## <a name="example"></a>例

1. **[ラジオ](control-radio.md)** コントロールを追加して **ScreenFills** という名前を付け、その **[Items](properties-core.md)** プロパティを次の値に設定します。

    `["Red", "Green"]`

    [コントロールの追加、命名、構成についてはこちらをご覧ください](../add-configure-controls.md)。

1. 既定の**画面**コントロールに**Source** という名前を付け、別の**画面**コントロールを追加して **Target** という名前を付けます。

1. **[ソース]** で、 **[シェイプ](control-shapes-icons.md)** コントロール (矢印など) を追加し、その **[onselect](properties-core.md)** プロパティを次の数式に設定します。

    `Navigate(Target, ScreenTransition.Fade)`

    **[Navigate](../functions/function-navigate.md)** 関数または[その他の関数](../formula-reference.md)については各関連記事を参照してください。

1. **Target** に **[シェイプ](control-shapes-icons.md)** コントロール (矢印など) を追加し、その **[OnSelect](properties-core.md)** プロパティを次の数式に設定します。

    `Navigate(Source, ScreenTransition.Fade)`

1. **Target** の **[Fill](properties-color-border.md)** プロパティを次の数式に設定します。

    `If("Red" in ScreenFills.Selected.Value, RGBA(255, 0, 0, 1), RGBA(54, 176, 75, 1))`

1. **ソース**画面を選択し、Alt キーを押したまま、 **[ラジオ](control-radio.md)** コントロールのいずれかのオプションを選択してから、 **[シェイプ](control-shapes-icons.md)** コントロールを選択します。

    **ターゲット**は選択した色で表示されます。

1. **[ターゲット]** で、**ソース**に戻る **[図形](control-shapes-icons.md)** コントロールを選択します。

1. optional **[ラジオ](control-radio.md)** コントロールの [その他] オプションを選択し、 **[図形](control-shapes-icons.md)** コントロールを選択して、**ターゲット**がもう一方の色で表示されることを確認します。

1. optional左側のナビゲーションバーで **[ターゲット]** をポイントし、表示される省略記号を選択して **[上へ移動]** を選択して、画面の順序を変更します。

    **ターゲット**は、ユーザーがアプリを開いたときに最初に表示されます。

## <a name="accessibility-guidelines"></a>アクセシビリティのガイドライン

### <a name="color-contrast"></a>色のコントラスト

**スクリーン**がテキストの実質的な背景である場合、以下の間には適切な色のコントラストが必要です。

- **[Fill](properties-color-border.md)** とテキスト
- **[BackgroundImage](properties-visual.md)** とテキスト (該当する場合)

たとえば、 **スクリーン**に **[ラベル](control-text-box.md)** があり、ラベルの塗りつぶしが透明な場合、カードの **[Fill](properties-color-border.md)** は実質的にはラベルの背景色になります。

また、テキストに加えて、 **[評価](control-rating.md)** コントロールの星のイメージのような重要なグラフィック オブジェクトとの色のコントラストも確認してください。

### <a name="screen-reader-support"></a>スクリーン リーダーのサポート

- 各**スクリーン**には意味のある名前を付ける必要があります。 スクリーン名は、他のコントロールと同様に、コントロール ウィンドウのツリー ビューまたはプロパティ ウィンドウのヘッダーで表示および編集できます。

    > [!NOTE]
  > 新しい**スクリーン**が読み込まれると、スクリーン リーダーでその名前が通知されます。

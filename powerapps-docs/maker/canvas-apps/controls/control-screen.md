---
title: 'スクリーン コントロール: リファレンス | Microsoft Docs'
description: 各種プロパティとサンプルを含む画面コントロールに関する情報
author: emcoope-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 10/25/2016
ms.author: emcoope
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 6fedff6d6ffc34fe390ec6978672d699480a7cb9
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61548733"
---
# <a name="screen-control-in-powerapps"></a>PowerApps の画面コントロール

アプリ内で 1 つまたは複数の他のコントロールを含む UI 要素。

## <a name="description"></a>説明

ほとんどのアプリには、 **[ラベル](control-text-box.md)** コントロールや **[ボタン](control-button.md)** コントロールのほか、データを表示したりナビゲーションをサポートしたりするその他のコントロールを含む複数の **画面**コントロールがあります。 画面を追加し、画面の順序を変更、ナビゲーションを構成する方法については、確認[画面を追加する](../add-screen-context-variables.md)します。

## <a name="key-properties"></a>主要なプロパティ

**[BackgroundImage](properties-visual.md)** – 画面の背景に表示される画像ファイルの名前です。

**[Fill](properties-color-border.md)** – コントロールの背景色です。

## <a name="additional-properties"></a>その他のプロパティ

**高さ**-画面の高さ。 アプリが応答する場合 ([**に合わせてスケール**](../set-aspect-ratio-portrait-landscape.md#change-screen-size-and-orientation)は**オフ**) と、アプリが実行されているデバイスがこのプロパティよりも短い、画面が垂直方向にスクロールすることができます。

**[ImagePosition](properties-visual.md)** – 画面またはコントロールのサイズが画像と異なる場合の、画面またはコントロール内の画像の位置です (**Fill** (フィル)、**Fit** (サイズに合わせる)、**Stretch** (伸ばす)、**Tile** (タイル表示)、または **Center** (中央に表示))。

**名前**-画面の名前。

**OnHidden** – ユーザーがある画面から離れたときのアプリの動作。

**OnStart** – ユーザーがアプリを開くときのアプリの動作です。

- このプロパティで設定した数式は、アプリの最初の画面が表示される前に実行されます。 アプリ開始時にどの画面が最初に表示されるかを変更するには、[**Navigate**](../functions/function-navigate.md) 関数を呼び出します。
- [**UpdateContext**](../functions/function-updatecontext.md) 関数で[コンテキスト変数](../working-with-variables.md)を設定することはできません (どの画面もまだ表示されていないため)。 ただし、**Navigate** 関数でコンテキスト変数を渡し、[**Collect**](../functions/function-clear-collect-clearcollect.md) 関数を使用して[コレクション](../working-with-variables.md)を作成し、そのコレクションに入力することができます。
- アプリを更新する場合、このプロパティで設定した数式は、アプリが PowerApps Studio に読み込まれるときに実行されます。 このプロパティ変更の影響を確認するには、アプリを保存して閉じ、再読み込みする必要があります。
- **OnStart** プロパティは、実際には画面ではなくアプリのプロパティです。 編集の便宜を考慮して、このプロパティをアプリの最初の画面のプロパティとして表示し、変更します。 最初の画面を削除したか、画面の順序を変更したために、このプロパティを見つけられなくなることがあります。 その場合は、アプリを保存して閉じ、再読み込みすると、最初の画面のプロパティとして表示されます。

**OnVisible** – ユーザーが画面に移動したときのアプリの動作。

**印刷の向き**-画面の向き。 場合その**幅**がより大きい、**高さ**、印刷の向きになります**Layout.Horizontal**、それ以外のことが**Layout.Vertical**.

**サイズ**-画面のサイズを分類する正の整数。 分類は、画面を比較することによって決まります**幅**プロパティの値を[ **App.SizeBreakpoints** ](../functions/signals.md)プロパティ。 **する**型は、4 つの値で構成されています (**小さな**、 **Medium**、 **Large**、および**ExtraLarge**) 整数 1 ~ 4 に対応しています。

**幅**-画面の幅。 アプリが応答する場合 ([**に合わせてスケール**](../set-aspect-ratio-portrait-landscape.md#change-screen-size-and-orientation)は**オフ**) と、アプリが実行されているデバイスがこのプロパティよりも幅の狭い、画面が水平方向にスクロールすることができます。

## <a name="related-functions"></a>関連する関数

[**Distinct**( *DataSource*, *ColumnName* )](../functions/function-distinct.md)

## <a name="example"></a>例

1. **[ラジオ](control-radio.md)** コントロールを追加して **ScreenFills** という名前を付け、その **[Items](properties-core.md)** プロパティを次の値に設定します。

    `["Red", "Green"]`

    [コントロールの追加、命名、構成についてはこちらをご覧ください](../add-configure-controls.md)。

1. 既定の**画面**コントロールに**Source** という名前を付け、別の**画面**コントロールを追加して **Target** という名前を付けます。

1. **ソース**、追加、 **[図形](control-shapes-icons.md)** (矢印) などを制御し、設定、 **[OnSelect](properties-core.md)** プロパティをこの数式では:

    `Navigate(Target, ScreenTransition.Fade)`

    **[Navigate](../functions/function-navigate.md)** 関数または[その他の関数](../formula-reference.md)については各関連記事を参照してください。

1. **Target** に **[シェイプ](control-shapes-icons.md)** コントロール (矢印など) を追加し、その **[OnSelect](properties-core.md)** プロパティを次の数式に設定します。

    `Navigate(Source, ScreenTransition.Fade)`

1. **Target** の **[Fill](properties-color-border.md)** プロパティを次の数式に設定します。

    `If("Red" in ScreenFills.Selected.Value, RGBA(255, 0, 0, 1), RGBA(54, 176, 75, 1))`

1. 選択、**ソース**画面し、Alt キーを押したまま、いずれかのオプションを選択、 **[ラジオ](control-radio.md)** コントロールを選び、  **[図形](control-shapes-icons.md)** コントロール。

    **ターゲット**選択した色で表示されます。

1. **ターゲット**を選択、 **[図形](control-shapes-icons.md)** に返すときに**ソース**します。

1. (省略可能)他のオプションを選択、 **[ラジオ](control-radio.md)** コントロールを選び、 **[図形](control-shapes-icons.md)** ことを確認するコントロール**ターゲット**他の色で表示されます。

1. (省略可能)ポインターを合わせると、画面の順序を変更**ターゲット**左側のナビゲーション バーが表示されたら、省略記号を選択すると、および選択し、**上へ移動**します。

    **ターゲット**最初に、ユーザーがアプリを開くときに表示されます。

## <a name="accessibility-guidelines"></a>アクセシビリティのガイドライン

### <a name="color-contrast"></a>色のコントラスト

**スクリーン**がテキストの実質的な背景である場合、以下の間には適切な色のコントラストが必要です。

- **[Fill](properties-color-border.md)** とテキスト
- **[BackgroundImage](properties-visual.md)** とテキスト (該当する場合)

たとえば、 **スクリーン**に **[ラベル](control-text-box.md)** があり、ラベルの塗りつぶしが透明な場合、カードの **[Fill](properties-color-border.md)** は実質的にはラベルの背景色になります。

また、テキストに加えて、**[評価](control-rating.md)** コントロールの星のイメージのような重要なグラフィック オブジェクトとの色のコントラストも確認してください。

### <a name="screen-reader-support"></a>スクリーン リーダーのサポート

- 各**スクリーン**には意味のある名前を付ける必要があります。 スクリーン名は、他のコントロールと同様に、コントロール ウィンドウのツリー ビューまたはプロパティ ウィンドウのヘッダーで表示および編集できます。

    > [!NOTE]
  > 新しい**スクリーン**が読み込まれると、スクリーン リーダーでその名前が通知されます。

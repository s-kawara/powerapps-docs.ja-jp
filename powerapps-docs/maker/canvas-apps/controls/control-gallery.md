---
title: 'ギャラリー コントロール: リファレンス | Microsoft Docs'
description: 各種プロパティとサンプルを含むギャラリー コントロールに関する情報
documentationcenter: na
author: fikaradz
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: reference
ms.component: canvas
ms.date: 05/25/2017
ms.author: sharik
ms.openlocfilehash: fcb482844e430444fd95bb2d0c85a8da23c91d84
ms.sourcegitcommit: 79b8842fb0f766a0476dae9a537a342c8d81d3b3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2018
ms.locfileid: "37897733"
---
# <a name="gallery-control-in-powerapps"></a>PowerApps のギャラリー コントロール
その他のコントロールが含まれており、一連のデータを表示するコントロールです。

## <a name="description"></a>説明
**ギャラリー** コントロールを使用して、データ ソースの複数のレコードを表示できます。各レコードには、複数の種類のデータを含めることができます。 たとえば、**ギャラリー** コントロールで、名前、住所、電話番号などの項目を含む連絡先情報を複数表示することができます。 各データ フィールドは**ギャラリー** コントロール内に別個のコントロールとして表示され、テンプレートでそれらのコントロールを構成できます。 テンプレートは、水平/ランドスケープ方向の場合は**ギャラリー** コントロールの左端にギャラリー内の最初の項目として表示され、垂直/ポートレート方向の場合は**ギャラリー** コントロールの最上部に表示されます。 テンプレートで行った変更は、**ギャラリー** コントロール全体に反映されます。

イメージ、テキスト、および高さが可変の項目を含むギャラリーを表示するための定義済みのギャラリー テンプレートを利用できます。

## <a name="key-properties"></a>主要なプロパティ
**[Default](properties-core.md)** – アプリの起動時に、ギャラリーで選択されるデータ ソースからの項目またはレコードです。

**[Items](properties-core.md)** – ギャラリー、リスト、グラフなどのコントロールに表示されるデータのソースです。

**Selected** – 選択された項目です。

## <a name="additional-properties"></a>その他のプロパティ
**[AccessibleLabel](properties-accessibility.md)** – スクリーン リーダー用のラベルです。 項目の一覧の内容を説明する必要があります。

**AllItems** – ギャラリーのテンプレートの一部である追加のコントロール値を含む、ギャラリーのすべての項目です。

**[BorderColor](properties-color-border.md)** – コントロールの境界線の色です。

**[BorderStyle](properties-color-border.md)** – コントロールの境界線を **Solid** (実線)、**Dashed** (破線)、**Dotted** (点線)、**None** (なし) のいずれに指定します。

**[BorderThickness](properties-color-border.md)** – コントロールの境界線の太さです。

**[DisplayMode](properties-core.md)** – コントロールで、ユーザー入力を許可するか (**Edit**)、データの表示のみを許可するか (**View**)、許可しないか (**Disabled**) を設定します。

**[Fill](properties-color-border.md)** – コントロールの背景色です。

**[Height](properties-size-location.md)** – コントロールの上端と下端の距離です。

**Layout** – ユーザーがギャラリーをスクロールしたりスライダーを調整したりする方向です。上下 (**Vertical**) または左右 (**Horizontal**) から選択します。

**NavigationStep** – **ShowNavigation** プロパティが **true** に設定されている場合、ギャラリーの端にあるナビゲーション矢印の選択操作でギャラリーをどの程度スクロールするかを指定します。

**ShowNavigation** – ギャラリーの両端に矢印を表示し、それらの矢印のクリックまたはタップでギャラリー内の項目をユーザーがスクロールできるようにするかどうかを指定します。

**ShowScrollbar** – ユーザーがポインタをギャラリーに合わせたときにスクロール バーを表示するかどうかを指定します。

**Snap** – ユーザーがギャラリーをスクロールするとき、次の項目が完全に表示されるように自動的にスナップするかどうかを指定します。

**TemplateFill** – ギャラリーの背景色です。

**TemplatePadding** – ギャラリー内の項目間の距離です。

**TemplateSize** – 垂直/ポートレート方向のギャラリー向けのテンプレートの高さ、または水平/ランドスケープ方向のギャラリー向けのテンプレートの幅です。

**Transition** – ユーザーがポインタをギャラリー内の項目に合わせたときの視覚効果 (**ポップ**、**プッシュ**、または **None**) を指定します。

**[Visible](properties-core.md)** – コントロールを表示するか非表示にするかを指定します。

**[Width](properties-size-location.md)** – コントロールの左端と右端の間の距離です。

**WrapCount** – 水平または垂直レイアウトに合わせて行または列ごとに表示される項目の数です。

**[X](properties-size-location.md)** – コントロールの左端とその親コンテナー (親コンテナーがない場合は画面) の左端間の距離です。

**[Y](properties-size-location.md)** – コントロールの上端とその親コンテナー (親コンテナーがない場合は画面) の上端間の距離です。

## <a name="related-functions"></a>関連する関数
[**Filter**( *DataSource*, *Formula* )](../functions/function-filter-lookup.md)

## <a name="examples"></a>例
### <a name="show-and-filter-data"></a>データを表示およびフィルター処理する
* [テキストを表示します](control-text-box.md#show-data-in-a-gallery)
* [イメージを表示します](control-image.md#show-a-set-of-images-from-a-data-source)
* [リスト オプションを選択してデータをフィルター処理します](control-drop-down.md#example)
* [スライダーを調整してデータをフィルター処理します](control-slider.md#example)

### <a name="get-data-from-the-user"></a>ユーザーからデータを取得する
* [テキストを取得します](control-text-input.md#collect-data)
* [イメージを取得します](control-add-picture.md#add-images-to-an-image-gallery-control)
* [写真を取得します](control-camera.md#example)
* [サウンドを取得します](control-microphone.md#example)
* [図面を取得します](control-pen-input.md#create-a-set-of-images)


## <a name="accessibility-guidelines"></a>アクセシビリティのガイドライン
### <a name="color-contrast"></a>色のコントラスト
ギャラリー項目内のどこかをクリックすると、その項目が選択される場合、以下の間に適切な色のコントラストが必要です。
* **[BorderColor](properties-color-border.md)** とギャラリーの外側の色 (境界線がある場合)
* **[Fill](properties-color-border.md)** とギャラリーの外側の色 (境界線がない場合)

### <a name="screen-reader-support"></a>スクリーン リーダーのサポート
* **[AccessibleLabel](properties-accessibility.md)** が存在する必要があります。

    > [!NOTE]
  > ギャラリー内の項目が変更されると、スクリーン リーダーから通知されます。 **AccessibleLabel** についても通知されます。 これによって通知のコンテキストがわかるので、同じスクリーン上に複数のギャラリーがある場合にはさらに重要です。

### <a name="keyboard-support"></a>キーボードのサポート
* **ShowScrollbar** を **true** に設定することを検討してください。 ほとんどのタッチ スクリーン デバイスでは、スクロールが始まるまでスクロール バーは表示されません。
* ギャラリー項目内のどこかをクリックすると、その項目が選択される場合、キーボード ユーザーがギャラリー項目を選択できる方法も必要です。 たとえば、**OnSelect** プロパティが **Select(Parent)** に設定されている**[ボタン](control-button.md)** を追加するとします。

    > [!NOTE]
  > ギャラリーの外部のコントロールは、ギャラリー内のキーボード ナビゲーション順では考慮されません。 ギャラリー内のコントロールの **[TabIndex](properties-accessibility.md)** は対象になります。 詳細については、[アクセシビリティのプロパティ](properties-accessibility.md)に関するページを参照してください。

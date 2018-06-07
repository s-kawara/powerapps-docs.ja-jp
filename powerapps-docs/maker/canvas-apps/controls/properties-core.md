---
title: コアのプロパティ | Microsoft Docs
description: Disabled、Visible、および ReadOnly プロパティに関する参照情報
documentationcenter: na
author: gregli-msft
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: reference
ms.component: canvas
ms.date: 10/25/2016
ms.author: gregli
ms.openlocfilehash: 9631d197824b516f90d493c9db4aee75f3f7ce0d
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "31837351"
---
# <a name="core-properties-in-powerapps"></a>PowerApps のコアのプロパティ
ユーザーがコントロールを見て操作できるかどうかを構成します。

### <a name="properties"></a>プロパティ
**Default** – ユーザーが変更する前のコントロールの初期値です。

* **[カード](control-card.md)**、**[チェック ボックス](control-check-box.md)**、**[ドロップ ダウン](control-drop-down.md)**、**[ギャラリー](control-gallery.md)**、**[リスト ボックス](control-list-box.md)**、**[ラジオ](control-radio.md)**、**[評価](control-rating.md)**、**[スライダー](control-slider.md)**、**[テキスト入力](control-text-input.md)**、および**[トグル](control-toggle.md)** の各コントロールに適用されます。

**DelayOutput** – テキスト入力時に操作を遅延させる場合は true に設定します。

* **[テキスト入力](control-text-input.md)** コントロールと**[カード](control-card.md)** コントロールに適用されます。

**DisplayMode** – 値は **Edit、View**、**Disabled** のいずれかになります。 コントロールで、ユーザー入力を許可するか (**Edit**)、データの表示のみを許可するか (**View**)、許可しないか (**Disabled**) を構成します。  **View** モードでは、**[テキスト入力](control-text-input.md)**、**[ドロップ ダウン](control-drop-down.md)**、**[日付の選択](control-date-picker.md)** などの入力コントロールでテキスト値のみが表示され、対話型要素や装飾は表示されません。  これにより、フォームでの表示に適した値、または読み取り可能な出力になります。

* **[画像の追加](control-add-picture.md)**、**[オーディオ](control-audio-video.md)**、**[ボタン](control-button.md)**、**[カメラ](control-camera.md)**、**[チェック ボックス](control-check-box.md)**、**[縦棒グラフ](control-column-line-chart.md)**、**[日付の選択](control-date-picker.md)**、**[ドロップ ダウン](control-drop-down.md)**、**[エクスポート](control-export-import.md)**、**[ギャラリー](control-gallery.md)**、**[HTML テキスト](control-html-text.md)**、**[アイコン](control-shapes-icons.md)**、**[イメージ](control-image.md)**、**[インポート](control-export-import.md)**、**[ラベル](control-text-box.md)**、**[折れ線グラフ](control-column-line-chart.md)**、**[リスト ボックス](control-list-box.md)**、**[マイク](control-microphone.md)**、**[PDF ビューアー](control-pdf-viewer.md)**、**[ペン入力](control-pen-input.md)**、**[円グラフ](control-pie-chart.md)**、**[ラジオ](control-radio.md)**、**[評価](control-rating.md)**、**[シェイプ](control-shapes-icons.md)**、**[スライダー](control-slider.md)**、**[テキスト入力](control-text-input.md)**、**[タイマー](control-timer.md)**、**[トグル](control-toggle.md)**、および**[ビデオ](control-audio-video.md)** の各コントロールに適用されます。

**Items** – ギャラリー、リスト、グラフなどのコントロールに表示されるデータのソースです。

* **[縦棒グラフ](control-column-line-chart.md)**、**[ドロップ ダウン](control-drop-down.md)**、**[ギャラリー](control-gallery.md)**、**[折れ線グラフ](control-column-line-chart.md)**、**[リスト ボックス](control-list-box.md)**、**[円グラフ](control-pie-chart.md)**、および**[ラジオ](control-radio.md)** の各コントロールに適用されます。

**OnChange** – ユーザーが (スライダーを調整するなどして) コントロールの値を変更した場合のアプリの反応を指定します。

* **[画像の追加](control-add-picture.md)**、**[ドロップ ダウン](control-drop-down.md)**、**[リスト ボックス](control-list-box.md)**、**[ラジオ](control-radio.md)**、**[評価](control-rating.md)**、**[スライダー](control-slider.md)**、**[テキスト入力](control-text-input.md)**、および**[トグル](control-toggle.md)** の各コントロールに適用されます。

**OnSelect** – ユーザーがコントロールをタップまたはクリックした場合のアプリの反応を指定します。

* **[画像の追加](control-add-picture.md)**、**[ボタン](control-button.md)**、**[カメラ](control-camera.md)**、**[チェック ボックス](control-check-box.md)**、**[縦棒グラフ](control-column-line-chart.md)**、**[日付の選択](control-date-picker.md)**、**[ドロップ ダウン](control-drop-down.md)**、**[エクスポート](control-export-import.md)**、**[HTML テキスト](control-html-text.md)**、**[アイコン](control-shapes-icons.md)**、**[イメージ](control-image.md)**、**[インポート](control-export-import.md)**、**[ラベル](control-text-box.md)**、**[折れ線グラフ](control-column-line-chart.md)**、**[リスト ボックス](control-list-box.md)**、**[マイク](control-microphone.md)**、**[PDF ビューアー](control-pdf-viewer.md)**、**[ペン入力](control-pen-input.md)**、**[円グラフ](control-pie-chart.md)**、**[ラジオ](control-radio.md)**、**[評価](control-rating.md)**、**[シェイプ](control-shapes-icons.md)**、**[スライダー](control-slider.md)**、**[テキスト入力](control-text-input.md)**、**[タイマー](control-timer.md)**、および**[トグル](control-toggle.md)** の各コントロールに適用されます。

**Reset** – コントロールを既定値に戻すかどうかを指定します。  **[Reset](../functions/function-reset.md)** 関数に関する記事もご覧ください。

* **[オーディオ](control-audio-video.md)**、**[チェック ボックス](control-check-box.md)**、**[ドロップ ダウン](control-drop-down.md)**、**[リスト ボックス](control-list-box.md)**、**[マイク](control-microphone.md)**、**[ラジオ](control-radio.md)**、**[評価](control-rating.md)**、**[スライダー](control-slider.md)**、**[テキスト入力](control-text-input.md)**、**[タイマー](control-timer.md)**、**[トグル](control-toggle.md)**、および**[ビデオ](control-audio-video.md)** の各コントロールに適用されます。

**Text** – コントロールに表示されるテキスト、またはコントロールにユーザーが入力するテキストです。

* **[画像の追加](control-add-picture.md)**、**[ボタン](control-button.md)**、**[エクスポート](control-check-box.md)**、**[インポート](control-export-import.md)**、**[ラジオ](control-export-import.md)**、**[ラベル](control-text-box.md)**、**[テキスト入力](control-text-input.md)**、**[タイマー](control-timer.md)** の各コントロールに適用されます。

**Tooltip** – ポインターをコントロールに合わせたときに表示される説明テキストです。

* **[オーディオ](control-audio-video.md)**、**[ボタン](control-button.md)**、**[カメラ](control-camera.md)****[チェック ボックス](control-check-box.md)**、**[ドロップ ダウン](control-drop-down.md)**、**[HTML テキスト](control-html-text.md)**、**[イメージ](control-image.md)**、**[ラベル](control-text-box.md)**、**[リスト ボックス](control-list-box.md)**、**[マイク](control-microphone.md)**、**[PDF ビューアー](control-pdf-viewer.md)**、**[ペン入力](control-pen-input.md)**、**[ラジオ](control-radio.md)**、**[評価](control-rating.md)**、**[スライダー](control-slider.md)**、**[テキスト入力](control-text-input.md)**、**[タイマー](control-timer.md)**、**[トグル](control-toggle.md)**、および**[ビデオ](control-audio-video.md)** の各コントロールに適用されます。

**Value** – 入力コントロールの値です。

* **[チェック ボックス](control-check-box.md)**、**[ラジオ](control-radio.md)**、**[スライダー](control-slider.md)**、および**[トグル](control-toggle.md)** の各コントロールに適用されます。

**Visible** – コントロールを表示するか非表示にするかを指定します。

* **[画像の追加](control-add-picture.md)**、**[オーディオ](control-audio-video.md)**、**[ボタン](control-button.md)**、**[カメラ](control-camera.md)**、**[カード](control-card.md)**、**[チェック ボックス](control-check-box.md)**、**[縦棒グラフ](control-column-line-chart.md)**、**[日付の選択](control-date-picker.md)**、**[表示フォーム](control-form-detail.md)**、**[ドロップ ダウン](control-drop-down.md)**、**[編集フォーム](control-form-detail.md)**、**[エクスポート](control-export-import.md)**、**[ギャラリー](control-gallery.md)**、**[HTML テキスト](control-html-text.md)**、**[アイコン](control-shapes-icons.md)**、**[イメージ](control-image.md)**、**[インポート](control-export-import.md)**、**[ラベル](control-text-box.md)**、**[折れ線グラフ](control-column-line-chart.md)**、**[リスト ボックス](control-list-box.md)**、**[マイク](control-microphone.md)**、**[PDF ビューアー](control-pdf-viewer.md)**、**[ペン入力](control-pen-input.md)**、**[円グラフ](control-pie-chart.md)**、**[ラジオ](control-radio.md)**、**[評価](control-rating.md)**、**[シェイプ](control-shapes-icons.md)**、**[スライダー](control-slider.md)**、**[テキスト入力](control-text-input.md)**、**[タイマー](control-timer.md)**、**[トグル](control-toggle.md)**、および**[ビデオ](control-audio-video.md)** の各コントロールに適用されます。


---
title: プロパティの検索 | Microsoft Docs
description: コントロールやカテゴリ別に、またはアルファベット順にプロパティを検索します。
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 03/17/2016
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 6c69d32f21bb5d1222122c4ec129d765b390d98f
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "42863127"
---
# <a name="controls-and-properties-in-powerapps"></a>PowerApps のコントロールとプロパティ
プロパティのいずれかを設定して、コントロールの見た目と動作を構成します。 コントロールの種類ごとに、さまざまなプロパティのセットがあります。 一部のプロパティ (**Height** や **Width** など) はほぼすべての種類のコントロールで共通ですが、他のプロパティ (**CheckboxSize** など) は、コントロールの 1 つの種類に固有のものです。

## <a name="controls"></a>コントロール
**[画像の追加](controls/control-add-picture.md)** – データ ソースへのアップロードのために、ローカル デバイスから画像を読み込みます。

**[添付ファイル](controls/control-attachments.md)** – ローカルのデバイスからデータ ソースにファイルをダウンロードおよびアップロードします。

**[オーディオ](controls/control-audio-video.md)** – オーディオ クリップまたはビデオ クリップのオーディオ部分を再生します。

**[バーコード スキャナー (試験段階)](controls/control-barcodescanner.md)** – カメラを備えたデバイスを使用して、バーコードをスキャンします。

**[ボタン](controls/control-button.md)** – クリックまたはタップしてアプリを操作します。

**[カメラ](controls/control-camera.md)** – 写真を撮り、アプリまたはデータ ソースに写真を保存します。

**[カード](controls/control-card.md)** – **[フォームの編集](controls/control-form-detail.md)** コントロールや**[フォームの表示](controls/control-form-detail.md)** コントロール内のレコードの個々のフィールドを表示したり編集したりします。

**[チェック ボックス](controls/control-check-box.md)** – オプションを選択または選択解除して、**true** または **false** を指定します。

**[縦棒グラフ](controls/control-column-line-chart.md)** – 2 つの軸に対して相対的に垂直のバーの値を表示します。

**[列](controls/control-column.md)** - [**データ テーブル**](controls/control-data-table.md) コントロールの単一フィールドに表示エクスペリエンスを指定します。

**[コンボ ボックス](controls/control-combo-box.md)** - 提示された選択肢からユーザーが選択できるようにします。 検索と複数選択をサポートしています。

**[データ テーブル](controls/control-data-table.md)** – 表形式でデータを表示します。

**[日付の選択](controls/control-date-picker.md)** – クリックまたはタップして日付を指定します。

**[フォームの表示](controls/control-form-detail.md)** – フォームを使用してデータ ソースのレコードを表示します。

**[ドロップ ダウン](controls/control-drop-down.md)** – 下向き矢印が選択されるまで、リストの最初の項目を表示します。

**[フォームの編集](controls/control-form-detail.md)** – フォームを使用してデータ ソースのレコードを編集および作成します。

**[エンティティ フォーム](entity-form-control.md)** - 試験的機能: ユーザーが Common Data Service からリレーショナル データを表示、移動、編集できる動的フォームを追加します。

**[エクスポート](controls/control-export-import.md)** – PowerApps の他の場所で使用するためにデータをエクスポートします。

**[ギャラリー](controls/control-gallery.md)**  – 複数の種類のデータを含めることができるレコードの一覧を表示します。

**[HTML テキスト](controls/control-html-text.md)** – HTML タグを自動的に変換します。

**[アイコン](controls/control-shapes-icons.md)** – グラフィックをより魅力あるものにして、視覚的な効果を追加します。

**[イメージ](controls/control-image.md)** – ローカル ファイルやデータ ソースなどの画像を表示します。

**[インポート](controls/control-export-import.md)** – PowerApps の別の場所からデータをインポートします。

**[縦棒グラフ](controls/control-column-line-chart.md)** – 2 つの軸に対して相対的にデータ ポイントの値を表示します。

**[リスト ボックス](controls/control-list-box.md)** – リストの項目を 1 つまたは複数選択します。

**[マイク](controls/control-microphone.md)** – サウンドを録音し、アプリまたはデータ ソースに保存します。

**[PDF ビューアー (試験段階)](controls/control-pdf-viewer.md)** – インターネット上の PDF ファイルの内容を表示します。

**[入力ペン](controls/control-pen-input.md)** – イメージやテキストを描画し、アプリケーションまたはデータ ソースに保存します。

**[円グラフ](controls/control-pie-chart.md)** – 相互の値を相対的に表示します。

**[Power BI タイル](controls/control-power-bi-tile.md)** – アプリ内で Power BI タイルを表示します。

**[ラジオ](controls/control-radio.md)** – 相互に排他的なオプションを表示します。

**[評価](controls/control-rating.md)** – 1 ～指定された数の値を示します。

**[リッチ テキスト エディター (試験段階)](controls/control-richtexteditor.md)** – アプリのユーザーがリッチ テキストを書式設定できるようにします。

**[画面](controls/control-screen.md)** – 特定のタスクに関するデータを表示および更新します。

**[図形](controls/control-shapes-icons.md)** – 矢印や幾何学的図形 (四角形など) を表示します。

**[スライダー](controls/control-slider.md)** – ハンドルをドラッグして値を指定します。

**[ラベル](controls/control-text-box.md)** – テキスト、数値、日付、通貨などのデータを表示します。

**[テキスト入力](controls/control-text-input.md)** – テキスト、数値、その他のデータを入力します。

**[タイマー](controls/control-timer.md)** – 一定時間が経過した後のアプリの反応を構成します。

**[トグル](controls/control-toggle.md)** – ハンドルをドラッグして、**true** または **false** を指定します。

**[ビデオ](controls/control-audio-video.md)** – ローカル ファイル、データ ソース、YouTube のビデオ クリップを再生します。

## <a name="common-properties-by-category"></a>カテゴリ別の共通プロパティ
**[Color and border](controls/properties-color-border.md)** – コントロールの色と境界線をユーザーが操作できるかどうかを構成します。

**[Core](controls/properties-core.md)** – ユーザーがコントロールを見て操作できるかどうかを構成します。

**[Image](controls/properties-visual.md)** – 表示する画像とコントロールを塗りつぶす方法を構成します。

**[Size and location](controls/properties-size-location.md)** – コントロール (またはコントロールの要素) の大きさと画面上の表示位置を構成します。

**[Text](controls/properties-text.md)** – コントロールでのテキストの表示方法 (フォントの特徴、配置、行の高さなど) を構成します。  

## <a name="all-properties"></a>すべてのプロパティ
### <a name="a"></a>A
**[ActualZoom](controls/control-pdf-viewer.md)** – コントロールの実際の拡大率です。**Zoom** プロパティで要求された拡大率と異なる場合があります。  **[PDF ビューアー](controls/control-pdf-viewer.md)** コントロールに適用されます。

**[Align](controls/properties-text.md)** – コントロールの水平方向の中心に対するテキストの位置です。  多くのコントロールに適用されます。

**[AllItems](controls/control-gallery.md)** – ギャラリーのテンプレートの一部である追加のコントロール値を含む、ギャラリーのすべての項目です。  **[ギャラリー](controls/control-gallery.md)** コントロールに適用されます。

**AutoDisableOnSelect** – OnSelect の動作の実行時にコントロールを自動で無効化するかどうかを指定します。  **[ボタン](controls/control-button.md)** コントロールと**[イメージ](controls/control-image.md)** コントロールに適用されます。

**[AutoHeight](controls/properties-size-location.md)** – **[Text](controls/properties-core.md)** プロパティの内容がコントロールで表示できる文字数を超えている場合に、自動的にラベルの高さを増やすかどうかを指定します。 **[ラベル](controls/control-text-box.md)** コントロールに適用されます。

**AutoPause** – ユーザーが別の画面に移動した場合、オーディオまたはビデオ クリップを自動的に一時停止するかどうかを指定します。  **[オーディオ](controls/control-audio-video.md)**、**[タイマー](controls/control-timer.md)**、および**[ビデオ](controls/control-audio-video.md)** の各コントロールに適用されます。

**AutoStart** – ユーザーがオーディオまたはビデオ コントロールを含む画面に移動したときに、自動的にクリップの再生を開始するかどうかを指定します。  **[オーディオ](controls/control-audio-video.md)**、**[タイマー](controls/control-timer.md)**、および**[ビデオ](controls/control-audio-video.md)** の各コントロールに適用されます。

### <a name="b"></a>B
**[BackgroundImage](controls/properties-visual.md)** – 画面の背景に表示される画像ファイルの名前です。  **[画面](controls/control-screen.md)** コントロールに適用されます。

**[BorderColor](controls/properties-color-border.md)** – コントロールの境界線の色です。  多くのコントロールに適用されます。

**[BorderStyle](controls/properties-color-border.md)** – コントロールの境界線を **Solid** (実線)、**Dashed** (破線)、**Dotted** (点線)、**None** (なし) のいずれに指定します。  多くのコントロールに適用されます。

**[BorderThickness](controls/properties-color-border.md)** – コントロールの境界線の太さです。  多くのコントロールに適用されます。

**[Brightness](controls/control-camera.md)** – ユーザーが画像で認識する可能性のある光の量を指定します。  **[カメラ](controls/control-camera.md)** コントロールに適用されます。

### <a name="c"></a>C
**[CalculateOriginalDimensions](controls/control-image.md)** – **[OriginalHeight](controls/control-image.md)** プロパティと **[OriginalWidth](controls/control-image.md)** プロパティを有効にします。  **[イメージ](controls/control-image.md)** コントロールに適用されます。

**[Camera](controls/control-camera.md)** – 複数のカメラを備えたデバイスでの、アプリが使用するカメラの数値 ID です。  **[カメラ](controls/control-camera.md)** コントロールに適用されます。

**[CheckboxBackgroundFill](controls/control-check-box.md)** – チェック ボックス コントロール内のチェックマークを囲むボックスの背景色です。  **[チェック ボックス](controls/control-check-box.md)** コントロールに適用されます。

**[CheckboxBorderColor](controls/control-check-box.md)** – チェック ボックス コントロール内のチェックマークを囲む境界線の色です。  **[チェック ボックス](controls/control-check-box.md)** コントロールに適用されます。

**[CheckboxSize](controls/control-check-box.md)** – チェック ボックス コントロール内のチェックマークを囲むボックスの幅と高さです。  **[チェック ボックス](controls/control-check-box.md)** コントロールに適用されます。

**[CheckmarkFill](controls/control-check-box.md)** – チェック ボックス コントロール内のチェックマークの色です。  **[チェック ボックス](controls/control-check-box.md)** コントロールに適用されます。

**[ChevronBackground](controls/control-drop-down.md)** – ドロップダウン リストの下向き矢印の背景色です。  **[ドロップダウン](controls/control-drop-down.md)** コントロールに適用されます。

**[ChevronBackground](controls/control-drop-down.md)** – ドロップダウン リストの下向き矢印の色です。  **[ドロップダウン](controls/control-drop-down.md)** コントロールに適用されます。

**[Clear](controls/control-text-input.md)** – テキスト入力コントロールに、ユーザーがタップまたはクリックして、そのコントロールの内容をクリアできる "X" を表示するかどうかを指定します。  **[テキスト入力](controls/control-text-input.md)** コントロールに適用されます。

**[Color](controls/properties-color-border.md)** – コントロールのテキストの色です。  多くのコントロールに適用されます。

**[Contrast](controls/control-camera.md)** – ユーザーが画像内の似た色をどれだけ容易に区別できるかを指定します。  **[カメラ](controls/control-camera.md)** コントロールに適用されます。

**[CurrentFindText](controls/control-pdf-viewer.md)** – 使用されている現在の検索語です。  **[PDF ビューアー](controls/control-pdf-viewer.md)** コントロールに適用されます。

**[CurrentPage](controls/control-pdf-viewer.md)** – 実際に表示されている PDF ファイルのページ番号です。  **[PDF ビューアー](controls/control-pdf-viewer.md)** コントロールに適用されます。

### <a name="d"></a>D
**[Data](controls/control-export-import.md)** – ローカル ファイルにエクスポートするコレクションの名前です。  **[エクスポート](controls/control-export-import.md)** コントロールに適用されます。

**[DataField](controls/control-card.md)** – このカードが表示および編集するレコード内のフィールドの名前です。  **[カード](controls/control-card.md)** コントロールに適用されます。

**[DataSource](controls/control-form-detail.md)** – ユーザーが表示、編集、または作成するレコードが含まれるデータ ソース。  **[フォームの表示](controls/control-form-detail.md)** コントロールと**[フォームの編集](controls/control-form-detail.md)** コントロールに適用されます。

**[Default](controls/properties-core.md)** – ユーザーが変更する前のコントロールの初期値です。  多くのコントロールに適用されます。

**[DefaultDate](controls/control-date-picker.md)** – ユーザーが変更する前の日付コントロールの初期値です。  **[日付の選択](controls/control-date-picker.md)** コントロールに適用されます。

**[DefaultMode](controls/control-form-detail.md)** – フォーム コントロールの初期モードで、**Edit**、**New**、**View** のいずれかになります。  **[フォームの編集](controls/control-form-detail.md)** コントロールに適用されます。

**[Direction](controls/control-gallery.md)** – ランドスケープ方向のギャラリーの最初の項目を、左端近くまたは右端近くのどちらに表示するかを指定します。  **[ギャラリー](controls/control-gallery.md)** コントロールに適用されます。

**[Disabled](controls/properties-core.md)** – コントロールをユーザーが操作できるかどうかを指定します。  多くのコントロールに適用されます。

**[DisabledBorderColor](controls/properties-color-border.md)** – コントロールの **[Disabled](controls/properties-core.md)** プロパティが **true** に設定されている場合のコントロールの境界線の色です。  多くのコントロールに適用されます。

**[DisabledColor](controls/properties-color-border.md)** – コントロールの **[Disabled](controls/properties-core.md)** プロパティが **true** に設定されている場合のコントロール内のテキストの色です。  多くのコントロールに適用されます。

**[DisabledFill](controls/properties-color-border.md)** – コントロールの **[Disabled](controls/properties-core.md)** プロパティが **true** に設定されている場合のコントロールの背景色です。  多くのコントロールに適用されます。

**[DisplayName](controls/control-card.md)** – データ ソース内のフィールドのユーザー フレンドリな名前です。  **[カード](controls/control-card.md)** コントロールに適用されます。

**[DisplayMode](controls/properties-core.md)** – 値は Edit、View、Disabled のいずれかになります。 コントロールで、ユーザー入力を許可するか (Edit)、データの表示のみを許可するか (View)、許可しないか (Disabled) を構成します。

**[Document](controls/control-pdf-viewer.md)** – 二重引用符で囲んだ、PDF ファイルの URL です。  **[PDF ビューアー](controls/control-pdf-viewer.md)** コントロールに適用されます。

**[Duration](controls/control-timer.md)** – タイマーを実行する時間の長さを指定します。  **[タイマー](controls/control-timer.md)** コントロールに適用されます。

### <a name="e"></a>E
**[EndYear](controls/control-date-picker.md)** – 日付の選択コントロールでユーザーが設定可能な最後の年です。  **[日付の選択](controls/control-date-picker.md)** コントロールに適用されます。

**Error** – このプロパティの意味は、コントロールによって異なります。

* **[画像の追加](controls/control-add-picture.md)** コントロール - 画像のアップロードで問題が発生した場合は、このプロパティには該当するエラー文字列が含まれます。
* **[カード](controls/control-card.md)** コントロール – 検証が失敗した場合にこのフィールド用に表示するユーザー フレンドリなエラー メッセージです。
* **[フォームの編集](controls/control-form-detail.md)** コントロール – **[SubmitForm](functions/function-form.md)** 関数が失敗したときにこのフォームに表示するユーザー向けのエラー メッセージ。

**[ErrorKind](controls/control-form-detail.md)** – **SubmitForm** の実行時にエラーが発生した場合は、発生したエラーの種類。  **[フォームの表示](controls/control-form-detail.md)** コントロールと**[フォームの編集](controls/control-form-detail.md)** コントロールに適用されます。

**[Explode](controls/control-pie-chart.md)** – 円グラフ内のウェッジ間の距離です。  **[円グラフ](controls/control-pie-chart.md)** コントロールに適用されます。

### <a name="f"></a>F
**[Fill](controls/properties-color-border.md)** – コントロールの背景色です。  多くのコントロールに適用されます。

**[FindNext](controls/control-pdf-viewer.md)** – ドキュメントで **FindText** の次のインスタンスを検索します。  **[PDF ビューアー](controls/control-pdf-viewer.md)** コントロールに適用されます。

**[FindPrevious](controls/control-pdf-viewer.md)** – ドキュメントで **FindText** の前のインスタンスを検索します。  **[PDF ビューアー](controls/control-pdf-viewer.md)** コントロールに適用されます。

**[FindText](controls/control-pdf-viewer.md)** – ドキュメント内で検索する検索語です。  **[PDF ビューアー](controls/control-pdf-viewer.md)** コントロールに適用されます。

**[Font](controls/properties-text.md)** – テキストを表記するフォントのファミリー名です。  多くのコントロールに適用されます。

**[FontWeight](controls/properties-text.md)** – コントロール内のテキストの太さです。**Bold** (太字)、**Semibold** (中太)、**Normal** (標準)、**Lighter** (細字) から指定します。  多くのコントロールに適用されます。

### <a name="g"></a>G
**[GridStyle](controls/control-column-line-chart.md)** – 縦棒グラフまたは折れ線グラフで、X 軸と Y 軸のどちらか一方または両方を表示するか、または両方とも表示しないかを指定します。  **[縦棒グラフ](controls/control-column-line-chart.md)** コントロールと**[折れ線グラフ](controls/control-column-line-chart.md)** コントロールに適用されます。

### <a name="h"></a>H
**[HandleActiveFill](controls/control-slider.md)** – ユーザーが値を変更しているときのスライダーのハンドルの色です。  **[スライダー](controls/control-slider.md)** コントロールに適用されます。

**[HandleFill](controls/control-slider.md)** – トグルまたはスライダー コントロールのハンドル (位置が変わる要素) の色です。  **[スライダー](controls/control-slider.md)** コントロールに適用されます。

**[HandleHoverFill](controls/control-slider.md)** – スライダーのハンドルにユーザーがマウス ポインターを重ねているときのハンドルの色です。  **[スライダー](controls/control-slider.md)** コントロールに適用されます。

**[Height](controls/properties-size-location.md)** – コントロールの上端と下端の距離です。  多くのコントロールに適用されます。

**[HintText](controls/control-text-input.md)** - テキスト入力コントロールが空の場合に表示される薄いグレーのテキストです。  **[テキスト入力](controls/control-text-input.md)** コントロールに適用されます。

**[HoverBorderColor](controls/properties-color-border.md)** – コントロール上にユーザーがマウス ポインターを重ねているときのコントロールの境界線の色です。  多くのコントロールに適用されます。

**[HoverColor](controls/properties-color-border.md)** – コントロールにユーザーがマウス ポインターを重ねているときのコントロール内のテキストの色です。  多くのコントロールに適用されます。

**[HoverFill](controls/properties-color-border.md)** – コントロールにユーザーがマウス ポインターを重ねているときのコントロールの背景色です。  多くのコントロールに適用されます。

**[HTMLText](controls/control-html-text.md)** – HTML テキスト コントロールに表示される、HTML タグを含む可能性のあるテキストです。  **[HTML テキスト](controls/control-html-text.md)** コントロールに適用されます。

### <a name="i"></a>I
**[Image](controls/properties-visual.md)** – イメージ、オーディオ、マイクの各コントロールに表示される画像の名前です。  **[オーディオ](controls/control-audio-video.md)**、**[イメージ](controls/control-image.md)**、**[マイク](controls/control-microphone.md)**、および**[ビデオ](controls/control-audio-video.md)** の各コントロールに適用されます。

**[ImagePosition](controls/properties-visual.md)** – 画面またはコントロールのサイズが画像と異なる場合の、画面またはコントロール内の画像の位置です (**Fill** (フィル)、**Fit** (サイズに合わせる)、**Stretch** (伸ばす)、**Tile** (タイル表示)、または **Center** (中央に表示))。  多くのコントロールに適用されます。

**[Input](controls/control-pen-input.md)** – 入力です。  **[ペン入力](controls/control-pen-input.md)** コントロールに適用されます。

**[Italic](controls/properties-text.md)** – コントロール内のテキストを斜体にするかどうかを指定します。  多くのコントロールに適用されます。

**[Item](controls/control-form-detail.md)** – ユーザーが表示または編集する **DataSource** 内のレコード。  **[フォームの表示](controls/control-form-detail.md)** コントロールと**[フォームの編集](controls/control-form-detail.md)** コントロールに適用されます。

**[ItemBorderColor](controls/control-pie-chart.md)** – 円グラフ内の各ウェッジの周りの境界線の色です。  **[円グラフ](controls/control-pie-chart.md)** コントロールに適用されます。

**[ItemBorderThickness](controls/control-pie-chart.md)** – 円グラフ内の各ウェッジの周りの境界線の太さです。  **[円グラフ](controls/control-pie-chart.md)** コントロールに適用されます。

**ItemColorSet** – グラフ内の各データ ポイントの色です。  **[縦棒グラフ](controls/control-column-line-chart.md)**、**[折れ線グラフ](controls/control-column-line-chart.md)**、および**[円グラフ](controls/control-pie-chart.md)** の各コントロールに適用されます。

**[ItemPaddingLeft](controls/control-list-box.md)** – リスト ボックス内のテキストと左端の間の距離です。  **[リスト ボックス](controls/control-list-box.md)** コントロールに適用されます。

**[Items](controls/properties-core.md)** – ギャラリー、リスト、グラフなどのコントロールに表示されるデータのソースです。  多くのコントロールに適用されます。

**[ItemsGap](controls/control-column-line-chart.md)** – 縦棒グラフの縦棒間の距離です。  **[縦棒グラフ](controls/control-column-line-chart.md)** コントロールに適用されます。

### <a name="l"></a>L
**[LabelPosition](controls/control-pie-chart.md)** – ウェッジを基準とした、円グラフ内のラベルの場所です。  **[円グラフ](controls/control-pie-chart.md)** コントロールに適用されます。

**[LastSubmit](controls/control-form-detail.md)** – 最後に正常に送信されたレコード。サーバーが生成したフィールドを含みます。  **[フォームの編集](controls/control-form-detail.md)** コントロールに適用されます。

**Layout** – ユーザーがギャラリーをスクロールしたりスライダーを調整したりする方向です。上下 (**Vertical**) または左右 (**Horizontal**) から選択します。  **[ギャラリー](controls/control-gallery.md)** コントロールと**[スライダー](controls/control-slider.md)** コントロールに適用されます。

**[LineHeight](controls/properties-text.md)** – テキストの行間やリスト内の項目間などの距離です。  **[リスト ボックス](controls/control-list-box.md)**、**[ラジオ](controls/control-radio.md)**、**[ラベル](controls/control-text-box.md)**、**[テキスト入力](controls/control-text-input.md)** の各コントロールに適用されます。

**[Loop](controls/control-audio-video.md)** – オーディオまたはビデオ クリップを、再生終了と同時に先頭から自動的に再開するかどうかを指定します。  **[オーディオ](controls/control-audio-video.md)** コントロールと**[ビデオ](controls/control-audio-video.md)** コントロールに適用されます。

### <a name="m"></a>M
**[Markers](controls/control-column-line-chart.md)** – 縦棒グラフまたは折れ線グラフで各データ ポイントの値を表示するかどうかを指定します。  **[縦棒グラフ](controls/control-column-line-chart.md)** コントロールと**[折れ線グラフ](controls/control-column-line-chart.md)** コントロールに適用されます。

**[MarkerSuffix](controls/control-column-line-chart.md)** – **[Markers](controls/control-column-line-chart.md)** プロパティが **true** に設定されている縦棒グラフで、各値の後に表示するテキストです。  **[縦棒グラフ](controls/control-column-line-chart.md)** コントロールに適用されます。

**Max** – ユーザーがスライダーまたは評価を設定できる最大値です。  **[評価](controls/control-rating.md)** コントロールと**[スライダー](controls/control-slider.md)** コントロールに適用されます。

**[MaxLength](controls/control-text-input.md)** – ユーザーがテキスト入力コントロールに入力できる文字数です。  **[テキスト入力](controls/control-text-input.md)** コントロールに適用されます。

**Media** – オーディオまたはビデオ コントロールが再生するクリップの ID です。  **[画像の追加](controls/control-add-picture.md)**、**[オーディオ](controls/control-audio-video.md)**、および**[ビデオ](controls/control-audio-video.md)** の各コントロールに適用されます。

**[Mic](controls/control-microphone.md)** – 複数のマイクを備えたデバイスでの、アプリが使用するマイクの数値 ID です。  **[マイク](controls/control-microphone.md)** コントロールに適用されます。

**[Min](controls/control-slider.md)** – ユーザーがスライダーを設定できる最小値です。  **[スライダー](controls/control-slider.md)** コントロールに適用されます。

**[MinimumBarWidth](controls/control-column-line-chart.md)** – 縦棒グラフの縦棒の表示で許容される最も狭い幅です。  **[縦棒グラフ](controls/control-column-line-chart.md)** コントロールに適用されます。

**Mode** – このプロパティの意味は、コントロールによって異なります。

* **[フォームの編集](controls/control-form-detail.md)** コントロール – このコントロールのモードは、**Edit** (編集) または **New** (新規) です。
* **[ペン入力](controls/control-pen-input.md)** コントロール – このコントロールのモードは、**Draw** (描画)、**Erase** (削除)、または **Select** (選択) です。
* **[テキスト入力](controls/control-text-input.md)** コントロール – このコントロールのモードは、**SingleLine** (1 行)、**MultiLine** (複数行)、または **Password** (パスワード) です。

### <a name="n"></a>N
**[NavigationStep](controls/control-gallery.md)** – **[ShowNavigation](controls/control-gallery.md)** プロパティが **true** に設定されている場合は、ギャラリーの端にあるナビゲーション矢印の選択操作でギャラリーをどの程度スクロールするかを指定します。  **[ギャラリー](controls/control-gallery.md)** コントロールに適用されます。

**[NumberOfSeries](controls/control-column-line-chart.md)** – 縦棒グラフまたは折れ線グラフに反映されるデータ列の数です。  **[縦棒グラフ](controls/control-column-line-chart.md)** コントロールと**[折れ線グラフ](controls/control-column-line-chart.md)** コントロールに適用されます。

### <a name="o"></a>O
**[OnChange](controls/properties-core.md)** – ユーザーが (スライダーを調整するなどして) コントロールの値を変更したときのアプリの動作。  多くのコントロールに適用されます。

**OnCheck** – チェック ボックスまたはトグルの値が **true** に変わったときのアプリの動作。  **[チェック ボックス](controls/control-check-box.md)** コントロールと**[トグル](controls/control-toggle.md)** コントロールに適用されます。

**[OnEnd](controls/control-audio-video.md)** – オーディオまたはビデオ クリップの再生が終了したときのアプリの動作。  **[オーディオ](controls/control-audio-video.md)** コントロールと**[ビデオ](controls/control-audio-video.md)** コントロールに適用されます。

**[OnFailure](controls/control-form-detail.md)** – データ操作が失敗したときのアプリの動作。  **[フォームの編集](controls/control-form-detail.md)** コントロールに適用されます。

**[OnHidden](controls/control-screen.md)** – ユーザーがある画面から離れたときのアプリの動作。  **[画面](controls/control-screen.md)** コントロールに適用されます。

**[OnPause](controls/control-audio-video.md)** – オーディオまたはビデオ コントロールが再生しているクリップをユーザーが一時停止したときのアプリの動作。  **[オーディオ](controls/control-audio-video.md)** コントロールと**[ビデオ](controls/control-audio-video.md)** コントロールに適用されます。

**[OnReset](controls/control-form-detail.md)** – **[フォームの編集](controls/control-form-detail.md)** コントロールがリセットされたときのアプリの動作。  **[フォームの編集](controls/control-form-detail.md)** コントロールに適用されます。

**[OnSelect](controls/properties-core.md)** – ユーザーがコントロールをタップまたはクリックしたときのアプリの動作。  多くのコントロールに適用されます。

**OnStart** – ユーザーが開いたり、マイク コントロールで録音を開始したりしたときのアプリの動作。 **[オーディオ](controls/control-audio-video.md)**、**[マイク](controls/control-microphone.md)**、**[画面](controls/control-screen.md)**、および**[ビデオ](controls/control-audio-video.md)** の各コントロールに適用されます。

**[OnStateChange](controls/control-pdf-viewer.md)** – コントロールの状態が変化したときのアプリの動作。 **[PDF ビューアー](controls/control-pdf-viewer.md)** コントロールに適用されます。

**[OnStop](controls/control-microphone.md)** – ユーザーがマイク コントロールで録音を終了したときのアプリの動作。 **[マイク](controls/control-microphone.md)** コントロールに適用されます。

**[OnStream](controls/control-camera.md)** – **[ストリーム](controls/control-camera.md)** プロパティが更新されたときのアプリの動作。  **[カメラ](controls/control-camera.md)** コントロールに適用されます。

**[OnSuccess](controls/control-form-detail.md)** – データ操作が成功したときのアプリの動作。  **[フォームの編集](controls/control-form-detail.md)** コントロールに適用されます。

**[OnTimerEnd](controls/control-timer.md)** – タイマーが実行を完了したときのアプリの動作。  **[タイマー](controls/control-timer.md)** コントロールに適用されます。

**[OnTimerStart](controls/control-timer.md)** – タイマーが実行を開始したときのアプリの動作。  **[タイマー](controls/control-timer.md)** コントロールに適用されます。

**OnUncheck** – チェック ボックスまたはトグルの値が **false** に変わったときのアプリの動作。  **[チェック ボックス](controls/control-check-box.md)** コントロールと**[トグル](controls/control-toggle.md)** コントロールに適用されます。

**[OnVisible](controls/control-screen.md)** – ユーザーが画面に移動したときのアプリの動作。  **[画面](controls/control-screen.md)** コントロールに適用されます。

**[OriginalHeight](controls/control-image.md)** – 画像の元の高さです。**[CalculateOriginalDimensions](controls/control-image.md)** プロパティで有効にします。  **[イメージ](controls/control-image.md)** コントロールに適用されます。

**[OriginalWidth](controls/control-image.md)** – 画像の元の幅です。**[CalculateOriginalDimensions](controls/control-image.md)** プロパティで有効にします。  **[イメージ](controls/control-image.md)** コントロールに適用されます。

**[Overflow](controls/control-text-box.md)** – ラベルの **[Wrap](controls/control-text-box.md)** プロパティが **true** に設定され、**[Text](controls/properties-core.md)** プロパティの値がコントロールで一度に表示できる文字数を超えている場合に、ラベルにスクロール バーを表示するかどうかを指定します。  **[ラベル](controls/control-text-box.md)** コントロールに適用されます。

### <a name="p"></a>P
**[Padding](controls/properties-size-location.md)** – [インポート] ボタンまたは [エクスポート] ボタンのテキストと、ボタンの縁との距離です。  **[画像の追加](controls/control-add-picture.md)**、**[エクスポート](controls/control-export-import.md)**、および**[インポート](controls/control-export-import.md)** の各コントロールに適用されます。

**[PaddingBottom](controls/properties-size-location.md)** – コントロール内のテキストとそのコントロールの下端間の距離です。  多くのコントロールに適用されます。

**[PaddingLeft](controls/properties-size-location.md)** – コントロール内のテキストとそのコントロールの左端間の距離です。  多くのコントロールに適用されます。

**[PaddingRight](controls/properties-size-location.md)** – コントロール内のテキストとそのコントロールの右端間の距離です。  多くのコントロールに適用されます。

**[PaddingTop](controls/properties-size-location.md)** – コントロール内のテキストとそのコントロールの上端間の距離です。  多くのコントロールに適用されます。

**[Page](controls/control-pdf-viewer.md)** – 表示するページ番号です。  **[PDF ビューアー](controls/control-pdf-viewer.md)** コントロールに適用されます。

**[PageCount](controls/control-pdf-viewer.md)** – ドキュメントのページ数です。  **[PDF ビューアー](controls/control-pdf-viewer.md)** コントロールに適用されます。

**[Paused](controls/control-audio-video.md)** – メディア再生コントロールが現在一時停止している場合は *true*、それ以外の場合は *false* です。  **[オーディオ](controls/control-audio-video.md)** コントロールと**[ビデオ](controls/control-audio-video.md)** コントロールに適用されます。

**[Photo](controls/control-camera.md)** – ユーザーが写真を撮影すると取得される画像です。  **[カメラ](controls/control-camera.md)** コントロールに適用されます。

**[Pressed](controls/control-button.md)** – コントロールが押されている間は *true*、それ以外の時は *false* になります。  **[ボタン](controls/control-button.md)** コントロールに適用されます。

**[PressedBorderColor](controls/properties-color-border.md)** – コントロールをユーザーがタップまたはクリックしたときのコントロールの境界線の色です。  多くのコントロールに適用されます。

**[PressedColor](controls/properties-color-border.md)** – コントロールをユーザーがタップまたはクリックしたときのコントロール内のテキストの色です。  多くのコントロールに適用されます。

**[PressedFill](controls/properties-color-border.md)** – コントロールをユーザーがタップまたはクリックしたときのコントロールの背景色です。  多くのコントロールに適用されます。

### <a name="r"></a>R
**[RadioBackgroundFill](controls/control-radio.md)** – ラジオボタン コントロールの円の背景色です。  **[ラジオ](controls/control-radio.md)** コントロールに適用されます。

**[RadioBorderColor](controls/control-radio.md)** – ラジオボタン コントロールに含まれる各オプションの円の色です。  **[ラジオ](controls/control-radio.md)** コントロールに適用されます。

**[RadioSelectionFill](controls/control-radio.md)** – ラジオボタン コントロールで選択されたオプションの円の内側に表示される色です。  **[ラジオ](controls/control-radio.md)** コントロールに適用されます。

**[RadioSize](controls/control-radio.md)** – ラジオボタン コントロールの円の直径です。  **[ラジオ](controls/control-radio.md)** コントロールに適用されます。

**[RadiusBottomLeft](controls/properties-size-location.md)** – コントロールの左下隅を丸める度合いです。  多くのコントロールに適用されます。

**[RadiusBottomRight](controls/properties-size-location.md)** – コントロールの右下隅を丸める度合いです。  多くのコントロールに適用されます。

**[RadiusTopLeft](controls/properties-size-location.md)** – コントロールの左上隅を丸める度合いです。  多くのコントロールに適用されます。

**[RadiusTopRight](controls/properties-size-location.md)** – コントロールの右上隅を丸める度合いです。  多くのコントロールに適用されます。

**RailFill** – 値が **false** の場合の、トグル コントロール内の四角形の背景色、またはスライダー コントロールのハンドルの右側の線の色です。  **[スライダー](controls/control-slider.md)** コントロールと**[トグル](controls/control-toggle.md)** コントロールに適用されます。

**RailHoverFill** – 値が **false** の場合に、トグル コントロールまたはスライダーにポインターを合わせたときの、トグル コントロール内の四角形の背景色、またはスライダー コントロールのハンドルの右側の線の色です。  **[スライダー](controls/control-slider.md)** コントロールと**[トグル](controls/control-toggle.md)** コントロールに適用されます。

**[RatingFill](controls/control-rating.md)** – 評価コントロールの星の色です。  **[評価](controls/control-rating.md)** コントロールに適用されます。

**ReadOnly** – ユーザーがスライダーまたは評価コントロールの値を変更できるかどうかを指定します。  **[評価](controls/control-rating.md)** コントロールと**[スライダー](controls/control-slider.md)** コントロールに適用されます。

**[Repeat](controls/control-timer.md)** – タイマーが実行を完了したときに自動的に再開されるかどうかを指定します。  **[タイマー](controls/control-timer.md)** コントロールに適用されます。

**[Required](controls/control-card.md)** – データ ソースのフィールドの編集時に、カードに値が含まれている必要があるかどうかを指定します。  **[カード](controls/control-card.md)** コントロールに適用されます。

**[Reset](controls/properties-core.md)** – コントロールを既定値に戻すかどうかを指定します。  多くのコントロールに適用されます。  **[Reset](functions/function-reset.md)** 関数に関する記事もご覧ください。

### <a name="s"></a>S
**Selected** – 選択された項目です。  **[ドロップダウン](controls/control-drop-down.md)** コントロールと**[ギャラリー](controls/control-gallery.md)** コントロールに適用されます。

**[SelectedDate](controls/control-date-picker.md)** – 日付コントロールで現在選択されている日付です。  **[日付の選択](controls/control-date-picker.md)** コントロールに適用されます。

**[SelectionColor](controls/properties-color-border.md)** – リスト内で選択された項目のテキストの色、またはペン コントロールの選択ツールの色です。  **[ドロップダウン](controls/control-drop-down.md)**、**[リスト ボックス](controls/control-list-box.md)**、および**[ペン入力](controls/control-pen-input.md)** の各コントロールに適用されます。

**[SelectionFill](controls/properties-color-border.md)** – リストで選択された項目またはペン コントロールの選択領域の背景色です。  **[ドロップダウン](controls/control-drop-down.md)** コントロールと**[リスト ボックス](controls/control-list-box.md)** コントロールに適用されます。

**[SelectionThickness](controls/control-pen-input.md)** – ペン入力コントロールの選択ツールの太さです。  **[ペン入力](controls/control-pen-input.md)** コントロールに適用されます。

**[SelectMultiple](controls/control-list-box.md)** – ユーザーがリスト ボックスの複数の項目を選択できるかどうかを指定します。  **[リスト ボックス](controls/control-list-box.md)** コントロールに適用されます。

**[SeriesAxisMax](controls/control-column-line-chart.md)** – 縦棒グラフまたは折れ線グラフの Y 軸の最大値です。  **[縦棒グラフ](controls/control-column-line-chart.md)** コントロールに適用されます。

**[SeriesAxisMin](controls/control-column-line-chart.md)** – 縦棒グラフの Y 軸の最小値を決める値です。  **[縦棒グラフ](controls/control-column-line-chart.md)** コントロールに適用されます。

**ShowControls** – オーディオ プレイヤーまたはビデオ プレイヤーに再生ボタンと音量スライダーなどを表示するかどうか、およびペン コントロールに描画、削除、クリアなどのアイコンを表示するかどうかを指定します。  **[オーディオ](controls/control-audio-video.md)**、**[PDF ビューアー](controls/control-pdf-viewer.md)**、**[ペン入力](controls/control-pen-input.md)**、および**[ビデオ](controls/control-audio-video.md)** の各コントロールに適用されます。

**[ShowLabels](controls/control-pie-chart.md)** – 円グラフに、各ウェッジに関連付けられた値を表示するかどうかを指定します。  **[円グラフ](controls/control-pie-chart.md)** コントロールに適用されます。

**[ShowNavigation](controls/control-gallery.md)** – ギャラリーの両端に矢印を表示し、それらの矢印のクリックまたはタップでギャラリー内の項目をユーザーがスクロールできるようにするかどうかを指定します。  **[ギャラリー](controls/control-gallery.md)** コントロールに適用されます。

**[ShowScrollbar](controls/control-gallery.md)** – ユーザーがポインターをギャラリーに合わせたときにスクロール バーを表示するかどうかを指定します。  **[ギャラリー](controls/control-gallery.md)** コントロールに適用されます。

**ShowValue** – ユーザーがスライダーまたは評価の値を変更するか、ポインターをコントロールに合わせたときにその値を表示するかどうかを指定します。  **[評価](controls/control-rating.md)** コントロールと**[スライダー](controls/control-slider.md)** コントロールに適用されます。

**[Size](controls/properties-text.md)** – コントロールに表示されるテキストのフォント サイズです。  多くのコントロールに適用されます。

**[Snap](controls/control-gallery.md)** – ユーザーがギャラリーをスクロールするとき、次の項目が完全に表示されるように自動的にスナップするかどうかを指定します。  **[ギャラリー](controls/control-gallery.md)** コントロールに適用されます。

**Start** – オーディオまたはビデオ クリップを再生するかどうかを指定します。  **[オーディオ](controls/control-audio-video.md)**、**[タイマー](controls/control-timer.md)**、および**[ビデオ](controls/control-audio-video.md)** の各コントロールに適用されます。

**[StartTime](controls/control-audio-video.md)** – クリップの再生が開始するとき、オーディオまたはビデオ クリップの開始後の時刻です。  **[オーディオ](controls/control-audio-video.md)** コントロールと**[ビデオ](controls/control-audio-video.md)** コントロールに適用されます。

**[StartYear](controls/control-date-picker.md)** – 日付の選択コントロールでユーザーが設定可能な最初の年です。  **[日付の選択](controls/control-date-picker.md)** コントロールに適用されます。

**[Stream](controls/control-camera.md)** – **[StreamRate](controls/control-camera.md)** プロパティに基づいて自動的に更新された画像です。  **[カメラ](controls/control-camera.md)** コントロールに適用されます。

**[StreamRate](controls/control-camera.md)** – **[Stream](controls/control-camera.md)** プロパティの画像を更新する頻度です (ミリ秒単位)。  この値の範囲は、100 (0.1 秒) から 3,600,000 (1 時間) です。  **[カメラ](controls/control-camera.md)** コントロールに適用されます。

**[Strikethrough](controls/properties-text.md)** – コントロールに表示されるテキストに取り消し線を付けるかどうかを指定します。  多くのコントロールに適用されます。

### <a name="t"></a>T
**[TemplateFill](controls/control-gallery.md)** – ギャラリーの背景色です。  **[ギャラリー](controls/control-gallery.md)** コントロールに適用されます。

**[TemplatePadding](controls/control-gallery.md)** – ギャラリー内の項目間の距離です。  **[ギャラリー](controls/control-gallery.md)** コントロールに適用されます。

**[TemplateSize](controls/control-gallery.md)** – 垂直/ポートレート方向のギャラリー向けのテンプレートの高さ、または水平/ランドスケープ方向のギャラリー向けのテンプレートの幅です。  **[ギャラリー](controls/control-gallery.md)** コントロールに適用されます。

**[Text](controls/properties-core.md)** – コントロールに表示されるテキスト、またはコントロールにユーザーが入力するテキストです。  多くのコントロールに適用されます。

**[Time](controls/control-audio-video.md)** – メディア コントロールの現在位置です。  **[オーディオ](controls/control-audio-video.md)** コントロールと**[ビデオ](controls/control-audio-video.md)** コントロールに適用されます。

**[Tooltip](controls/properties-core.md)** – ポインターをコントロールに合わせたときに表示される説明テキストです。  多くのコントロールに適用されます。

**[Transition](controls/control-gallery.md)** – ユーザーがポインターをギャラリー内の項目に合わせたときの視覚効果 (**ポップ**、**プッシュ**、または **None**) を指定します。  **[ギャラリー](controls/control-gallery.md)** コントロールに適用されます。

**[Transparency](controls/control-image.md)** – 画像の背後にあるコントロールを表示する度合いです。  **[イメージ](controls/control-image.md)** コントロールに適用されます。

### <a name="u"></a>U
**[Underline](controls/properties-text.md)** – コントロールに表示されるテキストの下に線を引くかどうかを指定します。  多くのコントロールに適用されます。

**[Unsaved](controls/control-form-detail.md)** – ユーザーによる未保存の変更が **[フォームの編集](controls/control-form-detail.md)** コントロールに含まれている場合は true。  **[フォームの編集](controls/control-form-detail.md)** コントロールに適用されます。

**[Update](controls/control-card.md)** – フィールドのデータ ソースに書き戻す値です。  **[カード](controls/control-card.md)** コントロールに適用されます。

**[Updates](controls/control-form-detail.md)** – フォーム コントロールに読み込まれているレコードに対してデータ ソースに書き戻す値。  **[フォームの編集](controls/control-form-detail.md)** コントロールに適用されます。

### <a name="v"></a>V
**Valid** – **[カード](controls/control-card.md)** コントロールまたは**[フォームの編集](controls/control-form-detail.md)** コントロールに有効なエントリが含まれており、データ ソースへの送信準備ができているかどうかを示します。  **[カード](controls/control-card.md)** コントロールと**[フォームの編集](controls/control-form-detail.md)** コントロールに適用されます。

**[Value](controls/properties-core.md)** – 入力コントロールの値です。  **[チェック ボックス](controls/control-check-box.md)**、**[ラジオ](controls/control-radio.md)**、**[スライダー](controls/control-slider.md)**、および**[トグル](controls/control-toggle.md)** の各コントロールに適用されます。

**ValueFill** – 値が **true** の場合の、トグル コントロール内の四角形の背景色、またはスライダー コントロールのハンドルの左側の線の色です。  **[スライダー](controls/control-slider.md)** コントロールと**[トグル](controls/control-toggle.md)** コントロールに適用されます。

**ValueHoverFill** – 値が **true** の場合に、トグル コントロールまたはスライダーにポインターを合わせたときの、トグル コントロール内の四角形の背景色、またはスライダー コントロールのハンドルの左側の線の色です。  **[スライダー](controls/control-slider.md)** コントロールと**[トグル](controls/control-toggle.md)** コントロールに適用されます。

**[VerticalAlign](controls/properties-text.md)** – コントロールの垂直方向の中心に対するコントロール上でのテキストの位置です。  多くのコントロールに適用されます。

**[Visible](controls/properties-core.md)** – コントロールを表示するか非表示にするかを指定します。  多くのコントロールに適用されます。

### <a name="w"></a>W
**[Width](controls/properties-size-location.md)** – コントロールの左端と右端の間の距離です。  多くのコントロールに適用されます。

**[WidthFit](controls/properties-size-location.md)** – **[フォームの編集](controls/control-form-detail.md)** コントロールなどのコンテナー コントロールで、コントロールを水平方向に自動的に拡大して空の領域を埋めるかどうかを示します。 複数のカードでこのプロパティが **true** に設定されている場合、領域はカード間で分割されます。 詳細については、「[データ フォームのレイアウトについて](working-with-form-layout.md)」を参照してください。

**[Wrap](controls/control-text-box.md)**– 長すぎてラベルに収まらないテキストを次の行に折り返すかどうかを指定します。  **[ラベル](controls/control-text-box.md)** コントロールに適用されます。

**[WrapCount](controls/control-gallery.md)** – ギャラリーの項目ごとに表示されるレコード数を指定します。  **[ギャラリー](controls/control-gallery.md)** コントロールに適用されます。

### <a name="x"></a>X
**[X](controls/properties-size-location.md)** – コントロールの左端とその親コンテナー (親コンテナーがない場合は画面) の左端間の距離です。 多くのコントロールに適用されます。 複数の列を持つコンテナーの**[カード](controls/control-card.md)** コントロールの場合、このプロパティは、カードが表示される列を決定します。

**[XLabelAngle](controls/control-column-line-chart.md)** – 縦棒グラフまたは折れ線グラフの X 軸の下に表示されるラベルの角度です。  **[縦棒グラフ](controls/control-column-line-chart.md)** コントロールと**[折れ線グラフ](controls/control-column-line-chart.md)** コントロールに適用されます。

### <a name="y"></a>Y
**[Y](controls/properties-size-location.md)** – コントロールの上端とその親コンテナー (親コンテナーがない場合は画面) の上端間の距離です。 多くのコントロールに適用されます。 複数の行を持つコンテナーの**[カード](controls/control-card.md)** コントロールの場合、このプロパティは、カードが表示される行を決定します。

**[YAxisMax](controls/control-column-line-chart.md)** – 折れ線グラフの Y 軸の最大値です。  **[折れ線グラフ](controls/control-column-line-chart.md)** コントロールに適用されます。

**[YAxisMin](controls/control-column-line-chart.md)** – 折れ線グラフの Y 軸の最小値です。  **[折れ線グラフ](controls/control-column-line-chart.md)** コントロールに適用されます。

**[YLabelAngle](controls/control-column-line-chart.md)** – 折れ線グラフまたは縦棒グラフの Y 軸の横に表示されるラベルの角度です。  **[縦棒グラフ](controls/control-column-line-chart.md)** コントロールと**[折れ線グラフ](controls/control-column-line-chart.md)** コントロールに適用されます。

### <a name="z"></a>Z
**Zoom** – カメラからの画像、または PDF ビューアーでのファイルの表示を拡大する割合です。  **[カメラ](controls/control-camera.md)** コントロールと **[PDF ビューアー](controls/control-pdf-viewer.md)** コントロールに適用されます。

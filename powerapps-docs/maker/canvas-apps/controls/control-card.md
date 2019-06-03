---
title: 'カード コントロール: リファレンス | Microsoft Docs'
description: 各種プロパティとサンプルを含むカード コントロールに関する情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.component: canvas
ms.date: 10/25/2016
ms.author: gregli
ms.reviewer: anneta
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: cc4338e37b7ecde2e2e2e9ad5c5ac6e96d116b58
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61559485"
---
# <a name="card-control-in-powerapps"></a>PowerApps のカード コントロール
**[フォームの表示](control-form-detail.md)** または **[フォームの編集](control-form-detail.md)** コントロールの 1 つのフィールドの表示や編集を体験できます。

## <a name="description"></a>説明
**[フォームの表示](control-form-detail.md)** および **[フォームの編集](control-form-detail.md)** コントロールは、レコード全体を表示するためのコンテナーとして機能します。 各コンテナーは、個々のフィールドを表示したり、これらのフィールドを更新する方法を提供したりする一連の**カード** コントロールを保持できます。 各カードには、操作対象となるレコードのフィールドを指定する **DataField** プロパティがあります。  

さまざまなデータ タイプやユーザー体験用に、いくつかのカードが事前に定義されています。  たとえば、キーボードで使用しやすい、 **[テキスト入力](control-text-input.md)** コントロールで数値フィールドを編集するカードが存在する場合があります。 別のカードは、代わりに **[スライダー](control-slider.md)** コントロールを使用した数値の編集をサポートしている可能性があります。 フォーム コントロールが選択されていると、右側のウィンドウで、フィールドに基づいて容易にカードを選択できます。

カード自体には、コントロールが含まれています。 カードのコントロールが、1 つのフィールドを表示したり編集したりする体験を構成します。 たとえば、数値カードは、フィールドの表示名を提供する **[ラベル](control-text-box.md)** コントロールと、フィールドの値のためのエディターを提供する **[テキスト入力](control-text-input.md)** コントロールで構成されている可能性があります。 このカードにはまた、発生した検証エラーをすべて表示する **[ラベル](control-text-box.md)** コントロールや、フィールドが必要であることを示す一般的なアスタリスクのための **[ラベル](control-text-box.md)** コントロールも含まれている可能性があります。

事前に定義されたカードの各コントロールは、サイズの変更、移動、非表示化、コントロールの追加などの変更を行ってカスタマイズできます。 また、最初からコントロールを追加する、完全に空白のカードである "カスタム カード" から始めることもできます。

事前に定義されたカードは、既定では*ロック*されています。 ロックされたカードでは、カードまたはカード内のコントロールの特定のプロパティしか変更できず、またロックされたカードを削除することはできません。 **Advanced** ビューの **View** タブでカードのロックを表示したり、そのロックを解除したりできます。 プロパティがロックされていて変更できない場合は、その名前の横にロック アイコンが表示されます。 カードのロック解除は高度な操作であり、ロックを解除するとカードの自動数式生成が実行されず、カードを再びロックすることもできないため、くれぐれも慎重に行うようにしてください。

フォームのコンテナー内では **ThisItem** レコードが使用可能であり、そこにはレコードのすべてのフィールドが含まれています。  たとえば、カードの **[Default](properties-core.md)** プロパティは多くの場合、**ThisItem**.*FieldName* に設定されています。

**Parent** 参照を使用して、カードのプロパティを参照するためのコントロールを構成できます。  たとえば、コントロールは **Parent.Default** を使用して、フィールドの初期状態をデータ ソースから読み取ります。 必要な情報に直接アクセスする代わりに **Parent** を使用すると、カードのカプセル化が向上し、内部の数式を壊すことなくそれを別のフィールドに変更できます。

カードをカスタマイズしたり、ロック解除したり、作成したりする方法の例については、「[データ カードについて](../working-with-cards.md)」をご覧ください。

## <a name="key-properties"></a>主要なプロパティ
**DataField** – このカードが表示および編集するレコード内のフィールドの名前です。

* この名前は、数式ではなく、二重引用符で囲まれた 1 つの静的な文字列 (たとえば、 **"Name"** ) として指定します。
* カードは、その **DataField** プロパティを*空白*に設定してバインド解除します。 バインド解除されたカードでは、**Valid** および **Update** プロパティは無視されます。

**[Default](properties-core.md)** – ユーザーが変更する前のコントロールの初期値です。

* データ ソースに応じたフィールドの既定値を参照するには、カード内のコントロールごとに、このプロパティを **Parent.Default** に設定します。 たとえば、ユーザーがそのスライダーの一般的な値で始めるようにするには、スライダーの **[Default](properties-core.md)** プロパティを **Parent.Default** に設定します。

**DisplayMode** – 値は **Edit、View**、**Disabled** のいずれかになります。 カード内のコントロールで、ユーザー入力を許可するか (**Edit**)、データの表示のみを許可するか (**View**)、許可しないか (**Disabled**) を構成します。  

* 既定ではフォームの動作に関連するこのプロパティを構成すると、編集フォームと表示フォームの両方で 1 つのカードを使用できます。
* **View** モードでは、 **[テキスト入力](control-text-input.md)** 、 **[ドロップ ダウン](control-drop-down.md)** 、 **[日付の選択](control-date-picker.md)** などの子コントロールでテキスト値のみが表示され、対話型要素や装飾は表示されません。

**DisplayName** – データ ソース内のフィールドのユーザー フレンドリ名です。

* **[DataSourceInfo](../functions/function-datasourceinfo.md)** 関数は、このメタデータをデータ ソースから提供します。
* カード内のコントロールは、**Parent.DisplayName** を使用してフィールドの名前を参照します。

**Error** – 検証が失敗した場合にこのフィールド用に表示するユーザー フレンドリなエラー メッセージです。

* このプロパティは、**SubmitForm** が呼び出されたときに設定されます。  
* このメッセージは、データ ソースのメタデータと、カードの **Required** プロパティのチェックに基づいた検証の問題を示します。

**Required** – データ ソースのフィールドの編集時に、カードに値が含まれている必要があるかどうかを指定します。

* **[DataSourceInfo](../functions/function-datasourceinfo.md)** 関数は、必要なメタデータをデータ ソースから提供します。
* カード内のコントロールは、**Parent.Required** を使用して、そのカードのフィールドが必要かどうかを判定します。

**Update** – フィールドのデータ ソースに書き戻す値です。

* データ ソースに書き戻すためにカードの編集コントロールから値を取得するには、このプロパティの数式を使用します。 たとえば、そのカード内のスライダーからの値でデータ ソースを更新するには、カードの **Update** プロパティを **Slider.Value** に設定します。

**[Width](properties-size-location.md)** – コントロールの左端と右端の間の距離です。

**[WidthFit](properties-size-location.md)** – **[フォームの編集](control-form-detail.md)** コントロールなどのコンテナー コントロールで、コントロールを水平方向に自動的に拡大して空の領域を埋めるかどうかを示します。 複数のカードでこのプロパティが **true** に設定されている場合、領域はカード間で分割されます。 詳細については、「[データ フォームのレイアウトについて](../working-with-form-layout.md)」を参照してください。

## <a name="additional-properties"></a>その他のプロパティ
**[BorderColor](properties-color-border.md)** – コントロールの境界線の色です。

**[BorderStyle](properties-color-border.md)** – コントロールの境界線を **Solid** (実線)、**Dashed** (破線)、**Dotted** (点線)、**None** (なし) のいずれに指定します。

**[BorderThickness](properties-color-border.md)** – コントロールの境界線の太さです。

**[Fill](properties-color-border.md)** – コントロールの背景色です。

**[Height](properties-size-location.md)** – コントロールの上端と下端の距離です。

**Valid** – **カード** または **[フォームの編集](control-form-detail.md)** コントロールに、データ ソースに送信する準備ができている有効なエントリが含まれているかどうかを指定します。

**[Visible](properties-core.md)** – コントロールを表示するか非表示にするかを指定します。

**[X](properties-size-location.md)** – コントロールの左端とその親コンテナー (親コンテナーがない場合は画面) の左端間の距離です。 複数の列を持つコンテナーの **[カード](control-card.md)** コントロールの場合、このプロパティは、カードが表示される列を決定します。

**[Y](properties-size-location.md)** – コントロールの上端とその親コンテナー (親コンテナーがない場合は画面) の上端間の距離です。 複数の行を持つコンテナーの **[カード](control-card.md)** コントロールの場合、このプロパティは、カードが表示される行を決定します。

## <a name="examples"></a>例
例については、「[データ カードについて](../working-with-cards.md)」と「[データ フォームのレイアウトについて](../working-with-form-layout.md)」を参照してください。


## <a name="accessibility-guidelines"></a>アクセシビリティのガイドライン
### <a name="color-contrast"></a>色のコントラスト
以下の間には適切な色のコントラストが必要です。
* **[Fill](properties-color-border.md)** とすべての子コントロール。 たとえば、カードに **[ラベル](control-text-box.md)** があり、ラベルの塗りつぶしが透明な場合、カードの **[Fill](properties-color-border.md)** は実質的にはラベルの背景色になります。 そのため、カードの **[Fill](properties-color-border.md)** とラベルの **[Color](properties-color-border.md)** の間には適切なコントラストが必要です。

### <a name="screen-reader-support"></a>スクリーン リーダーのサポート
* **DisplayName** が存在する必要があります。

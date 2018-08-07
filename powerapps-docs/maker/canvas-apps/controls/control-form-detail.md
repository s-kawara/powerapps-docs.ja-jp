---
title: '[Display form (フォームの表示)] コントロールと [Edit form (フォームの編集)] コントロール: リファレンス | Microsoft Docs'
description: プロパティや例など、[Display form (フォームの表示)] コントロールと [Edit form (フォームの編集)] コントロールに関する情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 07/06/2017
ms.author: gregli
ms.openlocfilehash: 6e34b107c9ad47b5eee7711f5c2b474eb3f1a836
ms.sourcegitcommit: 0f6d7bb9e524202c065b9a7ef92a7f54bdc4bc7c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/07/2018
ms.locfileid: "39017849"
---
# <a name="edit-form-and-display-form-controls-in-powerapps"></a>PowerApps の [Edit form (フォームの編集)] コントロールと [Display form (フォームの表示)] コントロール
データ ソースのレコードを表示、編集、および作成します。

## <a name="description"></a>説明
**[Display form (フォームの表示)]** コントロールを追加する場合、ユーザーはレコードのすべてのフィールド、または指定されたフィールドのみを表示できます。 **[Edit form (フォームの編集)]** コントロールを追加する場合、ユーザーはそれらのフィールドを編集したり、レコードを作成したり、変更をデータ ソースに保存したりできます。

![フォーム コントロールとフォーム ビュー コントロールの例](./media/control-form-detail/form-detail-intro.png)

**[[Gallery (ギャラリー)]](control-gallery.md)** コントロールを追加する場合、データ ソース内にテーブルを表示するようにコントロールを構成した後、ユーザーがギャラリーで選択したレコードを表示するようにフォームを構成することができます。 編集内容を保存したり、編集をキャンセルしたり、レコードを作成したりするためにユーザーが選択できる **[[Button (ボタン)]](control-button.md)** コントロールを 1 つ以上追加することもできます。 コントロールを組み合わせて使用することにより、[理想的なソリューションを作成](../working-with-forms.md)できます。

### <a name="record-selection"></a>レコードの選択
どちらのタイプのフォームでも、その **DataSource** プロパティをレコードのテーブルに設定し、そのテーブル内の特定のレコードを表示するようにフォームの **Item** プロパティを設定します。 たとえば、フォームの **Item** プロパティを、**[[Gallery (ギャラリー)]](control-gallery.md)** コントロールの **SelectedItem** プロパティに設定できます。 ユーザーがギャラリーでレコードを選択すると、そのレコードがフォームに表示されます。ただし、フォームに表示するフィールドは増やすことができます。 ユーザーがギャラリーに戻って別のレコードを選択すると、ギャラリーの **SelectedItem** プロパティが変化します。 この変更により、フォームの **Item** プロパティが更新され、新しく選択されたレコードがフォームに表示されます。

それぞれのフォーム コントロールには 1 つ以上の **[[Card (カード)]](control-card.md)** コントロールが含まれます。 カードの **[DataField](control-card.md)** プロパティを設定することにより、[カードに表示するフィールドとその他の詳細を指定](../add-form.md)します。

### <a name="create-a-record"></a>レコードを作成する
**[Edit form (フォームの編集)]** コントロールが **[Edit (編集)]** モードのとき、ユーザーは、フォームの **Item** プロパティで指定されたレコードを更新できます。 検査した場合、**Mode** プロパティは **Edit** を返します。

ただし、**[Edit form (フォームの編集)]** コントロールが **[New (新規)]** モードのとき、**Item** プロパティは無視されます。 フォームは既存のレコードを表示しません。代わりに、各フィールドの値は、フォームの構成時に使用したデータ ソースの既定値と一致します。 **[NewForm](../functions/function-form.md)** 関数を使用することで、フォームはこのモードに切り替わります。

たとえば、**[New (新規)]** を表示するようにボタンの **[Text](properties-core.md)** プロパティを設定し、その **[OnSelect](properties-core.md)** プロパティを **[NewForm](../functions/function-form.md)** 関数を含む数式に設定できます。 ユーザーがそのボタンを選択すると、フォームは **[New (新規)]** モードに切り替わり、ユーザーは既知の値で始まるレコードを作成できます。

**[ResetForm](../functions/function-form.md)** 関数が実行されるか、**[SubmitForm](../functions/function-form.md)** 関数が正常に実行された場合、フォームは **[Edit (編集)]** モードに戻ります。

* **[Cancel (キャンセル)]** を表示するようにボタンの **[Text](properties-core.md)** プロパティを設定し、その **[OnSelect](properties-core.md)** プロパティを **[ResetForm](../functions/function-form.md)** 関数を含む数式に設定できます。 ユーザーがそのボタンを選択すると、進行中の変更は破棄され、フォーム内の値は再びデータ ソースの既定値と一致します。
* **[Save changes (変更を保存)]** を表示するようにボタンの **[Text](properties-core.md)** プロパティを設定し、その **[OnSelect](properties-core.md)** プロパティを **[SubmitForm](../functions/function-form.md)** 関数を含む数式に設定できます。 ユーザーがそのボタンを選択し、データ ソースが更新されている場合、フォーム内の値はデータ ソースの既定値にリセットされます。

### <a name="save-changes"></a>変更を保存
既に説明したように **[Save changes (変更を保存)]** ボタンを作成する場合、ユーザーはレコードを作成または更新した後、そのボタンを選択して変更内容をデータ ソースに保存することができます。 代わりに、同じタスクを実行するように **[[Image (画像)]](control-image.md)** コントロールまたはその他のコントロールを構成できます (**[SubmitForm](../functions/function-form.md)** 関数でそのコントロールを構成する場合)。 いずれの場合も、**Error**、**ErrorKind**、**OnSuccess**、および **OnFailure** の各プロパティが結果についてのフィードバックを提供します。

**[SubmitForm](../functions/function-form.md)** 関数が実行されると、まず、ユーザーが送信しようとしているデータが検証されます。 必須のフィールドに値が含まれていないか、別の値がその他の制約に準拠していない場合、**ErrorKind** プロパティが設定され、**OnFailure** 式が実行されます。 データが有効である (つまり、フォームの **Valid** プロパティが **true** である) 場合にのみユーザーが選択できるよう、**[Save changes (変更を保存)]** ボタンまたはその他のコントロールを構成できます。 **Error** および **ErrorKind** プロパティをリセットするには、ユーザーは問題を修正するだけでなく、**[Save changes (変更を保存)]** ボタンをもう一度選択する (または、既に説明したように、**[Cancel (キャンセル)]** ボタンを選択して変更内容を破棄する) 必要もあることに注意してください。

データが検証に合格した場合、**[SubmitForm](../functions/function-form.md)** はデータをデータ ソースに送信しますが、ネットワークの遅延によっては少し時間がかかることがあります。

* 送信が成功した場合、**Error** プロパティはクリアされ、**ErrorKind** プロパティは **ErrorKind.None** に設定され、**OnSuccess** 式が実行されます。 ユーザーがレコードを作成した (つまり、フォームが以前は **[New (新規)]** モードだった) 場合、新しく作成されたレコードまたは別のレコードをユーザーが編集できるよう、フォームは **[Edit (編集)]** モードに切り替わります。
* 送信が失敗した場合、**Error** プロパティにはデータ ソースからの、問題を説明するユーザー向けのエラー メッセージが含まれます。 問題に応じて **ErrorKind** プロパティが適宜設定され、**OnFailure** 式が実行されます。

データ ソースによっては、2 人のユーザーが同じレコードを同時に更新しようとしたときにそのことを検出できます。この場合、**ErrorKind** は **ErrorKind.Conflict** に設定され、対応策は、もう一方のユーザーの変更でデータ ソースを更新し、このユーザーによって行われた変更を再適用することです。

> [!TIP]
> 進行中の変更をユーザーが破棄できるようにフォーム上に **[キャンセル]** ボタンを表示する場合、このボタンの **[OnSelect](properties-core.md)** プロパティに **[ResetForm](../functions/function-form.md)** 関数を追加します (このプロパティに、画面を変更するための **[Navigate](../functions/function-navigate.md)** 関数も含まれている場合でも)。 そのようにしないと、フォームはそのユーザーによる変更を保持します。

### <a name="layout"></a>レイアウト
既定では、カードは電話アプリでは 1 列に配置され、タブレット アプリでは 3 列に配置されます。 フォームを構成するときに、フォームの列の数と、カードを列にスナップするかどうかを指定できます。 これらの設定は、カードの **X**、**Y**、および **Width** プロパティを設定するときにだけ使用されるため、プロパティとして公開されません。

詳細については、「[データ フォームのレイアウトについて](../working-with-form-layout.md)」を参照してください。

## <a name="key-properties"></a>主要なプロパティ
**DataSource** – ユーザーが表示、編集、または作成するレコードが含まれるデータ ソース。

* このプロパティを設定しない場合、ユーザーはレコードを表示、編集、または作成できず、追加のメタデータまたは検証は提供されません。

**DefaultMode** -フォーム コントロールの最初のモード。  下記の **Mode** の説明で、使用可能な値と値の意味を確認してください。 

**DisplayMode** - フォーム コントロール内のデータ カードとコントロールでこのモードを使用します。  

**Mode** プロパティ ベースから派生しているため、個別には設定できません。

| モード | DisplayMode | 説明 |
| --- | --- | --- |
| **FormMode.Edit** |**DisplayMode.Edit** |データ カードとコントロールは編集可能で、レコードへの変更を受け入れる準備ができています。 |
| **FormMode.New** |**DisplayMode.Edit** |データ カードとコントロールは編集可能で、新しいレコードを受け入れる準備ができています。 |
| **FormMode.View** |**DisplayMode.View** |データ カードとコントロールは編集できず、表示に最適化されています。 |

**Error** – **[SubmitForm](../functions/function-form.md)** 関数が失敗したときにこのフォームに表示するユーザー向けのエラー メッセージ。

* このプロパティは **[Edit form (フォームの編集)]** コントロールのみに適用されます。
* このプロパティは、**[SubmitForm](../functions/function-form.md)**、**EditForm**、または **[ResetForm](../functions/function-form.md)** 関数の実行時にのみ変化します。
* エラーが発生しない場合、このプロパティは *空* であり、**ErrorKind** は **ErrorKind.None** に設定されます。
* 可能な場合、ユーザーの言語でエラー メッセージが返されます。 一部のエラー メッセージはデータ ソースから直接返され、ユーザーの言語ではない場合があります。

**ErrorKind** – **SubmitForm** の実行時にエラーが発生した場合、発生したエラーの種類。

* **[Edit form (フォームの編集)]** コントロールのみに適用されます。
* このプロパティには、**[Errors](../functions/function-errors.md)** 関数と同じ列挙があります。 **[Edit form (フォームの編集)]** コントロールは以下の値を返す可能性があります。

| ErrorKind | 説明 |
| --- | --- |
| **ErrorKind.Conflict** |別のユーザーが同じレコードを変更した結果、変更が競合しています。 **[Refresh](../functions/function-refresh.md)** 関数を実行してレコードを再読み込みし、変更をもう一度やり直してください。 |
| **ErrorKind.None** |不明な種類のエラーです。 |
| **ErrorKind.Sync** |データ ソースがエラーを報告しました。 詳細については、**Error** プロパティを確認してください。 |
| **ErrorKind.Validation** |一般的な検証の問題が検出されました。 |

**Item** – ユーザーが表示または編集する **DataSource** 内のレコード。

**LastSubmit** – 最後に正常に送信されたレコード。サーバーが生成したフィールドを含みます。

* このプロパティは **[Edit form (フォームの編集)]** コントロールのみに適用されます。
* 一意の番号を持つ **ID** フィールドなど、何らかのフィールドをデータ ソースが自動的に生成または計算する場合、**SubmitForm** が正常に実行された後、**LastSubmit** プロパティがこの新しい値になります。
* このプロパティの値は **OnSuccess** 式で利用できます。

**Mode** – コントロールは **[Edit (編集)]** または **[New (新規)]** モードです。

| モード | 説明 |
| --- | --- |
| **FormMode.Edit** |ユーザーはフォームを使用してレコードを編集できます。 フォームのカードの値は、ユーザーが変更する既存のレコードのものが事前設定されます。 **[SubmitForm](../functions/function-form.md)** 関数が正常に実行された場合、既存のレコードが変更されます。 |
| **FormMode.New** |ユーザーはフォームを使用してレコードを作成できます。 フォームのコントロールの値は、データ ソースのレコードの既定値が事前設定されます。 **[SubmitForm](../functions/function-form.md)** 関数が正常に実行された場合、レコードが作成されます。 |
| **FormMode.View** |ユーザーはフォームを使用してレコードを表示できます。 フォームのコントロールの値は、データ ソースのレコードの既定値が事前設定されます。 |

以下の変更のいずれかが発生すると、フォームは **[New (新規)]** モードから **[Edit (編集)]** モードに切り替わります。

* フォームが正常に送信され、レコードが作成されます。 この新しいレコードに自動で選択を移動するようギャラリーが設定されている場合、ユーザーが追加の変更を行えるよう、作成されたレコードに対してフォームは **[Edit (編集)]** モードになります。
* **[EditForm](../functions/function-form.md)** 関数が実行されます。
* **[ResetForm](../functions/function-form.md)** 関数が実行されます。 たとえば、この関数が構成されている **[Cancel (キャンセル)]** ボタンをユーザーが選択します。

**OnFailure** – データ操作が失敗したときのアプリの応答方法。

* このプロパティは **[Edit form (フォームの編集)]** コントロールのみに適用されます。

**OnReset** – **[Edit form (フォームの編集)]** コントロールがリセットされたときのアプリの応答方法。

* このプロパティは **[Edit form (フォームの編集)]** コントロールのみに適用されます。

**OnSuccess** – データ操作が成功したときのアプリの応答方法。

* このプロパティは **[Edit form (フォームの編集)]** コントロールのみに適用されます。

**Unsaved** – ユーザーによる未保存の変更が **[Edit form (フォームの編集)]** コントロールに含まれている場合は True。

* このプロパティは **[Edit form (フォームの編集)]** コントロールのみに適用されます。
* このプロパティを使用して、未保存の変更が失われる前にユーザーに警告します。  現在のレコードの変更を保存する前にユーザーが **[[Gallery (ギャラリー)]](control-gallery.md)** コントロールで別のレコードを選択することを防ぐには、ギャラリーの **[Disabled](properties-core.md)** プロパティを **Form.Unsaved** に設定した上で、更新操作を無効にします。

**Updates** – フォーム コントロールに読み込まれているレコードに対してデータ ソースに書き戻す値。  

* このプロパティは **[Edit form (フォームの編集)]** コントロールのみに適用されます。
* このプロパティを使用して、コントロール内部のカードからフィールド値を抽出します。  その後、これらの値を使用し、**[Patch](../functions/function-patch.md)** 関数呼び出し、または接続によって公開されている別のメソッドによってデータ ソースを手動で更新することができます。  **[SubmitForm](../functions/function-form.md)** 関数を使用している場合、このプロパティを使用する必要はありません。
* このプロパティは、値のレコードを返します。  たとえば、**[Name (名前)]** および **[Quantity (数量)]** フィールドに対するカード コントロールがフォーム コントロールに含まれており、それらのカードに対する **[Update](control-card.md)** プロパティの値がそれぞれ "Widget" および 10 を返す場合、フォーム コントロールに対する **Updates** プロパティは **{ Name: "Widget", Quantity: 10 }** を返します。

**Valid** – **[[Card (カード)]](control-card.md)** または **[フォームの編集 (Edit form)]** コントロールに有効なエントリが含まれており、データ ソースへの送信準備ができているかどうか。

* このプロパティは **[Edit form (フォームの編集)]** コントロールのみに適用されます。
* **[Form (フォーム)]** コントロールの **Valid** プロパティは、フォーム内のすべての **[[Card (カード)]](control-card.md)** コントロールの **Valid** プロパティを集約します。 フォームの **Valid** プロパティは、そのフォーム内のすべてのカードのデータが有効である場合にのみ **true** です。そうでない場合、フォームの **Valid** プロパティは **false** です。
* フォーム内のデータが有効だがまだ送信されていない場合にのみ、変更の保存をボタンで有効にするには、ボタンの **DisplayMode** プロパティを次の式に設定します。
  
    **SubmitButton.DisplayMode = If(IsBlank( Form.Error ) || Form.Valid, DisplayMode.Edit, DisplayMode.Disabled)**

## <a name="additional-properties"></a>その他のプロパティ
**[BorderColor](properties-color-border.md)** – コントロールの境界線の色です。

**[BorderStyle](properties-color-border.md)** – コントロールの境界線を **Solid** (実線)、**Dashed** (破線)、**Dotted** (点線)、**None** (なし) のいずれに指定します。

**[BorderThickness](properties-color-border.md)** – コントロールの境界線の太さです。

**[Fill](properties-color-border.md)** – コントロールの背景色です。

**[Height](properties-size-location.md)** – コントロールの上端と下端の距離です。

**[Visible](properties-core.md)** – コントロールを表示するか非表示にするかを指定します。

**[Width](properties-size-location.md)** – コントロールの左端と右端の間の距離です。

**[X](properties-size-location.md)** – コントロールの左端とその親コンテナー (親コンテナーがない場合は画面) の左端間の距離です。

**[Y](properties-size-location.md)** – コントロールの上端とその親コンテナー (親コンテナーがない場合は画面) の上端間の距離です。

## <a name="more-information"></a>詳細
フォームの動作の詳細については、「[データ フォームについて](../working-with-forms.md)」を参照してください。

## <a name="accessibility-guidelines"></a>アクセシビリティのガイドライン
### <a name="screen-reader-support"></a>スクリーン リーダーのサポート
* **[ラベル](control-text-box.md)** を使用して見出しをフォームに追加することを検討してください。

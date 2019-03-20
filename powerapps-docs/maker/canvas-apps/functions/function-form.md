---
title: EditForm 関数、NewForm 関数、SubmitForm 関数、ResetForm 関数、ViewForm 関数 | Microsoft Docs
description: 構文と例を含む PowerApps の EditForm 関数、NewForm 関数、SubmitForm 関数、ResetForm 関数、ViewForm 関数の参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 07/06/2017
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 930439325b60b60fefed18b66c22d9d4f97f55b7
ms.sourcegitcommit: 4db9c763455d141a7e1dd569a50c86bd9e50ebf0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2019
ms.locfileid: "57802103"
---
# <a name="editform-newform-submitform-resetform-and-viewform-functions-in-powerapps"></a>PowerApps の EditForm 関数、NewForm 関数、SubmitForm 関数、ResetForm 関数、ViewForm 関数
**[編集フォーム](../controls/control-form-detail.md)** コントロールで、項目の表示、編集、または作成、内容の保存、コントロールのリセットを行います。

## <a name="overview"></a>概要
これらの関数は**編集フォーム** コントロールの状態を変更します。  フォーム コントロールは、次のモードのいずれかにあります。

| モード | 説明 |
| --- | --- |
| **FormMode.Edit** |フォームは既存のレコードに設定され、ユーザーはフィールドの値を変更できます。  完了すると、ユーザーはレコードに変更を保存できます。 |
| **FormMode.New** |フォームは既定の値で設定され、ユーザーはフィールドの値を変更できます。  完了すると、ユーザーはレコードをデータ ソースに追加できます。 |
| **FormMode.View** |フォームは既存のレコードに設定されますが、ユーザーはフィールドの値を変更できません。 |

## <a name="description"></a>説明
これらの関数は多くの場合、ユーザーが編集内容の保存、編集内容の破棄、またはレコードの作成を行えるようにするために、**[ボタン](../controls/control-button.md)** コントロールまたは**[イメージ](../controls/control-image.md)** コントロールの **[OnSelect](../controls/properties-core.md)** 数式から呼び出されます。 [コントロールとこれらの関数を組み合わせて](../working-with-forms.md)、理想的なソリューションを作成することができます。

これらの関数は値を返しません。

### <a name="submitform"></a>SubmitForm
ボタン コントロールの **[OnSelect](../controls/properties-core.md)** プロパティで **SubmitForm** 関数を使用して、フォーム コントロール内の変更内容をデータ ソースに保存します。

この関数では、変更が送信される前に妥当性の問題がチェックされます。これは必須の印が付いたフィールド、または値に対する 1 つ以上の制約があるフィールドに関して実行されます。 この動作は、**[Validate](function-validate.md)** 関数の動作と同じです。

**SubmitForm** ではフォームの **[Valid](../controls/control-form-detail.md)** プロパティもチェックされます。これは、フォーム コントロールに含まれている**[カード](../controls/control-card.md)** コントロールのすべての **[Valid](../controls/control-card.md)** プロパティが集計されたものです。 問題が発生した場合、データは送信されず、それに応じてフォーム コントロールの **[Error](../controls/control-form-detail.md)** プロパティと **[ErrorKind](../controls/control-form-detail.md)** プロパティが設定されます。

妥当性に問題がない場合、**SubmitForm** によって変更内容がデータ ソースに送信されます。

* 送信が成功した場合、フォームの **[OnSuccess](../controls/control-form-detail.md)** 動作が実行され、**[Error](../controls/control-form-detail.md)** プロパティと **[ErrorKind](../controls/control-form-detail.md)** プロパティがクリアされます。  フォームが **FormMode.New** モードだった場合は **FormMode.Edit** モードに戻ります。
* 送信が成功しなかった場合、フォームの **[OnFailure](../controls/control-form-detail.md)** 動作が実行され、それに応じて **[Error](../controls/control-form-detail.md)** プロパティと **[ErrorKind](../controls/control-form-detail.md)** プロパティが設定されます。  フォームのモードはそのままです。  

### <a name="editform"></a>EditForm
**EditForm** 関数では、フォーム コントロールのモードが **FormMode.Edit** に変更されます。 このモードでは、フォーム コントロールの **[Item](../controls/control-form-detail.md)** プロパティの内容がフォームの入力に使用されます。  フォームがこのモードのときに **SubmitForm** 関数が実行されると、レコードの作成ではなく変更が行われます。  **FormMode.Edit** は、フォーム コントロールの既定のモードです。

### <a name="newform"></a>NewForm
**NewForm** 関数では、フォーム コントロールのモードが **FormMode.New** に変更されます。 このモードでは、フォーム コントロールの **[Item](../controls/control-form-detail.md)** プロパティの内容が無視され、フォームの **[DataSource](../controls/control-form-detail.md)** プロパティの既定値がフォームに入力されます。 フォームがこのモードのときに **SubmitForm** 関数が実行されると、レコードの変更ではなく作成が行われます。

### <a name="resetform"></a>ResetForm
**ResetForm** 関数では、ユーザーが変更を行う前に、フォームの内容が初期値にリセットされます。 フォームのモードが **FormMode.New** である場合は **FormMode.Edit** にリセットされます。 さらに、フォーム コントロールの **[OnReset](../controls/control-form-detail.md)** 動作も実行されます。  **[Reset](function-reset.md)** 関数を使用して個々のコントロールをリセットすることもできますが、使用できるのはそのフォーム内のみです。

### <a name="viewform"></a>ViewForm
**ViewForm** 関数を使用すると、フォーム コントロールのモードが **FormMode.View** に変更されます。 このモードでは、フォーム コントロールの **[Item](../controls/control-form-detail.md)** プロパティの内容がフォームの入力に使用されます。  **SubmitForm**と**ResetForm**このモードでの関数の影響がありません。

### <a name="displaymode-property"></a>DisplayMode プロパティ
**Mode** プロパティを介して、現在のモードを読み取ることができます。  また、このモードは **DisplayMode** プロパティの値を決定し、この値をフォーム コントロール内のデータ カードとコントロールで使用できます。  多くの場合、データ カードの**DisplayMode**プロパティに設定する**Parent.DisplayMode** (フォームを参照) は、コントロールの**DisplayMode**プロパティ (を参照します。データ カード) で: 

| モード | DisplayMode | 説明 |
| --- | --- | --- |
| **FormMode.Edit** |**DisplayMode.Edit** |データ カードとコントロールは編集可能で、レコードへの変更を受け入れる準備ができています。 |
| **FormMode.New** |**DisplayMode.Edit** |データ カードとコントロールは編集可能で、新しいレコードを受け入れる準備ができています。 |
| **FormMode.View** |**DisplayMode.View** |データ カードとコントロールは編集できず、表示に最適化されています。 |

## <a name="syntax"></a>構文
**SubmitForm**( *FormName* )

* *FormName* - 必須。 データ ソースに送信するフォーム コントロール。

**EditForm**( *FormName* )

* *FormName* - 必須。  **FormMode.Edit** モードに切り替えるフォーム コントロール。

**NewForm**( *FormName* )

* *FormName* - 必須。 **FormMode.New** モードに切り替えるフォーム コントロール。

**ResetForm**( *FormName* )

* *FormName* - 必須。 初期値にリセットするフォーム コントロール。 さらに、フォームのモードを **FormMode.New** から **FormMode.Edit** に切り替えます。

**ViewForm**( *FormName* )

* *FormName* - 必須。  **FormMode.View** モードに切り替えるフォーム コントロール。

## <a name="examples"></a>例
完全な例については、[データ フォーム](../working-with-forms.md)についての記事を参照してください。

1. ボタン コントロールを追加して、**Save** と表示されるように **[Text](../controls/properties-core.md)** プロパティを設定し、**[OnSelect](../controls/properties-core.md)** プロパティを次の式に設定します。
   
    **SubmitForm( EditForm )**
2. フォーム コントロールの **[OnFailure](../controls/control-form-detail.md)** プロパティを空白に設定し、その **[OnSuccess](../controls/control-form-detail.md)** プロパティを次の数式に設定します。
   
    **Back()**
3. **[ラベル](../controls/control-text-box.md)** コントロールに **ErrorText** という名前を付けて、**[Text](../controls/properties-core.md)** プロパティを次の数式に設定します。
   
    **EditForm.Error**
   
    ユーザーが **[Save]** ボタンを選択すると、フォーム コントロール内の変更内容が、基盤となるデータ ソースに送信されます。
   
   * 送信が成功すると、変更が保存されます。または、フォーム コントールが **New** モードの場合、レコードが作成されます。 **ErrorText** が "*空白*" の場合、前の画面がもう一度表示されます。
   * 送信が失敗すると、**ErrorText** にわかりやすいエラー メッセージが表示されます。ユーザーが問題を修正してやり直せるように、現在の画面は表示されたままになります。
4. ボタン コントロールを追加して、**Cancel** と表示されるように **[Text](../controls/properties-core.md)** プロパティを設定し、**[OnSelect](../controls/properties-core.md)** プロパティを次の式に設定します。
   
    **ResetForm( EditForm ); Back()**
   
    ユーザーが **[Cancel]** ボタンを選択すると、フォーム コントロールの値が編集を開始する前の値にリセットされ、前の画面が再度表示されます。また、フォーム コントロールのモードが **New** だった場合、**Edit** に戻ります。
5. ボタン コントロールを追加して、**New** と表示されるように **[Text](../controls/properties-core.md)** プロパティを設定し、**[OnSelect](../controls/properties-core.md)** プロパティを次の式に設定します。
   
    **NewForm( EditForm ); Navigate( EditScreen, None )**
   
    ユーザーが **New** ボタンを選択すると、フォーム コントロールは **New** モードに切り替わります。フォーム コントロールのデータ ソースの既定値がそのコントロールに入力されて、フォーム コントロールが含まれた画面が表示されます。 **SubmitForm** 関数が実行されると、レコードの更新ではなく作成が行われます。


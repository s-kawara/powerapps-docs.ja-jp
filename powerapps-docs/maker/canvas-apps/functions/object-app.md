---
title: アプリ オブジェクト |Microsoft Docs
description: 構文と例については、PowerApps でアプリ オブジェクトを含む参照情報
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 05/29/2019
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 232accd1050fb84816e86ea95069b8c8778f6586
ms.sourcegitcommit: 562c7ed5fbb116be1cbb0f45e3f6e75e3e4cf011
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/31/2019
ms.locfileid: "66451612"
---
# <a name="app-object-in-powerapps"></a>PowerApps でアプリ オブジェクト

現在実行中のアプリとアプリの動作の制御に関する情報を提供します。

## <a name="description"></a>説明

などのコントロールを**アプリ**オブジェクトのプロパティを指定する画面が表示されていると、紛失していないため、変更を保存するユーザー入力が求めを提供します。 すべてのアプリが、**アプリ**オブジェクト。

一部のプロパティの数式を記述する、**アプリ**オブジェクト。 上部にある、**ツリー ビュー**ペインで、**アプリ**するとしては、他の制御や画面のオブジェクトします。 表示し、数式バーの左側のドロップダウン リストで選択して、オブジェクトのプロパティのいずれかを編集します。

> [!div class="mx-imgBorder"]
> ![ツリー ビュー ペインで、アプリケーション オブジェクト](media/object-app/appobject.png)

## <a name="activescreen-property"></a>ActiveScreen プロパティ

**ActiveScreen**プロパティが表示されている画面を識別します。

このプロパティは、画面のプロパティを参照または別の画面にどの画面が表示されているかを判断する比較に使用できる画面オブジェクトを返します。 式を使用することもできます。 **App.ActiveScreen.Name**表示されている画面の名前を取得します。

使用して、 **[戻る](function-navigate.md)** または **[Navigate](function-navigate.md)** 表示されている画面を変更する関数。

## <a name="onstart-property"></a>OnStart プロパティ

**OnStart**プロパティが、ユーザーにアプリを起動するときに実行します。 アプリの作成者は、このプロパティを使用してこれらのタスクを実行する多くの場合。

- 取得しを使用してコレクションにデータをキャッシュ、 **[収集](function-clear-collect-clearcollect.md)** 関数。
- 使用して、グローバル変数を設定、 **[設定](function-set.md)** 関数。
- 使用して最初の画面に移動、 **[Navigate](function-navigate.md)** 関数。

最初の画面が表示されるまでは、次の数式が評価されます。 画面が読み込まれていない、コンテキスト変数を設定することはできませんので、 **[UpdateContext](function-updatecontext.md)** 関数。 ただし、コンテキスト変数を渡すことができます、 **Navigate**関数。

変更した後、 **OnStart**プロパティ、テストを置くことによって、**アプリ**オブジェクト、**ツリー ビュー**ペインが表示されたら、省略記号 (...) を選択すると、および順に選択**実行 OnStart**します。 異なり、アプリが初めて読み込まれるときに、既存のコレクションおよび変数は既に設定されます。 最初に空のコレクションを使用して、 **[ClearCollect](function-clear-collect-clearcollect.md)** 関数の代わりに、**収集**関数。

> [!div class="mx-imgBorder"]
> ![OnStart の実行のアプリ-項目のショートカット メニュー](media/object-app/appobject-runonstart.png)

## <a name="confirmexit-properties"></a>ConfirmExit プロパティ

だれも望まない未保存の変更が失われます。 使用して、 **ConfirmExit**と**ConfirmExitMessage**プロパティをアプリを閉じる前に、ユーザーに警告します。

> [!NOTE]
> **ConfirmExit**などに、埋め込まれているアプリで Power BI と SharePoint は機能しません。

> [!NOTE]
> 現時点では、これらのプロパティを参照できるだけの最初の画面上のコントロール場合、**遅延読み込み**(新しいアプリの既定値である) のプレビュー機能を有効にします。 参照が行われた場合、PowerApps Studio が、エラーに表示されませんが、結果として発行されたアプリが PowerApps Mobile またはブラウザーで表示されません。 この制限の解消に取り組んでいるところアクティブにします。 オフにする一方、**遅延読み込み**で**ファイル** > **アプリ設定** > **詳細設定**(**プレビュー機能**)。

### <a name="confirmexit"></a>ConfirmExit

**ConfirmExit**ブール型プロパティは、するときに、 *true*アプリを閉じる前に確認のダイアログ ボックスが開きます。 このプロパティは、既定では、 *false*、ダイアログ ボックスは表示されません。

このプロパティを使用して、確認のダイアログ ボックスを表示するかどうか、ユーザーが変更したが、保存されていません。 変数を確認したり、プロパティを制御する式を使用して (たとえば、 **Unsaved**のプロパティ、 [**編集フォーム**](../controls/control-form-detail.md)コントロール)。

どのような状況のデータが失われ、これらの例のようになりますで、確認のダイアログ ボックスが表示されます。

- 実行している、 [**終了**](function-exit.md)関数。
- ブラウザーでアプリを実行すると: 場合
  - ブラウザーまたはアプリが実行されているブラウザー タブを閉じています。
  - ブラウザーの戻るボタンを選択します。
- アプリが PowerApps Mobile (iOS または Android) で実行されている: 場合
  - 実行している、 [**起動**](function-param.md)関数。<br>**起動**関数別のタブが開き、データが失われないため、ダイアログ ボックスのブラウザーでは発生しません。
  - PowerApps Mobile のさまざまなアプリに切り替えにスワイプします。
  - Android デバイスで [戻る] ボタンを選択します。

確認のダイアログ ボックスの正確な外観は、デバイスと PowerApps のバージョン間で異なる場合があります。

確認のダイアログ ボックスは、PowerApps Studio に表示されません。

### <a name="confirmexitmessage"></a>ConfirmExitMessage

既定では、確認のダイアログ ボックスなどを示します、一般的なメッセージ、 **「が未保存の変更」。** ユーザーの言語。

使用**ConfirmExitMessage**確認のダイアログ ボックスでカスタム メッセージを指定します。 このプロパティは、する場合*空白*既定値が使用します。 カスタムのメッセージは、確認のダイアログ ボックス内に収まるため、メッセージをいくつかの行に最大で必要に応じて切り捨てられます。

ブラウザーで、確認のダイアログ ボックスは、ブラウザーから、一般的なメッセージに表示可能性があります。

### <a name="example"></a>例

1. 2 つのフォーム コントロールを含むアプリを作成**AccountForm**と**ContactForm**します。

1. 設定、**アプリ**オブジェクトの**ConfirmExit**プロパティをこの式に。

    ```powerapps-dot
    AccountForm.Unsaved Or ContactForm.Unsaved
    ```

    ユーザーのいずれかの形式のデータを変更し、それらの変更を保存せず、アプリを閉じるにはしようとする場合、このダイアログ ボックスが表示されます。

    > [!div class="mx-imgBorder"]
    > ![汎用的な確認のダイアログ ボックス](media/object-app/confirm-native.png)

1. 設定、**アプリ**オブジェクトの**ConfirmExitMessage**に次の式のプロパティ。

    ```powerapps-dot
    If( AccountsForm.Unsaved,
        "Accounts form has unsaved changes.",
        "Contacts form has unsaved changes."
    )
    ```

    ユーザー アカウントのフォームのデータを変更し、それらの変更を保存せず、アプリを閉じるにはしようとする場合、このダイアログ ボックスが表示されます。

    > [!div class="mx-imgBorder"]
    > ![フォームに固有の確認のダイアログ ボックス](media/object-app/confirm-native-custom.png)

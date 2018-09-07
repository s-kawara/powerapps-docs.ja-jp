---
title: データ カードについて | Microsoft Docs
description: PowerApps で、フォーム カードを使用して、データ ソースから情報を収集して表示します。
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 04/26/2016
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: db0e42a45af217e9e5703242c2a5a867a52b687b
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "42850532"
---
# <a name="understand-data-cards-in-powerapps"></a>PowerApps のデータ カードについて

**[カード](controls/control-card.md)** コントロールは、キャンバス アプリの**[編集フォーム](controls/control-form-detail.md)** コントロールと**[表示フォーム](controls/control-form-detail.md)** コントロールの構成要素です。 フォームはレコード全体を表し、各カードはそのレコードの 1 つのフィールドを表します。

デザイン ワークスペースでフォーム コントロールを選択すると、右側のウィンドウでのカード操作が非常に簡単になります。 そのウィンドウでは、表示するフィールド、各フィールドの表示方法、表示の順序を選択できます。 この例では、SharePoint リストから作成し、**Assets** という名前を付けたアプリの**編集フォーム** コントロールを示しています。

![最初の画面](./media/working-with-cards/first-screen.png)

カードを使用するにあたり、[フォームの追加](add-form.md)に関するページと[データ フォーム](working-with-forms.md)に関するページを参照してください。 このトピックの残りの部分では、カードのしくみ、カスタマイズ方法、作成方法について詳しく説明します。

## <a name="predefined-cards"></a>定義済みのカード

PowerApps には、文字列、数値、その他のデータ型用の定義済みのカードのセットが用意されています。 右側のウィンドウでは、使用できるバリエーションを確認したり、フィールドに使用するカードを変更したりできます。

![](./media/working-with-cards/selected-card.png)

この例では単一行テキストのカードが選択されていますが、URL のテキストが長すぎて 1 行に表示できなくなっています。 これを、ユーザーが編集するのに十分な広さがある、複数行テキストのカードに変更してみましょう。

![](./media/working-with-cards/multiline-edit.png)

このデータ ソースの複数のフィールドが表示されていませんが、フィールドのチェック ボックスを選択することで表示したり非表示にしたりできます。 この例では **SecurityCode** フィールドについて説明します。

![](./media/working-with-cards/add-security-code.png)

## <a name="customize-a-card"></a>カードをカスタマイズ
カードには、他のコントロールが含まれます。 **編集フォーム** コントロールで、**[挿入]** タブから追加する標準の **[テキスト入力](controls/control-text-input.md)** コントロールにデータを入力します。  

カードのコントロールを操作して、その見た目を変更する方法の例を見てみましょう。

1. 最初に、**SecurityCode** フィールド用に最後に挿入したカードに戻ります。 このカードをクリックするか 1 回タップして選択します。
   
    ![](./media/working-with-cards/select-security-code.png)
2. カード内の**[テキスト入力](controls/control-text-input.md)** コントロールをクリックまたはタップして選択します。
   
    ![](./media/working-with-cards/select-text-input.png)
3. 選択ボックスをドラッグして、カード内でこのコントロールを移動します。さらに、選択ボックスの枠上のハンドルをドラッグして、コントロールのサイズを変更します。
   
    ![](./media/working-with-cards/customize-text-input.png)  

カード内のコントロールに対しては、サイズ変更、移動、その他の変更操作を実行できます。ただし、このコントロールを削除するには、最初にロックを解除する必要があります。

## <a name="unlock-a-card"></a>カードのロックを解除
包含するコントロールに加えて、カード自体も、他のコントロールと同様に、プロパティと数式を備えたコントロールです。 フォームにフィールドを表示することを選択すると、右側のウィンドウで自動的にカードが作成され、必要な数式が生成されます。  これらの数式は右側のウィンドウの **[詳細設定]** タブで確認できます。

![](./media/working-with-cards/advanced-locked.png)

ここには、カードの最も重要なプロパティの 1 つである **[DataField](controls/control-card.md)** プロパティが表示されています。 このプロパティは、データ ソースのどのフィールドがこのカードに表示され、ユーザーが編集できるかを示します。  

**[詳細設定]** タブの上部にあるバナーは、このカードのプロパティがロックされていることを示します。 **[DataField](controls/control-card.md)**、**[DisplayName](controls/control-card.md)**、**[Required](controls/control-card.md)** の各プロパティの横にも錠アイコンが表示されます。 これらの数式は右ウィンドウで自動的に作成されたもので、これらのプロパティが誤って変更されるのを防ぐためにロックされています。

![](./media/working-with-cards/lock-icons.png)

上部のバナーをクリックまたはタップしてカードのロックを解除すると、これらのプロパティを変更できます。

![](./media/working-with-cards/unlocked-card.png)

ここでは、**[DisplayName](controls/control-card.md)** を変更して、**Asset** と **ID** の間にスペースを挿入します。 この変更を行うことで、自動的に生成された値が変更されます。  右側のウィンドウで、このカードに異なるラベルが設定されています。

![](./media/working-with-cards/change-display-name.png)

これでこのカードを管理できるようになりました。必要に応じてさらに修正を行えます。 しかし、先ほどのようにカードをある表現から別の表現に (たとえば、単一行のテキストから複数行のテキストに) 変更することはできません。 それは、あらかじめ定義されたカードを、管理できる "カスタム カード" に変換したためです。  

> [!IMPORTANT]
> ロックを解除した場合、カードをもう一度ロックすることはできません。 カードをロック状態に戻すには、カードを削除し、右側のウィンドウにもう一度挿入します。

カード内のコントロールの追加や削除などのさまざまな方法を使用して、ロックを解除したカードの見た目や動作を変更できます。 たとえば、**[挿入]** タブの **[アイコン]** メニューから星の図形を追加できます。

![](./media/working-with-cards/add-star.png)

これで、星がカードの一部になり、フォーム内でカードの順序を変更した場合にこのコントロールもカードと共に移動するようになります。

もう 1 つの例として、**ImageURL** カードのロックを解除し、次に **[挿入]** タブから **画像**コントロールを追加してみます。

![](./media/working-with-cards/add-image.png)

数式バーで、このコントロールの **Image** プロパティを *TextBox*.**Text** に設定します。ここで、*TextBox* は URL を保持する**テキスト入力**コントロールの名前です。

> [!TIP]
> Alt キーを押すと、各コントロールの名前が表示されます。

![](./media/working-with-cards/show-image.png)

画像が表示され、その URL を編集することができます。 **Parent.Default** を **Image** プロパティとして使用することもできましたが、その場合はユーザーが URL を変更しても画像が更新されません。

このアプリの 2 番目の画面でも同じ作業を行えます。ここでは、**表示フォーム** コントロールを使用して、レコードの詳細を表示します。 ここでは、ユーザーがこの画面で URL を編集できないように、ラベルを非表示にします (カードではなくラベルの **Visible** プロパティを **false** に設定します)。

![](./media/working-with-cards/show-image-display.png)

## <a name="interact-with-a-form"></a>フォームの操作
カードのロックを解除すると、カードとそこに含まれるフォームとの間の操作方法を変更できます。

コントロールがカードとどのように連携する必要があるか、およびカードがフォームとどのように連携する必要があるかに関するいくつかのガイドラインを次に示します。 これらはガイドラインにすぎません。 PowerApps の他のコントロールと同様に、PowerApps の他のコントロールを参照する数式を作成できます。これは、カードとカード内のコントロールにも当てはまります。 創造力を生かして、さまざまな方法でアプリを作成できます。  

### <a name="datafield-property"></a>DataField プロパティ
カードで最も重要なプロパティは **[DataField](controls/control-card.md)** プロパティです。  このプロパティは、検証、更新されるフィールド、カードのその他の側面に作用します。

### <a name="information-flowing-in"></a>入力される情報
フォームは、コンテナーとして、**ThisItem** をそこに含まれるすべてのカードで利用できるようにします。 このレコードには、現在対象になっているレコードのすべてのフィールドが含まれます。  

すべてのカードの **[Default](controls/properties-core.md)** プロパティを **ThisItem**.*FieldName* に設定する必要があります。  特定の状況下では、この値を途中の段階で変換することができます。 たとえば、文字列の書式を設定したり、ある言語の値を別の言語に変換したりできます。

カード内の各コントロールでは、**Parent.Default** を参照してフィールドの値を取得する必要があります。 これによりある程度のカードのカプセル化が提供されるため、カードの内部数式を変更することなく、カードの **[Default](controls/properties-core.md)** プロパティを変更できます。

既定では、**[DataField](controls/control-card.md)** プロパティに基づいて、**DefaultValue** プロパティと **[Required](controls/control-card.md)** プロパティがデータ ソースのメタデータから取得されます。 これらの数式を独自のロジックでオーバーライドし、**[DataSourceInfo](functions/function-datasourceinfo.md)** 関数を使用してデータ ソースのメタデータを統合することができます。

### <a name="information-flowing-out"></a>出力される情報
ユーザーによってカード内のコントロールが使用され、レコードが変更されたら、**[SubmitForm](functions/function-form.md)** 関数を使用してこれらの変更をデータ ソースに保存します。 この関数が実行されると、フォーム コントロールは、変更するフィールドを識別するために各カードの **[DataField](controls/control-card.md)** プロパティの値を読み取ります。  

フォーム コントロールは、各カードの **[Update](controls/control-card.md)** プロパティの値も読み取ります。 この値は、このフィールドのデータ ソースに格納されます。 ここは、カードの **[Default](controls/properties-core.md)** の数式で適用された変換を反転するなど、別の変換を適用するための場所です。

**Valid** プロパティは、**[DataField](controls/control-card.md)** プロパティに基づいて、データ ソースのメタデータから設定されます。 また、**[Required](controls/control-card.md)** プロパティと、**[Update](controls/control-card.md)** プロパティに値が含まれているかどうかにも基づきます。 **[Update](controls/control-card.md)** プロパティの値が有効でない場合、**Error** プロパティはユーザー フレンドリなエラー メッセージを提供します。

カードの **[DataField](controls/control-card.md)** プロパティが "*空白*" の場合、カードは単にコントロールのコンテナーです。 フォームを送信するとき、その **Valid** プロパティと **[Update](controls/control-card.md)** プロパティは関与しません。

## <a name="dissecting-an-example"></a>例の解説
ここでは、基本的なデータ入力カードを構成するコントロールについて見ていきます。 各コントロールが見えやすいように、コントロール間のスペースが増やされています。

![](./media/working-with-cards/dissect-card1.png)

Alt キーを押したままにすると、このカードを構成するコントロールの名前が表示されます。

![](./media/working-with-cards/dissect-card2.png)

このカードは、次の 4 つのコントロールで構成されています。

| 名前 | 種類 | 説明 |
| --- | --- | --- |
| **TextRequiredStar** |**[ラベル](controls/control-text-box.md)** コントロール |星印を表示します。この印は、データ入力フォームで必須フィールドを示すためによく使用されます。 |
| **TextFieldDisplayName** |**[ラベル](controls/control-text-box.md)** コントロール |このフィールドのユーザー フレンドリ名を表示します。 この名前は、データ ソースのスキーマに含まれる名前と同じである必要はありません。 |
| **InputText** |**入力テキスト** コントロール |フィールドの初期値を表示します。ユーザーは、この値を変更できます。 |
| **TextErrorMessage** |**[ラベル](controls/control-text-box.md)** コントロール |検証で問題が発生した場合、ユーザー フレンドリなエラー メッセージをユーザーに表示します。 また、必須フィールドにおいて値が入力されることを保証します。 |

これらのコントロールにデータを入力するために、これらの重要な数式を使用して、そのプロパティをカードのプロパティから設定することができます。 これらの数式のいずれも特定のフィールドを参照していないことに注意してください。 代わりに、すべての情報がカードから取得されます。

| コントロールのプロパティ | 数式 | 説明 |
| --- | --- | --- |
| **TextRequiredStar.Visible** |**Parent.Required** |星印は、フィールドが必須フィールドの場合にのみ表示されます。 Required は、開発者またはデータ ソースのメタデータによって設定される数式です。 |
| **TextFieldDisplayName.Text** |**Parent.DisplayName** |このテキスト ボックス コントロールには、ユーザー フレンドリ名が表示されます。ユーザー フレンドリ名は、開発者またはデータ ソースのメタデータから提供され、カードの **[DisplayName](controls/control-card.md)** プロパティに設定されます。 |
| **InputText.Default** |**Parent.Default** |このテキスト入力コントロールに最初に表示される値は、カードの既定値によって提供されるデータ ソースのフィールドの値です。 |
| **TextErrorMessage.Text** |**Parent.Error** |検証で問題が発生した場合、カードの **Error** プロパティによって適切なエラー メッセージが提供されます。 |

これらのコントロールから情報を取得し、データ ソースにプッシュ転送するための重要な数式として、次の数式があります。

| コントロール名 | 数式 | 説明 |
| --- | --- | --- |
| **DataCard.DataField** |**"ApproverEmail"** |このカードでユーザーが表示して編集できるフィールドの名前。 |
| **DataCard.Update** |**InputText.Text** |**[SubmitForm](functions/function-form.md)** が実行されたときに検証され、データ ソースにプッシュ転送される値。 |


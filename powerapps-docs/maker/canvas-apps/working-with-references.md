---
title: レコードの参照とポリモーフィックな参照を理解する |Microsoft Docs
description: レコードの参照およびキャンバス アプリでの参照にポリモーフィックな動作します。
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 05/05/2019
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 99024b447841668bd887571a269c2fb14f5f5289
ms.sourcegitcommit: f6c9e525130a03b8c76f0a4b4e90419604c5823c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/10/2019
ms.locfileid: "65527091"
---
# <a name="understand-record-references-and-polymorphic-lookups-in-canvas-apps"></a>レコードの参照とキャンバス アプリでの参照にポリモーフィックを理解します。

学校で研究論文を記述したときにおそらく最後に、参照の一覧を提供します。 元のソースをだれかが追跡可能性がありますように web リンクではなく、書籍のタイトル、作成者、またはその他の情報が使用して、実際の背景情報のコピーが含まれていません。 1 つのリスト内のそれぞれに独自具体的な詳細を正しく引用、オーディオ録音の横にある新聞記事ソースのさまざまな種類が混在しています。 多くの場合、Wikipedia の記事は、たとえば、[参照の一覧が長い](https://en.wikipedia.org/wiki/Microsoft#References)します。

キャンバス アプリでは、通常のデータ ソースからダウンロードしたレコードのコピーで作業をします。 使用する、 [**ルックアップ**](functions/function-filter-lookup.md)と[**フィルター** ](functions/function-filter-lookup.md)関数と[**ギャラリー** ](controls/control-gallery.md)コントロールの**選択**プロパティを対象となる特定のレコードを識別します。 すべてのレコードを**フィルター**または**選択**簡単なフィールドを使用できるように、同じエンティティ型になります *。フィールド*表記します。 これらのコピーは、使用できるように多くの場合、参照情報を含める、 [**パッチ**](functions/function-patch.md)を元のソースを更新する関数。

キャンバス アプリをサポートしても*の参照を記録*します。 はるか研究論文の参照などの完全なコピーを含めずにレコードの参照は、レコードを指します。 このような参照は、任意のエンティティにレコードを参照できます。  研究論文の参照のようには、1 つの列内の別のエンティティからレコードを混在させることできます。

多くの操作レコードの参照では、レコードの操作と同じです。 相互に完全なレコードをレコードの参照を比較することができます。 レコードの参照の値を設定することができます、**パッチ**と完全なレコードの参照と同様に機能します。

1 つの重要な相違がある。 参照しているエンティティを 1 つのレコードの参照フィールドを直接アクセスすることはできません。 これは、キャンバス アプリでは、数式を記述するときにすべての種類が認識される必要があるためにです。 アプリが実行されるまで、レコードの参照の型がわからないため、単純なものは使用できません。*フィールド*直接表記します。 持つエンティティ型を動的に決定する必要があります最初、 [ **IsType** ](functions/function-astype-istype.md)関数を使用しています *。フィールド*表記の結果に、 [ **AsType** ](functions/function-astype-istype.md)関数。

*エンティティ型*エンティティ内の各レコードのスキーマを参照します。 各エンティティには、別の名前とデータ型のフィールドの一意のセットがあります。 エンティティの各レコードは、その構造体を継承します。2 つのレコードは、同じエンティティから来た場合、同じエンティティ型があります。

## <a name="polymorphic-lookups"></a>ポリモーフィックな参照

Common Data Service では、レコード間の関係をサポートします。 内の各レコード、**アカウント**エンティティには、**主要連絡先**ルックアップ フィールド内のレコードを**連絡先**エンティティ。 内のレコードが、参照に参照できるだけ**連絡先**と答えると、レコードを参照できませんし、**チーム**エンティティ。 フィールドと常に把握するため細部が重要ですが、参照の使用可能ななります。

Common Data Service には、ポリモーフィックな参照は、すべてのエンティティ セット内のレコードに参照できますもサポートしています。 たとえば、**所有者**内のレコードにフィールドを参照できます、**ユーザー**エンティティまたは**チーム**エンティティ。 異なるレコードで同じのルックアップ フィールドは、さまざまなエンティティ内のレコードを参照してくださいでした。 この場合は、常にわからないなりますフィールド使用できます。  

キャンバスのレコードの参照は、共通のデータ サービスのポリモーフィックな参照を操作するために設計されました。 このコンテキストでは、2 つの概念の違いは、外部のレコードの参照を使用することもできます。

使用してこれらの概念を探索を開始する次のセクションで、**所有者**参照。

## <a name="show-the-fields-of-a-record-owner"></a>レコードの所有者のフィールドを表示します。

Common Data Service 内のすべてのエンティティが含まれています、**所有者**フィールド。 このフィールドを削除することはできません、追加することはできません、常に値が必要です。

内のフィールドを表示する、**アカウント**エンティティ。

1. 開いている[このサイト](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)します。
1. 左側のナビゲーション バーで、選択**データ** > **エンティティ**します。
1. エンティティの一覧で選択**アカウント**します。
1. 右上隅にある フィルター一覧を開きます (に設定されています**既定**既定)、し、**すべて**します。
1. スクロールして、**所有者**フィールドが表示されます。

> [!div class="mx-imgBorder"]
> ![アカウント エンティティの所有者 フィールド](media/working-with-references/owner-field.png)

このルックアップ フィールドがいずれかからレコードを参照できる、**チーム**エンティティまたは**ユーザー**エンティティ。 これらのエンティティ内のすべてのレコードのアクセス許可がある、**所有者**; に問題が発生する場合は、サポートされているロールを確認します。

次の図の単純なギャラリーを表示する**アカウント**、場所、**アカウント**エンティティがデータ ソースとしてアプリに追加されました。

> [!div class="mx-imgBorder"]
> ![ギャラリー コントロールに表示されるアカウント](media/working-with-references/accounts-gallery.png)

> [!IMPORTANT]
> このトピックでは、全体では、グラフィックスは、いくつかの名前と Common Data Service で出荷されるサンプル データの一部ではないその他の値を表示します。 手順が正確に特定の結果の制御を構成する方法を示しますが、お客様のエクスペリエンス、組織のデータは異なります。

ギャラリーに各アカウントの所有者を表示する式を使用していらっしゃるかもしれません**ThisItem.Owner.Name**します。 ただし、名前フィールド、**チーム**エンティティが**チーム名**、名前フィールドと、**ユーザー**エンティティが**フル_ネーム**します。 参照の種類は、アプリを実行するまで使用しているし、内のレコードの間で異なることが、アプリを知ることはできません、**アカウント**エンティティ。

この変動に対応する式が必要です。 エンティティの種類のデータ ソースを追加する必要もあります**所有者**可能性があります (この場合、**ユーザー**と**チーム**)。 アプリには、これらの 3 つのデータ ソースを追加します。

> [!div class="mx-imgBorder"]
> ![データ ペインで、アカウント、チーム、およびユーザーのエンティティ](media/working-with-references/accounts-datasources.png)

これらのデータ ソースを配置、次の数式を使用して、ユーザーまたはチームの名前を表示します。

```powerapps-dot
If( IsType( ThisItem.Owner, [@Teams] ),
    "Team: " & AsType( ThisItem.Owner, [@Teams] ).'Team Name',
    "User: " & AsType( ThisItem.Owner, [@Users] ).'Full Name' )
```

> [!div class="mx-imgBorder"]
> ![アカウントが表示される [所有者] フィールドでギャラリー コントロールの表示](media/working-with-references/accounts-displayowner.png)

この数式で、 **IsType**関数のテスト、**所有者**フィールドに対して、**チーム**エンティティ。 そのエンティティ型の場合、 **AsType**関数にキャスト、**チーム**レコード。 この時点でのすべてのフィールドにアクセスすることができます、**チーム**、エンティティを含む**チーム名**を使用して*します。フィールド*表記します。 場合**IsType**が判断した、**所有者**内のレコードがない、**チーム**、エンティティ内のレコードがそのフィールドにする必要があります、**ユーザー**エンティティのため**所有者**フィールドは必須です (することはできません*空白*)。

使用している、[グローバルの曖昧性除去演算子](functions/operators.md#disambiguation-operator)の **[@Teams]** と **[@Users]** グローバル エンティティ型を使用していることを確認します。 この場合、必要はありませんが、フォームすることを推奨します。 一対多のリレーションシップは、ギャラリーのレコードのスコープで多くの場合、競合し、この方法は、その混乱を回避できます。

レコードの参照のすべてのフィールドを使用する必要があります最初に使用する、 **AsType**関数を特定のエンティティ型にキャストします。 直接フィールドにアクセスすることはできません、**所有者**フィールド、システムが使用するエンティティの種類を認識しないためです。

**AsType**場合、関数がエラーを返します、**所有者**フィールドは、使用できるように要求されているエンティティ型に一致しない、 **IfError**関数を次の式を簡略化します。 まず、実験的な機能を有効に**数式レベル エラー管理**:

> [!div class="mx-imgBorder"]
> ![実験的なスイッチ数式レベル エラー管理を有効にするには](media/working-with-references/accounts-iferror.png)

これと前の公式を置き換えます。

```powerapps-dot
IfError(
    "Team: " & AsType( ThisItem.Owner, [@Teams] ).'Team Name',
    "User: " & AsType( ThisItem.Owner, [@Users] ).'Full Name' )
```

## <a name="filter-based-on-an-owner"></a>所有者に基づくフィルター処理します。

おめでとうございます: レコードの参照の操作の最も困難な側面が完了しました。 他のユース ケースは、レコードのフィールドにアクセスしないためより簡単です。 適例をフィルター処理すると、このセクションで説明します。

追加、**コンボ ボックス**ギャラリーの上部を制御し、新しいコントロールのこれらのプロパティを設定します。

- **項目**: `Users`
- **SelectMultiple**: `false`

> [!div class="mx-imgBorder"]
> ![項目プロパティのユーザーに設定されているギャラリー上のコンボ ボックス コントロールを追加](media/working-with-references/filter-insert-combobox.png)

このコンボ ボックスで選択した特定のユーザーがギャラリーをフィルター処理設定ギャラリーの**項目**プロパティをこの式にします。

```powerapps-dot
Filter( Accounts, Owner = ComboBox1.Selected )
```

> [!div class="mx-imgBorder"]
> ![コンボ ボックス コントロールで設定された値に基づいてフィルター処理されたギャラリー](media/working-with-references/filter-accounts.png)

> [!IMPORTANT]
> このトピックの手順は、正確に手順を実行する場合は正確です。 ただし、コントロールが別の名前を持つ場合、その名前を使用してコントロールを参照する数式は失敗します。 削除して、同じ種類のコントロールを追加した場合、コントロールの名前の末尾に番号を変更します。 すべての数式のエラーを表示する、すべてのコントロールの正しい名前が含まれていることを確認します。

使用する必要はありません**IsType**または**AsType**または完全なレコードを他のレコードの参照へのレコードの参照を比較するためです。 アプリのエンティティ型を知っている**ComboBox1.Selected**から派生されるため、**ユーザー**エンティティ。 アカウント所有者は、チームは、フィルター条件に一致しません。

ユーザーまたはチーム別のフィルタ リングをサポートすることで、少し手の込んだ取得できます。

1. ギャラリーのサイズを変更して、画面の上部し、挿入コンボ ボックスを移動するには、スペース、 [**ラジオ**コントロール](controls/control-radio.md)ギャラリー上し、新しいコントロールのこれらのプロパティを設定。

    - **項目**: `[ "All", "Users", "Teams" ]`
    - **レイアウト**: `Layout.Horizontal`

1. **コンボ ボックス**制御は、このプロパティ設定 (コンボ ボックスが消える場合は、選択**ユーザー**ラジオ コントロールで)。

    - **表示される**: `Radio1.Selected.Value = "Users"`

1. コピーして貼り付ける、**コンボ ボックス**制御、コピーを元に直接移動およびコピーのこれらのプロパティを設定します。

    - **項目**: `Teams`
    - **表示される**: `Radio1.Selected.Value = "Teams"`

    アプリのオプション ボタン コントロールの状態にし、一度に 1 つだけのコンボ ボックスが表示されます。 互いの上に直接のでその内容を変更するのと同じコントロールに表示されます。

1. 最後に、設定、**項目**のプロパティ、**ギャラリー**コントロールに次の式。

    ```powerapps-dot
    Filter( Accounts,
        Radio1.Selected.Value = "All"
        Or (Radio1.Selected.Value = "Users" And Owner = ComboBox1.Selected)
        Or (Radio1.Selected.Value = "Teams" And Owner = ComboBox1_1.Selected)
    )
    ```

    > [!div class="mx-imgBorder"]
    > ![すべてのレコードまたは特定のユーザーまたはチームを表示するフィルター選択されたギャラリー](media/working-with-references/filter-combobox.png)

これらの変更では、すべてのレコードを表示したり、ユーザーまたはチームのいずれかに基づきフィルター処理します。

> [!div class="mx-imgBorder"]
> ![オプション ボタン コントロールでコンボ ボックスをベースのさまざまなフィルター処理された結果を示すアニメーション](media/working-with-references/filter-allthree.gif)

数式は委任可能な完全です。 ラジオ ボタンの値を比較する部分では、定数は、すべてのレコードであり、フィルターの残りの部分が Common Data Service に送信される前に評価されます。

所有者の種類でフィルター処理する場合は、使用、 **IsType**関数がのまだ委任可能な。

> [!div class="mx-imgBorder"]
> ![IsType を使用して、所有者の種類によってフィルター処理します。](media/working-with-references/filter-bytype.png)

## <a name="update-the-owner-by-using-patch"></a>修正プログラムを使用して、所有者を更新します。

更新することができます、**所有者**フィールドの他のすべての参照と同じようにします。 最初のチームには、現在選択されているアカウントの所有者を設定します。

```powerapps-dot
Patch( Accounts, Gallery1.Selected, { Owner: First( Teams ) } )
```

アプリの種類を知っているために、次のこのアプローチが通常の参照と違いはありません**最初 (チーム)** します。 最初のユーザーを代わりにする場合でその部分を置き換える**最初 (ユーザー)** します。 **パッチ**関数に伝えますが、**所有者**フィールドは、これらの 2 つのエンティティ型のいずれかに設定することができます。

この機能をアプリに追加します。

1. **ツリー ビュー**ペインで、**ラジオ**コントロールと、2 つ**コンボ ボックス**同時コントロール。

1. 省略記号のメニュー選択**これらの項目をコピー**:

    > [!div class="mx-imgBorder"]
    > ![ツリー ビューを使用して複数のコントロールのコピー](media/working-with-references/patch-copy.png)

1. [同じ] メニューで、次のように選択します**貼り付け**:。

    > [!div class="mx-imgBorder"]
    > ![ツリー ビューを使用して複数のコントロールの貼り付け](media/working-with-references/patch-paste.png)

1. コピーしたコントロールをギャラリーの右側に移動します。

    > [!div class="mx-imgBorder"]
    > ![ギャラリーの右側にコピーしたコントロールを移動](media/working-with-references/patch-position.png)

1. 先ほどコピーした選択**ラジオ**を制御して、これらのプロパティを変更します。

    - 項目: `[ "Users", "Teams" ]`
    - 既定値: `If( IsType( Gallery1.Selected.Owner, Users ), "Users", "Teams" )`

    > [!div class="mx-imgBorder"]
    > ![ラジオ コントロールからのすべての選択肢の削除](media/working-with-references/patch-noall.png) 

1. **ラジオ**コントロールで、**ユーザー**ように、**コンボ ボックス**ユーザーを一覧表示するコントロールを表示します。

1. 選択、表示可能な**コンボ ボックス**、制御し、設定、 **DefaultSelectedItems**に次の式のプロパティ。

    ```powerapps-dot
    If( IsType( Gallery1.Selected.Owner, Users ),
        AsType( Gallery1.Selected.Owner, Users ),
        Blank()
    )
    ```

    > [!div class="mx-imgBorder"]
    > ![ユーザーのコンボ ボックスの既定のプロパティの設定](media/working-with-references/patch-default-users.png)

1. **ラジオ**コントロールで、**チーム**ように、**コンボ ボックス**チームを一覧表示するコントロールを表示します。

1. 選択、**ラジオ**を今すぐ不可視から離れた場所の選択コントロール**コンボ ボックス**ユーザーを制御します。

1. 選択、表示可能な**コンボ ボックス**チームは、制御し、設定、 **DefaultSelectedItems**に次の式のプロパティ。

    ```powerapps-dot
    If( IsType( Gallery1.Selected.Owner, Teams ),
        AsType( Gallery1.Selected.Owner, Teams ),
        Blank()
    )
    ```

    > [!div class="mx-imgBorder"]
    > ![チームのコンボ ボックスの既定のプロパティの設定](media/working-with-references/patch-default-teams.png)

1. 挿入、**ボタン**コントロールを下に移動、**コンボ ボックス**、制御し、ボタンの**テキスト**プロパティを`"Patch Owner"`します。

1. 設定、 **OnSelect**の次の数式にボタンのプロパティ。

    ```powerapps-dot
    Patch( Accounts, Gallery1.Selected,
        { Owner: If( Radio1_1.Selected.Value = "Users",
                ComboBox1_2.Selected,
                ComboBox1_3.Selected ) } )
    ```

    > [!div class="mx-imgBorder"]
    > ![ボタン コントロールを設定する式](media/working-with-references/patch-button.png)

先ほどコピーした**ラジオ**と**コンボ ボックス**コントロールは、ギャラリーで現在選択されているアカウントの所有者を表示します。 同じコントロールとボタンを選択して、チームまたはユーザーに、アカウントの所有者を設定できます。

> [!div class="mx-imgBorder"]
> ![ユーザーまたはチームのいずれかで所有者のアニメーションが表示された修正プログラム](media/working-with-references/patch-allthree.gif)

## <a name="show-the-owner-by-using-a-form"></a>フォームを使用して、所有者を表示します。

表示することができます、**所有者**カスタム カードを追加することで、フォーム内でフィールド。 この執筆時点で、フォームのコントロール フィールドの値を変更することはできません。

1. 挿入、**編集フォーム**コントロールのサイズを変更し、右下隅に移動します。

1. **プロパティ**] タブの右側のウィンドウを開いて、**データ ソース**、一覧表示し、[**アカウント**:

    > [!div class="mx-imgBorder"]
    > ![追加フィールドを空白の値を表示するフォーム コントロール](media/working-with-references/form-insert.png)  

1. フォームの設定**項目**プロパティを`Gallery1.Selected`:

    > [!div class="mx-imgBorder"]
    > ![追加フィールドに入力、ギャラリーで選択された項目からを表示するフォーム コントロール](media/working-with-references/form-item.png)

1. **プロパティ**選択の右側のウィンドウのタブ**フィールドを編集**します。

1. **フィールド**ウィンドウで、省略記号を選択し、**カスタム カードの追加**:

    > [!div class="mx-imgBorder"]
    > ![カスタム カードを追加するためのコマンド](media/working-with-references/form-customcard.png)

    フォーム コントロールの下部に新しいカードが表示されます。

1. すべてのテキストを表示する、必要に応じて、カードのサイズを変更します。

    > [!div class="mx-imgBorder"]
    > ![空白を挿入のカスタム カード](media/working-with-references/form-inserted-customcard.png)

1. 挿入、**ラベル**カスタムのカードに制御し、ラベルの**テキスト**プロパティに、ギャラリーで使用した式。

    ```powerapps-dot
    If( IsType( ThisItem.Owner, Teams ),
        "Team: " & AsType( ThisItem.Owner, Teams ).'Team Name',
        "User: " & AsType( ThisItem.Owner, Users ).'Full Name' )
    ```

    > [!div class="mx-imgBorder"]
    > ![ラベル コントロールで [所有者] フィールドを示すカスタムのカード](media/working-with-references/form-displayowner.png)

ギャラリーで各選択範囲のレコードの所有者を含む、アカウントの他のフィールドは、フォームに表示されます。 使用して、所有者を変更する場合、**パッチ** ボタン、フォーム コントロールでは、その変更も表示されます。

> [!div class="mx-imgBorder"]
> ![ギャラリーでの変更に応答して、フォーム コントロールを示すアニメーション](media/working-with-references/form-allthree.gif)

## <a name="show-the-fields-of-a-customer"></a>顧客のフィールドを表示します。

Common Data Service で、**顧客**ルックアップ フィールドは、別のポリモーフィックな参照と同じように**所有者**します。

**所有者**に制限は、0、1 つ、以上を含めることができますが、エンティティ、エンティティごとに 1 つ**顧客**ルックアップ フィールド。 **連絡先**システム エンティティが含まれています、**会社名**フィールドが、**顧客**ルックアップ フィールド。

> [!div class="mx-imgBorder"]
> ![会社名 フィールドを示す必要のない顧客のデータ型のエンティティにお問い合わせください。](media/working-with-references/customer-companyname.png)

さらに追加することができます**顧客**を選択してエンティティにルックアップ フィールド、**顧客**新しいフィールドのデータ型。

![フィールドを作成するときにデータ型の一覧から顧客データの種類します。](media/working-with-references/customer-datatype.png)

A**顧客**ルックアップ フィールドは、いずれかからレコードを参照できる、**アカウント**エンティティまたは**連絡先**エンティティ。 使用して、 **IsType**と**AsType**これらのエンティティを持つ関数がデータ ソースとして追加すると良いをこれでは (おくことができます**チーム**と**ユーザー**インプレース)。

> [!div class="mx-imgBorder"]
> ![アカウント、データ ペインで、チーム、ユーザー、および連絡先エンティティ](media/working-with-references/customer-datasources.png)

処理を行う、**顧客**と**所有者**フィールドはよく似ているため、アプリをそのままコピーできること (**ファイル** > **として保存**、し、別の名前を指定) と、これらの単純な置換を行います。

| Location | **所有者**サンプル | **顧客**サンプル |
|----------|-----------|------------------|
| 全体で | **所有者** | **' Customer Name'** |
| 全体で | **ユーザー** | **アカウント** |
| 全体で | **チーム** | **連絡先** |
| ギャラリーの**項目**プロパティ | **アカウント** | **連絡先** |
| フォームの**項目**プロパティ | **アカウント** | **連絡先** |
| 最初の引数**修正プログラム**<br>ボタンの**OnSelect**プロパティ | **アカウント** | **連絡先** |
| オプションのフィルター処理**項目**プロパティ | **[&nbsp;"All",&nbsp;"Users",&nbsp;"Teams"&nbsp;]** | **[&nbsp;"All",&nbsp;"Accounts",&nbsp;"Contacts"&nbsp;]** |
| ラジオの修正プログラムを適用**項目**プロパティ | **["Users"、「チーム」]** | **[ "Accounts", "Contacts" ]** |
| コンボ ボックスの**Visible**プロパティ | **「ユーザー」** と **「チーム」** | **「アカウント」** と **"Contacts"** |

たとえば、新しいギャラリーがある必要がありますこれ**項目**プロパティ。

```powerapps-dot
Filter( Contacts,
    Radio1.Selected.Value = "All"
    Or (Radio1.Selected.Value = "Accounts" And 'Company Name' = ComboBox1.Selected)
    Or (Radio1.Selected.Value = "Contacts" And 'Company Name' = ComboBox1_1.Selected)
)
```

> [!div class="mx-imgBorder"]
> ![単純な変更が適用される所有者アプリから派生したユーザーのアプリ](media/working-with-references/customer-simple-update.png)

2 つの重要な違い**顧客**と**所有者**ギャラリーとフォーム内で数式への更新が必要です。

1. 間の一対多リレーションシップ**アカウント**と**連絡先**名前によってこれらのエンティティ型を参照するときに優先します。 代わりに**アカウント**を使用して、  **\[\@アカウント]**; の代わりに**連絡先**を使用して、  **\[ \@アドレス帳]** します。 使用して、[グローバルの曖昧性除去演算子](functions/operators.md#disambiguation-operator)でエンティティ型を参照することを確認する**IsType**と**AsType**します。 この問題は、ギャラリーとフォームのコントロールのレコードのコンテキストにのみ存在します。

1. **所有者**フィールドには、値が必要ですが、**顧客**フィールドは、*空白*します。 型名のない、正しい結果を表示するには、この場合のテスト、 [ **IsBlank**関数](functions/function-isblank-isempty.md)、し、代わりに、空のテキスト文字列を表示します。

フォームには、カスタム カードに表示されたら、同次数式は、これらの変更の両方がだけでなく**テキスト**ギャラリーのラベル コントロールのプロパティ。

```powerapps-dot
If( IsBlank( ThisItem.'Company Name' ), "",
    IsType( ThisItem.'Company Name', [@Accounts] ),
        "Account: " & AsType( ThisItem.'Company Name', [@Accounts] ).'Account Name',
    "Contact: " & AsType( ThisItem.'Company Name', [@Contacts] ).'Full Name'
)
```

> [!div class="mx-imgBorder"]
> ![ギャラリーのサブタイトルのラベル コントロールの Text プロパティを更新します。](media/working-with-references/customer-update.png)

これらの変更を表示および変更、**会社名**フィールドに、**連絡先**エンティティ。

> [!div class="mx-imgBorder"]
> ![連絡先の選択を変更するアニメーション表示ベースのギャラリー コントロールの他のコントロールとフォームの変更を促進](media/working-with-references/customer-allthree.gif)

> [!NOTE]
> 本稿執筆**顧客**参照でこれらの制限があります。
>
> - 特定のレコードに基づいて一覧をフィルター処理することはできません、**連絡先**または**アカウント**エンティティ。 フィルターのラジオ ボタン コントロール、前の例では機能しません。
> - 動作している顧客に専用フィールドでは、システム定義 **' Company Name'** 上、**連絡先**エンティティで、前の例で使用されました。 カスタム顧客フィールドの追加がまだサポートされています。
> - 使用して顧客フィールドをオフにすることはできません**パッチ**に設定する*空白*します。

## <a name="understand-regarding-lookup-fields"></a>ルックアップ フィールドの関連を理解します。

**に関する**ルックアップ フィールドは、このトピックで既に使ったこと少し異なります。 このトピックでは、前に説明するパターンを適用することから始めます、し、その他のテクニックを学習します。

単に始めることができます、 **Fax**エンティティ。 このエンティティがポリモーフィックな**に関する**ルックアップ フィールドを参照できます**アカウント**、**連絡先**、およびその他のエンティティ。 アプリに対して実行できる**顧客**これを変更および**Fax**:

| Location | **顧客**サンプル | **Fax**サンプル |
|----------|-----------|------------------|
| 全体で | **' Customer Name'** | **に関する** |
| ギャラリーの**項目**プロパティ | **連絡先** | **Fax の数します。** |
| フォームの**項目**プロパティ | **連絡先** | **Fax の数します。** |
| 最初の引数**修正プログラム**<br> ボタンの**OnSelect**プロパティ | **連絡先** | **Fax の数します。** |

ここでも、データ ソースを追加する必要があります: この時点の**Fax**します。 **ビュー** ] タブで [**データソース**:

> [!div class="mx-imgBorder"]
> ![データ ペインのアカウント、チーム、ユーザー、連絡先、および Fax のエンティティの表示](media/working-with-references/faxes-datasources.png)

重要な違い**に関する**に制限がないことです**アカウント**と**連絡先**します。 実際には、エンティティの一覧は、カスタム エンティティで拡張可能です。 アプリのほとんどは変更しない限り、このポイントに対応できますが、ギャラリーとフォームのラベルの数式を更新する必要があります。

```powerapps-dot
If( IsBlank( ThisItem.Regarding ), "",
    IsType( ThisItem.Regarding, [@Accounts] ),
        "Account: " & AsType( ThisItem.Regarding, [@Accounts] ).'Account Name',
    IsType( ThisItem.Regarding, [@Contacts] ),
        "Contacts: " & AsType( ThisItem.Regarding, [@Contacts] ).'Full Name',
    ""
)
```

> [!div class="mx-imgBorder"]
> ![関連の検索のサブタイトルのコントロールの Text プロパティを更新](media/working-with-references/regarding-label.png)

操作するこれらの変更を行った後、**に関する**参照と同様、**所有者**と**顧客**参照。

> [!div class="mx-imgBorder"]
> ![Fax の変更を示すアニメーション ベースのギャラリー コントロールをその他のコントロールとフォームへの更新プログラムを推進](media/working-with-references/regarding-allthree.gif)

> [!NOTE]
> 本稿執筆**に関する**参照でこれらの制限があります。
>
> - 特定のレコードに基づいて一覧をフィルター処理することはできません。 フィルターのラジオ ボタン コントロール、前の例では機能しません。
> - 使用して、[関連] フィールドをオフにすることはできません**パッチ**に設定する*空白*します。

## <a name="understand-regarding-relationships"></a>リレーションシップの関連を理解します。

**に関する**異なります**所有者**と**顧客**前者には多対一のリレーションシップが含まれているためです。 定義上、反転、一対多のリレーションシップを使用すると、書き込み**最初 (アカウント)。Fax**します。

バックアップして、エンティティの定義を見てみましょう。 Common Data Service などのエンティティで**Fax**、**タスク**、**電子メール**、**ノート**、**電話**、**文字**、および**チャット**として指定されて[*アクティビティ*](../../developer/common-data-service/activity-entities.md)します。 独自に作成することも[カスタム活動エンティティ](../../developer/common-data-service/custom-activities.md)します。 その設定は、下に表示を表示または活動エンティティを作成するときに**詳細設定**:

![エンティティを作成するときに、アクティビティ エンティティ設定](media/working-with-references/activity-entitytype.png)

他のエンティティは、として有効になっている場合、アクティビティのエンティティに関連付けることができます、*アクティビティ タスク*エンティティの設定にします。 **アカウント**、**連絡先**、他の数多くの標準エンティティはそのように指定されていると (もう一度、**より多くの設定**)。

![エンティティを作成するときに、アクティビティ タスク設定](media/working-with-references/activity-entityuse.png)

すべての活動エンティティとアクティビティ タスク エンティティ、暗黙的なリレーションシップがあります。 フィルターを変更する場合**すべて**画面の上部にある選択、 **Fax**エンティティ、および選択し、**リレーションシップ**] タブの [すべてのエンティティをのターゲットにすることができます**に関する**参照が表示されます。

> [!div class="mx-imgBorder"]
> ![多対一のリレーションシップに関する表示 Fax エンティティのリレーションシップ](media/working-with-references/activity-manytoone.png)

リレーションシップを表示する場合、**アカウント**エンティティのソースは、すべてのエンティティを**に関する**ルックアップ フィールドが表示されます。

> [!div class="mx-imgBorder"]
> ![一対多のリレーションシップに関する表示、アカウント エンティティのリレーションシップ](media/working-with-references/activity-onetomany.png)

どのような意味でしょうか。

- 数式を記述するときに、活動エンティティの一覧が固定されていないことと、独自に作成することができますを考慮する必要があります。 数式では、予期しないアクティビティ エンティティを適切に処理する必要があります。
- タスクのアクティビティとアクティビティは、一対多リレーションシップを持ちます。 簡単に、アカウントに関連するすべての fax を要求することができます。

アプリでは、この概念の詳細。

1. 別の画面を追加します。

    > [!div class="mx-imgBorder"]
    > ![空の画面を挿入します。](media/working-with-references/activitypointer-newscreen.png)

1. ギャラリー コントロールを挿入して、サイズを変更し、画面の左側に移動します。

1. **プロパティ** タブの右側のペインで、設定ギャラリーの**項目**に**アカウント**:

    > [!div class="mx-imgBorder"]
    > ![プロパティ ウィンドウでアカウントに項目を設定します。](media/working-with-references/activitypointer-accounts.png)

1. ギャラリーのレイアウトを設定します**タイトル**、タイトル フィールドに設定して**アカウント名**:

    > [!div class="mx-imgBorder"]
    > ![プロパティ ペインでギャラリー コントロールのタイトルのレイアウトを設定します](media/working-with-references/activitypointer-account-name.png)

1. 2 番目のギャラリーを追加、サイズを変更し、画面の右側に移動します。

1. 新しいギャラリーの設定**項目**プロパティを`Gallery2.Selected.Faxes`します。

    この手順では、指定したアカウントの fax のフィルター処理された一覧が返されます。

    > [!div class="mx-imgBorder"]
    > ![Fax の items プロパティのセット ベースのギャラリー コントロール](media/working-with-references/activitypointer-faxes.png)

1. ギャラリーのレイアウトを設定します**タイトルとサブタイトル**、表示するタイトル フィールドを設定し、**サブジェクト**フィールド (小文字可能性がある**サブジェクト**)。

    > [!div class="mx-imgBorder"]
    > ![サブジェクト フィールドにタイトルを設定](media/working-with-references/activitypointer-subject.png)

アカウントの一覧で項目を選択すると、fax の一覧には、そのアカウントのみに fax が表示されます。

> [!div class="mx-imgBorder"]
> ![Fax の一覧を運転アカウント ギャラリーで選択範囲を示すアニメーション](media/working-with-references/activitypointer-allthree.gif)

## <a name="activity-entity"></a>活動エンティティ

前のセクションの説明に従って、アカウントのすべての fax を表示できます。 ただし、fax、電子メール メッセージ、電話、および他の操作を含む、アカウントのすべてのアクティビティを表示することもできます。

後者のシナリオで使用する、**アクティビティ**エンティティ。 このエンティティを表示するには、オン**すべて**右上隅にあるエンティティの一覧からフィルターを削除します。

> [!div class="mx-imgBorder"]
> ![アクティビティのエンティティを示すエンティティの一覧](media/working-with-references/activitypointer-entity.png)

**アクティビティ**エンティティが特別な。 レコードを追加するたびに、 **Fax**エンティティ、システムもでレコードを作成、**アクティビティ**アクティビティのすべてのエンティティに共通するフィールドを持つエンティティ。 これらのフィールドの**サブジェクト**最も興味深いの 1 つです。

前の例の 1 つだけの行を変更することで、すべてのアクティビティを表示できます。 置換`Gallery2.Selected.Faxes`で`Gallery2.Selected.Activities`:

> [!div class="mx-imgBorder"]
> ![Fax 活動を変更する、2 つ目のギャラリーの items プロパティの変更](media/working-with-references/activitypointer-gallery.png)

レコードの発信元、**アクティビティ**、エンティティがそれでも使用、 **IsType**はアクティビティの種類を特定する関数。 使用する前にもう一度、 **IsType**では、エンティティ型には、データ ソースを追加する必要があります。

> [!div class="mx-imgBorder"]
> ![データ ペインの IsType 関数に必要なすべてのエンティティの表示](media/working-with-references/activity-datasources.png)

次の数式を使用すると、ギャラリー内のラベル コントロールでレコードの種類を表示できます。

```powerapps-dot
If( IsType( ThisItem, [@Faxes] ), "Fax",
    IsType( ThisItem, [@'Phone Calls'] ), "Phone Call",
    IsType( ThisItem, [@'Email Messages'] ), "Email Message",
    IsType( ThisItem, [@Chats] ), "Chat",
    "Unknown"
)
```

> [!div class="mx-imgBorder"]
> ![Fax メッセージ、電話、およびその他のアクティビティの情報を表示するための式に text プロパティを設定します。](media/working-with-references/activitypointer-type.png)

使用することも**AsType**の特定の型のフィールドにアクセスします。 たとえば、次の数式の各アクティビティの種類を決定し、電話の呼び出しから電話番号と呼び出しの方向を示しています、**電話番号**エンティティ。

```powerapps-dot
If( IsType( ThisItem, [@Faxes] ), "Fax",
    IsType( ThisItem, [@'Phone Calls'] ),
       "Phone Call: " &
       AsType( ThisItem, [@'Phone Calls'] ).'Phone Number' &
       " (" & AsType( ThisItem, [@'Phone Calls'] ).Direction & ")",
    IsType( ThisItem, [@'Email Messages'] ), "Email Message",
    IsType( ThisItem, [@Chats] ), "Chat",
    "Unknown"
)
```

> [!div class="mx-imgBorder"]
> ![詳細については、電話の拡張テキスト プロパティ](media/working-with-references/activitypointer-phonecall.png)

その結果、アプリには、アクティビティの完全な一覧が表示されます。 **サブジェクト**数式ではそのアカウントかどうかどうか、すべての種類のアクティビティ、フィールドが表示されます。 についてわかっているアクティビティの種類は、その型の名前と各アクティビティについての種類に固有の情報を表示できます。

> [!div class="mx-imgBorder"]
> ![アクティビティのさまざまな種類の情報を表示する画面を完了しました](media/working-with-references/activitypointer-complete.png)

## <a name="notes-entity"></a>ノートのエンティティ

ここまでは、すべての**に関する**例として、アクティビティに基づいているが、**ノート**エンティティは別のケースを表します。

エンティティを作成するときに、添付ファイルが有効にできます。

![エンティティを作成するときに、添付ファイルやメモを有効にします。](media/working-with-references/notes-entity.png)

このチェック ボックスを選択する場合は作成します、**に関する**との関係、**ノート**のエンティティ、次の図として表示、**アカウント**エンティティ。

> [!div class="mx-imgBorder"]
> ![一対多のリレーションシップを介してノートへの関係を示すアカウント エンティティ](media/working-with-references/notes-relationships.png)

使用する以外、この違い、**に関する**のアクティビティを使用する同じ方法で参照します。 添付ファイルを指定することに一対多リレーションシップを有効になっているエンティティ**ノート**、この例のように。

`First( Accounts ).Notes`

> [!NOTE]
> 本稿執筆、**に関する**参照は使用できません、**ノート**エンティティ。 読み取ることができませんかに基づいてフィルター処理、**に関する**フィールド、およびするを使用して、フィールドを設定できません**パッチ**します。
>
> ただし、逆**ノート**一対多のリレーションシップは、添付ファイルが有効になっているレコードのノートの一覧をフィルター処理できます。 使用することも、 [ **Relate** ](functions/function-relate-unrelate.md)にレコードのメモを追加する関数**ノート**が、テーブルは、この例のように最初に、作成する必要があります。
>
>`Relate( ThisItem.Notes, Patch( Notes, Defaults( Notes ), { Title: "A new note" } ) )`

## <a name="activity-parties"></a>アクティビティの関係者

キャンバス アプリは、この記事の執筆時点の活動関係者をサポートされていません。

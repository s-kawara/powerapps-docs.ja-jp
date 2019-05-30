---
title: 関連付けられており、関数の関連付けを解除 |Microsoft Docs
description: を含む構文と例を、関連情報を参照し、PowerApps の関数の関連付けを解除
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 01/22/2019
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 4b2c6b9518e987ef17f2ff2b50987568c8a0b69f
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61527209"
---
# <a name="relate-and-unrelate-functions-in-powerapps"></a>関連付けられており、PowerApps の関数の関連付けを解除

関連して、一対多または多対多のリレーションシップによって 2 つのエンティティのレコードの関連付けを解除します。

## <a name="description"></a>説明

**Relate**関数は、Common Data Service で一対多または多対多のリレーションシップによって 2 つのレコードをリンクします。 **Unrelate**関数は、プロセスを反転し、リンクを削除します。

一対多のリレーションシップで多数のエンティティから外部キー フィールドに 1 つのエンティティのレコードには、そのポイントがあります。 **関連**1 つのエンティティの特定のレコードをポイントするには、このフィールドを設定中に**Unrelate**このフィールドを設定します。*空白*します。 ときに既にフィールドで設定されている場合**Relate**が呼び出されると、既存のリンクは、新しいリンクを優先して失われます。 使用して、このフィールドを設定することも、 [**パッチ**](function-patch.md)関数または **[編集フォーム](../controls/control-form-detail.md)** コントロールは使う必要はありません、 **関連付け**関数。

多対多のリレーションシップでは、レコードにリンクする、システムは、非表示の結合テーブルを保持します。 この結合テーブルには直接アクセスすることはできません。一対多の射影でのみ読み取りおよびによって設定できるよう、 **Relate**と**Unrelate**関数。 どちらの関連エンティティには、外部キーがあります。

最初の引数で指定したエンティティのデータは、変更を反映するように更新されますが、2 番目の引数で指定したエンティティのデータはありません。 更新データが手動である必要があります、 **[更新](function-refresh.md)** 操作の結果を表示する関数。

決してこれらの関数を作成またはレコードを削除します。 のみ関連または既に存在する 2 つのレコードの関連付けを解除します。

これらの関数を使用するだけで[動作の数式](../working-with-formulas-in-depth.md)します。

> [!NOTE]
> これらの関数は、プレビュー機能の一部と、その動作が使用可能な場合にのみ、**リレーショナル データ、オプションのセット、および cd の他の新機能**機能を有効にします。 これは、新しいアプリの既定で有効になっているアプリ レベルの設定です。 この機能のスイッチを検索するには、開く、**ファイル**メニューの **アプリ設定**、し、**詳細設定**します。 お客様のフィードバックは弊社にとって非常に重要です。ご意見を [PowerApps コミュニティ フォーラム](https://powerusers.microsoft.com/t5/Expressions-and-Formulas/bd-p/How-To)にお寄せください。

## <a name="syntax"></a>構文

**Relate**( *Entity1RelatedTable*, *Entity2Record* )

* *Entity1RelatedTable* - 必須。 レコードの*Entity1*、テーブルの*Entity2*一対多または多対多のリレーションシップによって関連するレコード。
* *Entity2Record* - 必須。 *Entity2*レコードのリレーションシップを追加します。

**Unrelate**( *Entity1RelatedTable*, *Entity2Record* )

* *Entity1RelatedTable* - 必須。 レコードの*Entity1*、テーブルの*Entity2*一対多または多対多のリレーションシップによって関連するレコード。
* *Entity2Record* - 必須。 *Entity2*リレーションシップから削除するレコード。

## <a name="examples"></a>例

検討してください、**製品**に示すように、次のリレーションシップを持つエンティティ、 [PowerApps ポータルのエンティティのビューアー](../../common-data-service/create-edit-entities-portal.md):

| リレーションシップの表示名 | 関連エンティティ | リレーションシップの種類 |
| --- | --- |
| 製品の予約 | 予約 | 一対多 |
| 製品&harr;にお問い合わせください | お問い合わせ | 多対多 |

**製品**と**予約**一対多で関連するリレーションシップ。  最初のレコードを関連付ける、**予約**の最初のレコードを持つエンティティ、**製品**エンティティ。

`Relate( First( Products ).Reservations, First( Reservations ) )`

これらのレコード間のリレーションシップを削除するには。

`Unrelate( First( Products ).Reservations, First( Reservations ) )`

ありませんが作成または削除、または a レコードでは、レコード間の関係のみが変更されました。

**製品**と**連絡先**多対多で関連するリレーションシップ。  最初のレコードを関連付ける、**連絡先**の最初のレコードを持つエンティティ、**製品**エンティティ。

`Relate( First( Products ).Contacts, First( Contacts ) )`

多対多リレーションシップは対称も実現できればこの方向が逆にします。

`Relate( First( Contacts ).Products, First( Products ) )`

これらのレコード間のリレーションシップを削除するには。

`Unrelate( First( Products ).Contacts, First( Contacts ) )`

または。

`Unrelate( First( Contacts ).Products, First( Products ) )`

次のようにその説明はこれらの操作を使用してアプリを使用してこれらのエンティティで正確に**ギャラリー**と**コンボ ボックス**関連するレコードを選択するコントロール。

これらの例は、環境にインストールされているサンプル データに依存します。 いずれか[サンプル データを含む試用版環境を作成](../../model-driven-apps/overview-model-driven-samples.md#get-sample-apps)または[サンプル データを既存の環境に追加する](../../model-driven-apps/overview-model-driven-samples.md#install-or-uninstall-sample-data)します。

### <a name="one-to-many"></a>一対多

#### <a name="relate-function"></a>**関連**関数

まず、製品に関連付けられている予約を再割り当てを表示したり、簡単なアプリを作成します。

1. 作成、[一からタブレット アプリ](../data-platform-create-app-scratch.md)します。

1. **[ビュー]** タブで **[データソース]** を選択します。

1. **データ**ペインで、**データ ソースの追加** > **Common Data Service** > **製品** > **接続**します。  

    製品エンティティは、上に読み込まれたサンプル データの一部です。

     ![データ ソースとしての製品のエンティティを追加します。](media/function-relate-unrelate/products-connect.png)

1. **挿入** タブで、追加の空の垂直 **[ギャラリー](../controls/control-gallery.md)** コントロール。

1. 追加したコントロールの名前があることを確認**Gallery1**、移動して、画面の左側にある入力のサイズを変更します。

1. **プロパティ**タブで、設定**Gallery1**の**項目**プロパティを**製品**とその**レイアウト**に**イメージとタイトル**します。

    ![ProductsGallery を構成します。](media/function-relate-unrelate/products-gallery.png)

1. **Gallery1**、いることを確認、**ラベル**コントロールの名前は**Title1**、し、設定、**テキスト**プロパティを**ThisItem.Name**します。

    ![Gallery1 のラベルを構成します。](media/function-relate-unrelate/products-title.png)

1. 次の項目を挿入することを回避するために画面を選択**Gallery1**します。  2 つ目の空の垂直方向の追加**ギャラリー**を制御する、ということを確認して**Gallery2**します。

    **Gallery2**の予約をユーザーが選択したすべての製品が表示されます**Gallery1**します。

1. 移動およびサイズ変更**Gallery2**画面の右上のクアドラントを入力します。

1. (省略可能)青色の追加**ラベル**上記コントロール**Gallery2**次の図に示すように、します。

1. 数式バーで設定、**項目**プロパティの**Gallery2**に**Gallery1.Selected.Reservations**します。

    ![Gallery2 項目を構成します。](media/function-relate-unrelate/reservations-gallery.png)

1. プロパティ ウィンドウで、設定**Gallery2**の**レイアウト**に**タイトル**します。

    ![Gallery2 レイアウトを構成します。](media/function-relate-unrelate/reservations-gallery-right.png)

1. **Gallery2**、追加、 **[コンボ ボックス](../controls/control-combo-box.md)** 制御、ということを確認します**ComboBox1**、移動すると、ブロックを回避することをサイズ変更、。他のコントロール**Gallery2**します。

1. **プロパティ**タブで、設定**ComboBox1**の**項目**プロパティを**製品**します。

    ![製品に Items プロパティを設定します。](media/function-relate-unrelate/reservations-combo-right.png)

1. 下にスクロール、**プロパティ** タブで設定し、 **ComboBox1**の**複数選択を許可する**プロパティを**オフ**します。

    ![設定を Off に複数の選択を許可します。](media/function-relate-unrelate/reservations-singleselect-right.png)

1. 数式バーに次のように設定します。 **ComboBox1**の**DefaultSelectedItems**プロパティを**ThisItem."製品 Reservation"** します。

    ![ReserveCombo DefaultSelectedItems を設定します。](media/function-relate-unrelate/reservations-combo.png)

1. **Gallery2**設定**NextArrow2**の**OnSelect**に次の式のプロパティ。

    ```powerapps-dot
    Relate( ComboBox1.Selected.Reservations, ThisItem )
    ```

    現在の予約変更で、ユーザーが選択されている製品、ユーザーがこのアイコンを選択**ComboBox1**します。

    ![NextArrow2 を構成します。](media/function-relate-unrelate/reservations-relate.png)

1. F5 キーを押して、プレビュー モードでアプリをテストします。

このアプリを使用、ユーザーから移動できます予約を 1 つの製品間。 ユーザーの 1 つの製品での予約で別の製品が選択できる**ComboBox1**し、 **NextArrow2**その予約を変更します。

![アプリの一対多で関連付け関数を示します](media/function-relate-unrelate/reservations-reassign.gif)

#### <a name="unrelate-function"></a>**関連付けを解除**関数

この時点では、1 つのレコードのリレーションシップを移動するが完全にリレーションシップを削除することはできません。 使用することができます、 **Unrelate**予約レコードを任意の製品から切断する関数。

1. **[ビュー]** タブで **[データソース]** を選択します。

1. **データ**ペインで、**データ ソースの追加** > **Common Data Service** > **予約** > **接続**します。

1. **Gallery2**、設定、 **OnSelect**の数式**NextArrow2**に次の式。

    ```powerapps-dot
    If( IsBlank( ComboBox1.Selected ),
        Unrelate( Gallery1.Selected.Reservations, ThisItem ),
        Relate( ComboBox1.Selected.Reservations, ThisItem )
    );
    Refresh( Reservations )
    ```
    ![適切なアイコンを構成します。](media/function-relate-unrelate/reservations-relate-unrelate.png)

1. コピー **Gallery2**を選択し、ctrl + C キーを押してクリップボードに

1. 複製を貼り付ける**Gallery2**を同じキーを押して CTRL + V、画面し、画面の右下のクアドラントに移動します。

1. (省略可能)上記のラベルを追加した場合は**Gallery2**、そのラベルを前の 2 つの手順を繰り返します。

1. 重複していることを確認**Gallery2**という**Gallery2_1**、し、設定、**項目**プロパティをこの式に。

    ```powerapps-dot
    Filter( Reservations, IsBlank( 'Product Reservation' ) )
    ```

    委任の警告が表示されますが、この例ではデータ量が小規模のいても関係ありません。

    ![Gallery2_1 の Items プロパティを設定します。](media/function-relate-unrelate/reservations-lost.png)

選択をクリアするこれらの変更により**ComboBox1**その人が製品を予約していない場合に問い合わせてください。 製品を予約していないユーザーの連絡先に表示**Gallery2_1**ユーザーは、成果物への各連絡先を割り当てることができます。

   ![関連付けを示し、関数アプリの一対多の関連付けを解除](media/function-relate-unrelate/reservations-lostandfound.gif)

### <a name="many-to-many"></a>多対多

#### <a name="create-a-many-to-many-relationship"></a>多対多リレーションシップを作成します。

サンプル データには、多対多リレーションシップが含まれていませんが、製品のエンティティと連絡先エンティティのいずれかを作成します。 ユーザーは、1 つ以上の連絡先と 1 つ以上の製品には、各連絡先に各製品を関連付けることができます。

1. [このページ](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)、**データ**左側のナビゲーション バーで、**エンティティ**。

    ![エンティティの一覧を開きます](media/function-relate-unrelate/entity-list.png)

1. すべてのエンティティを含めるエンティティのフィルターを変更します。

    既定では、sample エンティティは表示されません。

    ![エンティティのフィルターを削除します。](media/function-relate-unrelate/entity-all.png)

1. スクロールし、開く、**製品**エンティティ、および選択**リレーションシップ**します。

    ![Product エンティティのリレーションシップ タブ](media/function-relate-unrelate/entity-relationships.png)

1. 選択**リレーションシップの追加** > **多対多**します。

    ![多対多リレーションシップを追加します。](media/function-relate-unrelate/entity-manytomany.png)

1. 選択、**連絡先**リレーションシップのエンティティ。

    ![Contact エンティティを選択します。](media/function-relate-unrelate/entity-contact.png)

1. 選択**完了** > **エンティティの保存**します。

    ![製品エンティティのリレーションシップの一覧](media/function-relate-unrelate/entity-done.png)

#### <a name="relate-and-unrelate-contacts-with-one-or-more-products"></a>関連付けられており、1 つまたは複数の製品と連絡先の関連付けを解除

似ていますが、このトピックの前半で作成した別のアプリを作成しますが、新しいアプリが多対多リレーションシップを提供します。 それぞれの連絡先は 1 つだけではなく複数の製品を予約することになります。

1. タブレット用の空のアプリで作成**Gallery1**として、[最初の手順](#one-to-many)このトピックについて説明します。

1. もう 1 つの空白の垂直方向の追加**ギャラリー**制御、ということを確認します。 **Gallery2**、し、画面の右上隅に移動します。

    このトピックで後で追加します、**コンボ ボックス**で**Gallery2**します。

1. 数式バーに次のように設定します。 **Gallery2**の**項目**プロパティを**Gallery1.Selected.Contacts**します。

    ![ContactsGallery を構成します。](media/function-relate-unrelate/contacts-gallery.png)

1. **プロパティ**タブで、設定**レイアウト**に**イメージとタイトル**します。

    ![ContactsGallery を構成します。](media/function-relate-unrelate/contacts-gallery-right.png)

1. **Gallery2**、いることを確認、**ラベル**コントロールの名前は**Title2**、し、設定、**テキスト**プロパティを**ThisItem. 'Full Name'** します。

    コンソール アプリケーションは、この手順を完了し、製品に連絡先を割り当てるまでそのコントロールで、テキストは表示されません。

    ![連絡先の名前を表示します。](media/function-relate-unrelate/contacts-title.png)

1. 削除**NextArrow2**、挿入、**キャンセル**アイコン、ということを確認して **#icon1**します。

1. 設定、**キャンセル**アイコンの**OnSelect**に次の式のプロパティ。 

    ```powerapps-dot
    Unrelate( Gallery1.Selected.Contacts, ThisItem )
    ```

    ![[キャンセル] アイコンを構成します。](media/function-relate-unrelate/contacts-unrelate.png)

1. **[ビュー]** タブで **[データソース]** を選択します。

1. **データ**ペインで、**データ ソースの追加** > **Common Data Service** > **連絡先** > **接続**します。

1. **Gallery2**、追加、**コンボ ボックス**制御、ということを確認します**ComboBox1**、し、設定、**項目**プロパティを**連絡先**します。

    ![コンボ ボックス アイテムのプロパティを構成します。](media/function-relate-unrelate/contacts-combo.png)

1. **プロパティ**タブで、設定**複数選択を許可する**に**オフ**します。

    ![コンボ ボックスのレイアウト プロパティを構成します。](media/function-relate-unrelate/contacts-combo-right.png)

1. 挿入、**追加**アイコン、およびセットの**OnSelect**に次の式のプロパティ。 

    ```powerapps-dot
    Relate( Gallery1.Selected.Contacts, ComboBox1.Selected )
    ```

    ![構成の追加 アイコン](media/function-relate-unrelate/contacts-relate.png)

このアプリでは、ユーザーことができますようになりました自由に関連し、各製品に一連の連絡先の関連付けを解除します。

- 製品には、連絡先を追加するには画面の下部にあるコンボ ボックスで、連絡先を選択し、、**追加**アイコン。
- 製品から連絡先を削除するには、選択、**キャンセル**その連絡先のアイコン。

    多対多リレーションシップでは、一対多とは異なり、複数の製品と同じメンバーを関連付けるができます。

![関連付けを示し、関数アプリの多対多の関連付けを解除](media/function-relate-unrelate/contacts-relate-unrelate.gif)

#### <a name="in-reverse-relate-and-unrelate-products-with-multiple-contacts"></a>逆の順序で関連付けられており、複数の連絡先と製品の関連付けを解除。

多対多のリレーションシップは、対称です。 連絡先に製品を追加し、いずれかの方向からリレーションシップを表示する方法を表示する 2 つの画面間を反転し、例を拡張できます。

1. 設定、 **OnVisible**プロパティの**Screen1**に **(製品) を更新**します。

    一対多または多対多リレーションシップの最初の引数のエンティティのデータのみを更新すると、 **Relate**または**Unrelate**呼び出しを更新します。 2 つ目は、このアプリの画面間を反転する場合に手動で更新である必要があります。

    ![Refresh 関数に OnVisible プロパティを設定します。](media/function-relate-unrelate/contacts-refresh.png)

1. 重複する**Screen1**します。

    重複した名前が付けられます**Screen1_1**連絡先側からの関係を調べるときの基礎とします。

    ![画面が重複しています](media/function-relate-unrelate/contacts-duplicate.png)

1. 逆方向のビューを作成するこれらのコントロールでの数式を変更する**Screen1_1**:

    - Screen1_1.OnVisible = `Refresh( Contacts )`
    - Gallery1_1.Items = `Contacts`
    - Title1_1.Text = `ThisItem.'Full Name'`
    - Label1_1.Text = `"Selected Contact Products"`
    - Gallery2_1.Items = `Gallery1_1.Selected.Products`
    - Title2_1.Text = `ThisItem.Name`
    - Icon1_1.OnSelect = `Unrelate( Gallery1_1.Selected.Products, ThisItem )`
    - ComboBox1_1.Items = `Products`
    - Icon2_1.OnSelect = `Relate( Gallery1_1.Selected.Products, ComboBox1_1.Selected )`

    結果は次のように、前の画面がリレーションシップには、**連絡先**側です。

    ![連絡先の管理を開始する多対多リレーションシップを表示します。](media/function-relate-unrelate/reverse-screen.png)

1. 挿入、**矢印アップ ダウン**アイコンとその**OnSelect**プロパティを**Navigate (Screen1、None)** 。  同じ処理を行う**Screen1**式を持つ**Navigate (Screen1_1、None)** します。

    ![画面間のナビゲーションを追加します。](media/function-relate-unrelate/reverse-navigate.png)

この新しい画面でユーザーことができます製品に連絡先を追加し、連絡先のビューに反転し、関連付けられている製品を参照してください。 リレーションシップは、対称と 2 つの画面間で共有されます。

![どちらの側から多対多のリレーションシップを示します](media/function-relate-unrelate/contacts-reverse.gif)

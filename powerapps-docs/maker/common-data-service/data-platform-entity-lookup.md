---
title: 検索フィールドを使用してエンティティ間の関連付けの作成 | Microsoft Docs
description: 検索フィールドを使用して PowerApps でエンティティ間の関連付けを作成する方法の詳細な手順。
author: lancedMicrosoft
manager: kvivek
ms.service: powerapps
ms.component: cds
ms.topic: conceptual
ms.date: 02/21/2019
ms.author: lanced
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---

# <a name="create-a-relationship-between-entities"></a>エンティティ間の関連付けを作成
1 つのエンティティのデータは、多くの場合、別のエンティティのデータに関連しています。 たとえば、**教師**エンティティと**クラス**エンティティがある場合、**クラス**エンティティには**教師**エンティティへの検索関係があり、どの教師がクラスを教えるかを示します。 **教師**エンティティからのデータを表示するための検索フィールドを使用できます。 これは一般的に検索フィールドと呼ばれます。

## <a name="define-a-relationship"></a>関連付けの定義
1 種類のエンティティから別の種類へと、複数の種類の関連付けを作成できます (またはエンティティとそれ自体の間)。 エンティティごとに複数のエンティティとの関連付けができ、各エンティティは別のエンティティに対して複数の関連付けを持つことができます。 共通の顧客間関係の種類は次のとおりです:

* **多対 1** - このタイプの関係付けでは、エンティティ A の各レコードはエンティティ B の複数のレコードとマッチングできますが、エンティティ B の各レコードはエンティティ A の 1 つのレコードとのみマッチングできます。たとえば、クラスには 1 つの教室があります。 これは、最も一般的な関連付けで、フィールド一覧では**検索フィールド**として表示されます
* **1 対多** - このタイプの関係付けでは、エンティティ B の各レコードはエンティティ A の複数のレコードとマッチングできますが、エンティティ A の各レコードはエンティティ B の 1 つのレコードとのみマッチングできます。たとえば、1 人の教師が複数のクラスで教えます。
* **多対多** - このタイプの関係付けでは、エンティティ A の各レコードはエンティティ B の複数のレコードにマッチングでき、その逆も同様です。 たとえば、生徒は複数のクラスに出席し、各クラスには複数の生徒がいます。

## <a name="add-a-lookup-field-many-to-one-relationship"></a>検索フィールドを追加する (多対 1 の関連付け)

エンティティへの検索関連を追加するには、**関連付け**タブで関連付けを作成し、関連付けを作成するエンティティを指定します。

1. [powerapps.com](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) で**データ**セクションを展開し、左側のナビゲーション ウィンドウで**エンティティ**をクリックまたはタップします。

    ![エンティティの詳細](./media/data-platform-cds-create-entity/entitylist.png "エンティティ リスト")

2. 既存のエンティティ、または [エンティティの新規作成](data-platform-create-entity.md) をクリックまたはタップします

3. **関連付け**をクリックします

4. **関連付けを追加**をクリックすると、新しいパネルが開いて関連付けを作成するエンティティを選択できます。 **関連エンティティ**ドロップダウンからエンティティを選択します。

    > [!div class="mx-imgBorder"] 
    > ![多対一の関連付け](./media/data-platform-cds-newrelationship/manytoone-1.png "多対一の関連付け")

5. エンティティを選択した後、検索フィールドが主エンティティで表示され、エンティティ名 (この例では教室) が既定で設定されますが、必要に応じて変更できます。

    ![多対一の関連付け](./media/data-platform-cds-newrelationship/manytoone-2.png "多対一の関連付け")

6. **完了**をクリックしてエンティティへの関連付けを追加し、**エンティティの保存**をクリックします。

    > [!div class="mx-imgBorder"] 
    > ![多対一の関連付け](./media/data-platform-cds-newrelationship/manytoone-3.png "多対一の関連付け")

## <a name="add-a-one-to-many-relationship"></a>一対多の関連付けを追加する

一対多の関連付けを追加するには、**関連付け**タブで関連付けを作成し、関連付けを作成するエンティティを指定します。

1. [powerapps.com](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) で**データ**セクションを展開し、左側のナビゲーション ウィンドウで**エンティティ**をクリックまたはタップします。

    ![エンティティの詳細](./media/data-platform-cds-create-entity/entitylist.png "エンティティ リスト")

2. 既存のエンティティ、または [エンティティの新規作成](data-platform-create-entity.md) をクリックまたはタップします

3. **関連付け**をクリックします

4. **関連付けを追加**の右側にある下矢印をクリックすると、両方の種類の関連付けの選択ができます。 **一対多**をクリックすると、新しいパネルが開いて関連付けを作成するエンティティを選択できます。 **関連エンティティ**ドロップダウンからエンティティを選択します。

    ![一対多の関連付け](./media/data-platform-cds-newrelationship/onetomany-1.png "一対多の関連付け")

5. エンティティを選択した後、検索フィールドが主エンティティで表示され、エンティティ名 (この例ではクラス) が既定で設定されますが、必要に応じて変更できます。

    > [!NOTE]
    > 1 対多の関連付けの場合、検索フィールドは現在選択したエンティティ上ではなく、関連エンティティ上で作成されます。 現在のエンティティで検索が必要な場合は、多対 1 の関連付けを作成してください。

    > [!div class="mx-imgBorder"] 
    > ![一対多の関連付け](./media/data-platform-cds-newrelationship/onetomany-2.png "一対多の関連付け")

6. **完了**をクリックしてエンティティへの関連付けを追加し、**エンティティの保存**をクリックします。

    > [!div class="mx-imgBorder"] 
    > ![一対多の関連付け](./media/data-platform-cds-newrelationship/onetomany-3.png "一対多の関連付け")

## <a name="add-a-many-to-many-relationship"></a>多対多関連付けの追加

現在これは、詳細メニューによってのみ使用できます。 PowerApps のホーム ページで、左のメニューから「詳細」をクリックします。 関連付けを作成する方法の詳細については、[N:N の関連付けの作成](/dynamics365/customer-engagement/customize/create-and-edit-nn-many-to-many-relationships) を参照してください

## <a name="use-a-lookup-field-in-an-app"></a>アプリで検索フィールドを使用します
検索フィールドを含むエンティティから [アプリを自動的に作成](../canvas-apps/data-platform-create-app.md) する場合、エンティティの**プライマリ名**フィールドからのデータを含む**ドロップダウン**コントロールとして表示されます。

## <a name="add-1n-and-nn-relationships-for-canvas-apps"></a>キャンバス アプリの 1:N および N:N の関連付けを追加
**関連付け** 機能を使用して、Common Data Service の 1 対多または多対多の関係を通じて 2 つのレコードをリンクします。 詳細: [PowerApps の関連付けと関連付け解除関数](../canvas-apps/functions/function-relate-unrelate.md)

## <a name="next-steps"></a>次のステップ
* [Common Data Service データベースを使用してアプリを生成](../canvas-apps/data-platform-create-app.md)
* [Common Data Service データベースを使用してアプリを最初から作成](../canvas-apps/data-platform-create-app-scratch.md)


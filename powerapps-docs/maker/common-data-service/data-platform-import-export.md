---
title: Common Data Service からデータをインポートまたはエクスポートする
description: Excel のデータを取得してデータをエクスポートする機能を使用して、Excel または CSV ファイルから Common Data Service のエンティティにデータを一括インポートおよびエクスポートする
author: sabinn-msft
ms.service: powerapps
ms.topic: conceptual
ms.component: cds
ms.date: 05/14/2018
ms.author: sabinn
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="import-or-export-data-from-common-data-service"></a>Common Data Service からデータをインポートまたはエクスポートする

Microsoft Excel または CSV ファイルからデータを一括インポートおよびエクスポートするには、更新された Common Data Service 環境に対して、Excel ファイルからデータを取得し、データをエクスポートする機能を使用します。

Excel または CSV ファイルからエンティティへファイルをインポートする方法は 2 つあります。

## <a name="option-1-import-by-creating-and-modifying-a-file-template"></a>オプション 1: ファイル テンプレートを作成し、変更して、インポート

すべてのエンティティには、入力ファイルに存在する必要があるフィールドが必要です。 テンプレートを作成することをお勧めします。 最初に、エンティティのデータをエクスポートします。 エンティティにデータをインポートするには、同じファイル (データで変更) を使用します。 このテンプレートは、時間と手間を節約します。 各エンティティに必要なフィールドを考慮する必要はありません。

1. テンプレート ファイルを準備します。

    a. エンティティ データを CVS ファイルにエクスポートします。 **データをエクスポートします。**の手順に従います。  
    b. データが一意であることを確認する計画を定義します。 **主キー**または**代替キー**を使用します。  
    c. データをエンティティにインポートする前に、データが一意であることを確認する手順については、次のセクションを参照してください。 

1. データでファイルを変更します。

    - Excel または CSV ファイルから作成したテンプレートにデータをコピーします。

1. ファイルをインポートします。  
    a. [powerapps.com](https://web.powerapps.com/) で、**データ** セクションを展開します。 左側のナビゲーション ウィンドウで、**エンティティ**を選択します。  
    b. データをインポートするエンティティを選択します。  
    c. 上の省略記号またはメニューを選択します。 **データ取得**を選択します。 **Excel からデータを取得**を選択します。  

    > [!NOTE]
    > 複数のエンティティにデータをインポートするには、トップ メニューの**データを取得**を選択します。 **Excel ファイルからデータを取得**を選択します。 その後、複数のエンティティを選択し**次へ**をクリックします。

    > [!div class="mx-imgBorder"] 
    > ![**アカウント** エンティティにデータをインポートする例](./media/data-platform-import-export/import-data-to-account.png)

    d. **データのインポート**画面で、Excel または CSV ファイルからデータをインポートするかどうかを選択します。  
    e. **アップロード**を選びます。  
    f. ファイルを選択します。 プロンプトに従ってファイルをアップロードします。  

    > [!div class="mx-imgBorder"] 
    > ![**アカウント** エンティティへファイルをアップロードする例](./media/data-platform-import-export/upload-account.png)

    g. ファイルがアップロードされ、**マッピングの状態**が緑になったら、右上にある**インポート**を選択します。 マッピング エラーをナビゲートして修正するには、次のセクションを参照してください。  

    > [!div class="mx-imgBorder"] 
    > ![正常な**マッピングの状態**および**インポート** ボタンの例](./media/data-platform-import-export/success-map-imp.png)

    h. インポートが正常に終了すると、挿入と更新の合計数が表示されます。  

    > [!div class="mx-imgBorder"] 
    > ![挿入と更新の回数を示す正常なインポートの例](./media/data-platform-import-export/success-imp-insert.png)

    > [!NOTE]
    > upsert (更新または挿入) ロジックを使用して、すでにレコードが存在する場合はレコードを更新するか、新しいレコードを挿入します。

## <a name="option-2-import-by-bringing-your-own-source-file"></a>オプション 2: 独自のソース ファイルを使用してインポート

Common Data Service エンティティの特定のエンティティに必要なフィールドを知っている上級ユーザーの場合は、独自の Excel または CSV ソース ファイルを定義します。 **ファイルのインポート**の手順を実行してください。

## <a name="navigate-mapping-errors"></a>マッピング エラーをナビゲートします。

ファイルをアップロードした後にマッピングのエラーが表示される場合は、**状態をマップ**を選択します。 フィールド マッピング エラーを確認および修正するには、次のステップに進みます。

1. **表示**の下の、右側にあるドロップダウン メニューを使用し、**マッピングされていないフィールド**、**エラーのフィールド**、または**必須フィールド**を使用可能にします。

    > [!TIP]
    > 表示された警告またはエラーによって、**フィールド マッピング** ドロップダウン メニューの**マップされていないフィールド**または**エラーのフィールド**を確認してください。

    > [!div class="mx-imgBorder"] 
    > ![フィールド マッピングによる警告による部分一致の例](./media/data-platform-import-export/partial-match.png)

    > [!div class="mx-imgBorder"] 
    > ![フィールド マッピングの問題をナビゲートする例](./media/data-platform-import-export/navigate-mappings.png)

    > [!div class="mx-imgBorder"] 
    > ![フィールド マッピングによる警告の検査と修正の例](./media/data-platform-import-export/inspect-warnings.png)

2. すべてのエラーと警告を解決したら、右上隅の**変更の保存**を選択します。 **データのインポート**画面に戻ります。
3. **マッピングの状態**が緑で**完了済み**と表示されたら、右上隅の**インポート**を選択します。
4. **インポートが正常に完了しました**というメッセージが表示されると、挿入および更新の合計が表示されます。

## <a name="ensure-uniqueness-when-you-import-data-into-an-entity-from-excel-or-csv"></a>Excel または CSV からエンティティにデータをインポートする際の一意性を保証する

Common Data Service エンティティは、Common Data Service エンティティ テーブル内のレコードを一意に識別するために主キーを使用します。 Common Data Service エンティティの主キーは、グローバル一意識別子 (GUID) です。 これは、レコードの識別のための既定の基準となります。 Common Data Service エンティティにデータをインポートするなどのデータ操作では、既定の主キーが表示されます。

例:   
**アカウント**のエンティティの主キーは **accountid** です。

   > [!div class="mx-imgBorder"] 
   > ![**アカウント** エンティティからのサンプル エクスポート ファイルは、主キーとしての **accountid** を示しています](./media/data-platform-import-export/export-pk.png)

場合によっては、外部ソースからのデータを統合するときに主キーが機能しないことがあります。 主キーの代わりにレコードを識別する代替キーを定義するには、Common Data Service を使用します。

例:   
**アカウント**のエンティティ用に、代替キーとして自然キー ベースの ID を使用して **transactioncurrencyid** を設定する場合があります。 たとえば前述した GUID 値 **88c6c893-5b45-e811-a953-000d3a33bcb9** の代わりに **US Dollar** を使用します。 キーとして**通貨記号**または**通貨の名前**を選択できます。

   > [!div class="mx-imgBorder"] 
   > ![**通貨**エンティティで代替キーを作成する例](./media/data-platform-import-export/create-ak.png)

   > [!div class="mx-imgBorder"] 
   > ![**アカウント** エンティティからのサンプル エクスポート ファイルは、自然キーとしての**通貨名**を示しています](./media/data-platform-import-export/export-nk.png)

代替キーを指定した後も、ユーザーは主キーを識別子として引き続き使用できます。 前のサンプルでは、GUID が有効なデータであれば、最初のファイルは有効です。

## <a name="export-data-to-csv"></a>CSV へのデータのエクスポート

標準エンティティまたはカスタム エンティティから一度だけデータをエクスポートできます。 また、一度に複数のエンティティからデータをエクスポートすることもできます。 複数のエンティティからデータをエクスポートすると、各エンティティは独自の Microsoft CSV ファイルにエクスポートされます。

1. [powerapps.com](https://web.powerapps.com/) で、**データ** セクションを展開します。 左側のナビゲーション ウィンドウで、**エンティティ**を選択します。
1. データをエクスポートするエンティティを選択します。
1. 上の省略記号またはメニューを選択します。 **エクスポート**を選択します。 **データ**を選択します。

    > [!div class="mx-imgBorder"] 
    > ![**アカウント** エンティティからデータをエクスポートする例](./media/data-platform-import-export/export-account.png)

    > [!NOTE]
    > 複数のエンティティからデータをエクスポートするには、トップ メニューで**エクスポート**を選択します。 **データ**を選択します。 複数のエンティティを選択することができます。

1. エクスポートが正常に終了すると**エクスポートしたデータをダウンロード**ができます。 このダウンロードは、ダウンロード可能 CSV ファイルにリンクされます。

    > [!div class="mx-imgBorder"] 
    > ![リンク ダウンロード可能ファイルでエクスポートが成功したサンプル エクスポート](./media/data-platform-import-export/export-success.png)

## <a name="unsupported-data-types"></a>サポートされていないデータの種類

次のデータの種類は現在サポートされていません。

- タイムゾーン
- MultiSelect オプション セット
- イメージ

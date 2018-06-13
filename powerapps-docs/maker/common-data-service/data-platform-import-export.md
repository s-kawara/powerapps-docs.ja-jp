---
title: Common Data Service for Apps からのデータのインポート/エクスポート
description: Excel からのデータ取得機能とデータのエクスポート機能を使って、Common Data Service (CDS) for Apps のエンティティに Excel または CSV ファイルのデータを一括でインポート/エクスポートする
author: sabinn-msft
ms.service: powerapps
ms.topic: conceptual
ms.component: cds
ms.date: 05/14/2018
ms.author: sabinn
ms.openlocfilehash: 7f3e16be5bba1874759e0f9e40dc455f1e29c2bc
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "34697580"
---
# <a name="import-or-export-data-from-the-common-data-service-for-apps"></a>Common Data Service for Apps からのデータのインポート/エクスポート

Excel または CSV ファイルからデータを一括インポート/エクスポートする機能が必要な場合、新しくなった Common Data Service (CDS) for Apps 環境で Excel ファイルからのデータ取得機能と、データのエクスポート機能を使用することができます。

Excel または CSV ファイルからエンティティにファイルをインポートする方法は 2 つあります

## <a name="option-1-import-by-creating-and-modifying-a-file-template"></a>オプション 1: ファイル テンプレートの作成と変更によるインポート

すべてのエンティティには、入力ファイルに必要な必須フィールドがあります。 よりシームレスな方法として、最初にエンティティからデータをエクスポートし、そのデータを (自分のデータで変更した) 同じファイルを使用してエンティティにインポートすることでテンプレートを作成する方法をお勧めします。 これにより、各エンティティの必須フィールドについて考慮する時間と労力が節約されます。

1. ファイル テンプレートを準備する

    - 最初に、「CSV にデータをエクスポートする」の手順に従って、エンティティ データを CSV ファイルにエクスポートします
    - 主キーまたは代替キーのどちらかを使用してデータの一意性を確保する計画を定義します
    - データをエンティティにインポートする前に一意性を確保する方法については、以下のセクションを参照してください

1. ファイルを自分のデータで変更する

    - 作成したテンプレートに、Excel または CSV ファイルのデータをコピーします

1. ファイルをインポートする
    - [powerapps.com](https://web.powerapps.com/) で、**[データ]** セクションを展開し、左側のナビゲーション ウィンドウで **[エンティティ]** をクリックまたはタップします
    - データをインポートするエンティティを選択します
    - 上部にある省略記号またはメニューをクリックし、**[Get Data]\(データを取得\)** を選択して、**[Excel からデータを取得]** をクリックまたはタップします

> [!NOTE]
> 複数のエンティティにデータをインポートする場合は、上部のメニューで **[Get Data]\(データを取得\)** を選択して、**[Excel からデータを取得]** をクリックまたはタップします。 複数のエンティティを選択して、**[次へ]** を押すことができます

![アカウント エンティティへのデータのインポートの例](./media/data-platform-import-export/import-data-to-account.png)

- この例では、Excel または CSV ファイルを使用したデータのインポートを選択できる、**[データのインポート]** 画面に移動します
- **[アップロード]** をクリックまたはタップします
- ファイルを選択し、指示に従って、ファイルのアップロードを開始します

![アカウント エンティティへのファイルのアップロードの例](./media/data-platform-import-export/upload-account.png)

- ファイルがアップロードされ、[Mapping Status]\(マッピング ステータス\) が緑色になったら、右上隅の **[インポート]** をクリックします。 マッピング中にエラーが発生した場合は、以下のセクションを参照してマッピング エラーを確認し、修正してください

![マッピング ステータスの成功と、[インポート] ボタンの例](./media/data-platform-import-export/success-map-imp.png)

- **インポートが正常に完了すると**、挿入と更新の合計が表示されます

![挿入と更新の回数を示す成功したインポートの例](./media/data-platform-import-export/success-imp-insert.png)

> [!NOTE]
> 既に存在するレコードを更新するか、新しいレコードを挿入するには、Upsert (Update または Insert) のロジックを使用します。

## <a name="option-2-import-by-bringing-your-own-source-file"></a>オプション 2: 自身のソース ファイルの使用によるインポート

Common Data service for Apps エンティティの所定のエンティティに必要なフィールドを熟知している上級ユーザーは、自分で Excel または CSV のソース ファイルを定義し、「**ファイルをインポートする**」の手順に従うことができます

## <a name="navigating-mapping-errors"></a>マッピング エラーのナビゲーション

ファイルのアップロード後にマッピング エラーが発生した場合は、**[Map status]\(マッピング ステータス\)** をクリックして以下の手順に従い、フィールド マッピング エラーを検査して修正します。

- 右側のドロップダウンの **[表示]** で、**[マップされていないフィールド]** または **[Fields with error]\(エラーがあるフィールド\)** または **[必須フィールド]** を選びます

> [!TIP]
> 警告とエラーのどちらが表示されているかに応じて、**[Field Mappings]\(フィールド マッピング\)** のドロップダウン操作で **[マップされていないフィールド]** または **[Fields with error]\(エラーがあるフィールド\)** の検査から始めます

![フィールド マッピングの警告が原因による部分一致の例](./media/data-platform-import-export/partial-match.png)

![フィールド マッピングの問題のナビゲーションの例](./media/data-platform-import-export/navigate-mappings.png)

![ フィールド マッピングの警告の調査と修正の例](./media/data-platform-import-export/inspect-warnings.png)

- すべてのエラーと警告を修正したら、右上隅の **[変更の保存]** をクリックすると、**[データのインポート]** 画面に戻ります
- **[Mapping Status]\(マッピング ステータス\)** 列に **[完了]** が緑色で示されたら、右上隅の **[インポート]** をクリックします
- **[インポートが正常に完了しました]** というメッセージが表示されると、挿入と更新の合計が表示されます

## <a name="ensuring-uniqueness-while-importing-data-into-entity-from-excel-or-csv"></a>エンティティに Excel または CSV のデータをインポート中に一意性を確保する

Common Data Service for Apps エンティティは主キーを使用して CDS エンティティ テーブル内のレコードを一意に識別します。 CD エンティティの主キーは、グローバル一意識別子 (GUID) で、レコード識別の既定の基礎となります。 CDS エンティティへのデータのインポートのようなデータ操作によって既定の主キーが表示されます。

例: アカウント エンティティの主キーが accountid

![主キーとして accountid が示されているアカウント エンティティからのサンプル エクスポート ファイル](./media/data-platform-import-export/export-pk.png)

場合によっては、外部ソースからのデータの統合では主キーが要件を十分に満たさない可能性があります。 このため、CDS では主キーの代わりにレコードを一意に識別する代替キーを定義できます。

例: アカウント エンティティで、ナチュラル キー ベースの識別を使用して 'transactioncurrencyid' を代替キーとして使用することができます (例: 上記の GUID 値 *88c6c893-5b45-e811-a953-000d3a33bcb9* の代わりに ‘US Dollar’ を使用する)。 通貨記号、または通貨名をキーとして選択することもできます。

![通貨エンティティの代替キーの作成例](./media/data-platform-import-export/create-ak.png)

![ナチュラル キーとして通貨名が示されているアカウント エンティティからのサンプル エクスポート ファイル](./media/data-platform-import-export/export-nk.png)

代替キーを指定した後も、引き続き主キーを識別子として使用することができます。 したがって、指定した GUID が有効なデータであれば、上記の最初のサンプル ファイルも有効です。

## <a name="export-data-to-csv"></a>CSV にデータをエクスポートする

標準エンティティまたはカスタム エンティティからデータを 1 回限りエクスポートしたり、複数のエンティティから一度にデータをエクスポートしたりすることができます。 複数のエンティティからデータをエクスポートした場合、各エンティティがそれぞれ異なる Microsoft CSV ファイルにエクスポートされます。

1. [powerapps.com](https://web.powerapps.com/) で、**[データ]** セクションを展開し、左側のナビゲーション ウィンドウで **[エンティティ]** をクリックまたはタップします
1. データをエクスポートするエンティティを選択します
1. 上部にある省略記号またはメニューをクリックし、**[エクスポート]** を選択して、**[データ]** をクリックまたはタップします

    ![アカウント エンティティからのデータのエクスポートの例](./media/data-platform-import-export/export-account.png)

    > [!NOTE]
    > 複数のエンティティからデータをエクスポートする場合、上部のメニューで **[エクスポート]** を選択して、**[データ]** をクリックまたはタップします。 複数のエンティティを選択できるようになります

1. エクスポートが正常に完了すると、**[エクスポートされたデータのダウンロード]** ができるようになります。このデータにはダウンロード可能な CSV ファイルへのリンクが含まれています

    ![ダウンロード可能なファイルのリンクが表示されエクスポートが成功したことを示すサンプルのエクスポート](./media/data-platform-import-export/export-success.png)

## <a name="unsupported-data-types"></a>サポートされていないデータ形式

次のデータ形式は現在サポートされていません

- タイムゾーン
- 複数選択オプション セット
- イメージ

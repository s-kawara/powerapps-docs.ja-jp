---
title: SharePoint 接続の概要 | Microsoft Docs
description: For SharePoint は、使用可能な関数、応答、および例を参照してください。
author: NickWaggoner
manager: kvivek
ms.service: powerapps
ms.topic: reference
ms.custom: canvas
ms.reviewer: anneta
ms.date: 04/03/2019
ms.author: niwaggon
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 65ce3b7736b55f3734d6da7d945965ed791a3ce4
ms.sourcegitcommit: 4fe0a71efd54c1f4d22a279aa74c6bde3d908b9d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/04/2019
ms.locfileid: "59007891"
---
# <a name="connect-to-sharepoint-from-a-canvas-app"></a>キャンバス アプリから SharePoint に接続します。

![SharePoint](./media/connection-sharepoint-online/sharepointicon.png)

カスタムの一覧からアプリを自動的に生成する SharePoint サイトに接続するか、既存のアプリにデータを追加したり、アプリをゼロから作成する前に、接続を作成します。

によって、データが存在するいずれかまたは両方の手法を実行できます。

- SharePoint Online サイトまたはオンプレミス サイトでは、カスタムの一覧からデータを表示します。
- イメージを表示し、(SharePoint Online のみ) ライブラリのビデオまたはオーディオ ファイルを再生します。

## <a name="generate-an-app"></a>アプリを生成する

PowerApps には、カスタム リストでデータを管理する場合は、 [3 画面アプリを自動的に生成](../app-from-sharepoint.md)します。 ユーザーは、最初の画面で一覧を参照して、2 番目の画面で項目の詳細を表示、作成、または 3 番目の画面で項目を更新できます。

> [!NOTE]
> SharePoint リストに含まれている場合、**選択肢**、**ルックアップ**、または**ユーザーまたはグループ**列を参照してください[ギャラリーでデータを表示する](connection-sharepoint-online.md#show-list-columns-in-a-gallery)このトピックで後述します。

## <a name="create-a-connection"></a>接続を作成する

1. [PowerApps にサインイン](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)を選択します**データ** > **接続**左側のナビゲーション バーで、**新しい接続**近く、左上隅にあります。

    > [!div class="mx-imgBorder"]
    > ![データを選択 >、左側のナビゲーション バーでの接続および左上隅の近くの新しい接続を順に選択します。](./media/connection-sharepoint-online/new-connection.png)

1. 右上隅の近くの検索ボックスに入力するか貼り付けます**SharePoint**、し、 **SharePoint**します。

    > [!div class="mx-imgBorder"]
    > ![右上隅の近くの検索ボックスには、入力または貼り付けます SharePoint、し、SharePoint を選択します。](./media/connection-sharepoint-online/select-sharepoint.png)

1. これらの一連の手順のいずれかを実行します。

    - SharePoint Online に接続するには、選択**直接接続 (クラウド サービス)** を選択します**作成**、(メッセージは表示) する場合に資格情報を提供します。

        > [!div class="mx-imgBorder"]
        > ![SharePoint Online に接続するには、直接接続 (クラウド サービス) を選択します。](./media/connection-sharepoint-online/select-online.png)

        接続を作成すると既存のアプリにデータを追加またはアプリをゼロから作成できます。

    - オンプレミス サイトに接続するには、選択 **、オンプレミス データ ゲートウェイを使用して接続**します。

        > [!div class="mx-imgBorder"]
        > ![オンプレミス サイトに接続する、次のように選択します * * オンプレミス データ ゲートウェイを使用して接続)。](./media/connection-sharepoint-online/select-onprem.png)

        認証の種類として **[Windows]** を指定し、資格情報を入力します  (資格情報にドメイン名が含まれる場合は、*<ドメイン>\<エイリアス>* 形式で入力します)。

        > [!div class="mx-imgBorder"]
        > ![資格情報の指定](./media/connection-sharepoint-online/specify-creds.png)

        **ゲートウェイを選択する**、ゲートウェイを使用し、するを選択します**作成**です。

        > [!NOTE]
        > インストールされているオンプレミス データ ゲートウェイがあるない場合[いずれかをインストール](../gateway-reference.md)、し、ゲートウェイの一覧を更新するアイコンを選択します。

        > [!div class="mx-imgBorder"]
        > ![ゲートウェイの選択](./media/connection-sharepoint-online/choose-gateway.png)

        接続を作成すると既存のアプリにデータを追加またはアプリをゼロから作成できます。

## <a name="add-data-to-an-existing-app"></a>既存のアプリにデータを追加します。

1. PowerApps Studio では、更新、オンにするアプリを開きます、**ビュー** 、タブを選び**データソース**します。

    > [!div class="mx-imgBorder"]
    > ![データ ソースを選択し、表示 タブ](./media/connection-sharepoint-online/view-data-sources.png)

1. **データ**ペインで、**データ ソースの追加** > **SharePoint**します。

1. **SharePoint サイトへの接続**、内のエントリを選択、**最近使ったサイト**リスト (または型または貼り付けを使用するサイトの URL)、し、 **Connect**します。

    > [!div class="mx-imgBorder"]
    > ![サイトを選択します。](./media/connection-sharepoint-online/select-sp-site.png)

1. **一覧の選択**、チェック ボックスをオン**ドキュメント**または 1 つまたは複数のリストを使用し、する**Connect**:

    > [!div class="mx-imgBorder"]
    > ![一覧 の ドキュメントのチェック ボックスまたは、使用する 1 つ以上のリストを選択し、接続を選択](./media/connection-sharepoint-online/select-sp-tables.png)

    すべての種類のリストが既定で表示されるわけではありません。 PowerApps ではカスタム リストはサポートされますが、テンプレート ベースのリストはサポートされません。 使用するリストの名前が表示されない場合、一番下までスクロールし、ボックスが含まれているリストの名前を入力**カスタム テーブル名の入力**します。

    > [!div class="mx-imgBorder"]
    > ![カスタム リスト名を入力するボックスで、リストの名前を入力します。](./media/connection-sharepoint-online/custom-list.png)

    データ ソースまたはソースは、アプリに追加されます。

## <a name="build-your-own-app-from-scratch"></a>ゼロからアプリをビルドします。

概念を適用[アプリをゼロから作成](../get-started-create-from-blank.md)Excel ではなく SharePoint にします。

## <a name="show-list-columns-in-a-gallery"></a>ギャラリーのリスト内の列を表示します。

カスタム リストがこのような列が含まれる場合にデータを表示、**ギャラリー**コントロール、数式バーを使用して、**テキスト**プロパティを 1 つ以上の**ラベル**そのギャラリー コントロール:

- **選択肢**または**ルックアップ**列指定**ThisItem** 。_ColumnName_**します。値**その列のデータを表示します。

    たとえば、**Location** という名前の**選択肢**列がある場合は「**ThisItem.Location.Value**」と指定し、**PostalCode** という名前の**ルックアップ**列がある場合は「**ThisItem.PostalCode.Value**」と指定します。

- **ユーザーまたはグループ**列指定**ThisItem** 。_ColumnName_**します。DisplayName**ユーザーまたはグループの名前を表示します。

    たとえば、**Manager** という名前の**ユーザーまたはグループ**列の名前を表示する場合は、「**ThisItem.Manager.DisplayName**」と指定します。

    メール アドレスや役職など、ユーザーに関する別の情報を表示することもできます。 オプションの完全な一覧を表示するには指定**ThisItem** 。_ColumnName_**します。** (末尾はピリオドを含む)。

    > [!NOTE]
    > **CreatedBy**列指定**ThisItem.Author.DisplayName**の一覧で項目を作成したユーザーの表示名を表示します。 **ModifiedBy** 列のリストの項目を変更したユーザーの表示名を表示するには、「**ThisItem.Editor.DisplayName**」と指定します。

- **Managed Metadata**列指定**ThisItem** 。_ColumnName_**します。ラベル**その列のデータを表示します。

    たとえば、**Languages** という名前の **管理されたメタデータ**列がある場合は「**ThisItem.Languages.Label**」と指定します。

## <a name="show-data-from-a-library"></a>ライブラリからデータを表示

追加できるかどうか、SharePoint ライブラリにいくつかのイメージがある、**ドロップダウン**ユーザーに表示するイメージを指定できるように、アプリを制御します。 適用することも、同じ原則、他のコントロールになど**ギャラリー**コントロール、および他の種類のビデオなどのデータ。

1. 既に、していない場合は[接続を作成](#create-a-connection)、し[既存のアプリにデータを追加](#add-data-to-an-existing-app)します。

1. 追加、**ドロップダウン**制御、および名前を付けます**ImageList**します。

1. 設定、**項目**プロパティの**ImageList**に**ドキュメント**します。

1. **プロパティ**オープンの右側のウィンドウのタブ、**値**、一覧表示し、**名前**します。

    ライブラリ内のイメージのファイル名が表示される**ImageList**します。

    > [!div class="mx-imgBorder"]
    > ![イメージの一覧](./media/connection-sharepoint-online/dropdown-items.png)

1. 追加、**イメージ**を制御して、設定、**イメージ**プロパティをこの式に。

    `ImageList.Selected.'Link to item'`

1. F5 キーを押すし、別の値を選択**ImageList**します。

    指定したイメージが表示されます。

    > [!div class="mx-imgBorder"]
    > ![サンプル イメージ](./media/connection-sharepoint-online/golden-honey.png)

できます[サンプル アプリをダウンロード](https://pwrappssamples.blob.core.windows.net/samples/spdoclib_blogapp.msapp)を SharePoint ライブラリからデータを表示するより複雑な方法を示しています。

1. アプリをダウンロードした後に開く[PowerApps Studio](https://us.create.powerapps.com/studio/#)を選択します**開く**左側のナビゲーション バーで、**参照**。
1. **開く**ダイアログ ボックスの検索しダウンロードしたファイルを開き、このトピックの最初の 2 つの手順に従ってデータ ソースとして SharePoint ライブラリを追加します。

> [!NOTE]
> 既定では、このアプリが表示されます[委任の警告](../delegation-overview.md)は、ライブラリには、500 未満の項目が含まれている場合無視できます。

この単一画面アプリでは、左上隅にある一覧には、ライブラリ内のすべてのファイルが表示されます。

- 入力または貼り付けるいずれかのファイルを検索できます。 または検索ボックスに使用できる文字は、上部します。
- ライブラリにフォルダーが含まれている場合は、タイトル バーのすぐ下のフォルダーの一覧で、フィルターのアイコンを選択して、ファイルの一覧をフィルターできます。

ファイルが見つかったら、選択で表示するよう、**ビデオ**、**イメージ**、または**オーディオ**に沿って、右側にあるコントロール。

> [!div class="mx-imgBorder"]
> ![サンプル イメージ](./media/connection-sharepoint-online/library-app.png)

## <a name="known-issues"></a>既知の問題

### <a name="lists"></a>一覧表示します。

PowerApps はスペースが含まれている列名を読み取ることができますが、スペースは 16 進数のエスケープ コードに置き換えられます **"\_x0020\_"** します。 たとえば、SharePoint の **"Column Name"** は、PowerApps のデータ レイアウトに表示されるときや数式で使用されるときは **"Column_x0020_Name"** と表示されます。

列のすべての種類はサポートされているし、列のすべての種類は、あらゆる種類のカードをサポートします。

| 列の種類 | サポート | 既定のカード |
| --- | --- | --- |
| 1 行テキスト |はい |テキストの表示 |
| 複数行テキスト |はい |View text |
| 選択肢 |はい |ルックアップの表示<br>ルックアップの編集<br>複数選択の表示<br>複数選択の編集 |
| Number |はい |パーセンテージの表示<br>評価の表示<br>View text |
| 通貨 |はい |パーセンテージの表示<br>評価の表示<br>View text |
| 日付と時刻 |はい |View text |
| ルックアップ |はい |ルックアップの表示<br>ルックアップの編集<br>複数選択の表示<br>複数選択の編集 |
| ブール値 (はい/いいえ) |はい |View text<br>トグルの表示 |
| 人物またはグループ |はい |ルックアップの表示<br>ルックアップの編集<br>複数選択の表示<br>複数選択の編集 |
| ハイパーリンク |はい |URL の表示<br>View text |
| 画像 |はい (読み取り専用) |画像の表示<br>View text |
| 添付ファイル |はい (読み取り専用) |添付ファイルの表示|
| 集計値 |はい (読み取り専用) | |
| タスクの結果 |いいえ | |
| 外部データ |いいえ | |
| 管理されたメタデータ |はい (読み取り専用) | |
| 評価 |いいえ | |

### <a name="libraries"></a>ライブラリ

- PowerApps からライブラリにファイルをアップロードすることはできません。
- PDF ビューアー コントロールでは、ライブラリから PDF ファイルを表示できません。
- PowerApps Mobile をサポートしていない、**ダウンロード**関数。
- 場合は、ユーザーは、PowerApps Mobile または Windows 10 アプリでアプリを実行するを使用して、**起動**ギャラリーでライブラリのコンテンツを表示する関数。

## <a name="next-steps"></a>次の手順

- [データ ソースからデータを表示する方法](../add-gallery.md)を学習する。
- [詳細を表示する方法とレコードを作成または更新する方法](../add-form.md)を学習する。
- 接続できる他の種類の[データ ソース](../connections-list.md)を確認する。

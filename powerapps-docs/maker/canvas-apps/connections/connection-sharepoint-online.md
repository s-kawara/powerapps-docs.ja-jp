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
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61549355"
---
# <a name="connect-to-sharepoint-from-a-canvas-app"></a>キャンバス アプリから SharePoint に接続します。

![SharePoint](./media/connection-sharepoint-online/sharepointicon.png)

SharePoint サイトに接続してカスタム リストから自動的にアプリを生成するか、既存のアプリにデータを追加したりアプリをゼロから作成したりする前に、接続を作成します。

データが存在する場所に応じて、次のいずれかまたは両方の方法をとることができます。

- SharePoint Online サイトまたはオンプレミス サイトのカスタムリストからデータを表示します。
- ライブラリー内のイメージを表示し、ビデオまたはオーディオファイルを再生します (SharePoint Online のみ)。

## <a name="generate-an-app"></a>アプリを生成する

カスタム リスト内のデータを管理する場合は、PowerAppsが [3 画面アプリを自動的に生成](../app-from-sharepoint.md)します。 ユーザーは、最初の画面で一覧を参照し、2 番目の画面で項目の詳細を表示し、3 番目の画面で項目を作成または更新することができます。

> [!NOTE]
> SharePoint リストに、**選択肢**、**ルックアップ**、または**ユーザーまたはグループ**列が含まれている場合は、このトピックの後半の[ギャラリーでデータを表示する](connection-sharepoint-online.md#show-list-columns-in-a-gallery)を参照してください。

## <a name="create-a-connection"></a>接続を作成する

1. [PowerApps にサインイン](http://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)し、左側ナビゲーションバーで**データ**  >  **接続**を選択してから、左上隅の近くにある**新しい接続**を選択します。

    > [!div class="mx-imgBorder"]
    > ![データを選択 >、左側のナビゲーション バーでの接続および左上隅の近くの新しい接続を順に選択します。](./media/connection-sharepoint-online/new-connection.png)

1. 右上隅近くの検索ボックスに**SharePoint**と入力または貼り付けて、**SharePoint**を選択します。

    > [!div class="mx-imgBorder"]
    > ![右上隅の近くの検索ボックスには、入力または貼り付けます SharePoint、し、SharePoint を選択します。](./media/connection-sharepoint-online/select-sharepoint.png)

1. 以下の手順のいずれかを実行します。

    - SharePoint Online に接続するには、**直接接続 (クラウド サービス)** を選択し、**作成** を選択してから資格情報を入力します (要求された場合)。

        > [!div class="mx-imgBorder"]
        > ![SharePoint Online に接続するには、直接接続 (クラウド サービス) を選択します。](./media/connection-sharepoint-online/select-online.png)

        接続が作成され、既存のアプリにデータを追加するかまたはアプリをゼロから作成することができます。

    - オンプレミス サイトに接続するには、**オンプレミス データ ゲートウェイを使用して接続** を選択します。

        > [!div class="mx-imgBorder"]
        > ![オンプレミス サイトに接続する、次のように選択します * * オンプレミス データ ゲートウェイを使用して接続)。](./media/connection-sharepoint-online/select-onprem.png)

        認証の種類として **[Windows]** を指定し、資格情報を入力します (資格情報にドメイン名が含まれる場合は、 *<ドメイン>\<エイリアス>* 形式で入力します)。

        > [!div class="mx-imgBorder"]
        > ![資格情報を指定します。](./media/connection-sharepoint-online/specify-creds.png)

        **ゲートウェイを選択する**で、使用するゲートウェイを選択して**作成**を選択します。

        > [!NOTE]
        > オンプレミス データ ゲートウェイがインストールされていない場合は、[インストール](../gateway-reference.md)してから、アイコンを選択してゲートウェイのリストを更新します。

        > [!div class="mx-imgBorder"]
        > ![ゲートウェイを選択します。](./media/connection-sharepoint-online/choose-gateway.png)

        接続が作成され、既存のアプリにデータを追加するかまたはアプリをゼロから作成することができます。

## <a name="add-data-to-an-existing-app"></a>既存のアプリにデータを追加します。

1. PowerApps Studio で、更新するアプリを開き、**ビュー** タブを選択して、**データソース** を選択します。

    > [!div class="mx-imgBorder"]
    > ![データ ソースを選択し、表示 タブ](./media/connection-sharepoint-online/view-data-sources.png)

1. **データ** ペインで、**データ ソースの追加** > **SharePoint** を選択します。

1. **SharePoint サイトに接続** で、**最近利用したサイト** のリストからエントリーを選択し (または使用するサイトの URL を入力するか貼り付けて)、**接続** を選択します。

    > [!div class="mx-imgBorder"]
    > ![サイトを選択します。](./media/connection-sharepoint-online/select-sp-site.png)

1. **リストの選択**で、**ドキュメント** または使用する1 つ以上のリストのチェックボックスをオンにして、**接続**を選択します。

    > [!div class="mx-imgBorder"]
    > ![一覧 の ドキュメントのチェック ボックスまたは、使用する 1 つ以上のリストを選択し、接続を選択](./media/connection-sharepoint-online/select-sp-tables.png)

    既定では、すべての種類のリストが表示されるわけではありません。 PowerApps は、テンプレート ベースのリストではなく、カスタム リストをサポートしています。 使用するリストの名前が表示されない場合、一番下までスクロールし、**カスタム テーブル名の入力** ボックスにリストの名前を入力します。

    > [!div class="mx-imgBorder"]
    > ![カスタム リスト名を入力するボックスで、リストの名前を入力します。](./media/connection-sharepoint-online/custom-list.png)

    データ ソースまたはソースが、アプリに追加されます。

## <a name="build-your-own-app-from-scratch"></a>ゼロからアプリをビルドします。

[アプリをゼロから作成](../get-started-create-from-blank.md)の概念を、Excel ではなく SharePoint に適用します。

## <a name="show-list-columns-in-a-gallery"></a>ギャラリーのリスト内の列を表示します。

カスタム リストがこのような列が含まれる場合にデータを表示、**ギャラリー**コントロール、数式バーを使用して、**テキスト**プロパティを 1 つ以上の**ラベル**そのギャラリー コントロール:

- **選択肢**または**ルックアップ**列指定**ThisItem** 。_ColumnName_**します。値**その列のデータを表示します。

    たとえば、**Location** という名前の**選択肢**列がある場合は「**ThisItem.Location.Value**」と指定し、**PostalCode** という名前の**ルックアップ**列がある場合は「**ThisItem.PostalCode.Value**」と指定します。

- **ユーザーまたはグループ**列指定**ThisItem** 。_ColumnName_**します。DisplayName**ユーザーまたはグループの名前を表示します。

    たとえば、**Manager** という名前の**ユーザーまたはグループ**列の名前を表示する場合は、「**ThisItem.Manager.DisplayName**」と指定します。

    メール アドレスや役職など、ユーザーに関するさまざまな情報を表示することもできます。 オプションの完全なリストを表示するには、**ThisItem.ColumnName.** を指定します (末尾のピリオドを含む)。

    > [!NOTE]
    > リストに項目を作成したユーザーの表示名を表示するには、**CreatedBy** 列に **ThisItem.Author.DisplayName** を指定します。 リスト内の項目を変更したユーザーの表示名を表示するには、**ModifiedBy** 列に **ThisItem.Editor.DisplayName** を指定します。

- **Managed Metadata**列指定**ThisItem** 。_ColumnName_**します。ラベル**その列のデータを表示します。

    たとえば、**Languages** という名前の **管理されたメタデータ**列がある場合は「**ThisItem.Languages.Label**」と指定します。

## <a name="show-data-from-a-library"></a>ライブラリからデータを表示

SharePoint ライブラリに複数の画像がある場合は、**ドロップダウン** コントロールをアプリに追加して、表示する画像をユーザーが指定させることができます。 **ギャラリー** コントロールなどの他のコントロールや、ビデオなどの他の種類のデータにも同じ原則を適用できます。

1. まだ接続していない場合は、[接続を作成](#create-a-connection)してから、[既存のアプリにデータを追加](#add-data-to-an-existing-app)します。

1. **ドロップダウン** コントロールを追加し、**ImageList** という名前を付けます。

1. **ImageList** の **項目** プロパティを **ドキュメント** に設定します。

1. 右側のウィンドウの **プロパティ** タブで、**値** リストを開き、**名前** を選択します。

    ライブラリ内の画像ファイル名は、**ImageList** に表示されます。

    > [!div class="mx-imgBorder"]
    > ![イメージの一覧](./media/connection-sharepoint-online/dropdown-items.png)

1. **画像** コントロールを追加し、その **画像** プロパティを次の式に設定します。

    `ImageList.Selected.'Link to item'`

1. F5 キーを押して、**ImageList** で別の値を選択します。

    指定したイメージが表示されます。

    > [!div class="mx-imgBorder"]
    > ![サンプル イメージ](./media/connection-sharepoint-online/golden-honey.png)

SharePoint ライブラリのデータを表示するためのより複雑な方法を示す[サンプル アプリをダウンロード](https://pwrappssamples.blob.core.windows.net/samples/spdoclib_blogapp.msapp)できます。

1. アプリをダウンロードした後に開く[PowerApps Studio](https://us.create.powerapps.com/studio/#)を選択します**開く**左側のナビゲーション バーで、**参照**。
1. **開く** ダイアログ ボックスで、ダウンロードしたファイルを見つけて開き、このトピックの最初の 2 つの手順に従って SharePoint ライブラリをデータソースとして追加します。

> [!NOTE]
> 既定では、このアプリは[委任の警告](../delegation-overview.md)を表示しますが、ライブラリに含まれている項目が 500 未満である場合は無視できます。

この単一画面アプリでは、左下隅にあるリストには、ライブラリ内のすべてのファイルが表示されます。

- 上部の検索ボックスに１つ以上の文字を入力するか貼り付けることでファイルを検索できます。
- ライブラリにフォルダーが含まれている場合は、タイトル バーのすぐ下のフォルダーの一覧で、フィルターのアイコンを選択して、ファイルの一覧をフィルターできます。

必要なファイルが見つかったら、それらを選択して、右側の **ビデオ**、**イメージ**、または **オーディオ** コントロールに表示します。

> [!div class="mx-imgBorder"]
> ![サンプル イメージ](./media/connection-sharepoint-online/library-app.png)

## <a name="known-issues"></a>既知の問題

### <a name="lists"></a>リスト

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
- PowerApps Mobile は、**ダウンロード**機能をサポートしていません。
- ユーザーが PowerApps Mobile のアプリまたは Windows 10 アプリを実行する場合は、**起動**機能を使用してライブラリ コンテンツをギャラリーに表示します。

## <a name="next-steps"></a>次の手順

- [データ ソースからデータを表示する方法](../add-gallery.md)を学習する。
- [詳細を表示する方法とレコードを作成または更新する方法](../add-form.md)を学習する。
- 接続できる他の種類の[データ ソース](../connections-list.md)を確認する。

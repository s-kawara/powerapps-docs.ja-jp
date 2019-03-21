---
title: SharePoint リスト フォームのカスタマイズ | Microsoft Docs
description: PowerApps を使用して、SharePoint リストのエントリをユーザーが作成および更新するのに使用するフォームをカスタマイズします。
author: AFTOwen
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 12/17/2018
ms.author: anneta
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: ca97583948a289240bfb051fa8cac36a39e2ffee
ms.sourcegitcommit: c6ad6ba7814c5e7b12c3b7b76bf2e7718bf41b8c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/19/2019
ms.locfileid: "58198638"
---
# <a name="customize-a-sharepoint-list-form-by-using-powerapps"></a>PowerApps を使用した SharePoint リスト フォームのカスタマイズ

SharePoint リスト フォームは、ブラウザーで PowerApps を開くことで簡単にカスタマイズすることができます。 C# などの従来のコードを記述したり、InfoPath などの別のアプリをダウンロードしたりする必要はありません。 変更を発行すると、すべてのユーザーが使用できるように、SharePoint リスト内にフォームが埋め込まれます。 PowerApps では、分析レポートを確認したり、条件付き書式を簡単に作成したり、他のデータ ソースに接続することもできます。

このトピックの手順を行うには、カスタマイズがどのように機能しているかを確認できるように、単純なリストを作成してから、同じ概念を独自のリストに適用できます。

> [!NOTE]
> 自分のリストで **[フォームのカスタマイズ]** オプションが使用できない、または正常に動作しない場合は、[PowerApps がサポートしない](connections/connection-sharepoint-online.md#known-issues)データ型が含まれている場合があります。 また、フォームを別のリストまたは[環境](working-with-environments.md)に移動することはできません。

## <a name="create-a-list"></a>リストを作成します。

SharePoint サイトでリストを作成し、リストにこれらの列を追加します。

- **詳細** (はい/いいえ)
- **価格** (通貨)
- **利用可能** (時刻なしの日付)
- **色** (選択)

> [!div class="mx-imgBorder"]
> ![サイト コンテンツの選択 > 新規 > リスト、リスト名の種類および作成を選択します。 各列の選択列の追加、リストの種類を指定 (はい/いいえ、通貨、日付、選択)、リストの名前 (詳細は、価格、可用性、色) を指定し、保存を選択します。](./media/customize-list-form/create-list.gif)

## <a name="open-the-form"></a>フォームを開きます。

1. コマンド バーで選択**PowerApps**、し、**フォームをカスタマイズする**します。

    同じブラウザー タブに PowerApps Studio が開きます。

1. **[PowerApps Studio へようこそ]** ダイアログ ボックスが開いたら、**[スキップ]** を選びます。

> [!div class="mx-imgBorder"]
> ![コマンド バーで、PowerApps を選択し、カスタマイズ フォームを選択します。 同じブラウザー タブに PowerApps Studio が開きます。PowerApps Studio ダイアログ ボックスへようこそ を開くと場合、は、スキップを選択します。](./media/customize-list-form/create-form.gif)

## <a name="move-and-remove-a-field"></a>移動し、フィールドの削除

1. ドラッグ、**可用性**フィールドの一覧の一番下のフィールド。

    指定した順序で、フィールドが表示されます。

1. ポインターを合わせる、**添付ファイル**フィールドを選択し、表示される省略記号 (...) を選択します。**削除**します。

    フォームから指定したフィールドが表示されなくなります。

> [!div class="mx-imgBorder"]
> ![フィールドの一覧の一番下には、可用性のフィールドをドラッグします。 添付ファイル フィールドをポイントしが表示されたら、省略記号 (...) を選択し、[削除] を選択します。](./media/customize-list-form/move-remove-fields.gif)

## <a name="set-conditional-formatting"></a>条件付き書式を設定する

**[詳細]** を [はい] に設定した場合にのみ、**[価格]**、**[利用可能]**、**[色]** のフィールドが表示されるように構成できます。

1. 左側のナビゲーション バーで  **Details_DataCard1**、メモの末尾に表示される数字と**DataCardValue**します。

1. 設定、**可視性**のプロパティ、**色**、**可用性**、および**価格**カードをこの式に (置換、必要に応じて、数値を前の手順でメモしたもの):

    **If(DataCardValue2.Value = true, true)**

1. Alt キーを押しながら、**[詳細]** トグルをクリックまたはタップして、複数回選択します。

    構成した 3 つのフィールドが表示され、フォームから消えます。

> [!div class="mx-imgBorder"]
> ![左側のナビゲーション バーでは、DataCardValue の最後に表示される数字に注意してください。 次の数式にカードの色、可用性、および価格の可視性プロパティを設定します。 、Alt キーを押しながら、詳細コントロールを複数回選択します。](./media/customize-list-form/conditional-format.gif)

## <a name="save-and-publish-the-form"></a>保存して、フォームの発行

1. **[ファイル]** メニューを開き、**[保存]** を選択し、**[SharePoint に発行]** を 2 回選択します。

1. 左上隅で、戻る矢印を選択し、**[SharePoint に戻る]** を選択します。

> [!div class="mx-imgBorder"]
> ![ファイル メニューを開き保存 を選択し、SharePoint に発行を 2 回選択します。 左上隅で、[戻る] 矢印を選択し、SharePoint に戻る をクリックします。](./media/customize-list-form/save-form.gif)

## <a name="further-customize-your-form"></a>さらに、フォームをカスタマイズします。

1. 一覧を開き、選択**新規**コマンド バーで、**カスタマイズ**フォームの上部にあります。

1. これらのトピックについて説明するような方法のさまざまなフォームをカスタマイズします。

    - サイズ、向き、またはその両方を変更する (例: [フォームの幅を広げる](set-aspect-ratio-portrait-landscape.md))。
    - [1 つまたは複数のカードのカスタマイズ](working-with-cards.md)(たとえば、カードの表示テキストまたは入力コントロールを変更します)。
    - [ルックアップ フィールド](sharepoint-lookup-fields.md)を作成する。

    詳細情報:[SharePoint フォームの統合を理解します。](sharepoint-form-integration.md)

## <a name="use-the-default-form"></a>既定のフォームを使用する

1. SharePoint でリストから (右上隅の歯車アイコンを選んで) 設定ページを開き、**[リストの設定]** を選択します。

2. **[全般設定]** の下で **[フォームの設定]** を選択します。

3. **[フォームの設定]** ページで、これらのオプションのいずれかを選択し、**[OK]** を選択します。

    - **既定の SharePoint フォームを使用する**: ユーザーがリストを開き、コマンド バーで **[新規]** を選択すると、そのリストの既定のフォームが表示されます。

    - **Use a custom form created in PowerApps \(PowerApps で作成されたカスタム フォームを使用する\)**: ユーザーがリストを開き、コマンド バーで **[新規]** を選択すると、カスタム フォームが表示されます  (または、PowerApps でフォームをもう一度発行することもできます)。

    これらのオプションは、必要に応じて切り替えることができます。

    ![[フォームの設定] オプション](./media/customize-list-form/form-settings.png)

## <a name="delete-the-custom-form"></a>カスタム フォームの削除

1. SharePoint でリストから (右上隅の歯車アイコンを選んで) 設定ページを開き、**[リストの設定]** を選択します。

1. **[全般設定]** の下で **[フォームの設定]** を選択します。

1. **[フォームの設定]** ページで、**[既定の SharePoint フォームを使用する]** を選択し、**[Delete custom form]\(カスタム フォームの削除\)** を選択します。

    ![カスタム フォームの削除](./media/customize-list-form/use-default-sharepoint.png)

## <a name="q--a"></a>Q &AMP; A

### <a name="forms-vs-apps"></a>フォームとアプリ

**Q:** SharePoint または PowerApps から作成したスタンドアロン アプリから、カスタマイズしたフォームの違い

**A:** SharePoint リスト フォームをカスタマイズする場合は、フォームが PowerApps Studio または PowerApps Mobile でアプリとして表示されません。 フォームは、それを作成したリストからのみ開くことができます。

**Q:** SharePoint リストにデータを管理するためのフォームをカスタマイズする必要がありますとスタンドアロン アプリの作成とする必要がありますか。

**A:** ユーザーを (たとえば、デスクトップ ブラウザー) で SharePoint を離れることがなくデータを管理する場合は、フォームをカスタマイズします。 ユーザーが SharePoint の外部で (たとえばモバイル デバイスなどで) データを管理できるようにする場合は、アプリを作成します。

**Q:** フォームをカスタマイズし、同じリストのアプリを作成できますか。

**A:** はい。

**Q:** リストのカスタマイズし、同じ機能を使用してアプリを作成できますか。

**A:** はい。

**Q:** 自分の組織で、既定の環境以外の環境でフォームをカスタマイズできますか。

**A:** いいえ。

### <a name="manage-your-custom-form"></a>カスタム フォームを管理する

**Q:** 共有する方法は簡単にフォームの他のユーザーですか。

**A:** フォームを開き、選択**リンクのコピー**リンクを送信し、フォームを使用するすべてのユーザー。

**Q:** 他のユーザーに表示される自分の変更を加えずにフォームを更新できますか。

**A:** はい。 フォームの変更と保存は何度でもできますが、変更内容は **[SharePoint に発行]** を 2 回選択するまで他のユーザーには表示されません。

**Q:** リスト フォームをカスタマイズし、間違えた場合はできるは、以前のバージョンに戻しますか。

**A:** はい。

1. リストを開き、コマンド バーで **[PowerApps]** を選択し、**[フォームをカスタマイズ]** を選択します。

1. PowerApps Studio で、**[ファイル]**、**[すべてのバージョンの表示]** の順に選択します。 **[バージョン]** ページが新しいブラウザー タブに表示されます。

    > [!NOTE]
    > **[すべてのバージョンの表示]** ボタンが表示されていない場合は、**[保存]** を選択します。 ボタンが表示されるはずです。

1. **[バージョン]** ページ (つまり、ブラウザー タブ) を閉じずに、元のブラウザー タブの **[保存]** ページに戻って、左側のナビゲーション ウィンドウの上部にある矢印をクリックまたはタップします。次に、**[SharePoint に戻る]** をクリックまたはタップしてフォームのロックを解除し、PowerApps Studio を閉じます。

1. さきほどのブラウザー タブの **[バージョン]** ページに戻り、復元するバージョンを見つけて、**[復元]** を選択します。

    > [!NOTE]
    > フォームが別のユーザーによってロックされているために復元が失敗したというエラー メッセージが表示された場合は、そのユーザーがフォームのロックを解除するまで待機してからやり直してください。

**Q:** できるフォーム 1 つのリストから別に移動しますか。

**A:** いいえ。

### <a name="administer-your-custom-form"></a>カスタム フォームを管理する

**Q:** フォームを共有する方法はありますか

**A:** フォームを共有する必要はありません - フォームが SharePoint リストからのアクセス許可を継承します。 フォームのカスタマイズが完了したら、他のユーザーが使用できるように[そのフォームを SharePoint に発行しなおす](customize-list-form.md#save-and-publish-the-list-form-back-to-sharepoint)だけです。

**Q:** フォームをカスタマイズすることができますか。

**A:** を管理する SharePoint の権限を持っているユーザーは、設計、または、関連付けられているリストを編集します。

**Q:** 作成またはカスタム リスト フォームを使用する PowerApps のライセンスが必要ですか。

**A:** 必要があります、 [PowerApps を含む Office 365 プラン](https://docs.microsoft.com/power-platform/admin/pricing-billing-skus.md#licenses)します。

**Q:** ゲスト ユーザーがカスタム形式の一覧にアクセスすると起こりますか。

**A:** ゲスト ユーザーは、PowerApps を使用してカスタマイズされているリスト フォームへのアクセスを試みると、エラー メッセージを取得します。

**Q:** 管理者は、すればすべてのカスタマイズされたフォームの一覧で自分の組織ですか。

**A:** PowerApps のテナント管理者、または環境管理者のアクセス許可がある組織の既定の PowerApps 環境で、次の操作を行います。

1. [PowerApps 管理センター](https://admin.powerapps.com)で、環境のリストから、組織の既定の環境を選択します。

1. 既定の環境のページ上部で、**[リソース]** を選択します。

1. アプリのリストから、アプリの種類が **SharePoint Form** のアプリを探します。これらは、カスタマイズされたフォームです。

    ![カスタマイズされたフォームのリスト](./media/customize-list-form/all-customized-forms.png)

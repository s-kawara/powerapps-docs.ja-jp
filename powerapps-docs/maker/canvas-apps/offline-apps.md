---
title: オフライン対応キャンバス アプリを開発する | Microsoft Docs
description: オンラインまたはオフラインにかかわらず、ユーザーが生産性を高めることができるオフライン対応キャンバス アプリを開発します。
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 01/31/2019
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 8004a39e83ea3615ce8a77637a9f5c0271b67781
ms.sourcegitcommit: 157ab15738e2d0d1bf9097bbb7b9e3d9c29a4015
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/28/2019
ms.locfileid: "66265693"
---
# <a name="develop-offline-capable-canvas-apps"></a>オフライン対応キャンバス アプリを開発する

モバイル ユーザーは多くの場合、生産性を向上する必要がありますが限定されている場合や接続されていないもします。 キャンバス アプリをビルドすると、これらのタスクを実行できます。

- PowerApps Mobile を開き、オフラインのときにアプリを実行します。
- [Connection](../canvas-apps/functions/signals.md#connection) シグナル オブジェクトを使用して、アプリの接続状態 (オフライン、オンライン、または従量制課金接続) を判別します。
- オフライン時の基本的なデータ ストレージで、[コレクション](../canvas-apps/create-update-collection.md) と [LoadData や SaveData](../canvas-apps/functions/function-savedata-loaddata.md) などの関数を使用します。

## <a name="limitations"></a>制限事項

**LoadData**と**SaveData**ローカル デバイスに少量のデータを格納する単純なメカニズムをフォームに結合します。 これらの関数を使用すると、アプリに単純なオフライン機能を追加できます。

これらの関数は、メモリ内コレクションで動作するために、利用可能なアプリのメモリの量によって制限されます。 使用可能なメモリは、デバイス、オペレーティング システム、PowerApps Mobile を使用して、メモリ、および画面とコントロールの観点から、アプリの複雑さによって異なります。 多くのメガバイト単位のデータを格納する場合は、期待を実行しているデバイスで想定されるシナリオを使用してアプリをテストします。 一般に、使用可能なメモリのメガバイト数を 30 ~ 70 があります。

関数もしない自動的にマージ競合の解決、デバイスがオンラインにします。 どのようなデータが保存され、再接続を処理する方法の構成は、式を作成するときに、最大、メーカーが。

オフライン機能で更新プログラムは、このトピックに戻り、購読、 [PowerApps ブログ](https://powerapps.microsoft.com/blog/)します。

## <a name="overview"></a>概要

オフライン シナリオを設計するとき、アプリがデータを扱う方法を検討する必要があります最初。 PowerApps でアプリは主に、一連のデータにアクセス[コネクタ](../canvas-apps/connections-list.md)SharePoint、Office 365、Common Data Service など、プラットフォームを提供します。 RESTful エンドポイントを提供するサービスへのアプリのアクセスを可能にするカスタム コネクタを構築することもできます。 Web API や Azure Functions などのサービスが考えられます。 これらのコネクタは、すべてがインターネット経由で HTTPS を使用します。つまり、ユーザーは、データやサービスが提供するその他の機能にアクセスするには、オンラインである必要があります。

![PowerApps とコネクタ](./media/offline-apps/online-app.png)

### <a name="handling-offline-data"></a>オフライン データの処理

PowerApps では、することができますをフィルター処理、検索、並べ替え、集計、およびデータ ソースに関係なく一貫した方法でデータを操作します。 ソースの範囲は、アプリでメモリ内コレクションから SQL データベースおよび Common Data Service への SharePoint リストです。 一貫性のために簡単に別のデータ ソースを使用するアプリを再ターゲットすることができます。 さらに重要なオフラインのシナリオのことができますコレクションを使用するローカル データ管理のため、アプリのロジックをほとんど変更せずにします。 実際、ローカル コレクションは、オフライン データを処理するための主要メカニズムです。

## <a name="build-an-offline-app"></a>オフライン アプリをビルドします。

アプリの開発のオフラインの側面にフォーカスを保持するには、は、このトピックでは、Twitter に重点を置いた単純なシナリオを示しています。 Twitter の投稿を読むし、オフライン時のツイートを送信することができます、アプリを構築します。 アプリは、オンラインになったときに、ツイートを投稿し、ローカル データを再度読み込みます。

高レベルは、アプリは、これらのタスクを実行します。

- ユーザーがアプリを開いたとき。

  - デバイスがオンラインの場合、アプリが Twitter コネクタを使用してデータをフェッチし、そのデータをコレクションを設定します。
  - アプリを使用してローカル キャッシュ ファイルからデータを読み込みます、デバイスがオフラインの場合、 [ **LoadData** ](../canvas-apps/functions/function-savedata-loaddata.md)関数。
  - ユーザーは、ツイートを送信できます。 アプリがオンラインの場合、Twitter に直接、ツイートを投稿し、ローカル キャッシュを更新します。

- 5 分ごと、アプリがオンラインの間。

  - アプリは、ローカル キャッシュ内ですべてのツイートを投稿します。
  - アプリがローカル キャッシュを更新しを使用して保存、 [ **SaveData** ](../canvas-apps/functions/function-savedata-loaddata.md)関数。

### <a name="step-1-add-twitter-to-a-blank-phone-app"></a>手順 1:空の携帯電話アプリに Twitter を追加する.

1. PowerApps Studio では、選択**ファイル** > **新規**します。
1. **[空のアプリ]** タイルで、 **[携帯電話レイアウト]** を選択します。
1. **[ビュー]** タブで **[データソース]** を選択します。
1. **データ**ペインで、**データ ソースの追加**します。
1. 選択**新しい接続** > **Twitter** > **作成**です。
1. 資格情報を入力し、接続の作成、閉じます、**データ**ウィンドウ。

### <a name="step-2-collect-existing-tweets"></a>手順 2:既存のツイートを収集します。

1. **ツリー ビュー**ペインで、**アプリ**、し、設定、 **OnStart**に次の式のプロパティ。

    ```powerapps-dot
    If( Connection.Connected,
        ClearCollect( LocalTweets, Twitter.SearchTweet( "PowerApps", {maxResults: 10} ) );
            Set( statusText, "Online data" ),
        LoadData( LocalTweets, "LocalTweets", true );
            Set( statusText, "Local data" )
    );
    SaveData( LocalTweets, "LocalTweets" );
    ```

    > [!div class="mx-imgBorder"]
    > ![数式にツイートを読み込む](./media/offline-apps/load-tweets.png)

1. **ツリー ビュー**ウィンドウで、省略記号のメニューで選択、**アプリ**オブジェクトを選び**実行 OnStart**その数式を実行します。

    > [!div class="mx-imgBorder"]
    > ![ツイートを読み込むための式を実行します。](./media/offline-apps/load-tweets-run.png)

    > [!NOTE]
    > **LoadData**と**SaveData**関数は、ブラウザーがサポートされないために、PowerApps Studio でのエラーを表示可能性があります。 ただし、実行します通常このアプリをデバイスに展開した後。

この数式は、デバイスがオンラインかどうかを確認します。

- デバイスがオンラインの場合、数式に検索用語"PowerApps"で最大 10 個のツイートを読み込みます、 **LocalTweets**コレクション。
- デバイスがオフラインの場合、数式は、使用できる場合は、"LocalTweets"をという名前のファイルからローカル キャッシュを読み込みます。

### <a name="step-3-show-tweets-in-a-gallery"></a>手順 3:ギャラリーでツイートを表示します。

1. **挿入**] タブで [**ギャラリー** > **変動する高さを空白**します。

1. 設定、**項目**のプロパティ、 [**ギャラリー** ](controls/control-gallery.md)に制御を`LocalTweets`します。

1. ギャラリー テンプレートで 3 つの追加[**ラベル**](controls/control-text-box.md)コントロール、およびセット、**テキスト**これらの値のいずれかには、各ラベルのプロパティ。

    - `ThisItem.UserDetails.FullName & " (@" & ThisItem.UserDetails.UserName & ")"`
    - `Text(DateTimeValue(ThisItem.CreatedAtIso), DateTimeFormat.ShortDateTime)`
    - `ThisItem.TweetText`

1. テキストを太字で最後のラベル、ギャラリーのようにこのようにします。

    > [!div class="mx-imgBorder"]
    > ![サンプル ツイートを表示するギャラリー](./media/offline-apps/tweet-gallery.png)

### <a name="step-4-show-connection-status"></a>手順 4.接続の状態を表示します。

1. ギャラリーの下のラベルを挿入し、設定し、その**色**プロパティを**Red**します。

1. 最新のラベルの設定**テキスト**に次の式のプロパティ。

    `If( Connection.Connected, "Connected", "Offline" )`

この数式は、デバイスがオンラインかどうかを判断します。 かどうかは、ラベル**接続**、それ以外のことを示しています**オフライン**します。

### <a name="step-5-add-a-box-to-compose-tweets"></a>手順 5.ツイートを作成するためのボックスを追加します。

1. 接続状態のラベルの下に挿入、 [**テキスト入力**](controls/control-text-input.md)制御、および名前を変更して**NewTweetTextInput**します。

1. テキスト入力ボックスの設定**既定**プロパティを`""`します。

    > [!div class="mx-imgBorder"]
    > ![ギャラリーの状態情報とテキスト入力ボックス](./media/offline-apps/status-input.png)

### <a name="step-6-add-a-button-to-post-the-tweet"></a>手順 6:ツイートを投稿するためのボタンを追加します。

1. テキスト入力ボックスの下で追加、**ボタン**を制御して、設定、**テキスト**プロパティをこの値に。

    `"Tweet"`

1. ボタンの設定**OnSelect**に次の式のプロパティ。

    ```powerapps-dot
    If( Connection.Connected,
        Twitter.Tweet( "", {tweetText: NewTweetTextInput.Text} ),
        Collect( LocalTweetsToPost, {tweetText: NewTweetTextInput.Text} );
            SaveData( LocalTweetsToPost, "LocalTweetsToPost" )
    );
    Reset( NewTweetTextInput );
    ```  

1. **OnStart**プロパティを**アプリ**数式の末尾に行を追加します。

    ```powerapps-dot
    If( Connection.Connected,
        ClearCollect( LocalTweets, Twitter.SearchTweet( "PowerApps", {maxResults: 100} ) );
            Set( statusText, "Online data" ),
        LoadData( LocalTweets, "LocalTweets", true );
            Set( statusText, "Local data" )
    );
    SaveData( LocalTweets, "LocalTweets" );
    LoadData( LocalTweetsToPost, "LocalTweetsToPost", true );  // added line
    ```

    > [!div class="mx-imgBorder"]
    > ![数式をコメント解除された行を含むツイートを読み込むの実行します。](./media/offline-apps/load-tweets-save.png)

この数式は、デバイスがオンラインかどうかを決定します。

- デバイスがオンラインの場合は、すぐに、ツイートを投稿します。
- ツイートをキャプチャし、デバイスがオフラインの場合、 **LocalTweetsToPost**コレクション、デバイスに保存します。

数式がテキスト入力ボックス内のテキストにリセットされます。

### <a name="step-7-check-for-new-tweets"></a>手順 7:新しいツイートをチェック

1. ボタンの右側にある、追加、**タイマー**コントロール。

    > [!div class="mx-imgBorder"]
    > ![最終的なアプリ](./media/offline-apps/final-app.png)

1. タイマーの設定**期間**プロパティを**300000**します。

1. タイマーの設定**AutoStart**と**繰り返します**プロパティ**true**します。

1. タイマーの設定**OnTimerEnd**に次の式。

    ```powerapps-dot
    If( Connection.Connected,
        ForAll( LocalTweetsToPost, Twitter.Tweet( "", {tweetText: tweetText} ) );
        Clear( LocalTweetsToPost );
        ClearCollect( LocalTweets, Twitter.SearchTweet( "PowerApps", {maxResults: 10} ) );
        SaveData( LocalTweets, "LocalTweets" );
   )
    ```

この数式は、デバイスがオンラインかどうかを判断します。 アプリのすべての項目のツイートがの場合、 **LocalTweetsToPost**コレクションし、コレクションをクリアします。

## <a name="test-the-app"></a>アプリケーションをテストする

1. インターネットに接続されているモバイル デバイスでアプリを開きます。

    ギャラリーで、既存のツイートが表示され、状態を示しています**接続**します。

1. デバイスの機内モードを有効にして、wi-fi を無効化して、インターネットからデバイスを切断します。

    状態ラベルは、アプリがあること**オフライン**します。

1. デバイスがオフラインの間の記述を含むツイート**PowerApps**を選び、**ツイート**ボタンをクリックします。

    ツイートがローカルで格納されている、 **LocalTweetsToPost**コレクション。

1. デバイスの機内モードを無効にして、wi-fi を有効にすると、インターネットにデバイスを再接続します。

    5 分以内は、アプリは、ギャラリーに表示されると、ツイートを投稿します。

この記事では、オフライン アプリを構築するための PowerApps の機能について、その概要を説明しました。 いつものように、[フォーラム](https://powerusers.microsoft.com/t5/PowerApps-Forum/bd-p/PowerAppsForum1)にフィードバックをお送りください。また、作成したオフライン アプリを [PowerApps コミュニティ ブログ](https://powerusers.microsoft.com/t5/PowerApps-Community-Blog/bg-p/PowerAppsBlog)でサンプルとして共有してください。
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
ms.openlocfilehash: f9922c64769aeacd9b9b65cc3039b091ac7fe353
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61538363"
---
# <a name="develop-offline-capable-canvas-apps"></a>オフライン対応キャンバス アプリを開発する

モバイル アプリ開発者として直面する最も一般的なシナリオは、接続が制限されている場合やまったく接続できない場合でも、ユーザーの生産性を損なわないようにすることです。 PowerApps には、オフライン対応キャンバス アプリを開発するために役立つ機能と動作のセットがあります。 次のことが行えます。

* オフラインのときに PowerApps Mobile を起動できます。
* 開発したアプリをオフライン時に実行できます。
* [Connection](../canvas-apps/functions/signals.md#connection) シグナル オブジェクトを使用して、アプリの接続状態 (オフライン、オンライン、または従量制課金接続) を判別します。
* オフライン時の基本的なデータ ストレージで、[コレクション](../canvas-apps/create-update-collection.md) と [LoadData や SaveData](../canvas-apps/functions/function-savedata-loaddata.md) などの関数を使用します。

## <a name="limitations"></a>制限事項

**LoadData**と**SaveData**ローカル デバイスに少量のデータを格納する単純なメカニズムをフォームに結合します。 これらの関数を使用すると、アプリに単純なオフライン機能を追加できます。  

これらの関数は、メモリ内コレクションで動作するために、利用可能なアプリのメモリの量によって制限されます。 使用可能なメモリは、デバイス、オペレーティング システム、PowerApps Mobile を使用して、メモリ、および画面とコントロールの観点から、アプリの複雑さによって異なります。 多くのメガバイト単位のデータを格納する場合は、期待を実行しているデバイスで想定されるシナリオを使用してアプリをテストします。 一般に、使用可能なメモリの 30 日と 70 のメガバイト数の間にあるはずです。  

関数も自動的が解決しないマージの競合データが保存され、再接続を処理する方法の構成は、式を作成するときまで、メーカーが、デバイスがオフラインに戻るから接続する場合。

オフライン シナリオの機能の拡張に取り組んでいます。 このページと [PowerApps ブログ](https://powerapps.microsoft.com/blog/)を定期的にご覧ください。アップデートの予定を告知しています。

## <a name="how-to-build-offline-capable-apps"></a>オフライン対応アプリを構築する方法

オフライン シナリオで最初に検討することは、アプリがデータを操作する方法です。 PowerApps のアプリは、主に、一連の[コネクタ](../canvas-apps/connections-list.md) を通して、SharePoint、Office 365、Common Data Service などのプラットフォームが提供するデータにアクセスします。 RESTful エンドポイントを提供するサービスへのアプリのアクセスを可能にするカスタム コネクタを構築することもできます。 Web API や Azure Functions などのサービスが考えられます。 これらのコネクタは、すべてがインターネット経由で HTTPS を使用します。つまり、ユーザーは、データやサービスが提供するその他の機能にアクセスするには、オンラインである必要があります。

![PowerApps とコネクタ](./media/offline-apps/online-app.png)

### <a name="handling-offline-data"></a>オフライン データの処理
PowerApps の最も興味深い側面の 1 つは、データのフィルター処理、検索、並べ替え、集計、および操作を、データ ソースに関係なく一貫した方法で実行することを可能にする一連の機能と数式です。 ソースは、アプリ内のメモリ内コレクションから、SharePoint リスト、SQL データベース、および Common Data Service に及びます。 この一貫性によって、アプリのターゲットを簡単に変更して、別のバックエンドを使用することができます。 ここでさらに重要なのは、アプリのロジックをほとんど変更せずに、データ管理でローカル コレクションを使用できることです。 実際、ローカル コレクションは、オフライン データを処理するための主要メカニズムです。

## <a name="building-an-offline-twitter-app"></a>オフラインの Twitter アプリケーションを構築する
アプリ開発のオフラインの側面へのフォーカスを維持するために、Twitter に重点を置いた単純なシナリオを示します。 オフライン中に Twitter の投稿を読み、ツイートを送信することができるアプリを作成します。 アプリは、オンラインになったときに、ツイートを投稿し、ローカル データを再度読み込みます。

大まかに言えば、アプリは、次の動作を行います。

1. アプリの起動時 (最初の画面の **OnVisible** プロパティに基づきます):

   * デバイスがオンラインの場合は、Twitter コネクタに直接アクセスしてデータをフェッチし、そのデータをコレクションに設定します。
   * デバイスがオフラインの場合は、[LoadData](../canvas-apps/functions/function-savedata-loaddata.md) を使用してローカル キャッシュ ファイルからデータを読み込みます。
   * ユーザーはツイートを送信できます。オンラインの場合は Twitter に直接投稿され、ローカル キャッシュが更新されます。
2. オンラインの場合は 5 分間隔で次の操作を実行します。

   * ローカル キャッシュ内のツイートを投稿します。
   * ローカル キャッシュを更新し、[SaveData](../canvas-apps/functions/function-savedata-loaddata.md) を使用して保存します。

### <a name="step-1-create-a-new-phone-app"></a>手順 1:新しい電話アプリを作成します。
1. PowerApps Studio を開きます。
2. **[新規]** > **[空のアプリ]** > **[電話レイアウト]** をクリックするかタップします。

    ![空のアプリ, 電話レイアウト](./media/offline-apps/blank-app.png)

### <a name="step-2-add-a-twitter-connection"></a>手順 2:Twitter 接続の追加

1. **[コンテンツ]** > **[データ ソース]** をクリックするかタップし、**[データ ソース]** パネルで **[データ ソースの追加]** を選択します。

2. **[新しい接続]** をクリックするかタップし、**[Twitter]** を選択し、**[作成]** をクリックするかタップします。

3. 資格情報を入力し、接続を作成します。

    ![Twitter 接続の追加](./media/offline-apps/twitter-connection.png)

### <a name="step-3-load-tweets-into-a-localtweets-collection-on-app-startup"></a>手順 3:アプリの起動時に LocalTweets コレクションにツイートを読み込む
アプリで **Screen1** の **OnVisible** プロパティを選択し、次の数式をコピーします。

```powerapps-dot
If( Connection.Connected,
    ClearCollect( LocalTweets, Twitter.SearchTweet( "PowerApps", {maxResults: 100} ) );
        UpdateContext( {statusText: "Online data"} ),
    LoadData(LocalTweets, "Tweets", true);
        UpdateContext( {statusText: "Local data"} )
);
LoadData( LocalTweetsToPost, "LocalTweets", true );
SaveData( LocalTweets, "Tweets" )
```

![ツイートを読み込むための数式](./media/offline-apps/load-tweets.png)

この数式は、デバイスがオンラインかどうかをチェックします。

* デバイスがオンラインの場合は、**LocalTweets** コレクションに最大 100 個のツイートを、検索用語 "PowerApps" 付きで読み込みます。
* デバイスがオフラインの場合は、"Tweets" という名前のファイルからローカル キャッシュを読み込みます (使用できる場合)。

### <a name="step-4-add-a-gallery-and-bind-it-to-the-localtweets-collection"></a>手順 4.ギャラリーを追加して LocalTweets コレクションにバインド

1. 新しい柔軟な高さギャラリーを挿入します。**挿入** > **ギャラリー** > **変動する高さを空白**します。

2. **Items** プロパティを **LocalTweets** に設定します。

3. 各ツイートのデータを表示する 4 つの**ラベル** コントロールを追加し、次の **Text** プロパティを設定します。
   * **ThisItem.TweetText**
   * **ThisItem.UserDetails.FullName & " \@" & ThisItem.UserDetails.UserName**
   * **"RT: " & ThisItem.RetweetCount**
   * **Text(DateTimeValue(ThisItem.CreatedAtIso), DateTimeFormat.ShortDateTime)**
4. **イメージ** コントロールを追加し、**Image** プロパティを **ThisItem.UserDetails.ProfileImageUrl** に設定します。

### <a name="step-5-add-a-connection-status-label"></a>手順 5.接続状態ラベルを追加します。
新しい**ラベル** コントロールを追加し、その **Text** プロパティを次の数式に設定します。

```If( Connection.Connected, "Connected", "Offline" )```

この数式は、デバイスがオンラインかどうかをチェックします。 オンラインの場合、ラベルのテキストは [接続中] になり、それ以外の場合は [オフライン] になります。

### <a name="step-6-add-a-text-input-to-compose-new-tweets"></a>手順 6:新しいツイートを作成するテキスト入力の追加します。

1. "NewTweetTextInput" という名前の新しい**テキスト入力**コントロールを挿入します。

2. テキスト入力の **Reset** プロパティを **resetNewTweet** に設定します。

### <a name="step-7-add-a-button-to-post-the-tweet"></a>手順 7:ツイートを投稿するためのボタンを追加します。
1. **ボタン** コントロールを追加し、**Text** プロパティを "Tweet" に設定します。
2. **OnSelect** プロパティを次の式に設定します。

    ```powerapps-dot
    If( Connection.Connected,
        Twitter.Tweet( "", {tweetText: NewTweetTextInput.Text} ),
        Collect( LocalTweetsToPost, {tweetText: NewTweetTextInput.Text} );
            SaveData( LocalTweetsToPost, "LocalTweetsToPost" )
    );
    UpdateContext( {resetNewTweet: true} );
    UpdateContext( {resetNewTweet: false} )
    ```  

この数式は、デバイスがオンラインかどうかをチェックします。

* デバイスがオンラインの場合、テキストはすぐにツイートされます。
* デバイスがオフラインの場合、ツイートは **LocalTweetsToPost** コレクション内にキャプチャされてアプリに保存します。

その後、数式は、テキスト ボックス内のテキストをリセットします。

### <a name="step-8-add-a-timer-to-check-for-tweets-every-five-minutes"></a>手順 8:5 分ごとにツイートをチェックするタイマーを追加します。
新しい**タイマー** コントロールを追加します。

* **Duration** プロパティを 300000 に設定します。

* **AutoStart** プロパティを true に設定します。

* **OnTimerEnd** を次の数式に設定します。

    ```powerapps-dot
    If( Connection.Connected,
        ForAll( LocalTweetsToPost, Twitter.Tweet( "", {tweetText: tweetText} ) );
        Clear( LocalTweetsToPost);
        Collect( LocalTweetsToPost, {tweetText: NewTweetTextInput.Text} );
        SaveData( LocalTweetsToPost, "LocalTweetsToPost" );
        UpdateContext( {statusText: "Online data"} )
    )
    ```

この数式は、デバイスがオンラインかどうかをチェックします。 オンラインの場合、アプリは、**LocalTweetsToPost** コレクション内のすべての項目をツイートします。 その後、コレクションをクリアします。

これでアプリは完成しました。テストに進む前に、外観を確認しましょう。 左側のアプリは接続されています。右側のアプリはオフラインであり、再びオンラインになったときに投稿するためのツイートが 1 つあります。

![完成したアプリのオンライン モードとオフライン モード](./media/offline-apps/finished-app.png)

## <a name="testing-the-app"></a>アプリのテスト
次の手順でアプリをテストします。

1. モバイル デバイスがオンラインのときに PowerApps を実行します。 オンライン中に少なくとも 1 回アプリを実行して、アプリをデバイスにダウンロードする必要があります。
2. Twitter アプリを起動します。
3. ツイートが読み込まれ、状態に **[接続中]** が表示されます。
4. PowerApps を完全に閉じます。
5. デバイスを機内モードに設定して、確実にオフラインにします。
6. PowerApps を実行します。 Twitter アプリをオフラインで実行でき、このデバイスがオンライン状態のときに実行していたその他のアプリにアクセスできます (つまり、PowerApps は、デバイスにまだダウンロードされていないすべてのアプリを非表示にします)。
7. アプリをもう一度実行します。
8. 接続状態が正しく反映されていることを確認してください (**[オフライン]**)。
9. 新しいツイートを書きます。 それは、**LocalTweetsToPost** コレクション内にローカルに格納されます。
10. 機内モードを終了します。 タイマーがトリガーされた後、アプリは、ツイートを投稿します。

この記事では、オフライン アプリを構築するための PowerApps の機能について、その概要を説明しました。 いつものように、[フォーラム](https://powerusers.microsoft.com/t5/PowerApps-Forum/bd-p/PowerAppsForum1)にフィードバックをお送りください。また、作成したオフライン アプリを [PowerApps コミュニティ ブログ](https://powerusers.microsoft.com/t5/PowerApps-Community-Blog/bg-p/PowerAppsBlog)でサンプルとして共有してください。


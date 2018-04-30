---
title: キャンバス アプリとは | Microsoft Docs
description: PowerApps のキャンバスからカスタム基幹業務アプリを設計して作成する方法を説明します
documentationcenter: na
author: AFTOwen
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: conceptual
ms.component: canvas
ms.date: 03/14/2018
ms.author: anneta
ms.openlocfilehash: 224f75e4254807163ffdb646e9ea109af5f50db5
ms.sourcegitcommit: 8bd4c700969d0fd42950581e03fd5ccbb5273584
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="what-are-canvas-apps-in-powerapps"></a>PowerApps のキャンバス アプリとは
PowerApps へようこそ。 PowerApps は、ブラウザーや携帯電話、タブレットで動作するビジネス アプリを構築できるサービスです。しかも、コードを記述する必要はありません。 PowerApps では、PowerPoint の視覚的なドラッグ アンド ドロップの概念と、Excel のようなロジックおよびデータ操作のための式が組み合わされています。

PowerApps を使うと、[Microsoft とサード パーティのさまざまなソース](connections-list.md)からのビジネス データを、1 つの強力なアプリに統合することができます。 また、ユーザーが SharePoint、Power BI、Teams で実行できるアプリを作成することもできます。

アプリの構築に慣れていない場合は、PowerApps のテンプレートとサンプル データを利用できます。これらを使うとすぐにアプリを構築でき、後でビジネス ニーズに合うようにカスタマイズできます。 ある程度の経験や創造性があれば、すぐに独自のアプリをゼロから作成できます。 経験豊富な開発者であれば、高度な機能を活用して、まさに革新を起こすことができます。 想像できるのであれば、構築可能です。

## <a name="generate-an-app-automatically"></a>アプリを自動的に生成する
PowerApps では、次のようなデータ ソースからアプリを簡単に自動生成できます。

* [Common Data Service for Apps](data-platform-create-app.md)
* [SharePoint](app-from-sharepoint.md)
* [Excel](get-started-create-from-data.md)
* [SQL Server](connections/connection-azure-sqldatabase.md)
* [Salesforce](add-manage-connections.md)
* [Dynamics 365](connections/connection-dynamics-crmonline.md)

[テンプレートからアプリを生成する](get-started-test-drive.md)こともできます。 それぞれのテンプレートには、Dropbox などのクラウド アカウント内の架空データが使われています。 特定の画面や UI 要素 ([コントロール](reference-properties.md)と言います) を観察してその構成方法についての理解を深め、実際にカスタマイズしてみることによって独自のアプリに適用できる手法を見つけてください。

## <a name="customize-an-app"></a>アプリをカスタマイズする
アプリを自動生成するときは、PowerApps がデータを中心に既定のインターフェイスを設計しますが、ユーザーのワークフローに基づいてアプリの外観と動作をカスタマイズすることができます。 たとえば、表示するデータの種類、データを並べ替える方法、さらにはユーザーが入力またはスライダーの調整によって数値を指定できるかどうか、といったことを変更できます。 [画面](add-screen-context-variables.md)、[ギャラリー](customize-layout-sharepoint.md)、[フォーム](customize-forms-sharepoint.md)、他のコントロールを追加したりカスタマイズしたりして、アプリのパフォーマンスを最適化できます。

さらによいアプリにするためのアイデアについては、[サンプル アプリを開いて](open-and-run-a-sample-app.md)みてください。ある程度の創造性と少しの経験で生み出すことができる何かを感じ取ることができるでしょう。

![サンプル アプリ](./media/getting-started/sample-apps.png)

## <a name="create-an-app-from-scratch"></a>アプリを最初から作成する
アプリを自動的に生成する作業を 1 ～ 2 回経験し、カスタマイズのノウハウがある程度得られたら、[アプリを最初から作成](get-started-create-from-blank.md)してみましょう。 何もない状態から作業することで、アプリの設計やフロー、制御の幅が広がり、組み込むことができるデータ ソースの種類も増えます。

## <a name="share-and-run-an-app"></a>アプリの共有と実行
アプリを完成させクラウドに保存することで、組織内の人とアプリを共有できます。 アプリのアクセス許可のレベルは、ご自身で制御できます。アプリを実行できるユーザーまたはグループを決定し、その対象者がアプリをカスタマイズしたり、組織内の他のユーザーと共有したりできるかを決定します。

独自のアプリ、さらには共有されているすべてのアプリを Windows、iOS、Android、Web ブラウザーで実行できます。

詳細については、次のトピックをご覧ください。

* [他のユーザーとアプリを共有する](share-app.md)
* [Web ブラウザーでアプリを実行する](../../user/run-app-browser.md)
* [スマートフォンまたはタブレットでアプリを実行する](../../user/run-app-client.md)

## <a name="get-help-and-support"></a>役立つ情報を入手することや、サポートを受けることができます
PowerApps について知りたいことがある場合は、次の方法で役立つ情報を得られます。

* 左側のナビゲーション ウィンドウで詳細手順、概念、リファレンスのトピックを探す。
* 自分のペースで[ガイド付きの学習コース](https://docs.microsoft.com/powerapps/guided-learning/)を進める。
* [PowerApps コミュニティ](https://aka.ms/powerapps-community)で記事の閲覧や投稿を行う。ここでは、PowerApps のユーザーであれば誰でも質問を投稿したり、他の人の質問に回答したりできます。 質問を投稿する前にコミュニティを検索して、既に同じ質問が回答済みでないかを確認してください。
* [今後のウェビナー](webinars-listing.md#upcoming-webinars)で、PowerApps の特徴や機能を活用するのに役立つ内容が予定されていないかを確認する。 オンデマンドで[過去のウェビナー](webinars-listing.md#past-webinars)にアクセスすることもできます。
* [サポート チケット](https://powerapps.microsoft.com/support/pro/)を作成して技術的なサポートを受ける。 所属組織の PowerApps 管理者は、[PowerApps 管理センター](https://portal.office.com/Support/Support.aspx)でサポート チケットを開くこともできます。

また、Microsoft は PowerApps をさらに発展させるためにお客様のご協力を必要としています。

* Microsoft が PowerApps を改良するためのアイデアを投稿するには、[PowerApps アイデア](https://powerusers.microsoft.com/t5/PowerApps-Ideas/idb-p/PowerAppsIdeas)に移動して、そのアイデアについてお話しください。
* PowerApps で発生している問題を報告するには、[PowerApps フォーラム](https://powerusers.microsoft.com/t5/General-Discussion/bd-p/PowerAppsForum1)に移動して、Microsoft が調査できるように詳細をお知らせください。

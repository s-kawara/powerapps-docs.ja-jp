---
title: PowerApps で SharePoint からアプリを生成するためのクイック スタート |Microsoft Docs
description: SharePoint リストのデータを管理するアプリを PowerApps で自動的に生成する
author: AFTOwen
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 03/12/2018
ms.author: anneta
ms.openlocfilehash: b9404b2ac7d67f9594b77ee73de55b46a94e7afa
ms.sourcegitcommit: dfa0e1a7981814e15e6ca4720e2a5f930e859db1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/13/2018
ms.locfileid: "39016814"
---
# <a name="quickstart-for-generating-an-app-in-powerapps-from-sharepoint"></a>PowerApps で SharePoint からアプリを生成するためのクイック スタート

このクイック スタートでは、PowerApps を使用し、SharePoint で作成した一覧に基づいた最初のアプリを自動生成します。 このアプリでは、一覧内のすべての項目参照、1 つの項目の詳細の表示、項目の作成、更新、削除が可能です。

SharePoint に一覧がある場合は、このクイックスタートから概念と手法を習得できます。 このクイックスタートに厳密に従うには、**Title** という名前の列を含む **SimpleApp** という名前の一覧を SharePoint Online サイトに作成します。 一覧で、**バニラ**、**チョコレート**、**イチゴ**のエントリを作成します。

テキスト、日付、数字、通貨など、さまざまな種類の多くの列を含むはるかに複雑な一覧を作成することができます。 アプリを生成する場合の原則は変更されません。 データ ゲートウェイを介して[サイトに接続する](connect-to-sharepoint.md)場合は、オンプレミスの SharePoint サイトで一覧からアプリを生成することもできます。

PowerApps のライセンスを持っていない場合は、[無料でサインアップ](../signup-for-powerapps.md)できます。

## <a name="generate-an-app"></a>アプリを生成する
1. [PowerApps](https://web.powerapps.com) にサインインします。

    ![PowerApps ホーム ページ](./media/app-from-sharepoint/sign-in.png)

1. **[このようなアプリを作成します]** の下の **[Start from data]\(データから開始\)** にポインターを合わせ、**[このアプリの作成]** を選択します。

    ![アプリを作成するためのオプション](./media/app-from-sharepoint/make-this-app.png)

1. SharePoint タイルで、**[携帯電話レイアウト]** を選択します。

    ![アプリを作成するためのオプション](./media/app-from-sharepoint/sharepoint-tile.png)

1. **[直接接続]** オプションを選択し、**[作成]** を選択します。

    ![接続の作成](./media/app-from-sharepoint/create-connection.png)

1. **[SharePoint サイトへの接続]** で、SharePoint Online サイトの URL を入力するか貼り付け、**[移動]** を選択します。

    この例のように、リストの名前ではなくサイトの URL のみを含めます。<br>`https://microsoft.sharepoint.com/teams/Contoso`

1. **[リストを選択してください]** で、**SimpleApp** を選択し、**[接続]** を選択します。

数分待機すると、アプリがブラウザー画面に開き、一覧で作成した項目が表示されます。 リストに **Title** 以外の列が含まれている場合は、アプリにそのデータが表示されます。 画面上部あたりのタイトル バーに、リストの更新、リストの並べ替え、リスト内の項目の作成用のアイコンが表示されます。 オプションで、タイトル バーの下の検索ボックスを使用して、入力または貼り付けたテキストで一覧をフィルタリングできます。 

![ブラウズ画面](./media/app-from-sharepoint/browse-screen.png)

このアプリを使用したり、他のユーザーと共有したりする前に、さらに変更を加えたい場合があります。 続行する前に、ベスト プラクティスとして、Ctrl キーと S キーを押し、これまでの作業を保存します。 アプリの名前を指定し、**[保存]** を選択します。

## <a name="next-steps"></a>次の手順
このクイックスタートでは、SharePoint リストのデータを管理するアプリを作成しました。 次の手順として、より複雑なリストからアプリを生成し、ニーズに合わせて ([参照] 画面から) アプリをカスタマイズします。

> [!div class="nextstepaction"]
> [既定の参照画面のカスタマイズ](customize-layout-sharepoint.md)
---
title: PowerApps で Common Data Service for Apps 用のアプリを生成する (クイック スタート) | Microsoft Docs
description: PowerApps で Common Data Service for Apps のデータを管理するアプリを自動生成する
services: powerapps
documentationcenter: na
author: AFTOwen
manager: kfile
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2018
ms.author: anneta
ms.openlocfilehash: 78429fc5d0220b5cc9e8dc726583c2e9e543f85a
ms.sourcegitcommit: 59785e9e82da8f5bd459dcb5da3d5c18064b0899
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2018
---
# <a name="quickstart-for-generating-an-app-in-powerapps-for-the-common-data-service-for-apps"></a>PowerApps で Common Data Service for Apps 用のアプリを生成するためのクイック スタート

このクイック スタートでは、PowerApps で、[Common Data Service for Apps](../common-data-service/data-platform-intro.md) のサンプル アカウントの一覧に基づいた最初のアプリを自動生成します。 このアプリでは、すべてのアカウントの参照、1 つのアカウントの詳細の表示、アカウントの作成、更新および削除が可能です。

このクイック スタートに従うには、Common Data Service のデータベースが作成された、データが含まれる[環境](working-with-environments.md)に切り替える必要があります。 そのような環境がなく、管理者権限を保持している場合、この要件に合う[環境を作成](../../administrator/environments-administration.md#create-an-environment)します。

PowerApps のライセンスを持っていない場合は、[無料でサインアップ](../signup-for-powerapps.md)できます。

## <a name="generate-an-app"></a>アプリを生成する
1. [PowerApps にサインインします](https://web.powerapps.com)。

    ![PowerApps ホーム ページ](./media/data-platform-create-app/sign-in.png)

1. **[このようなアプリを作成します]** の下の **[Start from data]\(データから開始\)** にポインターを合わせ、**[このアプリの作成]** を選択します。

    ![アプリを作成するためのオプション](./media/data-platform-create-app/make-this-app.png)

1. **[データを使用して開始]** の下の右向きの矢印を選択します。

    ![矢印アイコン](./media/data-platform-create-app/right-arrow.png)

1. **[接続]** の下から、Common Data Service への接続を選択します。

1. (右端付近の) 検索ボックスに「**アカウント**」と入力し、**[Choose a table]\(テーブルの選択\)** の下の **[アカウント]** を選択し、**[接続]** を選択します。

    ![エンティティの選択](./media/data-platform-create-app/select-entity.png)

数分待機すると、アプリがブラウザー画面に開き、アカウントの一覧が表示されます。 画面上部あたりのタイトル バーに、一覧の更新、一覧の並べ替え、およびアカウントの作成用のアイコンが表示されます。 オプションで、タイトル バーの下の検索ボックスを使用して、入力または貼り付けたテキストで一覧をフィルタリングできます。 

既定で、一覧にはそのアカウントの画像、メール アドレス、市区町村、ID が表示されます。 ただし、ギャラリーと呼ばれる一覧をカスタマイズして、他の種類のデータを表示することも可能です。

![ブラウズ画面](./media/data-platform-create-app/browse-screen.png)

## <a name="save-the-app"></a>アプリの保存
このアプリを使用したり、他のユーザーと共有する前に、さらに変更を加えたいことでしょう。 続行する前に、ベスト プラクティスとして作業を保存します。

1. 左上隅にある **[ファイル]** タブをタップします。

1. **[アプリ設定]** ページで、アプリ名を **AppGen** に設定し、背景色を濃い赤に変更し、アイコンをチェック マークに変更します。

    ![アプリの設定ページ](./media/data-platform-create-app/app-settings.png)

1. 左端近くにある **[保存]** をクリックまたはタップします。

## <a name="next-steps"></a>次の手順
このクイック スタートでは、Common Data Service for Apps のアカウントのサンプル データを管理するアプリを作成しました。 次の手順では、ニーズに合わせて既定のブラウザー画面をカスタマイズします。

> [!div class="nextstepaction"]
> [既定のブラウザー画面のカスタマイズ](customize-layout-sharepoint.md).

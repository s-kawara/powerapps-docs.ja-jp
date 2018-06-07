---
title: クイック スタート - Common Data Service for Apps からアプリを生成する | Microsoft Docs
description: このクイック スタートでは、Common Data Service for Apps のデータを管理するためのアプリを、PowerApps で自動的に生成します
author: AFTOwen
ms.service: powerapps
ms.topic: quickstart
ms.component: canvas
ms.date: 05/06/2018
ms.author: anneta
ms.openlocfilehash: a058629f08e61f7299792697234b5d346b9d0c71
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "34453563"
---
# <a name="quickstart-generate-an-app-from-common-data-service-for-apps-in-powerapps"></a>クイック スタート: Common Data Service for Apps からアプリを生成する

このクイック スタートでは、Microsoft PowerApps を使用し、[Common Data Service (CDS) for Apps](../common-data-service/data-platform-intro.md) のサンプル アカウントの一覧を基にしてアプリを自動生成します。 このアプリでは、すべてのアカウントの参照、1 つのアカウントの詳細の表示、アカウントの作成、更新および削除が可能です。

PowerApps にサインアップしていない場合は、始める前に[無料でサインアップ](https://web.powerapps.com)してください。

## <a name="prerequisites"></a>前提条件
このクイック スタートに従うには、CDS for Apps のデータベースが作成され、データを含み、更新できる[環境に切り替える](working-with-environments.md)必要があります。 そのような環境がなく、管理者権限を保持している場合、この要件に合う[環境を作成](../../administrator/environments-administration.md#create-an-environment)します。

## <a name="generate-an-app"></a>アプリを生成する
1. [PowerApps](https://web.powerapps.com) にサインインし、必要に応じて、このトピックで前に説明したように環境を切り替えます。

    ![PowerApps ホーム ページ](./media/data-platform-create-app/sign-in.png)

1. **[このようなアプリを作成します]** の下の **[Start from data]\(データから開始\)** にポインターを合わせ、**[このアプリの作成]** を選択します。

    ![アプリを作成するためのオプション](./media/data-platform-create-app/make-this-app.png)

1. **[Common Data Service]** タイルで、**[電話レイアウト]** を選びます。

    ![接続タイル](./media/data-platform-create-app/connection-tile.png)

1. **[テーブルの選択]** で、**[アカウント]** を選び、**[接続]** を選びます。

1. **[PowerApps Studio へようこそ]** ダイアログ ボックスが表示されたら、**[スキップ]** を選択します。

ブラウザー画面でアプリが開き、ギャラリーと呼ばれるコントロールにアカウントの一覧が表示されます。 画面上部近くのタイトル バーには、ギャラリー内のデータの更新、ギャラリー内のデータのアルファベット順の並べ替え、およびギャラリーへのデータの追加を行うアイコンが表示されます。 オプションで、タイトル バーの下の検索ボックスを使用して、入力または貼り付けたテキストに基づいてギャラリーのデータをフィルタリングできます。 

既定で、ギャラリーにはメール アドレス、市区町村、アカウント名が表示されます。 「[次のステップ](data-platform-create-app.md#next-steps)」を見ていただくとわかるように、ギャラリーをカスタマイズして、データの表示方法を変更したり、他の種類のデータを表示したりすることさえできます。

![ブラウズ画面](./media/data-platform-create-app/browse-screen.png)

## <a name="save-the-app"></a>アプリの保存
このアプリを使用したり、他のユーザーと共有する前に、さらに変更を加えたいことでしょう。 続行する前に、ベスト プラクティスとして作業を保存します。

1. 左上隅にある **[ファイル]** タブを選びます。

1. **[アプリ設定]** ページで、アプリ名を **AppGen** に設定し、背景色を濃い赤に変更し、アイコンをチェック マークに変更します。

    ![アプリの設定ページ](./media/data-platform-create-app/app-settings.png)

1. 左端近くの **[保存]** を選んでから、左下隅の **[保存]** を選びます。

## <a name="next-steps"></a>次の手順
このクイック スタートでは、CDS for Apps のアカウントのサンプル データを管理するアプリを作成しました。 次の手順では、ニーズに合わせて既定のブラウザー画面のギャラリーと他の要素をカスタマイズします。

> [!div class="nextstepaction"]
> [ギャラリーをカスタマイズします](customize-layout-sharepoint.md)。

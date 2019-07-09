---
title: Common Data Service からキャンバス アプリの生成 |Microsoft Docs
description: PowerApps で Common Data Service 内のデータを管理するキャンバス アプリを自動的に生成します。
author: AFTOwen
manager: kvivek
ms.service: powerapps
ms.topic: quickstart
ms.custom: canvas
ms.reviewer: ''
ms.date: 05/06/2018
ms.author: anneta
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 7e06c24d4d83b0e176782b705d6a77e956b6043b
ms.sourcegitcommit: 4042388fa5e7ef50bc59f9e35df330613fea29ae
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/23/2019
ms.locfileid: "61549678"
---
# <a name="generate-a-canvas-app-from-common-data-service-in-powerapps"></a>PowerApps で Common Data Service からキャンバス アプリを生成します。

PowerApps では、[Common Data Service](../common-data-service/data-platform-intro.md)のサンプルアカウントのリストに基づいてキャンバスアプリを自動的に生成します。 このアプリでは、すべてのアカウントの参照、1 つのアカウントの詳細の表示、アカウントの作成、更新および削除が可能です。

PowerApps にサインアップしていない場合は、始める前に[無料でサインアップ](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)してください。

## <a name="prerequisites"></a>前提条件

このクイック スタートに従うに割り当てる必要があります、 [Environment Maker](https://docs.microsoft.com/power-platform/admin/database-security#predefined-security-roles)セキュリティの役割をする必要があります。[環境に切り替える](working-with-environments.md)を Common Data Service でのデータベースが作成されたら、で、データが含まれています。更新可能であるとします。 そのような環境がなく、管理者権限を保持している場合、この要件に合う[環境を作成](https://docs.microsoft.com/power-platform/admin/environments-administration#create-an-environment)します。

## <a name="generate-an-app"></a>アプリを生成する

1. [PowerApps](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) にサインインし、必要に応じて、このトピックで前に説明したように環境を切り替えます。

1. **[Make your own app]\(独自アプリの作成\)** の下の **[Start from data]\(データから開始\)** にポインターを合わせ、 **[このアプリの作成]** を選択します。

    ![アプリを作成するためのオプション](./media/data-platform-create-app/start-from-data.png)

1. **[Common Data Service]** タイルで、 **[携帯電話レイアウト]** を選択します。

    ![接続タイル](./media/data-platform-create-app/connection-tile.png)

1. **[テーブルの選択]** で、 **[アカウント]** を選び、 **[接続]** を選びます。

1. **[PowerApps Studio へようこそ]** ダイアログ ボックスが表示されたら、 **[スキップ]** を選択します。

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
このクイック スタートでは、Common Data Service のアカウントのサンプル データを管理するアプリを作成しました。 次の手順では、ニーズに合わせて既定のブラウザー画面のギャラリーと他の要素をカスタマイズします。

> [!div class="nextstepaction"]
> [ギャラリーをカスタマイズします](customize-layout-sharepoint.md)。

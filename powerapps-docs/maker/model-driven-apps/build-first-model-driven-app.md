---
title: PowerApps で初めてのモデル駆動型アプリを最初から作成するためのクイック スタート | Microsoft Docs
description: 簡単なモデル駆動型アプリを作成する方法について説明します
documentationcenter: ''
author: Mattp123
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: conceptual
ms.component: model
ms.date: 04/18/2018
ms.author: matp
ms.openlocfilehash: 3a9696a025608de3c142277da4059e7e8c5ec5ad
ms.sourcegitcommit: 45fac73f04aa03b5796ae6833d777f4757e67945
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/03/2018
---
# <a name="quickstart-build-your-first-model-driven-app-from-scratch"></a>クイック スタート: 初めてのモデル駆動型アプリを最初から作成する
モデル駆動型アプリの設計は、コンポーネントに焦点を当てたアプリ開発の手法です。 このクイック スタートでは、[!INCLUDE [powerapps](../../includes/powerapps.md)] 環境で使用可能な標準エンティティの 1 つを使って、モデル駆動型アプリを簡単に作成できるようにします。 

## <a name="sign-in-to-powerapps"></a>PowerApps へのサインイン
[PowerApps](https://web.powerapps.microsoft.com/) にサインインします。 まだ [!INCLUDE [powerapps](../../includes/powerapps.md)] アカウントを持っていない場合は、**[GET STARTED FREE]** リンクを選びます。 

## <a name="create-your-model-driven-app"></a>モデル駆動型アプリを作成する

1.  目的の環境を選択するか、または [PowerApps 管理センター](https://admin.powerapps.microsoft.com/)にアクセスして新しい環境を作成します。
2.  左ナビゲーション ウィンドウで、**[モデル駆動]** を選びます。 

    ![モデル駆動](media/build-first-model-driven-app/choose-design-mode.png)

3. 左側のウィンドウで **[アプリ]** を選んで、**[アプリの作成]** を選びます。

4.  **[新しいアプリの作成]** ページで、次の詳細を入力し、**[完了]** を選びます。 
  - **[名前]**: アプリの名前を入力します (例: *Myfirstapp*)。 
  - **[説明]**: アプリの内容または機能の短い説明を入力します (例: "*これは私の初めてのアプリです*")。
アプリの他のプロパティについては、「[アプリを作成する](https://docs.microsoft.com/dynamics365/customer-engagement/customize/create-edit-app#create-an-app)」をご覧ください。
 
    ![Create-new-app](media/build-first-model-driven-app/create-new-app.png)

## <a name="add-components-to-your-app"></a>アプリにコンポーネントを追加する
アプリ デザイナーから、コンポーネントをアプリに追加します。
1.  **[Open the Site Map Designer]\(サイト マップ デザイナーを開く\)** 矢印を選んで、サイトマップ デザイナーを開きます。 

    ![Create-new-sitemap](media/build-first-model-driven-app/new-sitemap.png)

2.  サイトマップ デザイナーで **[New Subarea]\(新しいサブエリア\)** を選び、右側のウィンドウで **[プロパティ]** タブを選んで、以下のプロパティを選びます。
  - **種類**: エンティティ
  - **エンティティ**: アカウント

    ![サイトマップにコンポーネントを追加する](media/build-first-model-driven-app/sitemap.png)

3.  **[保存して閉じる]** を選びます。
4.  アプリ デザイナーのキャンバスで **[フォーム]** を選び、右側のウィンドウの **[メイン フォーム]** グループで **[取引先企業]** フォームを選びます。

    ![アカウント メイン フォーム](media/build-first-model-driven-app/main-form.png)

5.  アプリ デザイナーのキャンバスで **[ビュー]** を選び、**[アクティブな取引先企業]**、**[すべてのアカウント]**、および **[自分のアクティブな取引先企業]** ビューを選びます。

    ![取引先企業ビュー](media/build-first-model-driven-app/views.png)

6. アプリ デザイナーのキャンバスで **[グラフ]** を選び、**[業種別取引先企業]** グラフを選びます。
7. アプリ デザイナーのツール バーで、**[保存]** を選びます。

    ![アプリ デザイナー ツール バーの保存](media/build-first-model-driven-app/app-designer-toolbar.png)
 
<!-- ##  Validate your app
This step checks for component dependencies that are required for the app to work, but haven't yet been added to the app. 

1. On the app designer canvas, select the component that indicates a dependency, such as the **Forms** component. Then, on the right-pane select the **Required** tab, expand **Entity Dependencies** and then select all required dependencies. 

    ![Add dependencies](media/build-first-model-driven-app/resolve-dependencies.png)

2. Select **Add Dependencies**.
3. On the app designer toolbar, select **Save**.  -->

## <a name="publish-your-app"></a>アプリを発行する
アプリ デザイナーのツール バーで、**[Publish]\(発行\)** を選びます。

アプリを発行した後は、アプリを実行したり、他のユーザーと共有したりできるようになります。

![簡単な取引先企業エンティティ アプリ](media/build-first-model-driven-app/accounts-quickstart-app.png)

## <a name="next-steps"></a>次の手順
このクイック スタートでは、簡単なモデル駆動型アプリを作成しました。 アプリを実行したときの表示を見るには、「[クイック スタート: モバイル デバイスでモデル駆動型アプリを実行する](../../user/run-app-client-model-driven.md)」をご覧ください。
アプリを共有する方法については、モデル駆動型アプリの共有方法に関する「[モデル駆動型アプリの共有](share-model-driven-app.md)」チュートリアルを続けてください。

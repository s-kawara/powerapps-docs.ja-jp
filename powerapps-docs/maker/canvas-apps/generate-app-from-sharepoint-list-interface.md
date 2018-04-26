---
title: SharePoint リスト内からアプリを生成する | Microsoft Docs
description: SharePoint リスト内から、アイテムを管理する 3 つの画面から成るアプリを生成します。SharePoint サイトはオンプレミスとクラウドのどちらにあってもかまいません。
documentationcenter: na
author: AFTOwen
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: conceptual
ms.component: canvas
ms.date: 03/18/2018
ms.author: anneta
ms.openlocfilehash: 50e897e9d75eec037039e81e6dbed524206b10d3
ms.sourcegitcommit: 8bd4c700969d0fd42950581e03fd5ccbb5273584
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="generate-an-app-from-within-sharepoint-using-powerapps"></a>PowerApps を使用して、SharePoint 内からアプリを生成する

PowerApps で、ユーザーがカスタム SharePoint Online リスト内のアイテムを管理できるアプリを自動的に生成します。 アプリには 3 つの画面があり、ユーザーは次のことができます。

* リスト内のすべてのレコードを閲覧する (**BrowseScreen1**)
* 特定のレコードのすべてのフィールドを表示する (**DetailsScreen1**)
* レコードを作成または編集する (**EditScreen1**)

SharePoint Online コマンド バーからカスタム リストのアプリを作成する場合、アプリはそのリストのビューとして表示されます。 Web ブラウザーだけでなく、iOS または Android デバイスでもアプリを実行できます。

> [!IMPORTANT]
> PowerApps は全種類の SharePoint データをサポートするわけではありません。 詳細については、「[Known issues (既知の問題)](connections/connection-sharepoint-online.md#known-issues)」を参照してください。

## <a name="generate-an-app"></a>アプリを生成する
1. SharePoint Online でカスタム リストを開き、コマンド バーで **[PowerApps]**、**[アプリの作成]** の順にクリックまたはタップします。

    ![アプリを作成する](./media/generate-app-from-sharepoint-list-interface/generate-new-app.png)

2. 表示されるパネルに、アプリの名前を入力し、**[作成]** をクリックまたはタップします。

    ![アプリの名前の指定](./media/generate-app-from-sharepoint-list-interface/app-name.png)

    新しいタブが Web ブラウザーに表示され、SharePoint リストに基づいて自動的に生成したアプリが表示されます。 PowerApps Studio にアプリが表示され、カスタマイズすることができます。

    ![既定のアプリ](./media/generate-app-from-sharepoint-list-interface/default-app.png)  
3. SharePoint リストのブラウザー タブをクリックまたはタップしてから、**[開く]** をクリックまたはタップします。

> [!NOTE]
> ブラウザー ウィンドウを (F5 キーを押すなどして) 更新しないとアプリが開かない場合もあります。

別のブラウザー タブでアプリが開きます。

## <a name="manage-the-app"></a>アプリを管理する
![コマンド バー](./media/generate-app-from-sharepoint-list-interface/command-bar.png)

* **[Edit in PowerApps]\(PowerApps で編集する)** をクリックまたはタップすると、別のブラウザー タブでアプリが開き、Web 用の PowerApps Studio でこのアプリを更新できるようになります。

* **[Make this view public]\(このビューを公開する)** をクリックまたはタップすると、組織内の他のユーザーがビューを見ることができるようになります。 既定では、自分が作成したビューのみが表示されます。 他のユーザーがこのアプリを編集できるようにする場合は、[他のユーザーとアプリを共有して](share-app.md)から、**編集可能**のアクセス許可を付与する必要があります。

* **[Remove this view]\(このビューを削除する)** をクリックまたはタップすると、SharePoint からビューが削除されますが、アプリは[削除](delete-app.md)しない限り PowerApps に残ります。

## <a name="next-steps"></a>次の手順
* 既定の[ギャラリー](customize-layout-sharepoint.md)、[フォーム](customize-forms-sharepoint.md)、[カード](customize-card.md)をカスタマイズします。

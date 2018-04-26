---
title: アプリを編集する | Microsoft Docs
description: アプリの編集とセッションのロックを行うシナリオについて、ステップバイステップの手順を示します。
documentationcenter: na
author: karthik-1
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: conceptual
ms.component: canvas
ms.date: 05/19/2017
ms.author: sharik
ms.openlocfilehash: 782674cd8d9bbcc81580302a9936bcf47de4b68b
ms.sourcegitcommit: 8bd4c700969d0fd42950581e03fd5ccbb5273584
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="edit-an-app-in-powerapps"></a>PowerApps でのアプリの編集
自分で作成したアプリ、所有しているアプリ、または "**編集可能**" アクセス許可を持っているアプリを編集できます。 アプリの編集は、Web 用の PowerApps Studio または Windows 用の PowerApps Studio で行うことができます。 別の場所で編集するために開かれているアプリを編集しようとすると、自分または別のユーザーがそのアプリを既に開いているという通知メッセージが表示されます。

## <a name="verify-your-permissions"></a>アクセス許可の確認
1. [PowerApps](https://web.powerapps.com) にサインインし、**[ファイル]** メニュー (左端) の **[アプリ]** をクリックまたはタップします。
   
    ![[ファイル] メニューの [アプリ] オプション](./media/edit-app/file-apps.png)
2. アプリ カテゴリ セレクターを開き、**[自分が所有しているアプリ]** または **[参加中のアプリ]** をクリックまたはタップします。
   
    ![アプリ カテゴリ セレクター](./media/edit-app/app-category.png)
   
    表示された一覧にある任意のアプリを編集することができます。 また、右上隅の近くにある検索ボックスに 1 つ以上の文字を入力して、アプリを検索することもできます。
   
    > [!NOTE]
> 編集するアプリがまだ表示されない場合は、右上隅の近くで、正しい環境を選択していることを確認してください。
   
    ![環境の一覧](./media/edit-app/environment-list.png)

## <a name="edit-an-app-in-powerapps-studio-for-web"></a>Web 用の PowerApps Studio でのアプリの編集
1. 前の手順のステップに従って、編集するアプリを検索します。
2. 右端近くのアプリの情報アイコンをタップまたはクリックします。
   
    ![情報アイコン](./media/edit-app/app-edit.png)
3. 右上隅の近くにある **[編集]** アイコンをクリックまたはタップし、**[Web で編集]** をクリックまたはタップします。
   
    ![[編集] アイコン](./media/edit-app/edit-icon.png)

## <a name="edit-an-app-in-powerapps-studio-for-windows"></a>Windows 用の PowerApps Studio でのアプリの編集
1. Windows 用の PowerApps Studio を開きます。
2. 既定で表示されるページで、編集するアプリを検索します。
   
    アプリを簡単に検索するには、右上隅の近くにある検索アイコンをクリックまたはタップし、アプリの名前の 1 文字以上を入力します。 また、一覧を名前、更新日付の新しい順、開いた日付の新しい順に並べ替えることもできます。 それでも目的のアプリが表示されない場合は、最初の手順で説明したように、適切な PowerApps 環境で作業していることを確認してください。
   
    ![](./media/edit-app/sort-filter.png)
3. 右端で、編集するアプリの鉛筆アイコンをクリックまたはタップします。
   
    灰色ではなく黒の鉛筆アイコンが表示されているすべてのアプリを編集できます。
   
    ![](./media/edit-app/app-editstudio.png)

## <a name="collaborate-on-an-app"></a>アプリでの共同作業
アプリに対して "**編集可能**" アクセス許可を持つすべてのユーザーが、そのアプリを編集できます。ただし、アプリを編集できるユーザーは一度に 1 人だけです。 他のユーザーが既に編集中であるアプリを編集しようとすると、このメッセージが表示されます。 他のユーザーがアプリを閉じるまで (または、そのユーザーのセッションがタイムアウトするまで)、編集作業を進めることはできません。

![](./media/edit-app/applock-otheruser.png)

また、アプリを編集用に開き、そのアプリを別のデバイスまたは別のブラウザー ウィンドウで開こうとしたときにも、このメッセージが表示されます。 前のセッションをオーバーライドできますが、保存していないすべての変更が失われる可能性があります。

![](./media/edit-app/applock-selfuser.png)

## <a name="next-steps"></a>次のステップ
[画面](add-screen-context-variables.md)、[コントロール](add-configure-controls.md)、または[データ接続](add-data-connection.md)を追加する方法の詳細について学びます。


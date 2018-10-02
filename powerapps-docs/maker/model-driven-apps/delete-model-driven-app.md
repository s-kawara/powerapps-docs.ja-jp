---
title: モデル駆動型アプリを削除する | MicrosoftDocs
description: PowerApps 環境からモデル駆動型アプリを削除する方法について説明します。
keywords: ''
ms.date: 05/31/2018
ms.service: crm-online
ms.custom: null
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - powerapps
ms.assetid: e82e7f64-37ad-41e5-acd7-16309881c6a2
author: Mattp123
ms.author: matp
manager: kvivek
ms.reviewer: null
ms.suite: null
ms.tgt_pltfrm: null
caps.latest.revision: 9
topic-status: Drafting
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---

# <a name="delete-a-model-driven-app"></a>モデル駆動型アプリを削除する

環境内で使われなくなったアプリを削除します。

1. [PowerApps](https://web.powerapps.com/) にサインインします。
2. [ソリューション エクスプローラー](advanced-navigation.md#solution-explorer)を開きます。 
3. ソリューション ウィンドウの**コンポーネント**で、**アプリ**を選択します。
4. 削除するアプリを選択し、コマンド バーで、**削除**を選択します。

    ![アプリの削除](media/app-module-solution-window.png "アプリの削除")

5. 表示される確認メッセージで、**削除**を選びます。

   アプリが環境から削除されます。
  
依存関係 (関連付けなど) がコンポーネントにある場合は、アプリを削除する前に、依存関係を削除する必要があります。 アプリの依存関係を確認するには、アプリを選択し、コマンド バーで、**依存関係を表示**を選択します。

> [!NOTE]
> アプリケーションを削除するとき、それに関連付けられているサイト マップを削除することをお勧めします。 関連付けられているサイト マップを削除しなかった場合、同じ名前で別のアプリを作成しようとしたときにサイト マップ デザイナーにエラーが表示されます。 ただし、エラーを無視することができます。アプリを再度作成するときに、エラーは表示されません。



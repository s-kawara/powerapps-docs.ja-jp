---
title: モデル駆動型アプリの削除 | MicrosoftDocs
description: PowerApps 環境からモデル駆動型アプリを削除する方法について説明します。
keywords: ''
ms.date: 05/31/2018
ms.service: crm-online
ms.custom: ''
ms.topic: article
applies_to:
- Dynamics 365 (online)
- Dynamics 365 Version 9.x
- powerapps
ms.assetid: e82e7f64-37ad-41e5-acd7-16309881c6a2
author: Mattp123
ms.author: matp
manager: kvivek
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
caps.latest.revision: 9
topic-status: Drafting
ms.openlocfilehash: 9512c0b1c13f408b92c0c18f08946ea9afa1e62b
ms.sourcegitcommit: aba996b1773ecdf62758e06b34eaf57bede29e08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/08/2018
ms.locfileid: "39696053"
---
# <a name="delete-a-model-driven-app"></a>モデル駆動型アプリの削除

ご使用の環境で古くなったアプリを削除します。

1. [PowerApps](https://web.powerapps.com/) にサインインします。
2. [ソリューション エクスプローラー](advanced-navigation.md#solution-explorer)を開きます。 
3. ソリューション ウィンドウの **[コンポーネント]** で **[アプリ]** を選択します。
4. 削除するアプリを選択し、コマンド バーの **[削除]** を選択します。

    ![アプリの削除](media/app-module-solution-window.png "アプリの削除")

5. 確認メッセージが表示されたら、**[削除]** を選択します。

   ご使用の環境からアプリが削除されました。
  
コンポーネントに依存関係 (リレーションシップなど) が含まれている場合は、アプリを削除する前にその依存関係を削除する必要があります。 アプリの依存関係を表示するには、アプリを選択し、コマンド バーの **[依存関係の表示]** を選択します。

> [!NOTE]
> アプリを削除する場合、それに関連付けられたサイト マップも削除することをお勧めします。 関連付けられたサイト マップを削除しないと、次に初めて同じ名前の別のアプリを作成しようとしたときに、サイト マップ デザイナーによってエラーが表示されます。 ただし、このエラーは無視することができ、再びアプリを作成しようとする場合には表示されません。



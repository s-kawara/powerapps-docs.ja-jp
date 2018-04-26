---
title: カスタム エンティティの削除とデータの消去のクイックスタート | Microsoft Docs
description: カスタム エンティティを削除し、すべてのデータを消去するクイックスタート
documentationcenter: na
author: clwesene
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: conceptual
ms.component: cds
ms.date: 3/21/2018
ms.author: clwesene
ms.openlocfilehash: 971016233578c4eadf397d662a0ea74187548635
ms.sourcegitcommit: 8bd4c700969d0fd42950581e03fd5ccbb5273584
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="quickstart-delete-a-custom-entity"></a>クイック スタート: カスタム エンティティを削除する
カスタム エンティティは削除できますが、標準エンティティは削除できません。

1. [powerapps.com](https://web.powerapps.com) で、**[データ]** セクションを展開し、左側のナビゲーション ウィンドウで **[エンティティ]** をクリックまたはタップします。

    ![エンティティの詳細](./media/data-platform-cds-create-entity/entitylist.png "エンティティの一覧")

2. エンティティの一覧で、削除するエンティティをクリックまたはタップし、コマンド バーの **[エンティティの削除]** オプションをクリックまたはタップします。
3. 表示されたダイアログ ボックスで、**[削除]** をクリックまたはタップするとエンティティが削除されます。

>[!NOTE]
>エンティティを削除すると、エンティティの定義と、エンティティに含まれるすべてのデータの両方が削除されます。 削除された場合は、エンティティおよびそれらに含まれるデータを回復できません。

>[!NOTE]
>アプリで使用されているエンティティを削除する場合、アプリまたはフローが壊れる可能性があります。

>[!NOTE]
>エンティティ A にエンティティ B の[ルックアップ フィールド](data-platform-entity-lookup.md)が存在する場合、エンティティ A を削除するためには、先にエンティティ B を削除しなければならないことがあります。


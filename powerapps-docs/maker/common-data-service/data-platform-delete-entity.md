---
title: カスタム エンティティの削除 | Microsoft Docs
description: カスタム エンティティを削除し、PowerApps のすべてのデータをクリアする手順
author: clwesene
manager: kfile
ms.service: powerapps
ms.component: cds
ms.topic: conceptual
ms.date: 03/21/2018
ms.author: clwesene
ms.openlocfilehash: 6ef9dc3a1c82fdee9927ffd533ed41386345eaf7
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "34167563"
---
# <a name="delete-a-custom-entity"></a>カスタム エンティティの削除
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


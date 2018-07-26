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
ms.openlocfilehash: b17da30916b06b5b76b16cc6bf9758b988549f6f
ms.sourcegitcommit: 0b051bba173353d7ceda3b60921e7e009eb00709
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2018
ms.locfileid: "39218650"
---
# <a name="delete-a-custom-entity"></a>カスタム エンティティの削除
カスタム エンティティは削除できますが、標準エンティティは削除できません。

1. [powerapps.com](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) で、**[データ]** セクションを展開し、左側のナビゲーション ウィンドウで **[エンティティ]** をクリックまたはタップします。

    ![エンティティの詳細](./media/data-platform-cds-create-entity/entitylist.png "エンティティの一覧")

2. エンティティの一覧で、削除するエンティティをクリックまたはタップし、コマンド バーの **[エンティティの削除]** オプションをクリックまたはタップします。

3. 表示されたダイアログ ボックスで、**[削除]** をクリックまたはタップするとエンティティが削除されます。

>[!NOTE]
>エンティティを削除すると、エンティティの定義と、エンティティに含まれるすべてのデータの両方が削除されます。 削除された場合は、エンティティおよびそれらに含まれるデータを回復できません。

>[!NOTE]
>アプリで使用されているエンティティを削除する場合、アプリまたはフローが壊れる可能性があります。

>[!NOTE]
>エンティティ A にエンティティ B の[ルックアップ フィールド](data-platform-entity-lookup.md)が存在する場合、エンティティ A を削除するためには、先にエンティティ B を削除しなければならないことがあります。


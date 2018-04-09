---
title: データ グループ | Microsoft Docs
description: Microsoft PowerApps のデータ グループをご紹介します。
services: powerapps
suite: powerapps
documentationcenter: na
author: manasmams
manager: kfile
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2018
ms.author: manasma
ms.openlocfilehash: 1adf0f4888d57b2d5636864e9bdd18e00848b9d8
ms.sourcegitcommit: c5e3991e0e4e9f22a1e094d699f35adabfb97c6c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/03/2018
---
# <a name="learn-all-about-data-groups"></a>データ グループについて詳しく学ぶ
データ グループは、[データ損失防止 (DLP) ポリシー](prevent-data-loss.md)内のサービスを分類する簡単な方法です。 **[ビジネス データのみ]** グループおよび **[許可されたビジネス データなし]** グループの 2 つのデータ グループが使用可能です。 組織は、特定のデータ グループにどのサービスが配置されるかを自由に決定できます。 サービスを分類するのに良い方法は、組織への影響に基づいて、サービスをグループ内に配置する方法です。 既定では、すべてのサービスが **[許可されたビジネス データなし]** データ グループに配置されます。 DLP ポリシーのプロパティを管理センターから作成または変更する場合に、データ グループ内のサービスを管理します。

## <a name="how-data-is-shared-between-data-groups"></a>データ グループ間でデータを共有する方法
異なるグループ内にあるサービスの間でデータを共有することはできません。 たとえば、SharePoint と Salesforce を **[ビジネス データのみ]** グループに配置し、Facebook と Twitter を **[許可されたビジネス データなし]** グループに配置した場合、SharePoint と Facebook の間でデータを移動する PowerApp を作成することはできません。 異なるグループ間にあるサービス間でデータを共有することはできませんが、特定のグループ内にあるサービス間ではデータを共有することができます。 そのため、上述の例の場合、SherePoint と Salesforce は同じデータ グループ内に配置されているため、ユーザーが作成した PowerApps は SharePoint と Salesforce の間でデータを共有できます。 重要なポイントは、特定のグループ内にあるサービスはデータを共有でき、異なるグループ間のサービスはデータを共有できないということです。

また、1 つのデータ グループを*既定の*グループとして指定する必要があります。 最初は、**[許可されたビジネス データなし]** グループが *既定の* グループであり、すべてのサービスがこのデータ グループ内にあります。 管理者は、この既定のデータ グループを **[ビジネス データのみ]** データ グループに変更できます。 

> [!NOTE]
> PowerApps に追加されるすべての新しいサービスは、指定した "*既定の*" グループに配置されます。 このため、**[許可されたビジネス データなし]** を既定のグループのままにして、組織がビジネス データを新しいサービスと共有することの影響を評価してから **[ビジネス データのみ]** グループに手動でサービスを追加することをお勧めします。

## <a name="add-services-to-a-data-group"></a>サービスをデータ グループに追加する
このチュートリアルでは、SharePoint と Salesforce をデータ損失防止 (DLP) ポリシーの **[ビジネス データのみ]** データ グループに追加します。

1. DLP ポリシーの **[ビジネス データのみ]** グループ ボックス内にある **[+ 追加]** リンクを選択します。    
   ![イメージの追加](./media/introduction-to-data-groups/add-to-data-group-1.png)  
2. SharePoint と Salesforce を選択し、次に **[サービスの追加]** を選択してビジネス データのみのグループに両方を追加します。    
   ![[サービスの追加] のイメージ](./media/introduction-to-data-groups/add-to-data-group-2.png)  
3. 上部にあるメニューから **[ポリシーの保存]** を選択します。  
   ![[ポリシーの保存]](./media/introduction-to-data-groups/add-to-data-group-4.png)
4. SharePoint と Salesforce の両方が、ビジネス データのみのグループにあることを確認します。  
   ![更新されたビジネス データのみのグループ](./media/introduction-to-data-groups/add-to-data-group-3.png)   

このチュートリアルでは、SharePoint と Salesforce を DLP ポリシーの **[ビジネス データのみ]** データ グループに追加しました。 DLP ポリシーの環境の一部である、アプリを作成したいずれかのユーザーが SharePoint または Salesforce との間でデータ、および **[許可されたビジネス データなし]** データ グループのサービスを共有する場合、このアプリの実行は許可されません。

## <a name="remove-services-from-a-data-group"></a>データのグループからのサービスの削除
すべてのサービスは、使用可能なデータ グループのいずれかに含まれる必要があるため、サービスを特定のグループから削除する場合は、そのサービスを別のグループに追加してから、ポリシーを保存します。  

## <a name="change-the-default-data-group"></a>既定のデータ グループの変更
このチュートリアルでは、既定のデータ グループを **[許可されたビジネス データなし]** データ グループから **[ビジネス データのみ]** データ グループに変更します。  

> [!IMPORTANT]
> PowerApps に追加されるすべての新しいサービスは、指定した "*既定の*" グループに配置されます。 このため、**[許可されたビジネス データなし]** を既定のグループのままにして、手動でサービスを **[ビジネス データのみ]** グループに追加することをお勧めします。

1. 既定のデータ グループとして指定するデータ グループの右上隅にある **[...]** を選択します。    
   ![既定のグループの変更](./media/introduction-to-data-groups/default-data-group-0.png)  
2. **[既定のグループとして設定]** を選択します。  
   ![既定のグループの変更](./media/introduction-to-data-groups/default-data-group-1.png)   
3. 上部にあるメニューから **[ポリシーの保存]** を選択します。  
   ![既定のグループの変更](./media/introduction-to-data-groups/add-to-data-group-4.png)
4. 選択したデータ グループが既定のデータグループとして指定されていることを確認してください。  
   ![既定のグループの変更](./media/introduction-to-data-groups/default-data-group-2.png)   

## <a name="next-steps"></a>次の手順
* [データ損失防止 (DLP) ポリシーに関する詳細](prevent-data-loss.md)
* [環境に関する詳細](environments-overview.md)
* [Microsoft PowerApps の詳細](../maker/canvas-apps/getting-started.md)

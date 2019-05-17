---
title: ソリューションの階層の表示 | MicrosoftDocs
description: ソリューションの階層を使用する方法を説明します。
keywords: null
ms.date: 04/10/2019
ms.service: powerapps
ms.custom: null
ms.topic: article
applies_to:
  - Dynamics 365 for Customer Engagement (online)
  - Dynamics 365 for Customer Engagement Version 9.x
  - powerapps
ms.assetid: null
author: Mattp123
ms.author: matp
manager: kvivek
ms.reviewer: null
ms.suite: null
ms.tgt_pltfrm: null
caps.latest.revision: null
topic-status: Drafting
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---

# <a name="view-solution-layers"></a>ソリューションの階層の表示
ソリューションの階層を使用すると、ある期間のソリューションの変更によって発生したすべてのコンポーネントの変更を表示できます。 ソリューションの階層で、コンポーネントの特定の変更されたプロパティと変更されていないプロパティの詳細を表示するためにドリルダウンできます。 

ソリューションの階層には次のような利点があります: 
-   ソリューションがコンポーネントを変更した順序を確認しましょう。 
-   コンポーネントへの変更を含めた特定のソリューションの、コンポーネントのすべてのプロパティを表示しましょう。 
-   ソリューションの変更によって導入されたコンポーネントの変更詳細を表示することによって、依存関係やソリューションの階層の問題に関するトラブルシューティングに使用できます。

## <a name="view-the-solution-layers-for-a-component"></a>コンポーネントのソリューションの階層を表示する
ソリューション エクスプローラーの **コンポーネント** リストまたは **依存関係の詳細** ダイアログ ボックスから、ソリューションの階層にアクセスできます。 

1. **コンポーネント** リストからソリューションの階層を表示するには、**コンポーネント** リストで [ソリューション エクスプローラーを開いて](../model-driven-apps/advanced-navigation.md#solution-explorer)、**取引先企業** などのコンポーネントを選択して、ツールバーの **ソリューションの階層** を選択します。 

   > [!div class="mx-imgBorder"] 
   > ![](media/solution-layers-toolbar.png "ソリューションの階層ボタン")

2. ソリューションの階層ページが表示され、最新のレイヤーが一番上になるように、取引先企業エンティティのようなコンポーネントの各レイヤーが表示されます。 ソリューションの階層の詳細を表示するには、それを選択します。 

   > [!div class="mx-imgBorder"] 
   > ![](media/solution-layers-list.png "ソリューションの階層リスト")

3. **ソリューションの階層** ダイアログ ボックスで、**変更されたプロパティ** タブには特定のソリューションの階層の一部として変更されたプロパティだけが表示されます。 

   > [!div class="mx-imgBorder"] 
   > ![](media/solution-layers-change-prop.png "ソリューションの階層の変更されたプロパティ")

4. **すべてのプロパティ** タブを選択して、変更されたプロパティと変更されていないプロパティを含む、ソリューションの階層のすべてのプロパティを表示します。 

   > [!div class="mx-imgBorder"] 
   > ![](media/solution-layers-all-prop.png "ソリューションの階層のすべてのプロパティ")

## <a name="see-also"></a>関連項目
[ソリューションの概要](solutions-overview.md)
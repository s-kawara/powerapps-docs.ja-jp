---
title: PowerApps でソリューション エクスプローラーを使用する | MicrosoftDocs
description: ソリューション エクスプローラーを使用してアプリを作成またはカスタマイズする方法について説明します
ms.custom: ''
ms.date: 06/18/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Dynamics 365 (online)
- Dynamics 365 Version 9.x
- powerapps
author: Mattp123
ms.assetid: 72bacfbb-96a3-4daa-88ff-11bdaaac9a3d
caps.latest.revision: 57
ms.author: matp
manager: kvivek
ms.openlocfilehash: 6abbe701a6207e68ac367fbe80495a7d04a6e682
ms.sourcegitcommit: aba996b1773ecdf62758e06b34eaf57bede29e08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/08/2018
ms.locfileid: "39691653"
---
# <a name="use-the-solution-explorer"></a>ソリューション エクスプローラーを使用する

 ソリューション エクスプローラー内で、次のスクリーンショットで確認できるように、左側にあるナビゲーション ウィンドウを利用してノードの階層を移動できます。  
  
 ![エンティティが折りたたまれた既定のソリューション](media/crm-itpro-cust-defaultsolutionentitiescollapsed.PNG "エンティティが折りたたまれた既定のソリューション")  
  
> [!NOTE]
>  ソリューション エクスプローラーでカスタマイズ ツールを使用するとき、マウスとキーボードを使用します。 アプリケーションのこの部分はタッチ操作向けに最適化されていません。  
  
 各ノードを選択するとき、ソリューション コンポーネントの一覧を参照できます。 コマンド バーで利用できるアクションは、選択したノードのコンテキストによって変わります。また、ソリューションが既定のソリューションであるか、マネージド ソリューションであるかによっても変わります。 既定のソリューションではないアンマネージド ソリューションの場合、**[既存の追加]** コマンドを使用し、ソリューションにまだ含まれていないソリューション コンポーネントを表示できます。  
  
マネージド ソリューションの場合、利用できるコマンドはありません。次のメッセージが表示されます。  

> [!NOTE]
> マネージド ソリューション内でコンポーネントを直接編集することはできません。 ソリューション コンポーネントのマネージド プロパティがカスタマイズを許可するように設定されている場合、PowerApps デザイン ツールを使用するか、別のアンマネージド ソリューションから編集できます。    
  
 既定のソリューションでソリューション コンポーネントを見つけ、そこで編集を試みるか、作成した別のアンマネージド ソリューションに追加してみる必要があります。 ソリューション コンポーネントはカスタマイズできない場合があります。 詳細情報: [マネージド プロパティ](solutions-overview.md#managed-properties)
  
 カスタマイズの多くにはエンティティが含まれます。 **[エンティティ]** ノードを展開すると、システムに存在し、何らかの方法でカスタマイズ可能なすべてのエンティティが一覧表示されます。 各エンティティをさらに展開すると、次のスクリーンショットのアカウント エンティティで示すような、エンティティに含まれるソリューション コンポーネントを確認できます。  
  
 ![アカウント エンティティが展開された既定のソリューション](media/crm-itpro-cust-defaultsolution.PNG "アカウント エンティティが展開された既定のソリューション")  
  
 ソリューション エクスプローラーに含まれる個々のソリューション コンポーネントをカスタマイズする方法については、次のトピックをご覧ください。  
  
-   エンティティ、エンティティ関係、フィールド、メッセージのカスタマイズについては、[メタデータ](create-edit-metadata.md)に関するページを参照してください。  
  
-   エンティティ フォームについては、[フォーム](../model-driven-apps/create-design-forms.md)に関するページを参照してください。  
  
-   プロセスについては、[プロセス](../model-driven-apps/guide-staff-through-common-tasks-processes.md)に関するページを参照してください。  
  
-   ビジネス ルールについては、[ビジネス ルール](../model-driven-apps/create-business-rules-recommendations-apply-logic-form.md)に関するページを参照してください。  

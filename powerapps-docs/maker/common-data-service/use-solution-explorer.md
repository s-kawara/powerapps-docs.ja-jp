---
title: PowerApps のソリューション エクスプローラーの使用 | MicrosoftDocs
description: ソリューション エクスプローラーを使用してカスタム アプリを作成またはカスタマイズする方法を学習
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
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="use-the-solution-explorer"></a>ソリューション エクスプローラーを使用する

 ソリューション エクスプローラー内で、次のスクリーンショットに示すように、左側のナビゲーション ウィンドウを使用して、ノードの階層を移動できます。  
  
 ![エンティティが折りたたまれた既定のソリューション](media/crm-itpro-cust-defaultsolutionentitiescollapsed.PNG "エンティティが折りたたまれた既定のソリューション")  
  
> [!NOTE]
>  ソリューション エクスプローラーでカスタマイズ ツールを使用するときは、マウスとキーボードを使用します。 アプリケーションのこの部分は、タッチ操作に最適化されていません。  
  
 各ノードを選択して、ソリューション コンポーネントの一覧を表示できます。 コマンド バーで使用できる操作は、ソリューションが既定のソリューションか管理ソリューションの場合、選択したノードの内容によって変化します。 既定のソリューションではないアンマネージド ソリューションでは、**既存を追加**コマンドを使用して、ソリューション内にすでに存在するソリューション コンポーネントを追加できます。  
  
管理ソリューションでは、使用可能なコマンドが存在しない場合は、メッセージが表示されます。  

> [!NOTE]
> 管理ソリューション内のコンポーネントは直接編集できません。 ソリューション コンポーネントの管理プロパティがカスタマイズを有効にしている場合には、PowerApps 設計ツールまたは他のアンマネージド ソリューションからコンポーネントを編集できます。    
  
 既定のソリューションのソリューション コンポーネントを見つける必要があります。そして、そこでそれを編集するか、作成した別のアンマネージド ソリューションに追加してみます。 ソリューション コンポーネントがカスタマイズ可能でない場合があります。 詳細: [管理プロパティ](solutions-overview.md#managed-properties)
  
 カスタマイズの多くには、エンティティが関係します。 何らかの方法でカスタマイズされたシステム内のすべてのエンティティの一覧を表示するには、**エンティティ**ノードを展開します。 次のスクリーンショットの取引先企業エンティティに表示されているように、エンティティに含まれているソリューション コンポーネントを表示するには、各エンティティをさらに展開します。  
  
 ![既定のソリューションによって展開される取引先企業エンティティ](media/crm-itpro-cust-defaultsolution.PNG "既定のソリューションによって展開される取引先企業エンティティ")  
  
 ソリューション エクスプローラーにある各ソリューション コンポーネントのカスタマイズの詳細については、以下のトピックを参照してください。  
  
-   エンティティ、エンティティの関連付け、フィールドおよびメッセージのカスタマイズについては、[メタデータ](create-edit-metadata.md) を参照してください。  
  
-   エンティティ フォームについては、[フォーム](../model-driven-apps/create-design-forms.md) を参照してください。  
  
-   プロセスについては、[プロセス](../model-driven-apps/guide-staff-through-common-tasks-processes.md) を参照してください。  
  
-   業務ルールについては、[業務ルール](../model-driven-apps/create-business-rules-recommendations-apply-logic-form.md) を参照してください。  

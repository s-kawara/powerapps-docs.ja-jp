---
title: PowerApps でモデル駆動型統合インターフェイス アプリのプロパティを指定する | MicrosoftDocs
description: アプリのグリッド コントロールを構成する方法について説明します
keywords: ''
ms.date: 06/06/2018
ms.service: crm-online
ms.custom: ''
ms.topic: article
applies_to:
- Dynamics 365 (online)
- Dynamics 365 Version 9.x
- powerapps
author: Mattp123
ms.assetid: 3ecea4a7-0d18-4ccd-9609-3a62179e9e1b
ms.author: matp
manager: kvivek
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
caps.latest.revision: 0
topic-status: Drafting
ms.openlocfilehash: 007ac566e317ee99bd85ab0675e5a53839800bb4
ms.sourcegitcommit: aba996b1773ecdf62758e06b34eaf57bede29e08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/08/2018
ms.locfileid: "39691605"
---
# <a name="specify-properties-for-model-driven-unified-interface-apps"></a>モデル駆動型統合インターフェイス アプリのプロパティを指定します

統合インターフェイス フレームワークでは応答性の高いデザインを原則とし、画面の大きさや方向に関係なく、最適な表示と対話性を提供します。 統合インターフェイス フレームワークを利用するモデル駆動型アプリでは、グリッド (ビュー) コントロールが応答性に優れています。 スマートフォンや小さなビューポートなどでコンテナーが小さくなると、グリッドがリストに変化します。 

"読み取り専用グリッド" コントロールにより、グリッドが異なる画面サイズにリフローされるしくみが指定されます。 アプリの作成者が統合インターフェイス アプリを使用するとき、カスタムのグリッドとリストに対して "読み取り専用グリッド" コントロールとそのプロパティを構成できます。
- **カード フォーム** プロパティ: 既定のリスト テンプレートの代わりに、リストのカード フォームを使用します。 カード フォームでは、既定のリスト テンプレートより、提供されるリスト項目が増えます。
- **リフロー動作**プロパティ: このパラメーターを使用し、グリッドがリストにリストにリフローされるのかどうかを指定します。

## <a name="allow-grid-to-reflow-into-list"></a>グリッドをリストにリフローする

"読み取り専用グリッド" コントロールをコントロール リストに追加することで、次の機能を構成できます。 
- モバイルなど、小さなディスプレイでグリッドをリストにリフローできます。
- グリッド専用またはリスト専用としてレンダリング モードを指定します。  

1. [ソリューション エクスプローラー](advanced-navigation.md#solution-explorer)を開きます。
2. ナビゲーション ウィンドウで **[エンティティ]** を開き、適切なエンティティを選択し (**[アカウント]** や **[連絡先]** など)、**[コントロール]** タブで **[コントロールの追加]** を選択します。

    ![[コントロールの追加] を開く](media/UnifiedInterface_ReadOnlyGrid_AddControl.png "[コントロールの追加] を開く")

3. コントロール リストから **[読み取り専用グリッド]** を選択し、**[追加]** を選択します。

    利用できるコントロールの一覧にコントロールが追加されます。
   
    ![コントロールの選択](media/UnifiedInterface_ReadOnlyGrid_SelectControl.png "コントロールの選択")
    
4. グリッドを読み取り専用にするデバイスを選択します (**Web**、**スマートフォン**、**タブレット**)。

    ![デバイスの種類を選択する](media/UnifiedInterface_ReadOnlyGrid_SelectDevice.png "デバイスを選択する")

5. **カード フォーム** プロパティを構成します。

    カード フォーム プロパティを使用し、既定のリスト テンプレートの代わりにリスト項目を表示できます。 カード フォームでは、既定のリスト テンプレートより、提供されるリスト項目が増えます。    

    a. **[カード フォーム]** の隣にある鉛筆アイコンを選択します。

    ![カード フォームの編集](media/UnifiedInterface_ReadOnlyGrid_CardForm.png "カード フォームの編集")

    b.  種類として **[エンティティ]** と **[カード フォーム]** を選択します。

    ![カード フォーム プロパティ](media/UnifiedInterface_ReadOnlyGrid_CardFormProperties.png "カード フォーム プロパティ")

    c. **[OK]** をクリックします。
6. **[リフロー動作]** プロパティを構成します。 
    
    a. **[リフロー動作]** の隣にある鉛筆アイコンを選択します。

    ![リフロー動作の編集](media/UnifiedInterface_ReadOnlyGrid_EditReflow.png "リフロー動作の編集")

    b. **[静的オプションにバインド]** ドロップダウンからグリッド フローの種類を選択します。
    |フローの種類|説明|
    |--------------|--------------------|
    |**リフロー**|十分なディスプレイ領域がないとき、リスト モードにレンダリングすることをグリッドに許可します。|
    |**グリッドのみ**|十分なディスプレイ領域がないときでき、リスト モードにレンダリングすることをグリッドに許可しません。|
    |**リストのみ**|グリッドで表示できるだけの領域が十分にあるときでも表示をリストに限定します。|
    
     ![リフロー動作のプロパティ](media/UnifiedInterface_ReadOnlyGrid_ReflowProperties.png "リフロー動作のプロパティ")

    c. **[OK]** をクリックします。


7.  変更を保存し、公開します。 


## <a name="conditional-image"></a>条件付きイメージ
一覧に値の代わりにカスタム アイコンを表示したり、JavaScript を利用することで列の値に基づいて選択するためのロジックを確立したりできます。 条件付きイメージの詳細については、「[リスト ビューに値の代わりにカスタム アイコンを表示する](../common-data-service/display-custom-icons-instead.md)」を参照してください。

## <a name="next-steps"></a>次の手順
[ビューを作成または編集する](create-edit-views.md)
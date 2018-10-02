---
title: PowerApps でモデル駆動型統一インターフェイス アプリ用プロパティを指定する | MicrosoftDocs
description: アプリのグリッド コントロールの構成方法を学習する
keywords: ''
ms.date: 06/06/2018
ms.service: crm-online
ms.custom: null
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - powerapps
author: Mattp123
ms.assetid: 3ecea4a7-0d18-4ccd-9609-3a62179e9e1b
ms.author: matp
manager: kvivek
ms.reviewer: null
ms.suite: null
ms.tgt_pltfrm: null
caps.latest.revision: 0
topic-status: Drafting
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---

# <a name="specify-properties-for-model-driven-unified-interface-apps"></a>モデル駆動型統一インターフェイス アプリ用プロパティを指定する

統一インターフェイス フレームワークは、応答性を高める設計原則を使用して、すべての画面サイズまたは表示方向に最適な表示および対話型エクスペリエンスを提供します。 統一インターフェイス フレームワークを使用するモデル駆動型アプリでは、グリッド (ビュー) コントロールは敏感に反応します。 コンテナのサイズが小さくなると—たとえば、電話およびより小さいビューポート上では—、グリッドがリストに変換されます。 

読み取り専用グリッド コントロールは、異なる画面サイズにグリッドがリフローする方法を指定します。 アプリ作成者として、 統一インターフェイス アプリで作業する場合、カスタムのグリッドおよびリストに対して、読み取り専用グリッドのコントロールとそのプロパティを構成することができます。
- **カード フォーム** プロパティ: 既定のリスト テンプレートではなくリストに対して、カード フォームを使用します。 カード フォームは、既定のテンプレートよりも、リスト項目に対してより多くの情報を提供します。
- **リフロー動作**プロパティ: このパラメーターを使用して、リストにリフローする、またはリフローしないグリッドを指定します。

## <a name="allow-grid-to-reflow-into-list"></a>グリッドのリストへのリフローを可能にする

読み取り専用グリッドのコントロールをコントロール一覧に追加すると、次の機能の構成が可能になります。 
- モバイルなどの小さい画面上のリストへのグリッドのリフローを可能にします。
- レンダリング モードをグリッドのみまたはリストのみとして指定します。  

1. [ソリューション エクスプローラー](advanced-navigation.md#solution-explorer)を開きます。
2. ナビゲーション ウィンドウで**エンティティ**を展開して、適切なエンティティ (**取引先企業**または**取引先担当者**など) を選択してから、**コントロール** タブで、**コントロールの追加**を選択します。

    ![コントロールの追加を開く](media/UnifiedInterface_ReadOnlyGrid_AddControl.png "コントロールの追加を開く")

3. コントロールのリストから**読み取り専用グリッド**を選択してから、**追加**を選択します。

    コントロールが使用可能なコントロールのリストに追加されます。
   
    ![コントロールの選択](media/UnifiedInterface_ReadOnlyGrid_SelectControl.png "コントロールの選択")
    
4. グリッドを読み取り専用にする対象のデバイス (**Web**、**電話**、または**タブレット PC**) を選択します。

    ![デバイスの種類の選択](media/UnifiedInterface_ReadOnlyGrid_SelectDevice.png "デバイスの選択")

5. **カード フォーム**プロパティを構成します。

    カード フォームのプロパティを使用して、既定のリスト テンプレートではなく、リスト アイテムを表示できます。 カード フォームは、既定のテンプレートよりも、リスト アイテムに対してより多くの情報を提供します。    

    a. **カード フォーム**の横にある鉛筆アイコンを選択します。

    ![カード フォームの編集](media/UnifiedInterface_ReadOnlyGrid_CardForm.png "カード フォームの編集")

    b.  **エンティティ**と**カード フォーム**の種類を選択します。

    ![カード フォームのプロパティ](media/UnifiedInterface_ReadOnlyGrid_CardFormProperties.png "カード フォームのプロパティ")

    c. **OK** を選択します。
6. **リフロー動作**プロパティを構成します。 
    
    a. **リフロー動作**の横にある鉛筆アイコンを選択します。

    ![リフロー動作の編集](media/UnifiedInterface_ReadOnlyGrid_EditReflow.png "リフロー動作の編集")

    b. **静的オプションにバインド**ドロップ ダウンからグリッド フローの種類を選択します。
    |フローの種類|内容|
    |--------------|--------------------|
    |**リフロー**|十分な表示領域がない場合に応じて、グリッドがリスト モードで表示されるようにします。|
    |**グリッドのみ**|十分な表示領域がない場合でも、グリッドのリストへのリフローを制限します。|
    |**リストのみ**|グリッドとして表示するための十分な領域のある場合でも、リストとしてのみ表示します。|
    
     ![リフロー動作のプロパティ](media/UnifiedInterface_ReadOnlyGrid_ReflowProperties.png "リフロー動作のプロパティ")

    c. **OK** を選択します。


7.  変更を保存して公開します。 


## <a name="conditional-image"></a>条件付き画像
JavaScript を使用することによって、リストの値の代わりにユーザー定義アイコンを表示できるし、列の値に基づいてそれらを選択するために使用するロジックを設定できます。 条件付き画像の詳細については、「[リスト ビューの値ではなくユーザー定義アイコンの表示](../common-data-service/display-custom-icons-instead.md)」を参照してください。

## <a name="next-steps"></a>次のステップ
[ビューの作成または編集](create-edit-views.md)

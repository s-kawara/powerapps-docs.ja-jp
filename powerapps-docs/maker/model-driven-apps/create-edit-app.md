---
title: PowerApps でアプリ デザイナーを使用してモデル駆動型アプリを作成または編集 | MicrosoftDocs
description: アプリ デザイナーを使用してアプリを作成または編集する方法を学習する
keywords: ''
ms.date: 02/05/2019
ms.service: crm-online
ms.custom: null
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - powerapps
author: Mattp123
ms.assetid: 2a44229e-44f0-4c4e-ba21-a476210d0a12
ms.author: matp
manager: kvivek
ms.reviewer: null
ms.suite: null
ms.tgt_pltfrm: null
caps.latest.revision: 19
topic-status: Drafting
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---

# <a name="create-a-model-driven-app-by-using-the-app-designer"></a>アプリ デザイナーを使用してモデル駆動型アプリを作成する

このトピックでは、タイル ベースのアプリ デザイナーを使用してモデル駆動型アプリを作成および編集する方法の基本事項について説明します。

## <a name="prerequisites"></a>前提条件
アプリを作成する前に、以下の前提条件を確認してください。
- PowerApps 環境。 詳細情報: [環境の作成](https://docs.microsoft.com/powerapps/administrator/create-environment)
- システム管理者またはシステム カスタマイザー セキュリティ ロール。 詳細情報: [定義済みのセキュリティ ロールについて](https://docs.microsoft.com/powerapps/maker/model-driven-apps/share-model-driven-app#about-predefined-security-roles)
 
<a name="createApp"></a>   
## <a name="create-an-app"></a>アプリの作成  

1.  [PowerApps](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) **ホーム** ページで、モデル駆動型アプリの **空のモデル駆動型アプリ** オプションを選択します。  

    > [!IMPORTANT]
    > **モデル駆動型** デザイン モードがない場合は、[環境の作成](https://docs.microsoft.com/powerapps/administrator/create-environment)が必要となることがあります。 

2. **新しいアプリケーションの作成**ページ上に、以下の情報を入力します。 

    - **名前** : アプリの名前を入力します。  
  
    - **一意の名前**: 一意の名前は指定するアプリの名前に基づいて自動的に設定されます。 発行者の接頭辞が使用されています 編集可能である一意の名前の一部を変更することができます。 一意の名前には英語の文字と数字のみを含めることができます。  
  
        > [!NOTE]
        >  発行者の接頭辞は、この発行者が含まれているソリューションに対して作成されたエンティティまたはフィールドに追加されるテキストです。   
  
    - **Description**: アプリの種類と動作に関する短い説明を入力します。  
  
    - **アイコン**: 既定では、**既定のアプリケーションの使用**サムネイル チェック ボックスがチェック済みです。 アプリケーションのアイコンとして、異なる Web リソースを選択するには、チェック ボックスをオフにし、次に、ドロップダウン リストからアイコンを選択します。 このアイコンはアプリのプレビュー タイルに表示されます。  
  
    - **既存のソリューションを使用してアプリを作成する**: インストールされたソリューションの一覧からアプリを作成するには、このオプションを選択します。 このオプションを選択すると、ヘッダー上の**完了**は**次へ**に切り替わります。 **次へ**を選択する場合、**既存のソリューションからアプリを作成する**ページが開きます。 **ソリューションの選択**ドロップダウン リストから、アプリを作成するソリューションを選択します。 選択したソリューションに対して使用可能なサイト マップがある場合、**サイトマップの選択**ドロップダウン リストが表示されます。 サイト マップを選択してから、**完了**を選択します。

      > [!NOTE]
      > サイト マップの追加時に**既定のソリューション**を選択することにより、そのサイト マップに関連付けられたコンポーネントは自動的にアプリに追加されます。  

      ![既存のソリューションを使用してアプリ ページを作成する](media/use-existing-solution-to-create-the-app.png "既存のソリューションを使用してアプリを作成する") 

    - **アプリの [ようこそ] ページを選択**: このオプションを使用すると、組織で利用できる Web リソースの中から選択することができます。 作成した [ようこそ] ページには、ビデオへのリンク、アップグレードの手順、開始方法に関する情報など、ユーザーにとって有用な情報を含めることができます。 [ようこそ] ページはアプリを開くと表示されます。 ユーザーは、[ようこそ] ページの**この [ようこそ] 画面を次回は表示しない**を選択して、アプリを次回起動するときにこのページを表示させないようにすることができます。 **次回このようこそ画面を表示しない** オプションはユーザーレベルの設定であり、管理者やアプリ メーカーによって制御できないことに注意してください。 [ようこそ] ページとして使用することができる HTML ファイルなどの Web リソースの作成方法の詳細については、[Web リソースを作成および編集して Web アプリケーションを拡張](create-edit-web-resources.md)を参照してください。  
      
    アプリのプロパティを後に編集するには、アプリ デザイナーの**プロパティ**タブに移動します。 詳細: [アプリ プロパティの管理](manage-app-properties.md)  
  
     > [!NOTE]
     >  **プロパティ**タブ上で一意の名前とアプリの URL の接頭辞を変更することはできません。  
  
3. **完了**を選択、または &mdash; **既存のソリューションを使用してアプリを作成する**を選択した場合は &mdash; **次へ**を選択して、組織でインポートした使用可能なソリューションから選択します。  
  
    新しいアプリが作成されて下書き状態が表示されます。 新しいアプリのアプリ デザイナー キャンバスが表示されます。 そこでは、エンティティ、ビュー、ダッシュボードなどのコンポーネントを追加してアプリを有用にできます。 詳細情報: [アプリ コンポーネントの追加または編集](add-edit-app-components.md)  
   
<a name="editApp"></a>   
## <a name="edit-an-app"></a>アプリの編集  
  
1.  [PowerApps](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) にサインインします。  

> [!IMPORTANT]
> **モデル駆動型** デザイン モードがない場合は、[環境の作成](https://docs.microsoft.com/powerapps/administrator/create-environment)が必要となることがあります。 

2. 左側のナビゲーション ウィンドウで**アプリ**を選択して、モデル駆動型アプリを選択し、ツール バーの**編集**を選択します。   

3. アプリ デザイナーで、必要に応じてアプリにコンポーネントを追加または編集します。 詳細情報: [アプリ コンポーネントの追加または編集](add-edit-app-components.md)  
 
  
### <a name="next-steps"></a>次のステップ  
 [アプリのコンポーネントの追加または編集](add-edit-app-components.md)   



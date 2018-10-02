---
title: PowerApps でモデル駆動型アプリ ビューの列を選択および構成する | MicrosoftDocs
description: アプリのビューを選択および構成する方法を学習する
keywords: ''
ms.date: 06/11/2018
ms.service: crm-online
ms.custom: null
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - powerapps
ms.assetid: 31bfcf18-58c3-491c-91b5-f9b0f5424852
author: Mattp123
ms.author: matp
manager: kvivek
ms.reviewer: null
ms.suite: null
ms.tgt_pltfrm: null
caps.latest.revision: 25
topic-status: Drafting
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---

# <a name="tutorial-choose-and-configure-columns-in-model-driven-app-views"></a>チュートリアル: モデル駆動型アプリ ビューの列を選択および構成する

<a name="BKMK_ChooseAndConfigureColumns"></a>   

 フィルター条件とともに、PowerApps ビューに表示される列はビューに表示される値にとって非常に重要です。 このチュートリアルでは、次のタスクを実行して、ビューを作成または編集します。  

-   [ビュー エディターを開く](choose-and-configure-columns.md#open-the-view-editor)  
   
-   [列を追加する](choose-and-configure-columns.md#BKMK_AddColumns)  
  
-   [列を削除する](choose-and-configure-columns.md#BKMK_RemoveColumns)  
  
-   [列の幅を変更する](choose-and-configure-columns.md#BKMK_ChangeColumnWidth)  
  
-   [列の移動](choose-and-configure-columns.md#BKMK_MoveAColumns)  
  
-   [列のプレゼンスを有効または無効にする](choose-and-configure-columns.md#BKMK_EnableOrDisablePresence)  
  
-   [検索列の追加](choose-and-configure-columns.md#BKMK_AddFindColumns)  

### <a name="open-the-view-editor"></a>ビュー エディターを開く

1.  [PowerApps](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) サイトで、**モデル駆動型** (ナビゲーション ウィンドウの左下) を選択します。  

    ![モデル駆動型の設計モード](../model-driven-apps/media/model-driven-switch.png)

2.  **データ**を展開して**エンティティ**を選択し、目的のエンティティを選択して**ビュー** タブを選択します。 

    > [!div class="mx-imgBorder"] 
    > ![[ビュー]](media/available-views.png)

3. 既存のビューを選択して開くか、ツール バーで **ビューの追加** を選択します。 

<a name="BKMK_AddColumns"></a>   
### <a name="add-columns"></a>列を追加する  
 現在のエンティティからの列、または現在のエンティティと 1:N のエンティティの関連付けを持つ関連エンティティのいずれかを含めることができます。  
  
 たとえば、列にユーザー所有のエンティティの所有者を表示する場合があります。 所有者の名前を表示するには、現在のエンティティの**所有者**フィールドを選択できます。 これは、所有者である人の**ユーザー**レコードを開くリンクとして表示されます。 この場合、[列のプレゼンスを有効または無効にする](choose-and-configure-columns.md#BKMK_EnableOrDisablePresence) オプションもあります。  
  
 レコードの所有者の電話番号を表示する場合は、**レコード タイプ**ドロップダウンから**所有ユーザー (ユーザー)** を選択し、**代表電話**フィールドを選択する必要があります。  
  
#### <a name="add-columns-to-views"></a>ビューへの列の追加  
  
1.  ビューを作成および編集しているとき、**列の追加** を選択します。 

    > [!div class="mx-imgBorder"] 
    > ![ビュー エディターの列の追加](media/view-editor.png)

    **列の追加**ダイアログ ボックスが表示されます。

    > [!div class="mx-imgBorder"] 
    > ![列を追加する](media/add-columns.png)
  
2.  関連エンティティのフィールドを含める場合は、**レコード タイプ**を選択します。  
  
3.  関連エンティティからも複数のフィールドを選択できます。  
  
4.  必要なフィールドを選択した後、**OK** を選択し、**列の追加**ダイアログ ボックスを閉じます。  
  
 列を追加する際、ビューの幅を拡大します。 ビューの幅がビューをページ内に表示するために使用できるスペースを超える場合は、隠れている列を水平スクロール バーでスクロールして表示することができます。  
  
> [!TIP]
>  特定の値を持つレコードのみが表示されるように特定のフィールドのデータにフィルターをビューで適用する場合、ビューのその列を含めないでください。 たとえば、アクティブなレコードのみを表示する場合は、ビューのステータス列を含めないでください。 その代わり、ビューに表示されるすべてレコードがアクティブであることを表しているビューを指定します。  
  
> [!NOTE]
>  更新したエンティティの検索ダイアログ ビューに列を追加するとき、最初の 3 列のみが表示されます。  
  
<a name="BKMK_RemoveColumns"></a>   
### <a name="remove-columns"></a>列を削除する  
  
1.  ビューの作成と編集 のときに、削除する列を選択します。  
  
2.  **タスク**領域で、**削除**を選択します。  
  
3.  確認メッセージで、**OK** を選択します。  
  
<a name="BKMK_ChangeColumnWidth"></a>   
### <a name="change-column-width"></a>列の幅を変更する  
  
1.  ビューの作成と編集 のときに、変更する列を選択します。  
  
2.  **タスク**領域で、**プロパティの変更**を選択します。  
  
3.  **列のプロパティの変更**ダイアログ ボックスで、列幅を設定するオプションを選択し、**OK** を選択します。  
  
<a name="BKMK_MoveAColumns"></a>   
### <a name="move-a-column"></a>列の移動  
  
1.  ビューの作成と編集 のときに、移動する列を選択します。  
  
2.  **タスク**領域で、矢印を使用して、列を左右に移動します。  
  
<a name="BKMK_EnableOrDisablePresence"></a>   
### <a name="enable-or-disable-presence-for-a-column"></a>列のプレゼンスを有効または無効にする  
 次の条件が成り立つ場合、Skype for Business オンライン プレゼンス コントロールがリストに表示されます。このコントロールは、人が応対できるかどうかを示し、次の場合、ユーザーがインスタント メッセージングでそれらの人と対話できるようにします。  
  
-   ユーザーが、Edge または Internet Explorer を使用している。  
  
-   ユーザーに Skype for Business がインストールされている。  
  
-   ユーザーが Internet Explorer で Microsoft ActiveX を有効にしている。  
  
-   組織が、システム設定で、システムのプレゼンスを有効にしている。  
  
 プレゼンス コントロールとそれを有効にする設定は、電子メール対応エンティティ (ユーザー、取引先担当者、営業案件、潜在顧客、またはユーザー定義エンティティ) のプライマリ フィールドを表示する列に対してのみ使用できます。  
  
#### <a name="enable-or-disable-skype-for-business-presence-for-a-column"></a>列の Skype for Business プレゼンスを有効または無効にする  
  
1.  ビューの作成と編集 のときに、変更する列を選択します。  
  
2.  **タスク**領域で、**プロパティの変更**を選択します。  
  
3.  **列のプロパティの変更**ダイアログ ボックスで、**この列のプレゼンスを有効にする**を選択するかまたはその選択を解除し、**OK** を選択します。  
  
<a name="BKMK_AddFindColumns"></a>   
### <a name="add-find-columns"></a>検索列の追加  
 検索列とは、検索フィールドのレコードを検索する場合など、リストに表示される**レコードを検索します**ボックスを使用するときに、またはアプリケーションにエンティティのレコードの検索機能があるときはいつでも、アプリケーションが検索する列です。  
  
1.  **簡易検索**ビューを開きます。 簡易検索ビューの詳細については、「[ビューの種類](create-edit-views.md#types-of-views)」を参照してください。  
  
2.  **検索列の追加**を選択して、ダイアログ ボックスを開きます。  
  
3.  検索するデータが含まれているフィールドを選択します。  
  
4.  **OK** を選択して、**検索列の追加**ダイアログ ボックスを閉じます。  

## <a name="community-tools"></a>コミュニティ ツール

**ビュー レイアウト レプリケーター**および**ビュー デザイナー**は Dynamics 365 Customer Engagement 用に開発された XrmToolbox コミュニティが提供するツールです。 コミュニティ開発ツールのトピック、[開発者ツール](https://docs.microsoft.com/dynamics365/customer-engagement/developer/developer-tools) を参照してください。

> [!NOTE]
> コミュニティ ツールは Microsoft Dynamics の製品ではなく、コミュニティ ツールに対するサポートは提供されません。 このツールに関するご質問は、その発行元にお問い合わせください。 詳細: [XrmToolBox](https://www.xrmtoolbox.com)。 

## <a name="next-steps"></a>次のステップ
[ビューの作成または編集](create-edit-views.md)

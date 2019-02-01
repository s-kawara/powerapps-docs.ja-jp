---
title: PowerApps でモデル駆動型アプリ ビューの列を選択および構成する | MicrosoftDocs
description: アプリのビューを選択および構成する方法を学習する
keywords: ''
ms.date: 11/27/2018
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

# <a name="choose-and-configure-columns-in-model-driven-app-views"></a>モデル駆動型アプリ ビューの列を選択および構成する

<a name="BKMK_ChooseAndConfigureColumns"></a>   

 フィルター条件とともに、PowerApps ビューに表示される列はビューに表示される値にとって非常に重要です。 このトピックでは、次のタスクを実行して、ビューを作成または編集します。  

-   [ビュー エディターを開く](choose-and-configure-columns.md#open-the-view-editor)  
   
-   [列を追加する](choose-and-configure-columns.md#BKMK_AddColumns)  
  
-   [列を削除する](choose-and-configure-columns.md#BKMK_RemoveColumns)  
  
-   [列の幅を変更する](choose-and-configure-columns.md#BKMK_ChangeColumnWidth)  
  
-   [列の移動](choose-and-configure-columns.md#BKMK_MoveAColumns)  
    
  > [!IMPORTANT]
  > 最新バージョンのビュー デザイナーは現在プレビュー中です。 列の存在の有効化または無効化や検索列の追加などの一部の機能はまだサポートされていません。 これらのタスクを遂行するには、[ビューをクラシック ビュー デザイナーで開きます](/dynamics365/customer-engagement/customize/create-and-edit-views#open-the-classic-view-designer)。
  >  -   [列のプレゼンスを有効または無効にする](/dynamics365/customer-engagement/customize/choose-and-configure-columns#BKMK_EnableOrDisablePresence)  
  >
  >  -   [検索列の追加](choose-and-configure-columns.md#BKMK_AddFindColumns)  



### <a name="open-the-view-editor"></a>ビュー エディターを開く

1.  [PowerApps](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) にサインインします。  

2.  **データ**を展開して**エンティティ**を選択し、目的のエンティティを選択して**ビュー** タブを選択します。 

    > [!div class="mx-imgBorder"] 
    > ![[ビュー]](media/available-views.png)

3. 既存のビューを選択して開くか、ツール バーで **ビューの追加** を選択します。 

<a name="BKMK_AddColumns"></a>   
### <a name="add-columns"></a>列を追加する  
 現在のエンティティからの列、または現在のエンティティと 1:N のエンティティの関連付けを持つ関連エンティティのいずれかを含めることができます。  
  
 たとえば、列にユーザー所有のエンティティの所有者を表示する場合があります。 所有者の名前を表示するには、現在のエンティティの**所有者**フィールドを選択できます。 これは、所有者である人の**ユーザー**レコードを開くリンクとして表示されます。  
  
 レコードの所有者の電話番号を表示する場合は、**レコード タイプ**ドロップダウンから**所有ユーザー (ユーザー)** を選択し、**代表電話**フィールドを選択する必要があります。  
  
#### <a name="add-columns-to-views"></a>ビューへの列の追加  
  
1.  ビューの作成および編集中に、**フィールド**パネルが開いていることを確認します。 開いていない場合は、ツールバー上の**フィールドの追加**を選択します。 

    > [!div class="mx-imgBorder"] 
    > ![ビュー エディターの列の追加](media/fields-drawer-view-designer.png)

2.  ビュー デザイナーに追加するフィールドを選択します。 これにより、フィールドがビューの右側に列として追加されます。

3.  **関連**タブを選択して、関連するエンティティおよびその対応フィールドを表示します。
  
 列を追加する際、ビューの幅を拡大します。 ビューの幅がビューをページ内に表示するために使用できるスペースを超える場合は、隠れている列を水平スクロール バーでスクロールして表示することができます。  
  
> [!TIP]
>  特定の値を持つレコードのみが表示されるように特定のフィールドのデータにフィルターをビューで適用する場合、ビューのその列を含めないでください。 たとえば、アクティブなレコードのみを表示する場合は、ビューのステータス列を含めないでください。 その代わり、ビューに表示されるすべてレコードがアクティブであることを表しているビューを指定します。  
  
> [!NOTE]
>  更新したエンティティの検索ダイアログ ビューに列を追加するとき、最初の 3 列のみが表示されます。  
  
<a name="BKMK_RemoveColumns"></a>   
### <a name="remove-columns"></a>列を削除する  
  
1.  削除する列のヘッダーを選択します。  
  
2.  ドロップダウンで、**削除**を選択します。  
  
<a name="BKMK_ChangeColumnWidth"></a>   
### <a name="change-column-width"></a>列の幅を変更する  
  
1.  ビュー内の列の間の領域にマウス ポインターを移動します。  
  
2.  行が表示され、カーソルは両端矢印になります。  
  
3.  列を適切な幅にドラッグします。  
  
<a name="BKMK_MoveAColumns"></a>   
### <a name="move-a-column"></a>列の移動  
  
列ヘッダーを正しい場所にクリックおよびドラッグします。
  
> [!TIP]
>   また、移動する列のヘッダーをドロップダウンから選択して**右に移動**または**左に移動**を選択することができます。  
  
## <a name="next-steps"></a>次のステップ
[ビューの作成または編集](create-edit-views.md)

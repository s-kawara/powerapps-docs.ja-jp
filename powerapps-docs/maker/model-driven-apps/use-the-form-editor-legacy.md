---
title: PowerApps のモデル駆動型アプリ フォーム内でナビゲーションを変更する | MicrosoftDocs
description: フォーム内のナビゲーションを変更する方法を学習
ms.custom: ''
ms.date: 06/06/2018
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
  - powerapps
author: Mattp123
ms.assetid: 4c379202-9f0e-4003-a49c-efff53e7f79f
caps.latest.revision: 63
ms.author: matp
manager: kvivek
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="change-navigation-within-a-model-driven-app-form"></a>モデル駆動型アプリ フォーム内でナビゲーションを変更する

 フォーム内のナビゲーションを使用すると、アプリのユーザーは関連レコードの一覧を表示することができます。 各エンティティ関係を表示するかどうかを制御するプロパティがあります。 詳細情報: [主エンティティのナビゲーション ウィンドウ項目](../common-data-service/create-edit-1n-relationships-solution-explorer.md#navigation-pane-item-for-primary-entity)  
  
 表示されるように構成されているエンティティ関係は、フォーム エディター内で上書きされます。 フォーム ナビゲーションを介して Web リソースや他の Web サイトを表示するナビゲーション リンクを含めることができます。  
  
 詳細な手順については、「[Common Data Service のエンティティ関係の作成および編集](../common-data-service/create-edit-entity-relationships.md)」を参照してください  
  
 ナビゲーションの編集を可能にするには、最初にフォーム デザイナーの**ホーム**タブの**選択**グループから**ナビゲーション**を選択する必要があります。  
 
> [!div class="mx-imgBorder"] 
> ![ナビゲーション コマンド](media/navigation-command.png)
 
 右側のウィンドウで、**関連付けエクスプローラー**で、1:N (1 対多) または N:N (多対多) の関連付けに基づいてフィルターするか、使用可能な関連付けすべてを表示できます。 **未使用のチェック ボックスのみを示します**は無効および選択済となっています。 したがって 1 回に1つの関連付けを追加できます。  
 
 > [!div class="mx-imgBorder"] 
 > ![関連付けエクスプローラー](media/relationship-explorer.png)

 **関連付けエクスプローラー**から関連付けを追加するには、関連付けをダブルクリックすると、ナビゲーション領域の現在選択されている関係付けの下に追加されます。 ナビゲーション領域で関連付けをダブルクリックすると、**表示方法**タブのラベルを変更できます。**名前**タブに、関連付けに関する情報を表示できます。 エンティティの定義を開くには、**編集**ボタンを使用します。  
  
 ナビゲーション領域には、5 つのグループがあります。 それらをドラッグして場所を変え、ダブルクリックしてラベルを変更できますが、削除することはできません。 グループに何かあるときにのみ表示されます。 したがって、グループを表示させたくない場合は、何も追加しないでください。  
  
 Web リソースや外部 URL へリンクを追加するには、**挿入**タブの**コントロール**グループで**ナビゲーション リンク**ボタンを使用します。  
 
 ![ナビゲーション リンク](media/navigation-link.png)
 
<a name="BKMK_NavigationLinkProperties"></a>   
### <a name="navigation-link-properties"></a>ナビゲーション リンクのプロパティ  
 ナビゲーション リンクには、次のプロパティがあります。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|名前|**必須**: ラベルとして表示するテキストです。|  
|アイコン|32x32 ピクセルの Web リソースを使用します。 透明なバックグラウンドの PNG イメージの使用をお勧めします。|  
|Web リソース|フォームのメイン ウィンドウに表示する Web リソースを指定します。|  
|外部 URL|フォームのメイン ウィンドウに表示するページのURLを指定します。|  

<a name="BKMK_PrivacyNotices"></a>   

## <a name="privacy-notices"></a>プライバシーに関する声明  
 [!INCLUDE[cc_privacy_crm_website_preview_control](../../includes/cc-privacy-crm-website-preview-control.md)]    
  
 [!INCLUDE[cc_privacy_multimedia_control](../../includes/cc-privacy-multimedia-control.md)]  

## <a name="next-steps"></a>次のステップ

[フォーム エディターのユーザー インターフェイスの概要](form-editor-user-interface-legacy.md)

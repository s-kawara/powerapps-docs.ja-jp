---
title: PowerApps でモデル駆動型アプリ内のナビゲーションを変更する | MicrosoftDocs
description: フォーム内のナビゲーションを変更する方法について説明します
ms.custom: ''
ms.date: 06/06/2018
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
ms.assetid: 4c379202-9f0e-4003-a49c-efff53e7f79f
caps.latest.revision: 63
ms.author: matp
manager: kvivek
ms.openlocfilehash: 5a8156875f669854a4ba4649e50a23e340f3ceff
ms.sourcegitcommit: aba996b1773ecdf62758e06b34eaf57bede29e08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/08/2018
ms.locfileid: "39690054"
---
# <a name="change-navigation-within-a-model-driven-app-form"></a>モデル駆動型アプリ内のナビゲーションを変更する

 フォーム内を移動することで、アプリ ユーザーは関連レコードの一覧を表示できます。 各エンティティ リレーションシップには、その表示を制御するプロパティがあります。 詳細: [Navigation pane item for primary entity](../common-data-service/create-edit-1n-relationships-solution-explorer.md#navigation-pane-item-for-primary-entity) (プライマリ エンティティのナビゲーション ウィンドウ項目)  
  
 表示するように構成されるエンティティ リレーションシップはフォーム エディター内でオーバーライドできます。 フォーム ナビゲーション経由で Web リソースやその他の Web サイトを表示するためのナビゲーション リンクを含めることもできます。  
  
 詳しい手順については、「[Create and edit entity relationships for Common Data Service for Apps](../common-data-service/create-edit-entity-relationships.md)」 (Common Data Service for Apps のエンティティ リレーションシップの作成と編集) を参照してください。  
  
 ナビゲーションの編集を有効にするには、フォーム デザイナーの **[ホーム]** タブにある **[選択]** グループから **[ナビゲーション]** をまず選択する必要があります。  
 
 ![ナビゲーション コマンド](media/navigation-command.png)
 
 右側のウィンドウでは、**[関連付けエクスプローラー]** から、1:N (一対多) リレーションシップまたは N:N (多対多) リレーションシップのフィルターを適用したり、利用できるリレーションシップをすべて表示したりできます。 **[未使用の関連付けのみ表示する]** チェックボックスは選択された状態になっており、解除できません。 そのため、各リレーションシップを 1 回だけ追加できます。  
  
 ![関連付けエクスプローラー](media/relationship-explorer.png)

 **[関連付けエクスプローラー]** からリレーションシップを追加するには、リレーションシップをダブルクリックします。ナビゲーション領域で現在選択されているリレーションシップの下に追加されます。 ナビゲーション領域でリレーションシップをダブルクリックしてください。**[表示]** タブのラベルは変更できます。**[名前]** タブでは、リレーションシップに関する情報を確認できます。 エンティティの定義を開くには、**[編集]** ボタンを使用します。  
  
 ナビゲーション領域には 5 つのグループがあります。 ドラッグして位置を変更したり、ダブルクリックしてラベルを変更したりできますが、削除することはできません。 これらのグループは、グループ内に構成要素があるときにのみ表示されます。 そのため、グループを表示しない場合、それに何も追加しないでください。  
  
 **[挿入]** タブの **[コントロール]** グループの **[ナビゲーション リンク]** ボタンを使用し、Web リソースまたは外部 URL にリンクを追加します。  
 
 ![ナビゲーション リンク](media/navigation-link.png)
 
<a name="BKMK_NavigationLinkProperties"></a>   
### <a name="navigation-link-properties"></a>ナビゲーション リンクのプロパティ  
 ナビゲーション リンクには、次のプロパティがあります。  
  
|プロパティ|説明|  
|--------------|-----------------|  
|名前|**必須**: ラベルとして表示するテキスト。|  
|アイコン|32 x 32 ピクセルの Web リソースを使用します。 背景が透明の PNG 画像を使用することをお勧めします。|  
|Web リソース|フォームのメイン ウィンドウに表示する Web リソースを指定します。|  
|外部 URL|フォームのメイン ウィンドウに表示するページの URL を指定します。|  

<a name="BKMK_PrivacyNotices"></a>   

## <a name="privacy-notices"></a>プライバシーに関する声明  
 [!INCLUDE[cc_privacy_crm_website_preview_control](../../includes/cc-privacy-crm-website-preview-control.md)]    
  
 [!INCLUDE[cc_privacy_multimedia_control](../../includes/cc-privacy-multimedia-control.md)]  

## <a name="next-steps"></a>次の手順

[フォーム エディターのユーザー インターフェイスの概要](form-editor-user-interface-legacy.md)
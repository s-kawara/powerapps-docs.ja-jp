---
title: PowerAppsでエンティティを編集する| MicrosoftDocs
description: エンティティが編集可能なさまざまな方法を説明する
ms.custom: ''
ms.date: 05/15/2018
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
ms.assetid: 8b00780c-74f0-4e3a-b570-b9289d0d5383
caps.latest.revision: 41
ms.author: matp
manager: kvivek
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="edit-an-entity"></a>エンティティの編集

作成するユーザー定義エンティティはどれでも編集できます。 標準エンティティまたは管理ユーザー定義エンティティには、加えられる変更に制限があります。  
  
> [!NOTE]
> **標準** エンティティは、**システム** または **ユーザー定義** エンティティではない環境に含まれる共通エンティティです。 *管理ユーザー定義エンティティ*は、管理ソリューションのインポートによってシステムに追加されているエンティティです。 これらのエンティティを編集できる程度は、各エンティティに設定されている管理プロパティによって決まります。 編集できないすべてのプロパティは無効になります。 

デザイナーを使用してエンティティを編集する方法は 2 つあります。

|デザイナー|説明|
|--|--|
|[PowerApps ポータル](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)|簡単な優れたエクスペリエンスを提供しますが、一部の特殊な設定は使用できません。|
|ソリューション エクスプローラー|簡単ではありませんが、一般的な要件が少ない割に柔軟性が高くなっています。|

PowerApps ポータルとソリューション エクスプローラーの両方で、以下を実行できます。

- **エンティティ フィールドを編集する**。 詳細情報: [アプリ用 Common Data Service のフィールドの作成および編集](create-edit-fields.md)
  
- **エンティティ関係を編集する**。 詳細情報: [エンティティ間の関連付けの作成と編集](create-edit-entity-relationships.md)

- **キー**。 [レコードを参照する代替キーの定義](define-alternate-keys-reference-records.md)
  
また、エンティティをサポートするレコードを変更することもできます。  

- **業務ルール**。 詳細:[フォームにロジックを適用するために業務ルールおよびビジネス レコメンデーションを作成する](../model-driven-apps/create-business-rules-recommendations-apply-logic-form.md)

- **ビュー**。 詳細: [ビューの作成または編集](../model-driven-apps/create-edit-views.md)
  
- **フォーム**。 詳細: [フォームの作成および設計](../model-driven-apps/create-design-forms.md)

- **ダッシュボード**:  詳細: [ダッシュボードの作成または編集](../model-driven-apps/create-edit-dashboards.md)

- **グラフ**。 [システム グラフの作成または編集](../model-driven-apps/create-edit-system-chart.md)

## <a name="edit-using-powerapps-portal-designer"></a>PowerApps ポータル デザイナーを使用した編集

PowerApps ポータル デザイナー内には、編集できるプロパティが 3 つしかありません。
 - 表示名
 - 複数形の表示名
 - 説明

デザイナーで、編集するエンティティを選択し、クリックしてエンティティ デザイナーを開きます。 エンティティ プロパティを変更するには、以下に示すように **構成** コマンドをクリックして **エンティティの編集** を表示します。

![エンティティ プロパティの編集](media/edit-entity-properties-powerapps-portal-designer.png)

> [!NOTE]
>  多くの標準エンティティの名前は、アプリケーションの他のテキストで使用されている可能性もあります。 この名前が使用されていたテキストを見つけて変更するには、「[標準エンティティ メッセージの編集](edit-system-entity-messages.md)」を参照してください。

エンティティ オプションにそれ以外の変更を加える場合、ソリューション エクスプローラーを使用してエンティティを編集する必要があります。

## <a name="edit-using-solution-explorer"></a>ソリューション エクスプローラーを使用した編集

ソリューション エクスプローラーを使用してエンティティを編集する場合、エンティティを追加するアンマネージド ソリューションを見つける必要があります。

[!INCLUDE [cc_navigate-solution-from-powerapps-portal](../../includes/cc_navigate-solution-from-powerapps-portal.md)]
  
<a name="BKMK_ChangeEntityName"></a> 
  
## <a name="change-the-name-of-an-entity"></a>エンティティ名の変更  

アプリケーションでエンティティの名前を変更するには、**表示名**と**複数名**プロパティを使用します。 

> [!NOTE]
>  多くの標準エンティティの名前は、アプリケーションの他のテキストで使用されている可能性もあります。 この名前が使用されていたテキストを見つけて変更するには、「[標準エンティティ メッセージの編集](edit-system-entity-messages.md)」を参照してください。
  
<a name="BKMK_ChangeEntityIcon"></a>   

###  <a name="change-the-icons-used-for-custom-entities"></a>ユーザー定義エンティティで使用されるアイコンの変更  

既定では、Web アプリケーションのすべてのユーザー定義エンティティは同じアイコンを使用します。 カスタム エンティティに必要なアイコンのイメージ Web リソースを作成できます。 詳細情報:  [カスタム エンティティのアイコンを変更する](../model-driven-apps/change-custom-entity-icons.md).  
  
<a name="BKMK_EnableOptions"></a>  
 
###  <a name="entity-options-that-can-only-be-enabled"></a>唯一有効にすることができるエンティティ オプション  

次の表に、エンティティに対して有効にすることができるオプションを表示しますが、これらの項目は有効にされると、その後、無効にすることはできません。  

[!INCLUDE [cc_entity-set-once-options-table](../../includes/cc_entity-set-once-options-table.md)] 
  
<a name="BKMK_EnableDisableOptions"></a>  
 
###  <a name="enable-or-disable-entity-options"></a>エンティティを有効化または無効化  

次の表に、いつでも有効または無効にできるエンティティのオプションを示します。  

[!INCLUDE [cc_entity-changeable-options-table](../../includes/cc_entity-changeable-options-table.md)] 

### <a name="see-also"></a>関連項目

[エンティティの作成](create-edit-entities.md)<br />
[ソリューション エクスプローラーを使用してエンティティを作成および編集する](create-edit-entities-solution-explorer.md)

---
title: PowerApps ポータルを使用したエンティティの作成および編集 | MicrosoftDocs
description: PowerApps ポータルを使用してエンティティを作成および編集する方法について説明します。
ms.custom: ''
ms.date: 05/30/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
author: Mattp123
ms.assetid: fa04f99d-a5f9-48cb-8bfb-f0f50718ccee
caps.latest.revision: 41
ms.author: matp
manager: kvivek
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---

# <a name="create-and-edit-entities-using-powerapps-portal"></a>PowerApps ポータルを使用してエンティティを作成および編集する

[PowerApps ポータル](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)では、アプリ用 Common Data Service のエンティティを簡単に作成および編集できます。

ポータルでは一般的なオプションのほどんとを構成できますが、特定のオプションはソリューション エクスプローラーを使用してのみ設定できます。 詳細: 
- [アプリ用 Common Data Service でのエンティティの作成および編集](create-edit-entities.md)
- [ソリューション エクスプローラーを使用してエンティティを作成および編集する](create-edit-entities-solution-explorer.md)

## <a name="view-entities"></a>エンティティの表示

1. [PowerApps ポータル](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc)から、**モデル駆動型**または**キャンバス**設計モードを選択します。
2. **データ** > **エンティティ** を選択します。

![エンティティの表示](media/view-entities-portal.png)

一覧の次のビューを使用して表示されたエンティティをフィルター処理できます。 

![エンティティ ビュー](media/entity-views-portal.png)

 |ビュー|説明|
 |--|--|
 |**すべて**| すべてのエンティティを表示します|
 |**ユーザー定義**|ユーザー定義エンティティのみ表示します|
 |**既定**|標準エンティティのみ表示します |

それらに適用される **タグ** によってエンティティをグループ化するために **グループ** を選択することもできます。

## <a name="create-an-entity"></a>エンティティの作成

[エンティティを表示](#view-entities)しながら、メニュー バーで **新しいエンティティ** を選択します。 これには、[新しいエンティティ] パネルが開きます。

![新しいエンティティ パネル](media/new-entity-panel.png)

以下のフィールドにデータを入力

|フィールド|説明|
|--|--|
|**表示名です**|これは、アプリに表示されるエンティティの単数形の名前です。 これは後で変更できます。|
|**複数形の表示名**|これは、アプリに表示されるエンティティの複数形の名前です。 これは後で変更できます。|
|**名前**|このフィールドは、ユーザーが入力する**表示名**に基づいて事前設定されます。 これには、CDS ソリューション発行者のカスタマイズ接頭辞が含まれます。 エンティティが保存されたら、これを変更できません。|
|**説明**|エンティティの目的でわかりやすい説明を入力してください。|

**次へ**を選択して続行します。**新しいエンティティ** ウィンドウが閉じてフィールドの一覧が表示されます。

**プライマリ名** フィールドは、この時点で表示される唯一のフィールドです。 フィールドの **表示名** または **名前** を変更する場合は、**プライマリ名** フィールドを選択して編集します。 既定値は、以下に表示されます。

![[プライマリ名] パネル](media/primary-name-panel.png)

エンティティを作成するか、エンティティの編集を続けるには、**エンティティの保存** を選択します。

![エンティティの保存](media/save-entity-portal.png)

## <a name="edit-an-entity"></a>エンティティの編集

[エンティティを表示](#view-entities)しているときに、編集するエンティティを選択します。

エンティティの**表示名**、**複数形の表示名**、**説明** を編集する場合、メニューから [設定] を選択します。

![エンティティ設定](media/entity-settings-portal.png)

他の項目については、タブから選択します。

### <a name="fields"></a>フィールド

「[フィールドの作成および編集](create-edit-fields.md)」を参照してください。

### <a name="relationships"></a>関係

「[エンティティ間の関連付けの作成と編集](create-edit-entity-relationships.md)」を参照

### <a name="business-rules"></a>業務ルール

「[フォームにロジックを適用するために業務ルールおよびビジネス レコメンデーションを作成する](../model-driven-apps/create-business-rules-recommendations-apply-logic-form.md)」を参照

### <a name="views"></a>[ビュー]

「[ビューの作成または編集](../model-driven-apps/create-edit-views.md)」を参照

### <a name="forms"></a>フォーム

「[フォームの作成および設計](../model-driven-apps/create-design-forms.md)」を参照

### <a name="dashboards"></a>ダッシュボード

「[ダッシュボードの作成または編集](../model-driven-apps/create-edit-dashboards.md)」を参照

### <a name="charts"></a>グラフ

「[システム グラフの作成](../model-driven-apps/create-edit-system-chart.md)」を参照

### <a name="keys"></a>キー

「[レコードを参照する代替キーの定義](define-alternate-keys-reference-records.md)」を参照

### <a name="data"></a>データ

エンティティ内のデータを表示します。
エンティティの使用できるビューから選択したり、すべてのフィールドを表示するには、**ビューの選択** メニューを使用します。

![ビューの選択](media/entity-data-select-view.png)

そのほかのデータを表示するには、フォームの下部の **次のページ** と **前のページ** コマンドを使用します。

## <a name="delete-an-entity"></a>エンティティの削除

システム管理者のセキュリティ ロールを持つユーザーとして、管理ソリューションの一部でないユーザー定義エンティティを削除できます。  
  
> [!IMPORTANT]
>  ユーザー定義エンティティを削除すると、そのエンティティのデータを保存しているデータベース テーブルが削除され、それらのテーブルに含まれるすべてのデータが失われます。 ユーザー定義エンティティと上位下位の関連付けのある関連レコードも削除されます。 上位下位の関連付けの詳細については、「[エンティティ間の関連付けの作成と編集](create-edit-entity-relationships.md)」を参照してください。  
  
> [!NOTE]
> 削除されたエンティティからのデータを回復する唯一の方法は、エンティティが削除される前の時点からデータベースを復元します。 詳細については、「[インスタンスのバックアップと復元](/dynamics365/customer-engagement/admin/backup-restore-instances)」を参照してください。

[エンティティを表示](#view-entities)しながら、エンティティを選択し、メニューまたはコンテキスト メニューから **エンティティの削除** を選択します。

![PowerApps ポータルを使用してエンティティを削除する](media/delete-entity-powerapps-portal.png)

削除を防止する依存関係がエンティティにする場合は、エラー メッセージが表示されます。 依存関係を特定および削除するには、ソリューション エクスプローラーを使用する必要があります。 詳細については、「[エンティティの依存関係の特定](create-edit-entities-solution-explorer.md#identify-entity-dependencies)」を参照してください

### <a name="see-also"></a>関連項目

[アプリ用 Common Data Service でのエンティティの作成および編集](create-edit-entities.md)<br />
[ソリューション エクスプローラーを使用してエンティティを作成および編集する](create-edit-entities-solution-explorer.md)



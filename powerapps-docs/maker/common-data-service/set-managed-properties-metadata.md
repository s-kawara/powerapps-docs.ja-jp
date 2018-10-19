---
title: アプリ用 Common Data Service メタデータで管理プロパティを設定する | MicrosoftDocs
description: ソリューションでメタデータ アイテムの管理プロパティを設定する方法を説明します
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
  - powerapps
author: Mattp123
ms.assetid: edaa7d4a-a95f-4d66-a9d9-2ad6051332f7
caps.latest.revision: 41
ms.author: matp
manager: kvivek
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---
# <a name="set-managed-properties-in-common-data-service-for-apps-metadata"></a>アプリ用 Common Data Service メタデータで管理プロパティを設定する 

管理プロパティは、管理ソリューションを使用してメタデータを含め、別の環境にインポートするときにのみ適用されます。 これらの設定により、ソリューション作成者は、管理ソリューションをインストールするユーザーに許可するカスタマイズのレベルをある程度制御することができます。 

> [!TIP]
> 一般に、ビジネス データに適したソリューションでメタデータを拡張できるようにすることをお勧めします。 これにより、標準エンティティでできるのと同じ方法で、ニーズに合わせてソリューションをカスタマイズできるようになります。
>
>ソリューションをサポートする機能を提供するが、ビジネス データが含まれていないメタデータについては、カスタマイズが許可される内容を制限すすることをお勧めします。

管理プロパティを設定するには、ソリューション エクスプローラーを使用する必要があります。

[!INCLUDE [cc_navigate-solution-from-powerapps-portal](../../includes/cc_navigate-solution-from-powerapps-portal.md)]

## <a name="entity-managed-properties"></a>エンティティ管理プロパティ

[エンティティを表示](create-edit-entities-solution-explorer.md#view-entities)しながら、エンティティを選択し、メニュー バーで **管理プロパティ** を選択できます。  これは、**管理プロパティ** ダイアログを開きます。

![エンティティの管理プロパティを設定する](media/set-managed-properties.png)
  
エンティティには、他の種類のソリューション コンポーネントよりも多くの管理プロパティがあります。 エンティティがカスタマイズ可能な場合、以下のオプションを設定できます。  

|オプション|説明|
|--|--|
|**カスタマイズ可能** |他のすべてのオプションを制御します。 このオプションが `False` の場合、そのほかの設定は一切適用されません。 これが `True` の場合、そのほかのカスタマイズ オプションを指定できます。 `False` の場合は、他のすべてのオプションを false に設定することに相当します。|
|**修正可能な表示名**|エンティティの表示名を変更できるかどうか。|
|**追加プロパティを変更可能** |他のオプションによりカバーされていないものすべてが適用されます。|
|**新しいフォームを作成可能**|エンティティに新しいフォームを作成できるかどうかを示します。|
|**新しいグラフを作成可能**|エンティティに新しいグラフを作成できるかどうかを示します。|
|**新しいビューを作成可能** |エンティティで新しいビューを作成できるかどうかを示します。|
|**階層関連付けを変更できる**|階層の関連付けの設定を変更できるかどうか。 詳細情報: [階層的に関連するデータを定義およびクエリする](define-query-hierarchical-data.md)|
|**変更履歴を有効化できる** |エンティティの **変更の追跡** プロパティを変更できるかどうか。|
|**外部検索インデックスとの同期の有効化が可能** |関連性検索が有効になれるようにエンティティを構成できるかどうか。 詳細情報: [関連性検索を構成して検索結果および検索パフォーマンスを向上させる](/dynamics365/customer-engagement/admin/configure-relevance-search-organization) |

## <a name="field-managed-properties"></a>フィールド管理プロパティ

フィールドを編集する方法については、「[PowerApps ソリューション エクスプローラーを使用したアプリ用 Common Data Service のフィールドの作成および編集](create-edit-field-solution-explorer.md)」を参照してください。

[フィールドを表示](create-edit-field-solution-explorer.md#view-fields)しながら、カスタム フィールドをアンマネージド ソリューションから選択し、メニュー バーで **その他の操作** >  **管理プロパティ** を選択します。

![フィールド管理プロパティを表示する](media/view-field-managed-properties-solution-explorer.png)  
  
これは、**管理プロパティ** ダイアログ ボックスを開きます。

![フィールド管理プロパティを設定する](media/set-field-managed-property.png)

**カスタマイズ可能**オプションは、そのほかのすべてのオプションを制御します。 このオプションが **False** の場合、そのほかの設定は一切適用されません。 これが **True** の場合、そのほかのカスタマイズ オプションを指定できます。  
  
フィールドがカスタマイズ可能な場合、**True** または **False** へ以下のオプションを設定できます。  
  
- **修正可能な表示名**
- **入力要求レベルを変更可能** 
- **追加プロパティを変更可能** : このプロパティは、特定の管理プロパティを持たない他のカスタマイズも制御します。

個別の全オプションを **False** に設定することは、**カスタマイズ可能** を **False** に設定することと同等です。  

変更を適用し、**設定** をクリックしてダイアログ ボックスを閉じます。

> [!NOTE]
> このフィールドが **日時** フィールドの場合、追加の **日時の動作を変更可能** プロパティを使用できます。 詳細: [日時フィールドの動作と形式](behavior-format-date-time-field.md)

## <a name="relationship-managed-properties"></a>関連付け管理プロパティ

エンティティの関連付けを表示しながら、関連付けをアンマネージド ソリューションから選択し、メニュー バーで **その他の操作** > **管理プロパティ** を選択します。
  
関連付けで管理プロパティだけが**カスタマイズ可能**です。 この単一の設定は、エンティティ関係に加えられるすべての変更を制御します。 


### <a name="see-also"></a>関連項目

[マネージド プロパティ](solutions-overview.md#managed-properties)<br />
[ソリューション エクスプローラーを使用してエンティティを作成および編集する](create-edit-entities-solution-explorer.md)<br />
[PowerApps ソリューション エクスプローラーを使用したアプリ用 Common Data Service のフィールドの作成および編集](create-edit-field-solution-explorer.md)<br />
[ソリューション エクスプローラーを使用して 1:N (1 対多) または N:1 (多対 1) のエンティティ関連付けを作成および編集する](create-edit-1n-relationships-solution-explorer.md)<br />
[ソリューション エクスプローラーを使用してアプリ用 Common Data Service で N:N (多対多) のエンティティの関連付けを作成する](create-edit-nn-relationships-solution-explorer.md)

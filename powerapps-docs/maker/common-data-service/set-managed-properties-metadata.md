---
title: アプリ用 Common Data Service メタデータで管理プロパティを設定する | MicrosoftDocs
description: ソリューション内のメタデータ項目の管理プロパティを設定する方法について説明します
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
ms.openlocfilehash: 46727f5a46e3fd518da52fac7d08a6e43992c00d
ms.sourcegitcommit: aba996b1773ecdf62758e06b34eaf57bede29e08
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/08/2018
ms.locfileid: "39692654"
---
# <a name="set-managed-properties-in-common-data-service-for-apps-metadata"></a>アプリ用 Common Data Service メタデータで管理プロパティを設定する 

管理プロパティは、マネージド ソリューションにメタデータを含めて別の環境にインポートする場合にのみ適用されます。 このような設定を使用してソリューションを作成すると、マネージド ソリューションをインストールするユーザーを許可するカスタマイズのレベルをある程度制御することができます。 

> [!TIP]
> 一般的に、ビジネス データを使用するメタデータをソリューション内で拡張できるようにすることをお勧めします。 こうすることで、標準エンティティの場合と同じ方法でニーズに合わせてソリューションを調整できます。
>
>ソリューションをサポートする機能を提供し、ビジネス データを含まないメタデータの場合、許可するカスタマイズを制限することをお勧めします。

管理プロパティの設定には、ソリューション エクスプローラーを使用する必要があります。

[!INCLUDE [cc_navigate-solution-from-powerapps-portal](../../includes/cc_navigate-solution-from-powerapps-portal.md)]

## <a name="entity-managed-properties"></a>エンティティの管理プロパティ

[エンティティの表示](create-edit-entities-solution-explorer.md#view-entities)中にエンティティを選択し、メニュー バーの **[管理プロパティ]** を選択します。  **[管理プロパティの設定]** ダイアログが開きます。

![エンティティの管理プロパティを設定する](media/set-managed-properties.png)
  
エンティティには、他の種類のソリューション コンポーネントよりも多くの管理プロパティがあります。 エンティティがカスタマイズ可能な場合は、次のオプションを設定できます。  

|オプション|説明|
|--|--|
|**カスタマイズ可能** |その他すべてのオプションを制御します。 このオプションが [`False`] の場合、他の設定は適用されません。 [`True`] の場合、他のカスタマイズ オプションを指定できます。 [`False`] の場合、その他すべてのオプションを [False] に設定した場合と同じです。|
|**修正可能な表示名**|エンティティの表示名を変更できるかどうかを指定します。|
|**追加プロパティを変更できる** |他のオプションの対象ではないものに適用されます。|
|**新しいフォームを作成可能**|エンティティの新しいフォームを作成できるかどうかを指定します。|
|**新しいグラフを作成可能**|エンティティの新しいグラフを作成できるかどうかを指定します。|
|**新しいビューを作成可能** |エンティティの新しいビューを作成できるかどうかを指定します。|
|**階層関連付けを変更できる**|階層関連付け設定を変更できるかどうかを指定します。 詳細情報: 「[Define and query hierarchically related data](define-query-hierarchical-data.md)」(階層的な関連データの定義とクエリを行う)|
|**変更履歴を有効化できる** |エンティティの **[変更履歴]** プロパティを変更できるかどうかを示します。|
|**外部検索インデックスとの同期の有効化が可能** |関連性検索を有効にするようにエンティティを構成できるかどうかを指定します。 詳細情報: 「[関連性検索を構成して検索結果および検索パフォーマンスを向上させる](/dynamics365/customer-engagement/admin/configure-relevance-search-organization)」 |

## <a name="field-managed-properties"></a>フィールドの管理プロパティ

フィールドの編集方法については、「[Create and edit fields for Common Data Service for Apps using PowerApps solution explorer](create-edit-field-solution-explorer.md)」(PowerApps ソリューション エクスプローラーを使用したアプリ用 Common Data Service のフィールドの作成と編集)

[フィールドの表示](create-edit-field-solution-explorer.md#view-fields)中にアンマネージド ソリューションからカスタム フィールドを選択し、メニュー バーの **[その他の操作]** >  **[管理プロパティ]** を選択します。

![フィールドの管理プロパティを表示する](media/view-field-managed-properties-solution-explorer.png)  
  
**[管理プロパティの設定]** ダイアログ ボックスが開きます。

![フィールドの管理プロパティを設定する](media/set-field-managed-property.png)

**[カスタマイズ可能]** オプションは、その他すべてのオプションを制御します。 このオプションが **[False]** の場合、他の設定は適用されません。 **[True]** の場合、他のカスタマイズ オプションを指定できます。  
  
フィールドがカスタマイズ可能な場合は、次のオプションを **[True]** または **[False]** に設定します。  
  
- **修正可能な表示名**
- **入力要求レベルを変更可能** 
- **追加プロパティを変更できる**: このプロパティは、特定の管理プロパティを持たない他のすべてのカスタマイズを制御します。

すべての個々のオプションを **[False]** に設定することは、**[カスタマイズ可能]** を **[False]** に設定することと同じです。  

選択内容を適用して **[設定]** をクリックすると、ダイアログ ボックスが閉じます。

> [!NOTE]
> このフィールドが **[日付と時間]** フィールドの場合、追加の **[日時の動作を変更可能]** プロパティを使用できるようになります。 詳細情報: 「[Behavior and format of the Date and Time field](behavior-format-date-time-field.md)」([日付と時間] フィールドの動作と形式)

## <a name="relationship-managed-properties"></a>関係の管理プロパティ

エンティティ関係を表示するときに、アンマネージド ソリューションから関係を選択し、メニュー バーの **[その他の操作]** > **[管理プロパティ]** を選択します。
  
関係については、管理プロパティのみが **[カスタマイズ可能]** です。 この 1 つの設定で、エンティティ関係に加えることができるすべての変更が制御されます。 


### <a name="see-also"></a>関連項目

[管理プロパティ](solutions-overview.md#managed-properties)<br />
[ソリューション エクスプローラーを使用したエンティティの作成と編集](create-edit-entities-solution-explorer.md)<br />
[PowerApps ソリューション エクスプローラーを使用したアプリ用 Common Data Service のフィールドの作成と編集](create-edit-field-solution-explorer.md)<br />
[ソリューション エクスプローラーを使用して 1:N (1 対多) または N:1 (多対 1) のエンティティ関係を作成および編集する](create-edit-1n-relationships-solution-explorer.md)<br />
[ソリューション エクスプローラーを使用してアプリ用 Common Data Service に N:N (多対多) のエンティティ関係を作成する](create-edit-nn-relationships-solution-explorer.md)
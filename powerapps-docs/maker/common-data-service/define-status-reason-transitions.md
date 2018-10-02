---
title: PowerApps でステータスの移行を定義する | MicrosoftDocs
description: ステータスの移行を定義する方法を説明します
ms.custom: ''
ms.date: 05/25/2018
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
ms.assetid: dbc4f436-0b23-42f9-8079-b0de482aaebe
caps.latest.revision: 11
ms.author: matp
manager: kvivek
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---

# <a name="define-status-reason-transitions-for-the-case-or-custom-entities"></a>サポート案件またはユーザー定義エンティティのステータス遷移の定義

インシデント (**サポート案件**) エンティティまたはユーザー定義エンティティのステータス遷移を指定することができます。

> [!NOTE]
> インシデント (サポート案件) エンティティは、Apps 環境用 Common Data Service には含まれていませんが、[Dynamics 365 for Customer Service](https://dynamics.microsoft.com/customer-service/) に使用され、[共通データ モデル](https://github.com/Microsoft/CDM/blob/master/schemaDocuments/core/applicationCommon/foundationCommon/crmCommon/service/Incident.cdm.json) 内で定義されます。
  
ステータスの遷移は、フィルターの追加のオプション レベルで、各ステータスのステータス値を何に変更するかを定義します。 有効なステータス値の組み合わせが多数存在する場合に、有効なオプションの限定した一覧を定義すると、レコードの正確な次のステータスを選択することが容易になります。  
  
<a name="BKMK_StatusAndStatusReasons"></a>

## <a name="what-is-the-connection-between-status-and-status-reason-fields"></a>状態とステータスのフィールド間の接続とは何ですか。  

別の状態値があるエンティティには、このデータを取得する次の 2 つのフィールドがあります。  
  
|表示名|説明|  
|------------------|-----------------|  
|**ステータス**|レコードの状態を表します。 通常**アクティブ**または**非アクティブ**。 新しい状態オプションを追加することはできません。|  
|**ステータス**|特定の状態にリンクされている理由を表します。 各状態は、少なくとも 1 つの可能なステータスを持っている必要があります。 追加のステータス オプションを追加できます。|  
  
フィールドのメタデータは、特定の状態に対してどの状態値が有効であるかを定義します。 たとえば、インシデント (**サポート案件**) エンティティの場合、既定の状態およびステータス オプションは次の通りです。  
  
|ステータス|ステータス|  
|------------|-------------------|  
|**アクティブ**|<li>**処理中**</li><li>**保留中**</li><li>**詳細待ち**</li><li>**調査中**</li>| 
|**解決**|<li>**問題解決済み**</li><li>**情報提供済み**</li>|
|**取り消されました**|<li>**取り消されました**</li><li>**統合**</li>|
  
  
<a name="BKMK_EditStatusReasonTransitions"></a>   

## <a name="edit-status-reason-transitions"></a>ステータスの遷移の編集
 
サポート案件エンティティとユーザー定義エンティティのステータス フィールド オプションを変更して、ユーザーが選択できる他のステータス オプションを定義できます。 唯一の制限は、アクティブ状態の各ステータス オプションが、非アクティブな状態への少なくとも 1 つのパスを許可する必要があるということです。 そうしないと、サポート案件を解決またはキャンセルすることができない条件を作成することになります。  

> [!NOTE]
> ステータスの遷移を編集するには、ソリューション エクスプローラーを使用する必要があります。 フィールドの編集方法の詳細は、[PowerApps ソリューション エクスプローラーを使用してアプリ用 Common Data Service のフィールドを作成および編集する](create-edit-field-solution-explorer.md) を参照してください。
  
 ステータスのフィールドを編集する際、**ステータスの遷移の編集**ボタンはメニューにあります。 

![ステータスの移行コマンドの編集](media/status-reason-transitions-command.png)

このボタンをクリックすると、**ステータスの移行**ダイアログに**ステータスの遷移を有効にする**を選択するオプションが提供されます。 このオプションが選択されている場合は、各ステータスに許可される*その他*ステータスの値を定義する必要があります。 適用されたフィルターを削除するには、**ステータスの遷移を有効にする**の選択をはずします。 定義済みの遷移は、保持されますが適用されません。  
  
スクリーン ショットは、次の条件を満たしている例を示しています。 
 
- サポート案件はいつでも統合できます。 ステータスの遷移がそれを許可していない場合は、サポート案件を結合することはできません。  
- アクティブなサポート案件をいつでもキャンセルできます。  
- 解決済みまたはキャンセルされたサポート案件は、再アクティブ化することはできません。  
- すべてのサポート案件は、解決する前に、**進行中** > **保留中** > **詳細待ち** > **調査中**の段階を経る必要があります。 この構成では、サポート案件にこれ以前の状態を設定できませんでした。  
  > [!NOTE]
  >  これは、実際の作業には良い例ではありませんが、状態の段階がステータスの遷移を通してどのように実行できるかを示しています。  
  
 ![サポート案件のステータスの遷移例](media/status-reason-transitions-example.PNG)  
  
### <a name="see-also"></a>関連項目  

[PowerApps ソリューション エクスプローラーを使用したアプリ用 Common Data Service のフィールドの作成および編集](create-edit-field-solution-explorer.md)<br />
[エンティティ メタデータ > エンティティ状態](/powerapps/developer/common-data-service/entity-metadata#entity-states)<br />
[カスタムの状態モデルの遷移の定義](/dynamics365/customer-engagement/developer/define-custom-state-model-transitions)


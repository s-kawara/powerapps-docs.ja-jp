---
title: Dynamics 365 ライセンスを必要とする制限付きのエンティティ | Microsoft Docs
description: Dynamics 365 ライセンスを必要とする Common Data Service (CDS) for Apps の制限付きエンティティのリストです。
author: clwesene
manager: kfile
ms.service: powerapps
ms.component: cds
ms.topic: reference
ms.date: 05/01/2018
ms.author: clwesene
ms.openlocfilehash: 79b6e386154b15ae6c625afbebbed18a8a86c420
ms.sourcegitcommit: b3b6118790d6b7b4285dbcb5736e55f6e450125c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2018
---
# <a name="restricted-entities-requiring-dynamics-365-licenses"></a>Dynamics 365 ライセンスを必要とする制限付きのエンティティ
アプリの作成者は、Common Data Service (CDS) for Apps 内で利用可能なほとんどのエンティティを使用して、PowerApps プラン 1 のライセンスのみを持つユーザーのアプリとフローを作成できます。 ただし、一部のエンティティには、アプリ ユーザーに PowerApps プラン 2 または Microsoft Flow プラン 2 のライセンスを求める複雑なビジネス ロジックが含まれています (詳細については、[エンティティのライセンス要件](data-platform-entity-licenses.md)に関するページを参照)。 Dynamics 365 製品に関連付けられているさらに小さなエンティティ セットでは、キャンバスおよびモデル駆動型のアプリ ユーザーは、エンティティ内のレコードを作成、更新、または削除する必要がある場合に、対応する Dynamics 365 製品のライセンスが求められます。 これらは*制限付き* エンティティと呼ばれます。

エンティティは、次の理由により Dynamics 365 ライセンスに制限される場合があります。

* エンティティは、通常、アプリケーションの外部では使用されない製品固有の構成を格納して維持するために使用されます。
* エンティティには、Dynamics 365 製品内で使用した場合に特定の方法でデータを作成して維持する高度なロジックが伴います。

アプリまたはフローでエンティティから情報を読み取るだけの場合、Dynamics 365 ライセンスは必要ありません。適切な PowerApps または Microsoft Flow のライセンスがあれば十分です。 

## <a name="restricted-entities-for-create-update-and-delete-operations"></a>作成、更新、削除操作の制限付きエンティティ
次の表に、制限付きエンティティと、エンティティ内に格納されているデータを作成、更新、または削除する PowerApps および Microsoft Flow のアプリ ユーザーの関連付けられている Dynamics 365 ライセンス要件の一覧を示します。 

|組織  |論理名  |必要なライセンス  |
|---------|---------|---------|
実際 |msdyn_actual |Dynamics 365 for Field Service <br> **または** Dynamics 365 for Project Service Automation<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
契約ビジネス プロセス |msdyn_bpf_baa0a411a239410cb8bded8b5fdd88e3 |Dynamics 365 for Field Service<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
予約仕訳帳 | msdyn_bookingjournal|Dynamics 365 for Field Service<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
予約セットアップ メタデータ | msdyn_bookingsetupmetadata|Dynamics 365 for Field Service <br> **または** Dynamics 365 for Project Service Automation<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
予約タイムスタンプ | msdyn_bookingtimestamp|Dynamics 365 for Field Service<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
作業指示ビジネス プロセスの場合 |msdyn_bpf_989e9b1857e24af18787d5143b67523b |Dynamics 365 for Field Service<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
Configuration |msdyn_configuration |Dynamics 365 for Field Service <br> **または** Dynamics 365 for Project Service Automation<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
権利 | entitlement | Dynamics 365 for Customer Service, Enterprise edition <br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
見積行|msdyn_estimateline|Dynamics 365 for Project Service Automation<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
見積もり|msdyn_estimate |Dynamics 365 for Project Service Automation<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
ファクト|msdyn_fact |Dynamics 365 for Project Service Automation<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
フィールド サービス設定 |msdyn_fieldservicesetting |Dynamics 365 for Field Service<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
フィールド サービス システム ジョブ |msdyn_fieldservicesystemjob |Dynamics 365 for Field Service<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
目標 | goal | Dynamics 365 for Sales Professional、 <br>**または** Dynamics 365 for Sales, Enterprise edition、 <br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
インシデント | incident | Dynamics 365 for Customer Service, Enterprise edition <br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
在庫仕訳帳 |msdyn_inventoryjournal |Dynamics 365 for Field Service<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
請求書プロセス |msdyn_bpf_d8f9dc7f099f44db9d641dd81fbd470d |Dynamics 365 for Project Service Automation<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
旅行 | journey | Dynamics 365 for Marketing <br> **または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
ナレッジ記事 | knowledgearticle | Dynamics 365 for Customer Service, Enterprise edition <br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
組織単位 |msdyn_organizationalunit |Dynamics 365 for Field Service <br> **または** Dynamics 365 for Project Service Automation<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
製品の在庫 |msdyn_productinventory |Dynamics 365 for Field Service<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
プロジェクト パラメーター|msdyn_projectparameter |Dynamics 365 for Project Service Automation<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
プロジェクト ステージ| msdyn_bpf_665e73aa18c247d886bfc50499c73b82|Dynamics 365 for Project Service Automation<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
プロジェクト タスクの依存関係|msdyn_projecttaskdependency |Dynamics 365 for Project Service Automation<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
プロジェクト タスク|msdyn_projecttask |Dynamics 365 for Project Service Automation<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
プロジェクト チーム メンバー|msdyn_projecteam |Dynamics 365 for Project Service Automation<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
注文書ビジネス プロセス | msdyn_bpf_2c5fe86acc8b414b8322ae571000c799|Dynamics 365 for Field Service<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
リソース割り当ての詳細 (非推奨)|msdyn_resourceassignmentdetail |Dynamics 365 for Project Service Automation<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
リソースの割り当て|msdyn_resourceassignment |Dynamics 365 for Project Service Automation<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
リソースの制限 (非推奨) |msdyn_workorderresourcerestriction | Dynamics 365 for Field Service<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
ルーティング規則セット | routingrule | Dynamics 365 for Customer Service, Enterprise edition <br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
スケジュール ボードの設定 |msdyn_scheduleboardsetting |Dynamics 365 for Field Service <br> **または** Dynamics 365 for Project Service Automation<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
スケジューリング パラメーター |msdyn_schedulingparameter |Dynamics 365 for Field Service <br> **または** Dynamics 365 for Project Service Automation<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
SLA| sla | Dynamics 365 for Customer Service, Enterprise edition <br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
システム ユーザー スケジューラの設定 |msdyn_systemuserschedulersetting|Dynamics 365 for Field Service <br> **または** Dynamics 365 for Project Service Automation<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
トランザクション接続|msdyn_transactionconnection |Dynamics 365 for Project Service Automation<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
トランザクション発生元|msdyn_transactionorigin |Dynamics 365 for Project Service Automation<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
トランザクションの種類|msdyn_transactiontype |Dynamics 365 for Project Service Automation<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
一意の番号|msdyn_uniquenumber |Dynamics 365 for Field Service<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
作業指示ビジネス プロセス |msdyn_bpf_d3d97bac8c294105840e99e37a9d1c39 |Dynamics 365 for Field Service<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン
作業指示の詳細生成キュー (非推奨)|msdyn_workorderdetailsgenerationqueue |Dynamics 365 for Field Service<br>**または** Dynamics 365 Customer Engagement プラン <br> **または** Dynamics 365 プラン

## <a name="licensing"></a>ライセンス
PowerApps および Dynamics 365 のライセンスの詳細については、「[ライセンスの概要](../../administrator/pricing-billing-skus.md)」ページを参照してください。


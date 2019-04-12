---
title: ユーザー アクセスの監査 (Common Data Service) | Microsoft Docs
description: ユーザー ID、アクセス時間、およびクライアントの種類を含むユーザー アクセスの監査機能のサポート。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: paulliew
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="audit-user-access"></a>ユーザー アクセスの監査

Common Data Service はユーザー アクセスの監査機能をサポートします。 記録される情報には、ユーザーが Common Data Service へのアクセスをいつ開始したか、アクセス元が Common Data Service の Web アプリケーションか、 か、Dynamics 365 for Outlook、または Web サービスへの SDK 呼び出しかが含まれます。  
  
## <a name="enable-user-access-auditing"></a>ユーザー アクセス監査の有効化  
 ユーザー アクセスの監査は、組織レベルで有効化されます。 ユーザー アクセス監査を有効化/無効化するには、対象組織のレコードを取得し、その組織の `Organization.IsUserAccessAuditEnabled` 属性を更新する必要があります。 組織に対するグローバル監査も、組織レコードの `Organization.IsAuditEnabled` 属性を `true` に設定して有効化する必要があります。 ユーザー アクセス元、例えば Web アプリケーション、Dynamics 365 for Outlook または SDK などを監査するには、アクセスしているエンティティで監査を有効にする必要があります。  
  
 ユーザー アクセス監査の頻度は、`Organization.UserAccessAuditingInterval` 属性を使用して読み取りまたは設定することができます。 既定の属性の値 4 は、4 時間ごとに、ユーザー アクセスが監査されることを示します。  
  
 組織およびエンティティの監査を有効にする方法の詳細については、「[監査のエンティティおよび属性の構成](configure-entities-attributes-auditing.md)」を参照してください。  
  
## <a name="filter-on-user-access-events"></a>ユーザー アクセス イベントのフィルタリング  
 ユーザー アクセスに関連する監査レコードを検索するには、コードによって組織の `Audit` レコードを取得し、`Audit.Action` の値でフィルタリングする必要があります。 サポートされている監査アクションを識別するため、`AuditAction` という列挙体が提供されています。 ユーザー アクセスに関連するアクションを、次の一覧に示します。  
  
-   `AuditAction.UserAccessviaWeb`  
  
-   `AuditAction.UserAccessviaWebServices`  
  
-   `AuditAction.UserAccessAuditStarted`  
  
-   `AuditAction.UserAccessAuditStopped`  
  
 `UserAccessviaWeb` は、Common Data Service の Web アプリケーションまたは Dynamics 365 for Outlook からのアクセスを示します。 `UserAccessviaWebServices` は SDK からの Web サービス要求を示します。 `AuditAction` 列挙体は、アプリケーションのプロジェクトに `OptionSets.cs` または `OptionSets.vb` を含めた場合に、コードで使用可能です。  
  
### <a name="see-also"></a>関連項目  
 [Dynamics 365 においてエンティティ データの変更を監査する](/dynamics365/customer-engagement/developer/audit-entity-data-changes)   
 [監査のエンティティおよび属性の構成](/dynamics365/customer-engagement/developer/configure-entities-attributes-auditing)     
 [サンプル: エンティティのデータ変更を監査する](/dynamics365/customer-engagement/developer/sample-audit-entity-data-changes)   
 [サンプル: ユーザー アクセスの監査](/dynamics365/customer-engagement/developer/sample-audit-user-access)

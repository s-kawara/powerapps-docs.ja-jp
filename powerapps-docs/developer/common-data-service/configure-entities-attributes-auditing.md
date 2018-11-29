---
title: 監査のエンティティおよび属性の構成 (アプリ用 Common Data Service) | Microsoft Docs
description: エンティティおよびそれらの属性の監査を有効および無効にするための構成要件について説明します。
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
# <a name="configure-entities-and-attributes-for-auditing"></a>監査のエンティティおよび属性の構成

監査は、組織、エンティティ、属性の 3 レベルで構成できます。 組織レベルはレベルが最も高く、その後にエンティティ レベル、属性レベルと続きます。 属性の監査が行われるようにするためには、属性、エンティティ、組織の各レベルで監査を有効にする必要があります。 エンティティの監査が行われるようにするためには、エンティティ レベルと組織レベルで監査を有効にする必要があります。  
  
 監査を有効/無効にする方法は組織レベルとエンティティまたは属性レベルで少し異なります。 組織レベルで監査を有効にするには、組織レコードの特定の属性を設定します。 しかし、エンティティ レベルと属性レベルでは、エンティティまたは属性のメタデータのプロパティを設定します。  
  
 システム管理者ロールまたはシステム カスタマイザー ロールを割り当てられていないユーザーは監査を有効/無効にできません。  
  
## <a name="enabling-auditing"></a>監査を有効にする方法  

 エンティティのメタデータの <xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.IsAuditEnabled> プロパティと、目的の各属性のメタデータの <xref:Microsoft.Xrm.Sdk.Metadata.AttributeMetadata.IsAuditEnabled> プロパティを `true` に設定すれば、そのエンティティのレコードに対するデータの変更をプラットフォームで記録できます。 しかし、エンティティの監査を有効にすると、そのエンティティのすべての属性の監査が既定で有効になります。 もちろん、一部またはすべての属性の監査を必要に応じて無効にすることもできます。 <xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.IsAuditEnabled> プロパティは、エンティティまたは属性のメタデータを作成または更新するときに設定できます。この作成または更新には、<xref:Microsoft.Xrm.Sdk.Messages.CreateEntityRequest>、<xref:Microsoft.Xrm.Sdk.Messages.UpdateEntityRequest>、<xref:Microsoft.Xrm.Sdk.Messages.CreateAttributeRequest>、<xref:Microsoft.Xrm.Sdk.Messages.UpdateAttributeRequest> の各要求を使用します。  
  
 エンティティの属性メタデータを変更した場合は、そのエンティティを <xref:Microsoft.Crm.Sdk.Messages.PublishXmlRequest> で公開しなければなりません。 エンティティ レベルで <xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.IsAuditEnabled> プロパティを変更しても公開は必要ありません。 通常、カスタマイズと公開は同一のユーザーが行います。 しかし、それらの作業を行うユーザーが異なる場合、公開アクションと公開操作の開始ユーザーは監査で記録されますが、更新アクションは記録されません。  
  
 さらに、監査を組織レベルで有効にするには、目的の組織レコードの <xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.IsAuditEnabled> 属性値を `true` に設定します。  
  
## <a name="disabling-auditing"></a>監査を無効にする方法  
 監査を無効にするには、既に述べたように、<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.IsAuditEnabled> を `false` に設定するだけです。 属性の監査を無効にした場合は、エンティティのカスタマイズを公開してください。 組織全体の監査を無効にするには、目的の組織のレコードの <xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.IsAuditEnabled> 属性を `false` に設定します。  
  
## <a name="entities-that-can-be-audited"></a>監査できるエンティティ  
 すべてのカスタム エンティティとカスタマイズ可能なほとんどのエンティティを監査できます。 カスタマイズ可能なエンティティの一覧については、" [どのエンティティがカスタマイズ可能か?](/dynamics365/customer-engagement/developer/which-entities-are-customizable)"を参照してください。  
  
 次の表は監査できないカスタマイズ不可能なエンティティの一覧を示します。 この表は、各エンティティのメタデータの `CanModifyAuditSettings` 属性値が `false` かをテストして求めたものです。  
  
||  
|-|  
|ActivityPointer|  
|Annotation|  
|BulkOperation|  
|カレンダー|  
|CalendarRule|  
|CustomerOpportunityRole|  
|割引|  
|DiscountType|  
|IncidentResolution|  
|KbArticle|  
|KbArticleComment|  
|KbArticleTemplate|  
|通知 |  
|OpportunityClose|  
|OrderClose|  
|ProductPriceLevel|  
|QuoteClose|  
|RecurrenceRule|  
|リソース |  
|ResourceGroup|  
|ResourceGroupExpansion|  
|ResourceSpec|  
|SalesLiteratureItem|  
|SalesProcessInstance|  
|Service|  
|件名​​|  
|テンプレート|  
|UoM|  
|UoMSchedule|  
|ワークフロー|  
|WorkflowLog|  
  
### <a name="see-also"></a>関連項目  
 [Dynamics 365 でのデータ管理](/dynamics365/customer-engagement/developer/manage-data)   
 [監査エンティティのデータ変更](/dynamics365/customer-engagement/developer/audit-entity-data-changes)   
 [監査済みデータの変更履歴の取得と削除](retrieve-and-delete-the-history-of-audited-data-changes.md)   
 [サンプル: エンティティのデータ変更を監査する](/dynamics365/customer-engagement/developer/sample-audit-entity-data-changes)   
 [Dynamics 365 でのデータ変更の監査](/dynamics365/customer-engagement/developer/audit-entity-data-changes)
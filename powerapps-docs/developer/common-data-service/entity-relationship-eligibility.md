---
title: 関連付け有効性エンティティ (アプリ用 Common Data Service) | Microsoft Docs
description: この記事では、エンティティがエンティティ関係に参加できるかどうかを判断するのに使用できるメッセージを示します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: mayadumesh
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="entity-relationship-eligibility"></a>エンティティの関連付けの有効性

エンティティ関係を作成する前に、それらのエンティティがその関連付けにふさわしいかどうかを確認してください。 次の表に、エンティティがエンティティ関係に参加できるかどうかを判断するのに使用できるメッセージを示します。  
  
|メッセージ|Web API 操作|SDK アセンブリ|  
|-------------|-----------------|----------------|  
|CanBeReferenced</br>指定されたエンティティが一対多の関連付けの主エンティティ (一) になるかどうかをチェックします。|<xref href="Microsoft.Dynamics.CRM.CanBeReferenced?text=CanBeReferenced Action" />|<xref:Microsoft.Xrm.Sdk.Messages.CanBeReferencedRequest>|  
|CanBeReferencing</br>指定されたエンティティが一対多の関連付けの参照エンティティ (多) になるかどうかをチェックします。|<xref href="Microsoft.Dynamics.CRM.CanBeReferencing?text=CanBeReferencing Action" />|<xref:Microsoft.Xrm.Sdk.Messages.CanBeReferencingRequest>|  
|CanManyToMany</br>エンティティが多対多の関連付けに参加できるかどうかをチェックします。|<xref href="Microsoft.Dynamics.CRM.CanManyToMany?text=CanManyToMany Action" />|<xref:Microsoft.Xrm.Sdk.Messages.CanManyToManyRequest>|  
|GetValidManyToMany</br>多対多の関連付けに参加できる一連のエンティティを返します。|<xref href="Microsoft.Dynamics.CRM.GetValidManyToMany?text=GetValidManyToMany Function" />|<xref:Microsoft.Xrm.Sdk.Messages.GetValidManyToManyRequest>|  
|GetValidReferencedEntities</br>指定されたエンティティから、1 対多の関連付けの主エンティティ (1 の側) として有効な一連のエンティティを返します。|<xref href="Microsoft.Dynamics.CRM.GetValidReferencedEntities?text=GetValidReferencedEntities Function" />|<xref:Microsoft.Xrm.Sdk.Messages.GetValidReferencedEntitiesRequest>|  
|GetValidReferencingEntities</br>指定されたエンティティに、1 対多の関連付けの関連エンティティ (多の側) として有効な一連のエンティティを返します。|<xref href="Microsoft.Dynamics.CRM.GetValidReferencingEntities?text=GetValidReferencingEntities Function" />|<xref:Microsoft.Xrm.Sdk.Messages.GetValidReferencingEntitiesRequest>|  
  
### <a name="see-also"></a>関連項目  
 [エンティティ関係メタデータをカスタマイズする](/dynamics365/customer-engagement/developer/customize-entity-relationship-metadata)   
 [Dynamics 365 のメタデータ モデルの拡張](/dynamics365/customer-engagement/developer/org-service/use-organization-service-metadata)   
 [エンティティの関連付けのメタデータ](/dynamics365/customer-engagement/developer/customize-entity-relationship-metadata)   
 [エンティティの関連付けのメッセージ](entity-relationship-metadata-messages.md)   
 [エンティティ関係の動作](/dynamics365/customer-engagement/developer/entity-relationship-behavior)   
 [1:N のエンティティ関係の作成](/dynamics365/customer-engagement/developer/org-service/create-retrieve-entity-relationships#BKMK_Create1NEntityRelationship)   
 [N:N のエンティティ関係の作成](/dynamics365/customer-engagement/developer/org-service/create-retrieve-entity-relationships#BKMK_CreateNNEntityRelationship)

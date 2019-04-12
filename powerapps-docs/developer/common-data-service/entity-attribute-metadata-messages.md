---
title: エンティティ属性メタデータのメッセージ (Common Data Service) | Microsoft Docs
description: プロパティまたはフィールドとも呼ばれる、エンティティ属性メタデータの編集に使用されるメッセージについて。
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
# <a name="entity-attribute-metadata-messages"></a>エンティティ属性のメタデータのメッセージ

<!-- 
Was Mike Carter
https://docs.microsoft.com/dynamics365/customer-engagement/developer/entity-attribute-metadata-messages -->

エンティティの属性とは、エンティティ内のデータ要素を格納するコンテナーのことです。 *属性*および*プロパティ* (クラスのプロパティ) という用語がしばしば*エンティティの属性*という用語と区別なく使われます。 モデル駆動型アプリは、エンティティ属性を参照するときに*フィールド*という用語を使用します。  

> [!NOTE]
> Web API を使用してエンティティの属性を作成および更新することができます。 詳細については、[属性の作成](webapi/create-update-entity-definitions-using-web-api.md#create-attributes)を参照してください。

## <a name="entity-attribute-messages"></a>エンティティの属性に関するメッセージ  
 次の表に、エンティティ属性に関する操作を実行するために使用できるメッセージを示します。  
  
|メッセージ|Web API 操作|SDK アセンブリ|   
|-------------|-----------------|-----------------|  
|CreateAttribute</br></br>エンティティ属性の作成|属性の JSON 定義を使用して、EntityMetadata 属性のコレクション評価されたナビゲーション プロパティに投稿します。 詳細: [属性の作成](webapi/create-update-entity-definitions-using-web-api.md#create-attributes)|<xref:Microsoft.Xrm.Sdk.Messages.CreateAttributeRequest>| 
|DeleteAttribute</br></br>エンティティの属性の削除|属性の URL の対する削除。|<xref:Microsoft.Xrm.Sdk.Messages.DeleteAttributeRequest>|  
|DeleteOptionValue</br></br><xref:Microsoft.Xrm.Sdk.Metadata.PicklistAttributeMetadata> または <xref:Microsoft.Xrm.Sdk.Metadata.StatusAttributeMetadata> 属性からのオプションを削除します|<xref href="Microsoft.Dynamics.CRM.DeleteOptionValue?text=DeleteOptionValue Action" />|<xref:Microsoft.Xrm.Sdk.Messages.DeleteOptionValueRequest>|  
|InsertOptionValue</br></br><xref:Microsoft.Xrm.Sdk.Metadata.PicklistAttributeMetadata> 属性にオプションを追加します|<xref href="Microsoft.Dynamics.CRM.InsertOptionValue?text=InsertOptionValue Action" />|<xref:Microsoft.Xrm.Sdk.Messages.InsertOptionValueRequest>|<xref:Microsoft.Xrm.Sdk.Metadata.PicklistAttributeMetadata> 属性にオプションを追加します。|  
|InsertStatusValue</br></br><xref:Microsoft.Xrm.Sdk.Metadata.StatusAttributeMetadata> 属性にオプションを追加します|<xref href="Microsoft.Dynamics.CRM.InsertStatusValue?text=InsertStatusValue Action" />|<xref:Microsoft.Xrm.Sdk.Messages.InsertStatusValueRequest>|  |<xref:Microsoft.Xrm.Sdk.Metadata.PicklistAttributeMetadata> 属性内のオプションの順序を変更します|<xref href="Microsoft.Dynamics.CRM.OrderOption?text=OrderOption Action" />|<xref:Microsoft.Xrm.Sdk.Messages.OrderOptionRequest>|  
|RetrieveAttribute</br></br>エンティティの属性の取得|[EntityMetadata 属性をクエリ](webapi/query-metadata-web-api.md#bkmk_queryAttributesexample) 内で言及された Web API クエリを使用してエンティティの属性を取得します。|<xref:Microsoft.Xrm.Sdk.Messages.RetrieveAttributeRequest>|  
|UpdateAttribute</br></br>エンティティの属性の更新|[エンティティの更新](webapi/create-update-entity-definitions-using-web-api.md#update-entities) を参照してください|<xref:Microsoft.Xrm.Sdk.Messages.UpdateAttributeRequest>|  
|UpdateStateValue</br></br><xref:Microsoft.Xrm.Sdk.Metadata.StateAttributeMetadata> 属性のラベルを更新します|<xref href="Microsoft.Dynamics.CRM.UpdateStateValue?text=UpdateStateValue Action" />|<xref:Microsoft.Xrm.Sdk.Messages.UpdateStateValueRequest>|  

### <a name="see-also"></a>関連項目  

[属性メタデータ](entity-attribute-metadata.md)<br />
[自動付番の属性を作成](create-auto-number-attributes.md)<br />
<!-- TODO: [Work with Attributes](org-service/work-attribute-metadata.md)<br />
[Sample: Work with Attributes](org-service/sample-work-attribute-metadata.md) -->
---
title: Web API を使用してオプション セットを作成および更新 (Common Data Service) | Microsoft Docs
description: メタデータ駆動のアーキテクチャを使用してユーザー定義エンティティや追加のシステム エンティティ属性を柔軟に作成するのに役立つ Common Data Service エンティティの作成および更新について説明します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
caps.latest.revision: 15
author: brandonsimons
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="create-and-update-option-sets-using-the-web-api"></a>Web API を使用してオプション セットを作成および更新

通常、*グローバル* オプション セットでフィールドを設定するのは、さまざまなフィールドを同じオプション セットで共有して、それらを 1 つの場所でメンテナンスできるようにするためです。 特定の属性に対してのみ定義される*ローカル* オプション セットとは異なり、グローバル オプション セットは再利用できます。 要求パラメーターの中で列挙体のときと同じように使われる例もあります。  
  
*[組織 URI]*`/api/data/v9.0/GlobalOptionSetDefinitions` への POST 要求を使用してグローバル オプション セットを設定するときは、値の設定をシステムに任せることをお勧めします。 具体的には新規の `OptionMetadata` インスタンスを作成するとき、引数として **null** 値を渡します。 オプションを変更すると、そのオプション セットが作成されたソリューションに設定されている発行者のコンテキストに固有の接頭辞がオプション値に含められます。 この接頭辞は、マネージド ソリューションや、マネージド ソリューションのインストール先の組織で定義されている任意のオプション セットの中で、オプション セットの重複が生じる可能性を減らす効果があります。 詳細については、[オプション セット オプションのマージ](../understand-managed-solutions-merged.md#merge-option-set-options) を参照してください。

 ## <a name="messages"></a>メッセージ  
 次の表に、グローバル オプション セットで使用できるメッセージを示します。  
  
|メッセージ|Web API 操作|  
|--|--|
|CreateOptionSet|*[組織 URI]*`/api/data/v9.0/GlobalOptionSetDefinitions` への `POST` リクエストを使用します。|
|DeleteOptionSet|*[組織 URI]*`/api/data/v9.0/GlobalOptionSetDefinitions(`*metadataid*`)` への `DELETE` リクエストを使用します。|
|RetrieveAllOptionSets|*[組織 URI]*`/api/data/v9.0/GlobalOptionSetDefinitions` への `GET` リクエストを使用します。| 
|RetrieveOptionSet|*[組織 URI]*`/api/data/v9.0/GlobalOptionSetDefinitions(`*metadataid*`)` への `GET` リクエストを使用します。|   


次の表に、ローカルおよびグローバル オプション セットで使用できるメッセージを示します。

|メッセージ|Web API 操作|  
|--|--|
|DeleteOptionValue</br>グローバル オプション セットから値の 1 つを削除します。|<xref href="Microsoft.Dynamics.CRM.DeleteOptionValue?text=DeleteOptionValue Action" />  
|InsertOptionValue</br>新しいオプションをグローバル オプション セットに挿入します。|<xref href="Microsoft.Dynamics.CRM.InsertOptionValue?text=InsertOptionValue Action" />| 
|InsertStatusValue</br>`Status` 属性に使用する新しいオプションをグローバル オプション セットに挿入します。|<xref href="Microsoft.Dynamics.CRM.InsertStatusValue?text=InsertStatusValue Action" />|
|OrderOption</br>オプション セット内のオプションの相対順序を変更します。|<xref href="Microsoft.Dynamics.CRM.OrderOption?text=OrderOption Action" />|
|UpdateOptionSet|<xref href="Microsoft.Dynamics.CRM.OptionSetMetadata?text=OptionSetMetadata EntityType" />から *[組織 URI]*`/api/data/v9.0/GlobalOptionSetDefinitions(`*metadataid*`)/Microsoft.Dynamics.CRM.OptionSetMetadata` で `PUT` リクエストを使用<br />ローカル オプション セットについては、*[組織 URI]*`/api/data/v9.0/EntityDefinitions(`*metadataid*`)/Attributes(`*metadataid*`)/Microsoft.Dynamics.CRM.PicklistAttributeMetadata/OptionSet` を使用します。|
|UpdateOptionValue</br>グローバル オプション セットのオプションを更新します。|<xref href="Microsoft.Dynamics.CRM.UpdateOptionValue?text=UpdateOptionValue Action" />|
|UpdateStateValue</br>`Status` 属性に使用される新しいオプションをオプション セットに挿入します。|<xref href="Microsoft.Dynamics.CRM.UpdateStateValue?text=UpdateStateValue Action" />|

### <a name="see-also"></a>関連項目

[オプション セットのカスタマイズ](../org-service/metadata-option-sets.md)
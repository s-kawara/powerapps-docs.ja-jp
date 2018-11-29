---
title: BusinessUnit エンティティ (アプリ用 Common Data Service) | Microsoft Docs
description: アプリ用 Common Data Service における持株会社や法人などの組織は、部署で構成されています。
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
# <a name="businessunit-entity"></a>BusinessUnit エンティティ

アプリ用 Common Data Service における持株会社や法人などの組織は、部署で構成されています。 *部署*は、最上位レベルの組織に属します。 部署は他の部署 (下位の部署) の親になることができます。 組織で最初に作成された部署は、ルート部署と呼ばれます。 部署を削除できますが、ルート部署を削除することはできません。  
  
- *上位の部署*は、階層内の 1 つ以上の部署から報告を受ける部署です。  
  
- *下位の部署*は、組織の事業階層の別の部署のすぐ下位にある部署です。  
  
 部署では、エンティティのメタデータ定義の所有権の種類に定義されたレコードを所有することができます。 
  
 セキュリティ ロールは部署と関連付けられます。 <xref:Microsoft.Crm.Sdk.Messages.WhoAmIRequest> メッセージを呼び出すと、現在のログオン ユーザーまたは偽装ユーザーの部署を見つけることができます。

### <a name="see-also"></a>関連項目

[BusinessUnit エンティティの参照](reference/entities/businessunit.md)
[セキュリティ エンティティ](security-model.md)
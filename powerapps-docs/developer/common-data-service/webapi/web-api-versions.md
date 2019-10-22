---
title: Common Data Service Web API のバージョン (Common Data Service)| Microsoft Docs
description: Common Data Service Web APIのバージョン管理の仕組み Common Data Service のWeb APIバージョンは、新しい機能が追加された v8.x リリースの動作とは異なり、同一の環境におけるバージョン固有の差異に対応しています。
ms.custom: ''
ms.date: 07/25/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: d9bb79a5-2bfa-4ffe-8cb4-60f192359489
caps.latest.revision: 34
author: brandonsimons
ms.author: jdaly
ms.reviewer: susikka
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="common-data-service-web-api-versions"></a>Common Data ServiceWeb API バージョン

Dynamics 365 の (v9.0) リリース以降、 Web API は同じ環境でのバージョン固有の違いをサポートしています。  
  
これは v8.*x* リリースでの動作とは異なります。 以前のリリースでは、新しい機能はその環境に適用された更新プログラムに応じて、サービスの任意のバージョンに利用可能でした。  v8.2 へのアップグレード後は、v8.0 および v8.1 のサービスはすべて同じでした。 これが可能だったのは、全ての変更が付加的だったためです。 削除されたものも破損変更もありませんでした。 その結果、v8.*x* のサービス URL で参照される特定のバージョンは、実際には重要ではありませんでした。  
  
今後は、特定の操作の削除などの潜在的な破損変更を含む、サービスの機能変更がなされる可能性があります。 これにより、継続的に改善が適用されるようになります。 このトピックでは、Web API が組織サービスとのパリティをまだ達成していないバージョン固有の違いや制限事項をすべて記録します。  
  
## <a name="web-api-version-specific-differences"></a>Web API のバージョン固有の相違点

<a name="BKMK_fetchresponse"></a>

### <a name="encoding-for-special-characters-in-fetchxml-query-response"></a>FetchXML クエリに応答する特殊文字のエンコード

v8.*x* バージョンの場合、リンク エンティティとその属性を含む FetchXMLクエリへの応答には、「. 」 が 「_x002e_」に、「@」 が 「_x0040_」になるような Unicode特殊文字が含まれます。 この特殊文字のエンコーディングは、v9.*x*でリリースされた FetchXML クエリの応答には存在していません。

### <a name="same-name-for-entity-and-attribute"></a>エンティティおよび属性と同じ名称

エンティティの名前とその属性のいずれかが同じ場合、v8.x インスタンスの属性名に 「1」 が付加されます。 たとえば、エンティティ **new_zipcode** に **new_zipcode** という名前の属性がある場合、属性名は **new_zipcode1**に変更されます。

v9.*x* インスタンスの場合は、属性名には何も追加されません。

## <a name="new-operations-added"></a>追加された新しい操作  

v9.x リリースの Web API に次の操作が追加されています。  
  
||||  
|-|-|-|  
|<xref:Microsoft.Crm.Sdk.Messages.GrantAccessRequest>|<xref:Microsoft.Crm.Sdk.Messages.ModifyAccessRequest>|<xref:Microsoft.Crm.Sdk.Messages.RetrieveSharedPrincipalsAndAccessRequest>|  

## <a name="web-api-limitations"></a>Web API の制限  

Common Data Service Web API には組織サービスの機能を持つ完全なパリティが用意されています。 Common Data Service の場合は、このトピックでは Common Data Service v8.x のリリースから繰り越された制限事項について説明します。 それ以前のリリースについては、[Dynamics CRM 2016 Web API の制限](https://msdn.microsoft.com/library/mt628816\(CRM.8\).aspx)を参照してください。  
 
> [!NOTE] 
> 複雑な戻り値と簡易な戻り値を含むユーザー定義のアクションを定義した場合、対応するアクションは Web API では利用できませんでしたが、2011 SOAP エンドポイントを使用して利用できました。 複雑な戻り値は、`EntityReference`、`Entity`、または `EntityCollection` です。 簡易な戻り値、または 1 つの複雑な戻り値の組み合わせを含めることができます。 詳細: [独自のアクションの作成](/dynamics365/customer-engagement/developer/create-own-actions)。

### <a name="see-also"></a>関連項目  

[Common Data Service Web API の使用](overview.md)<br />
[Web API を使用して Common Data Service を認証する](authenticate-web-api.md)<br />
[Web API の種類および操作](web-api-types-operations.md)<br />
[Web API を使用して演算を実行する](perform-operations-web-api.md)
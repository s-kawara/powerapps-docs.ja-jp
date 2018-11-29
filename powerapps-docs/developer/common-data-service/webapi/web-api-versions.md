---
title: アプリ用 Common Data Service Web API のバージョン (アプリ用 Common Data Service)| Microsoft Docs
description: アプリ用 Common Data Service Web API のバージョン管理がどのように機能するかを説明します。 アプリ用 Common Data Service Web API のバージョンは、新しい機能が付加的だった v8.x リリースでの動作とは異なり、同じ環境でのバージョン固有の違いをサポートしています。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: d9bb79a5-2bfa-4ffe-8cb4-60f192359489
caps.latest.revision: 34
author: brandonsimons
ms.author: jdaly
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="common-data-service-for-apps-web-api-versions"></a>アプリ用 Common Data Service Web API のバージョン

Dynamics 365 の (v9.0) リリース以降、 Web API は同じ環境でのバージョン固有の違いをサポートしています。  
  
これは v8.*x* リリースでの動作とは異なります。 以前のリリースでは、新しい機能はその環境に適用された更新プログラムに応じて、サービスの任意のバージョンに利用可能でした。  v8.2 へのアップグレード後は、v8.0 および v8.1 のサービスはすべて同じでした。 これが可能だったのは、全ての変更が付加的だったためです。 削除されたものも破損変更もありませんでした。 その結果、v8.*x* のサービス URL で参照される特定のバージョンは、実際には重要ではありませんでした。  
  
今後は、特定の操作の削除などの潜在的な破損変更を含む、サービスの機能変更がなされる可能性があります。 これにより、継続的に改善が適用されるようになります。 このトピックでは、Web API が組織サービスとのパリティをまだ達成していないバージョン固有の違いや制限事項をすべて記録します。  
  
## <a name="web-api-limitations"></a>Web API の制限  

アプリ用 Common Data Service Web API には組織サービスの機能を持つ完全なパリティが用意されています。 アプリ用 Common Data Service の場合、このトピックでは、アプリ用 Common Data Service v8.x リリースから引き継がれた制限について説明します。 それ以前のリリースについては、「[Dynamics CRM 2016 Web API の制限](https://msdn.microsoft.com/library/mt628816\(CRM.8\).aspx)」を参照してください。  
 
> [!NOTE] 
> 複雑な戻り値と簡易な戻り値を含むユーザー定義のアクションを定義した場合、対応するアクションは Web API では利用できませんでしたが、2011 SOAP エンドポイントを使用して利用できました。 複雑な戻り値は、`EntityReference`、`Entity`、または `EntityCollection` です。 簡易な戻り値、または 1 つの複雑な戻り値の組み合わせを含めることができます。 詳細: [独自のアクションの作成](/dynamics365/customer-engagement/developer/create-own-actions)。
 
## <a name="new-operations-added"></a>追加された新しい操作  
 v9.x リリースの Web API に次の操作が追加されています。  
  
||||  
|-|-|-|  
|<xref:Microsoft.Crm.Sdk.Messages.GrantAccessRequest>|<xref:Microsoft.Crm.Sdk.Messages.ModifyAccessRequest>|<xref:Microsoft.Crm.Sdk.Messages.RetrieveSharedPrincipalsAndAccessRequest>|  
  
### <a name="see-also"></a>関連項目  

[アプリ用 Common Data Service Web API を使用する](overview.md)<br />
[Web API を使用した アプリ用 Common Data Service への認証](authenticate-web-api.md)<br />
[Web API の種類および操作](web-api-types-operations.md)<br />
[Web API を使用して演算を実行する](perform-operations-web-api.md)

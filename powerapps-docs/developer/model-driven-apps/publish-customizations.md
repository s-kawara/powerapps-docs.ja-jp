---
title: カスタマイズの公開 (モデル駆動型アプリ) | MicrosoftDocs
description: カスタマイズの公開は、ユーザー インターフェイスに影響するデータへの変更を Web アプリケーションに知らせるものです。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: KumarVivek
ms.author: kvivek
manager: shilpas
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="publish-customizations"></a>カスタマイズを公開します

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/customize-dev/publish-customizations -->

カスタマイズの公開は、ユーザー インターフェイスに影響するデータへの変更を Web アプリケーションに知らせるものです。  
  
<a name="BKMK_WhenToPublishCustomizations"></a>   
## <a name="when-to-publish-customizations"></a>カスタマイズの公開のタイミング  
 新しいアイテムが作成されるか、既存のアイテムが削除されると、カスタマイズが自動的に公開されます。  
  
 ユーザー インターフェイスに影響するスキーマ メタデータまたはエンティティを更新した場合は、その後に、変更を公開しなければなりません。 少し間を置いて、関連する一連の変更をまとめて公開してもかまいません。  
  
 公開したカスタマイズだけがソリューションと共にエクスポートされます。 必ずカスタマイズを公開してからソリューションをエクスポートするようにしてください。  
  
 Dynamics 365 for tablets に表示されるカスタマイズを実行する際、ユーザーがいつでもカスタマイズを明示的に公開し、すべての項目が Dynamics 365 for tablets アプリケーションと同期されるようにする必要があります。  
  
> [!NOTE]
>  カスタマイズを公開すると、標準システム操作を干渉する可能性があります。 運用環境では、ユーザーの作業をできるだけ妨害しない時間帯にカスタマイズ公開をスケジュールすることをお勧めします。  
  
## <a name="publishing-programmatically"></a>プログラムによる公開  
 次の表に、カスタマイズの公開で使用できる 2 つのメッセージを示します。  
  
|メッセージ|説明|  
|-------------|-----------------|  
|<xref:Microsoft.Crm.Sdk.Messages.PublishAllXmlRequest>|すべてのカスタマイズを公開します。|  
|<xref:Microsoft.Crm.Sdk.Messages.PublishXmlRequest>|指定されたカスタマイズを公開します。|  
  
 `PublishXmlRequest` メッセージでは、公開するアイテムを指定するために <xref:Microsoft.Crm.Sdk.Messages.PublishXmlRequest.ParameterXml> パラメーターを使います。 `ParameterXML` は [Publish 要求スキーマ](publish-request-schema.md) に準拠しなければなりません。  
  
<a name="BKMK_RetrieveUnpublishedMetadata"></a>   
## <a name="retrieving-unpublished-metadata"></a>非公開メタデータの取得  
 モデル駆動型アプリで、カスタマイズ可能なアイテムの編集用アプリケーションを作成する場合は、それらのアイテムの非公開の定義を取得する必要があります。 開発者の定義した一部の変更が公開されていないときは、アプリケーションで取得してユーザー インターフェイスに表示できなければなりません。 
  
 非公開メタデータの取得には次の 2 つのメソッドを使用します。  
  
 **RetrieveAsIfPublished パラメーター**  
 エンティティ、属性、エンティティ関係、オプション セット データの取得には、次のメッセージを使用します。  
  
- <xref:Microsoft.Xrm.Sdk.Messages.RetrieveAllEntitiesRequest>  
  
- <xref:Microsoft.Xrm.Sdk.Messages.RetrieveAllOptionSetsRequest>  
  
- <xref:Microsoft.Xrm.Sdk.Messages.RetrieveAttributeRequest>  
  
- <xref:Microsoft.Xrm.Sdk.Messages.RetrieveEntityRequest>  
  
- <xref:Microsoft.Xrm.Sdk.Messages.RetrieveOptionSetRequest>  
  
- <xref:Microsoft.Xrm.Sdk.Messages.RetrieveRelationshipRequest>  
  
  **RetrieveUnpublished 要求**  
  ユーザー インターフェイス アイテム (フォーム、テンプレート、ビジュアル化、Web リソース定義) の取得には、次のメッセージを使用します。  
  
- <xref:Microsoft.Crm.Sdk.Messages.RetrieveUnpublishedRequest>  
  
- <xref:Microsoft.Crm.Sdk.Messages.RetrieveUnpublishedMultipleRequest>  
  
### <a name="see-also"></a>関連項目  
 [モデル駆動型アプリのカスタマイズ](/dynamics365/customer-engagement/developer/customize-dev/customize-applications)<br/>
 [メタデータ モデルの拡張](/dynamics365/customer-engagement/developer/org-service/use-organization-service-metadata)<br/>
 [Publish 要求スキーマ](publish-request-schema.md)<br/>
 [エンティティ フォームのカスタマイズ](customize-entity-forms.md)<br/>
 [エンティティ ビューのカスタマイズ](customize-entity-views.md)<br/>
 [グローバル オプション セットのカスタマイズ](/dynamics365/customer-engagement/developer/org-service/customize-global-option-sets)<br/>
 [SiteMap を使用したアプリケーション ナビゲーションの変更](/dynamics365/customer-engagement/developer/customize-dev/change-application-navigation-using-sitemap)


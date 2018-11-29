---
title: ダッシュボードによるデータの分析 (モデル駆動型アプリ) | MicrosoftDocs
description: Dynamics 365 Common Data Service for Apps のダッシュボード エンティティでは、さまざまなグラフ、グリッド、IFRAMES、または Web リソース からのデータを同時に提示できます。 ダッシュボードでは、ユーザーは顧客情報のさまざまな部分を比較および分析し、それらにデータ スナップショットを提供できます。
keywords: ''
ms.date: 10/31/2018
ms.service:
  - powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: 4b54597b-5603-2e6e-4630-bc120f711707
author: JimDaly
ms.author: jdaly
manager: shilpas
ms.reviewer: null
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="analyze-data-with-dashboards"></a>ダッシュボードによるデータの分析

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/customize-dev/analyze-data-with-dashboards -->

アプリ用 Common Data Service のダッシュボード エンティティでは、さまざまなグラフ、グリッド、IFRAMES、または Web リソース からのデータを同時に提示できます。 ダッシュボードでは、ユーザーは顧客情報のさまざまな部分を比較および分析し、それらにデータ スナップショットを提供できます。  
  
## <a name="types-of-dashboards"></a>ダッシュボードの種類  
組織所有のダッシュボードとユーザー所有のダッシュボードの 2 種類のダッシュボードがあります。  
  
**組織所有のダッシュボード。**

組織所有のダッシュボードは、`SystemForm` エンティティで表現され、割り当てたり共有したりすることはできません。 これらのダッシュボードは、ソリューション対応エンティティです。 このエンティティに対して更新操作を実行すると、更新の変更を公開して組織全体で使用可能にする必要があります。 <xref:Microsoft.Crm.Sdk.Messages.PublishAllXmlRequest> メッセージを使用してカスタマイズを公開する場合は、新規に作成された組織所有のダッシュボードも公開され、組織全体で使用可能になります。 または、<xref:Microsoft.Crm.Sdk.Messages.PublishXmlRequest> メッセージを使用し、ダッシュボード ID を要求メッセージのパラメーターとして使用することにより、特定のダッシュボードに対して行われた変更を公開できます。  
  
**ユーザーが所有するダッシュボード。**

ユーザー所有のダッシュボードは、`UserForm` エンティティによって表現され、他のユーザーに割り当てたり、他のユーザーと共有したりできます。また、ダッシュボードのアクセス特権に応じて、他のユーザーがダッシュボードを表示することもできます。  
  
> [!NOTE]
> 新しい対話型ダッシュボードをプログラムで作成または管理することはできません。 Webクライアントを使用した対話型ダッシュボードに関する作業の詳細については、[対話型エクスペリエンス ダッシュボードの構成](../../maker/model-driven-apps/configure-interactive-experience-dashboards.md)を参照してください。 
  
### <a name="see-also"></a>関連項目  
 [ダッシュボード用FormXMLを使用](understand-dashboards-dashboard-components-formxml.md)   
 [ダッシュボードに対するアクション](actions-dashboards.md)   
 [ダッシュボードの作成](create-dashboard.md)   
 [サンプル ダッシュボード](sample-dashboards.md)   
 [ダッシュボード エンティティ](/dynamics365/customer-engagement/developer/customize-dev/dashboard-entities)   <!-- TODO: Need to find the topic in powerapps repo to link--> [サンプル: ダッシュボードの作成、取得、更新および削除(CRUD)](/dynamics365/customer-engagement/developer/customize-dev/sample-create-retrieve-update-delete-dashboard) <!-- TODO: Need to find the topic in powerapps repo to link-->  
 [サンプル: ユーザー所有のダッシュボードの別のユーザーへの割り当て](/dynamics365/customer-engagement/developer/customize-dev/sample-assign-user-owned-dashboard-another-user)  <!-- TODO: Need to find the topic in powerapps repo to link--> [ビジュアル化データ記述スキーマ](visualization-data-description-schema.md)     
 [ビジュアル化とダッシュボードのカスタマイズ](customize-visualizations-dashboards.md)

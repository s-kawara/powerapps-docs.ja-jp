---
title: ダッシュボードに対するアクション (モデル駆動型アプリ) | MicrosoftDocs
description: 組織所有のダッシュボードおよびユーザー所有のダッシュボードに対する、作成、取得、更新、削除などのアクションの実行について。
keywords: ''
ms.date: 10/31/2018
ms.service:
  - powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: 339eb79d-5dec-885b-496f-bfa26e9cae08
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

# <a name="actions-on-dashboards"></a>ダッシュボードに対するアクション

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/customize-dev/actions-dashboards -->

組織所有のダッシュボードおよびユーザー所有のダッシュボードに対して、作成、取得、更新、削除などのアクションを実行できます。  
  
## <a name="actions-on-an-organization-owned-dashboard"></a>組織所有のダッシュボードに対するアクション  
 組織所有のダッシュボード (`SystemForm`) に対して以下のアクションを実行するには、アプリ用 Common Data Service (CDS) の自分のアカウントにシステム管理者ロールまたはシステム カスタマイザー ロールが割り当てられている必要があります。  
  
- 作成、取得、更新、および削除。 アプリ Web サービス用 CDS を使用するか、エンティティ フォームをカスタマイズすることにより、組織所有のダッシュボードを作成または更新できます。 システム ダッシュボードの作成の詳細については、「[システム ダッシュボードの作成](create-dashboard.md)」を参照してください。  
  
- ダッシュボードの作成または更新時に `SystemForm.IsDefault` 属性値を `true` に設定することにより、組織所有のダッシュボードを組織の既定のダッシュボードとして設定する。  
  
  > [!IMPORTANT]
  >  アプリ用 CDS Web サービスで使用できるメソッドを使用して、2 つのダッシュボードを既定として設定できます。 この設定をプログラムで更新する前に、他のダッシュボードが組織の既定のダッシュボードになっていないことを確認してください。  
  
  組織所有のダッシュボードを更新した後は、メタデータの変更を公開して、組織全体で参照できるようにする必要があります。 組織所有のダッシュボードへの変更を公開するには、<xref:Microsoft.Crm.Sdk.Messages.PublishAllXmlRequest> メッセージまたは <xref:Microsoft.Crm.Sdk.Messages.PublishXmlRequest> メッセージを使用します。 その方法を示すサンプル コードについては、[サンプル: ダッシュボードを作成、取得、更新、および削除 (CRUD)](/dynamics365/customer-engagement/developer/customize-dev/sample-create-retrieve-update-delete-dashboard)<!-- TODO Need to update the powerapps repo's topic link. As of now not found--> を参照してください。  
  
  組織所有のダッシュボード エンティティでサポートされるメッセージの一覧については、「[SystemForm エンティティ](../common-data-service/reference/entities/systemform.md)」を参照してください。  
  
## <a name="actions-on-a-user-owned-dashboard"></a>ユーザー所有のダッシュボードに対するアクション  
 ユーザー所有のダッシュボード (`UserForm`) に対しては、以下のアクションを実行できます。  
  
- 作成、取得、更新、および削除。 ユーザー所有のダッシュボードの作成の詳細については、「[ダッシュボードの作成](create-dashboard.md)」を参照してください。  
  
- <xref:Microsoft.Crm.Sdk.Messages.AssignRequest> メッセージを使用してユーザー所有のダッシュボードを別のユーザーまたはチームに割り当てることにより、ユーザー所有のダッシュボードの所有権を変更する。  
  
- <xref:Microsoft.Crm.Sdk.Messages.RetrievePrincipalAccessRequest> メッセージを使用して、指定されたセキュリティ プリンシパル (ユーザーまたはチーム) がユーザー所有のダッシュボードに対して持っているアクセス権を取得する。 <xref:Microsoft.Crm.Sdk.Messages.RetrieveSharedPrincipalsAndAccessRequest> メッセージを使用して、ユーザー所有のダッシュボードに対するアクセス権を持つすべてのセキュリティ プリンシパル (ユーザーまたはチーム) とそのアクセス権を取得することもできます。  
  
- <xref:Microsoft.Crm.Sdk.Messages.GrantAccessRequest>、<xref:Microsoft.Crm.Sdk.Messages.ModifyAccessRequest>、<xref:Microsoft.Crm.Sdk.Messages.RevokeAccessRequest> の各メッセージを使用して、ユーザー所有のダッシュボードを特定領域の他のユーザーおよびチームと共有することにより、それらのユーザーおよびチームと共同作業する。  
  
  ユーザー所有のダッシュボード エンティティでサポートされるメッセージの一覧については、「[UserForm エンティティ](../common-data-service/reference/entities/userform.md)」を参照してください。  
  
### <a name="see-also"></a>関連項目  
 [Microsoft Dynamics 365 用ダッシュボード](analyze-data-with-dashboards.md)   
 [ダッシュボード用 FormXML を使用](understand-dashboards-dashboard-components-formxml.md)   
 [ダッシュボードの作成](create-dashboard.md)   
 [サンプル ダッシュボード](sample-dashboards.md)   
 [ダッシュボード エンティティ](/dynamics365/customer-engagement/developer/customize-dev/dashboard-entities) <!-- TODO Need to update the powerapps repo's topic link. As of now not found-->  
 [サンプル: ダッシュボードの作成、取得、更新および削除 (CRUD)](/dynamics365/customer-engagement/developer/customize-dev/sample-create-retrieve-update-delete-dashboard) <!-- TODO Need to update the powerapps repo's topic link. As of now not found-->   
 [サンプル: ユーザー所有のダッシュボードの別のユーザーへの割り当て](/dynamics365/customer-engagement/developer/customize-dev/sample-assign-user-owned-dashboard-another-user) <!-- TODO Need to update the powerapps repo's topic link. As of now not found-->
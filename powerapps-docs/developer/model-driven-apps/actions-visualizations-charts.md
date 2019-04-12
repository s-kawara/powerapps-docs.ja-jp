---
title: ビジュアル化に対するアクション (グラフ)(モデル駆動型アプリ) | MicrosoftDocs
description: Common Data Service Web サービスを使用して、ビジュアル化エンティティの以下のアクションを実行できます。
keywords: ''
ms.date: 10/31/2018
ms.service:
  - powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: c7eb3bdf-9d6f-9bcc-8114-4c3dc5be2976
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

# <a name="actions-on-visualizations-charts"></a>ビジュアル化に対するアクション (グラフ)

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/customize-dev/actions-visualizations-charts -->

Common Data Service の Web サービスを使用して、ビジュアル化エンティティの以下のアクションを実行できます。  
  
## <a name="actions-on-organization-owned-visualizations"></a>組織所有のビジュアル化に対するアクション  
 組織所有のビジュアル化 (`SavedQueryVisualization`) にアクションを実行するには、システム管理者ロールまたはシステム カスタマイザー ロールが必要です。 組織所有のビジュアル化に対して以下のアクションを実行できます。  
  
- 組織所有のビジュアル化を作成、取得、更新、削除する。 詳細: [ビジュアル化の作成](create-visualization-chart.md)  
  
  > [!NOTE]
  >  組織所有のビジュアル化を更新したら、<xref:Microsoft.Crm.Sdk.Messages.PublishAllXmlRequest> メッセージを使用して、メタデータの変更を公開し、組織全体で参照できるようにする必要があります。 または、エンティティを公開するとき、そのエンティティに添付された未公開の組織所有のビジュアル化はすべて自動的に公開されます。  
  
- `SavedQueryVisualization.PrimaryEntityTypeCode` 属性を使用して、エンティティに添付されているすべての組織所有のビジュアル化を照会し、取得する。 複数の組織所有のビジュアル化を 1 つのエンティティに添付することができます。 ビジュアル化を添付できるエンティティの一覧については、「[ビジュアル化でサポートされているエンティティ](view-data-with-visualizations-charts.md#SupportedVisualizationEntities)」を参照してください。 エンティティに添付されている組織所有のビジュアル化をすべて取得する方法を示すコード サンプルについては、「[サンプル: エンティティに添付されているすべてのグラフの取得](/dynamics365/customer-engagement/developer/customize-dev/sample-retrieve-all-charts-attached-entity)」を参照してください。
  
  > [!NOTE]
  >  ビジュアル化は、作成した後で変更または更新して、別のエンティティに添付することはできません。 つまりこれは、組織所有のビジュアル化の更新アクションについて `SavedQueryVisualization.PrimaryEntityTypeCode` 属性が有効ではないことを意味します。
  
- `SavedQueryVisualization.IsDefault` 属性を `true` に設定して、組織所有のビジュアル化を、添付されているエンティティの既定のビジュアル化として指定する。 組織所有のビジュアル化をエンティティの既定のビジュアル化として設定すると、Common Data Service でそのエンティティのビジュアル化の表示を選択したときに、そのビジュアル化が既定で表示されます。
  
  > [!NOTE]
  >  Common Data Service の Web サービスを使用して、すでに既定のビジュアル化が設定されているエンティティに対して、組織所有のビジュアル化を既定として設定すると、両方のビジュアル化がそのエンティティの既定のビジュアル化としてマークされます。  あるエンティティの既定のビジュアル化としてビジュアル化を設定する場合は、他のビジュアル化がいずれもがそのエンティティの既定のビジュアル化として設定されていないことを確認してください。  
  
  組織所有のビジュアル化エンティティでサポートされるメッセージの一覧については、「[SavedQueryVisualization エンティティ](../common-data-service/reference/entities/savedqueryvisualization.md)」を参照してください。
  
## <a name="actions-on-user-owned-visualizations"></a>ユーザー所有のビジュアル化に対するアクション  
 ユーザー所有のビジュアル化 (`UserQueryVisualization`) に対して以下のアクションを実行できます。  
  
- ユーザー所有のビジュアル化を作成、取得、更新、削除する。 詳細: [ビジュアル化の作成](create-visualization-chart.md)  
  
- `UserQueryVisualization.PrimaryEntityTypeCode` 属性を使用して、エンティティに添付されているすべてのユーザー所有のビジュアル化を照会し、取得します。 複数のユーザー所有のビジュアル化を 1 つのエンティティに添付することができます。 ビジュアル化を添付できるエンティティの一覧については、「[ビジュアル化でサポートされているエンティティ](view-data-with-visualizations-charts.md#SupportedVisualizationEntities)」を参照してください。  
  
  > [!NOTE]
  >  ビジュアル化は、作成した後で変更または更新して、別のエンティティに添付することはできません。 つまりこれは、ユーザー所有のビジュアル化の更新アクションについて `UserQueryVisualization.PrimaryEntityTypeCode` 属性が有効ではないことを意味します。
  
- <xref:Microsoft.Crm.Sdk.Messages.AssignRequest> を使用してユーザー所有のビジュアル化を別のユーザーまたはチームに割り当てることにより、ユーザー所有のビジュアル化の所有権を変更する。  
  
- <xref:Microsoft.Crm.Sdk.Messages.RetrievePrincipalAccessRequest> を使用して、指定されたセキュリティ プリンシパル (ユーザーまたはチーム) がユーザー所有のビジュアル化に対して持っているアクセス権を取得する。 また、<xref:Microsoft.Crm.Sdk.Messages.RetrieveSharedPrincipalsAndAccessRequest> を使用して、ユーザー所有のビジュアル化に対するアクセス権を持つすべてのセキュリティ プリンシパル (ユーザーまたはチーム) と、そのアクセス権を取得することもできます。  
  
- <xref:Microsoft.Crm.Sdk.Messages.GrantAccessRequest>、<xref:Microsoft.Crm.Sdk.Messages.ModifyAccessRequest>、および <xref:Microsoft.Crm.Sdk.Messages.RevokeAccessRequest> の各メッセージを使用して、ユーザー所有のビジュアル化を特定領域の他のユーザーおよびチームと共有することにより、それらのユーザーおよびチームと共同作業する。  
  
  ユーザー所有のビジュアル化エンティティでサポートされるメッセージの一覧については、「[UserQueryVisualization エンティティ](../common-data-service/reference/entities/userqueryvisualization.md)」を参照してください。

### <a name="see-also"></a>関連項目  
 [グラフ](view-data-with-visualizations-charts.md)   
 [グラフの詳細: 基盤となるデータとグラフ表現](understand-charts-underlying-data-chart-representation.md)   
 [グラフの作成](create-visualization-chart.md)   
 [サンプル グラフ](sample-charts.md)   
 [サンプル: グラフの作成、取得、更新、および削除 (CRUD)](/dynamics365/customer-engagement/developer/customize-dev/sample-create-retrieve-update-delete-chart)  <!--TODO: Need to find the topic in Powerapps repo to link --> 
 [サンプル: エンティティに添付されているすべてのグラフの取得](/dynamics365/customer-engagement/developer/customize-dev/sample-retrieve-all-charts-attached-entity)   <!--TODO: Need to find the topic in Powerapps repo to link -->
 [サンプル: 他のユーザーへのグラフの割り当て](/dynamics365/customer-engagement/developer/customize-dev/sample-assign-chart-another-user)   <!--TODO: Need to find the topic in Powerapps repo to link -->
 [SavedQueryVisualization エンティティ](../common-data-service/reference/entities/savedqueryvisualization.md)   
 [UserQueryVisualization エンティティ](../common-data-service/reference/entities/userqueryvisualization.md)
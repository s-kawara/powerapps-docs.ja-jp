---
title: オフラインと Outlook のフィルターおよびテンプレート (Common Data Service) | Microsoft Docs
description: Common Data Service と Dynamics 365 for Outlook で同期する必要があるデータは、Office Outlook 用データ フィルターで決定されます。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: sriharibs
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="offline-and-outlook-filters-and-templates"></a>オフラインと Outlook のフィルターおよびテンプレート

Office Outlook 用データ フィルターは、Common Data Service と Dynamics 365 for Outlook で同期する必要があるデータを決定します。 Common Data Service は SDK を使用して既定のフィルターを変更し、一部またはすべてのユーザーに対してこの変更を配信する機能をサポートします。  
管理者がフィルター テンプレートを作成して公開するためのコードを作成できます。 これにより、Common Data Service 管理者は、Outlook ストアやオフライン データベースと同期させるための共通のフィルターや目的のフィルターを作成し、ユーザーに公開できます。 また、テンプレートを最初に公開した後でシステムに追加されたユーザー向けに、既定のフィルター テンプレートをカスタマイズして適用することもできます。 管理者は、ユーザー フィルターを公開した後でそのフィルターを更新または削除することもできます。  
これらのカスタマイズをサポートするため、保存済みクエリ (ビュー) 用の新しい 4 つのクエリの種類があります。 保存済みクエリ (ビュー) レコードを作成する場合は、<xref:Microsoft.Crm.Sdk.SavedQueryQueryType> 列挙体を使用して、`SavedQuery.QueryType` 属性でこれらの種類のいずれかを指定します。 これらには、ここで説明するメソッドを使用することによってのみアクセスできます。変更に使用できる UI はありません。 携帯電話の Outlook に対してすべてのデータを同期させることを回避するには、別のフィルターを指定できます。 フィルター テンプレートはソリューションに対応しているため、ソリューションと一緒にエクスポートできます。  
  
 次の表はフィルターとフィルター テンプレートで使用される新しいクエリの種類を示します。  
  
|クエリの種類|説明|  
|----------------|-----------------|  
|<xref:Microsoft.Crm.Sdk.SavedQueryQueryType.OutlookFilters>|Dynamics 365 for Outlook と同期させるエンティティのサブセットを定義します。 これらのフィルターで定義されるデータのサブセットは、取引先担当者、カレンダーなど、 Outlook のフォルダーに同期します。|  
|<xref:Microsoft.Crm.Sdk.SavedQueryQueryType.OfflineFilters>|オフライン アクセス対応 Dynamics 365 for Microsoft Office Outlook と同期させるエンティティのサブセットを定義します。 これらのフィルターで定義されるデータのサブセットは、オフライン データベースに同期します。|  
|<xref:Microsoft.Crm.Sdk.SavedQueryQueryType.OutlookTemplate>|Dynamics 365 for Outlook と同期させるために新しいユーザーに適用するフィルター テンプレートを定義します。|  
|<xref:Microsoft.Crm.Sdk.SavedQueryQueryType.OfflineTemplate>|オフライン アクセス対応 Dynamics 365 for Microsoft Office Outlook と同期させるために新しいユーザーに適用するフィルター テンプレートを定義します。|  
  
## <a name="instantiate-a-filter"></a>フィルターのインスタンスの作成

同期サブスクリプションが作成されると、既定のフィルター テンプレートのインスタンスがユーザーごとに `UserQuery` エンティティに対して自動的に作成されます。 Outlook またはオフライン データベースに対する同期が開始されると、対応するユーザーのフィルターが収集され、それらのフィルターを使用して同期対象のエントリと属性のコレクションがフィルター処理されます。 特定のエントリに対し複数のフィルターが指定されている場合、エントリの結果セットは個々のフィルターの結果を合わせたものになります。  

管理者が他のユーザーのフィルターにアクセスすることを許可する新しい権限 `prvAdminFilter` があります。 これは、Web アプリケーションでは [ユーザー同期フィルターの管理] と呼ばれます。 この権限がないと、ユーザーのフィルターを表示できるのは所有ユーザーのみなので、システム管理者のロールにはこの権限が含まれます。 ユーザー クエリで <xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.RetrieveMultiple*>  メソッドを呼び出したときに、呼び出し側が `prvAdminFilter` 特権を持っていない場合、取得されるのは所有ユーザーのレコードのみとなります。クエリには、`UserId` が呼び出し側と等しくない場合に、`QueryType` が <xref:Microsoft.Crm.Sdk.SavedQueryQueryType.OutlookFilters> または <xref:Microsoft.Crm.Sdk.SavedQueryQueryType.OfflineFilters> に等しく、かつ `OwnerId` が `UserId` に等しいという条件が含まれている必要があります。 その他の条件がクエリに追加されると、これは機能しません。  

新しいユーザーには、`SavedQuery.IsDefault` 属性で既定として指定されているフィルター テンプレートからフィルターが自動的に提供されます。 管理者は、この値を変更するとこの処理に影響する可能性があることを認識する必要があります。 各エンティティに適用できるのは、既定として指定されている 1 つのフィルター テンプレートのみです。 既定のフィルターがなく、フィルター テンプレートのみの場合もあります。 ユーザー定義エンティティを作成し、<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.IsAvailableOffline> プロパティを設定すると、既定のフィルター テンプレートが自動的に作成されます。  

システム フィルターと呼ばれる、管理者が定義できる新しい種類のフィルターがあります。 これらのフィルターは、クエリの種類が <xref:Microsoft.Crm.Sdk.SavedQueryQueryType.OutlookFilters> または <xref:Microsoft.Crm.Sdk.SavedQueryQueryType.OfflineFilters> である `SavedQuery` レコードとして定義されます。 システム フィルターは、すべてのユーザーに自動的に適用されます。ユーザーはこのフィルターを変更できません。  

追加できるフィルターの数には制限があります。 この設定は、ユーザーや管理者がフィルターを作成しすぎてサーバーのパフォーマンスに影響しないように、Common Data Service の展開管理者によって制御されます。 すべてのエンティティに対して同じ制限の設定が適用されます。  

既定では、システム フィルターとユーザー フィルターの両方で無制限に設定されます。  

## <a name="instantiate-a-template"></a>テンプレートのインスタンスの作成

ユーザーごとに 1 つ以上のフィルターのインスタンスを作成できます。 これを手動で行うには、<xref:Microsoft.Crm.Sdk.Messages.InstantiateFiltersRequest> を使用してフィルターのインスタンスを作成し、ユーザー クエリ レコードを作成します。 各ユーザー クエリ レコードには、フィルターへの逆参照が含まれます。 フィルターを更新する場合は、インスタンス作成を再び呼び出して更新するか、フィルター (ユーザー クエリ レコード) に対するユーザーの変更を無効にできます。  
  
## <a name="reset-a-users-filters-to-the-default"></a>ユーザーのフィルターを既定にリセットする

ユーザーのフィルターを既定にリセットするには、<xref:Microsoft.Crm.Sdk.Messages.ResetUserFiltersRequest> を使用します。  
  
### <a name="see-also"></a>関連項目

[Dynamics 365 for Outlook を拡張](extend-dynamics-365-outlook.md)<br />
[SavedQuery エンティティ参照](../reference/entities/savedquery.md)<br />
[サンプル: Outlook フィルターの取得](sample-create-retrieve-outlook-filters.md)<br /> 
<xref:Microsoft.Crm.Sdk.Messages.InstantiateFiltersRequest><br />
<xref:Microsoft.Crm.Sdk.Messages.ResetUserFiltersRequest>
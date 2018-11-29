---
title: アクセス チームと所有者チームを使用して、データを共有し共同作業を行う (アプリ用 Common Data Service) | Microsoft Docs
description: アクセス チームおよび所有者チームを使用して、共同作業したり情報を共有したりします。
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
# <a name="use-access-teams-and-owner-teams-to-collaborate-and-share-information"></a>アクセス チームおよび所有者チームを使用して、共同作業したり情報を共有したりする

*所有者* チームや *アクセス* チームでビジネス オブジェクトを共有し、アプリ用 Common Data Serviceの部署を超えてユーザーと共同作業ができます。 1 つのチームは 1 つの部署に属しますが、他の部署からのユーザーを含めることができます。 一人のユーザーを複数のチームに関連付けることができます。  
  
 所有者チームはレコードを所有し、チームにセキュリティ ロールが割り当てられています。 チームの特権は、セキュリティ ロールによって定義されます。 チームによって得られる特権に加えて、チームのメンバーは個々のセキュリティ ロールによって定義される特権と、メンバーとなっている他のチームの役割によって定義される特権を所有します。 チームは、チームが所有するレコードに対するフル アクセス権を所有しています。  
  
> [!NOTE]
>  チームはユーザー グループへのアクセスを提供しますが、ユーザー所有レコードを作成、更新、または削除するために必要な特権を付与するセキュリティ ロールと個々のユーザーを関連付ける必要があります。 これらの特権は、セキュリティ ロールをチームに割り当て、ユーザーをそのチームに追加することでは適用できません。  
  
 アクセス チームは独自のレコードを所有していないし、チームにセキュリティ ロールが割り当てられていません。 チームのメンバーは、個々のセキュリティ ロールによって定義される特権と、メンバーとなっているチームのロールによって定義される特権を所有します。 レコードはアクセス チームで共有され、チームには、そのレコードに対する読み取り、書き込み、または追加などのアクセス権が付与されます。  
  
 チームの機能は `Team` エンティティと `TeamTemplate` エンティティでサポートされます。 `Team` エンティティを使用して、所有者のチームおよびユーザー作成アクセス チームを作成します。 自動作成のアクセス チームの場合、`Team` エンティティと`TeamTemplate` エンティティが使用されます。  
  
<a name="BKMK_OwnerAccess"></a>   
## <a name="owner-team-or-access-team"></a>所有者チームまたはアクセス チームか。  
 チームの種類の選択は、目的、プロジェクトの特性、および組織の規模に依存する場合があります。 チームの種類の選択に使用できるガイドラインが少しあります。  
  
### <a name="when-to-use-owner-teams"></a>所有者のチームを使用するとき  
  
- 会社のビジネス ポリシーにより、ユーザー以外のエンティティで所有されるレコードが必要です。  
  
- アプリ用 CDS システムの設計時にチームの数を知ることができます。  
  
- 所有チームによる進行状況に関する日時レポートが必要です。  
  
### <a name="when-to-use-access-teams"></a>アクセス チームを使用するとき  
  
- チームは動的に形成されて解散されます。 通常これは、確立した担当地域、製品またはボリュームなどの、チームを定義する明確な基準が提供されない場合に発生します。  
  
- アプリ用 CDS システムの設計時にチームの数を知ることができません。  
  
- チーム メンバーにはレコードに対する別個のアクセス権が必要です。 複数のアクセス チームでレコードを共有でき、各チームにレコードに対する異なるアクセス権を提供できます。 たとえば、あるチームには取引先企業に対する読み取り専用アクセス権が与えられ、他のチームには同じ取引先企業に対する読み取り、書き込み、および共有アクセス権が与えられます。  
  
- レコードに対する所有権がなくても、固有の一連のユーザーは単一レコードに対するアクセスが必要です。  
  
> [!NOTE]
>  別の種類の "アクセス チーム" は、Web アプリケーションで使用されるアクセス チーム テンプレートによって対応します。 これは変更が頻繁に行われるチームの種類であり、これには特定の取引先企業レコードの営業チームなどが含まれます。 ユーザーが取引先企業内の営業チームに追加されると、Web アプリケーションが、裏で、このレコードに固有チームを作成し、ユーザーをそのチームに追加します。  
>   
>  この種類のアクセス チームについては、このトピックでは取り扱っていません。  
  
<a name="BKMK_SettingUp"></a>   
## <a name="setting-up-teams"></a>チームの設定  
 所有者およびアクセス チームの種類に加え、アクセス チームではさらに、ユーザーによる作成エンティティまたは自動作成 (システムで管理された) チームの 2 つに細分されます。 セットアップ情報は各チームの種類に固有のものになります。  
  
### <a name="owner-team"></a>所有者チーム  
 所有者チームは 1 つまたは複数のレコードを所有できます。 所有者チームを作成するには、`Team` エンティティを使用して、`Team.TeamType` 属性を `Owner` に設定します。 `TeamType` 値の一覧については、`Team` エンティティのメタデータを参照してください。  
  
> [!NOTE]
> 組織のエンティティ メタデータを表示するには、メタデータ ブラウザー ソリューションをインストールしてください。メタデータ ブラウザー ソリューションについては、「[組織のメタデータの参照](/dynamics365/customer-engagement/developer/browse-your-metadata)」を参照してください。 「[エンティティ参照](/dynamics365/customer-engagement/developer/about-entity-reference)」でエンティティの参照ドキュメントを参照することもできます。 
  
 チームをレコードの所有者にするには、レコードをチームに割り当てる必要があります。 割り当てるには、<xref:Microsoft.Crm.Sdk.Messages.AssignRequest> メッセージを使用します。 所有者チームにレコードを一括で割り当てるには、<xref:Microsoft.Crm.Sdk.Messages.ReassignObjectsOwnerRequest> メッセージまたは <xref:Microsoft.Crm.Sdk.Messages.ReassignObjectsSystemUserRequest> メッセージを使用します。  
  
 チームが所有するレコードでは <xref:Microsoft.Xrm.Sdk.Metadata.OwnershipTypes> プロパティを <xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.OwnershipType>.`TeamOwned` に設定する必要があります。  
  
 所有者のチームがレコードを所有せず、チームに割り当てられるセキュリティ ロールがない場合、<xref:Microsoft.Crm.Sdk.Messages.ConvertOwnerTeamToAccessTeamRequest> メッセージを使用してアクセス チームに変換できます。 この変換は一方向です。 アクセス チームを所有者のチームに変換し直すことはできません。 変換中、チームに関連付けられたすべてのキューとメールボックスが削除されます。  
  
 チームのメンバーを追加または削除するには、<xref:Microsoft.Crm.Sdk.Messages.AddMembersTeamRequest> メッセージおよび <xref:Microsoft.Crm.Sdk.Messages.RemoveMembersTeamRequest> メッセージを使用します。  
  
### <a name="user-created-access-team"></a>ユーザー定義アクセス チーム  
 複数のレコードを、ユーザー作成のアクセス チームと共有できます。 アクセス チームを作成するには、チーム エンティティを使用して `Team.TeamType` 属性を `Access` に設定します。 `TeamType` 値の一覧については、`Team` エンティティのメタデータを参照してください。 この情報は、組織のメタデータ内にあります。 前述のメタデータ ブラウザー情報を確認してください。  
  
 レコードをユーザー定義のアクセス チームと共有するには、<xref:Microsoft.Crm.Sdk.Messages.GrantAccessRequest> メッセージを使用します。 ユーザー定義チームの場合、`Team.SystemManaged` 属性は `false` です。 `Team.SystemManaged` 値の一覧については、`Team` エンティティのメタデータを参照してください。 この情報は、組織のメタデータ内にあります。 前述のメタデータ ブラウザー情報を確認してください。  
  
 チームのメンバーを追加または削除するには、<xref:Microsoft.Crm.Sdk.Messages.AddMembersTeamRequest> メッセージおよび <xref:Microsoft.Crm.Sdk.Messages.RemoveMembersTeamRequest> メッセージを使用します。  
  
 チーム メンバー別にレコードへのアクセス権を付与するには、複数のチームを作成し、各チームにレコードに対する異なるアクセス権のセットを付与します。  
  
### <a name="auto-created-system-managed-access-team"></a>自動作成された (システム管理) のアクセス チーム  
 自動作成された (システム管理された) チームは特定のレコードについて作成され、他のレコードをこのチームで共有することはできません。 システム管理チームでは、チーム テンプレートを用意する必要があります。 テンプレートを作成するには、チーム テンプレート エンティティを使用します。 このテンプレートで、チーム作成時に、エンティティの種類と、チームのユーザーに付与するエンティティ レコードに対するアクセス権 (読み取りや書き込みなど) を定義します。 テンプレートで指定するエンティティは、自動作成したアクセス チームで有効にする必要があります。 そのレコードに対し異なるアクセス権をチーム メンバーに与えるには、複数のチーム テンプレートを作成します。 たとえば、取引先企業エンティティでは、レコードを参照する必要のみがあるチーム用の読み取りアクセス権を 1 つのテンプレートに関連付けます。 2 番目のテンプレートに読み取り、書き込み、共有アクセス権を付与し、同じレコードにより多くのアクセス権が必要なチーム向けにします。  
  
 自動作成されたアクセス チームのエンティティを有効にするには、<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.AutoCreateAccessTeams> 属性を `true` に設定します。  
  
 エンティティに対して作成できるチーム テンプレートの最大数は <xref:Microsoft.Xrm.Sdk.Deployment.TeamSettings.MaxAutoCreatedAccessTeamsPerEntity> 展開設定で指定されます。 既定値は 2 です。 自動作成のアクセス チームに対して有効にできるエンティティの最大数は、<xref:Microsoft.Xrm.Sdk.Deployment.TeamSettings.MaxEntitiesEnabledForAutoCreatedAccessTeams> 展開設定で指定されます。 既定値は 5 です。 詳細: [展開エンティティおよび展開構成の設定](https://msdn.microsoft.com/library/gg328063.aspx) および [Windows PowerShell を使用した展開の管理](https://technet.microsoft.com/library/dn531202.aspx)  
  
 <xref:Microsoft.Crm.Sdk.Messages.AddUserToRecordTeamRequest> メッセージおよび <xref:Microsoft.Crm.Sdk.Messages.RemoveUserFromRecordTeamRequest> メッセージを使用して、特定のレコードにおけるユーザーを追加または削除すると、ユーザーはシステム管理チームで自動的に追加および削除されます。 最初のユーザーをレコードに追加してチーム ID が<xref:Microsoft.Crm.Sdk.Messages.AddUserToRecordTeamResponse.AccessTeamId> で返されると、実際のアクセス チームが作成されます。 このチームの `Team.SystemManaged` 属性は `true` に設定されます。 `Team.SystemManaged` 値の一覧については、`Team` エンティティのメタデータを参照してください。 この情報は、組織のメタデータ内にあります。 前述のメタデータ ブラウザー情報を確認してください。  メッセージの発信者はエンティティの共有特権および、テンプレートのアクセス権と一致するレコードのアクセス権を持っている必要があります。 たとえば、テンプレートで読み取りアクセス権限が指定されている場合、呼び出し元ユーザーはレコードの読み取りアクセス権が必要です。 チームに追加するため、テンプレートで指定する必要がある最小限のアクセス レベルは、基本的な (ユーザー) 読み取り権限です。  
  
 チーム テンプレートとシステム管理アクセス チーム間の親子関係のため、テンプレートを削除すると、テンプレートに関連付けられたすべてのチームは伝播規則に従い削除されます。  
  
 チーム テンプレートのアクセス権を変更する場合、この変更は、新しい自動作成アクセス チームにのみ適用されます。 既存のチームは影響を受けません。  
  
<a name="BKMK_ShortSummary"></a>   
## <a name="quick-reference-to-teams"></a>チームへのクイック リファレンス  
 次の情報を、利用できるチームのクイック リファレンスとして使用します。  
  
|チーム |使用すべきとき|使用する必要があるエンティティはどれか。|チーム テンプレートを使用するか。|チーム メンバーの追加または削除に使用するメッセージ。|レコードを所有しているか。|所有レコード数または、レコードのアクセス権があるか。|セキュリティ ロールを割り当て済みか。|  
|----------|------------------|-------------------------|------------------------|---------------------------------------------------------|-------------------|---------------------------------------------|----------------------------------|  
|所有者 |チームによるレコードの所有権が必要です。<br /><br /> チーム数は設計段階で分かります。|`Team`|いいえ|<xref:Microsoft.Crm.Sdk.Messages.AddMembersTeamRequest> <br /> <xref:Microsoft.Crm.Sdk.Messages.RemoveMembersTeamRequest>。|はい|複数のレコードを所有できます。|はい|  
|アクセス、ユーザー作成|複数レコードをチームで共有する必要があります。<br /><br /> チーム数は設計段階では分かりません。<br /><br /> チーム メンバーにはレコードに対する別個のアクセス権が必要です。|`Team`|いいえ|<xref:Microsoft.Crm.Sdk.Messages.AddMembersTeamRequest> <br /> <xref:Microsoft.Crm.Sdk.Messages.RemoveMembersTeamRequest>|いいえ|複数のレコードにアクセスできます。|番号 レコードに対するアクセス権を付与します。|  
|アクセス、自動作成された (システム管理)|ユーザーの一意のセットは 1 つのレコードに対応します。<br /><br /> チーム メンバーにはレコードに対する別個のアクセス権が必要です。<br /><br /> レコードごとにチームを自動作成することをお勧めします。|`TeamTemplate`<br /><br /> `Team`|はい|<xref:Microsoft.Crm.Sdk.Messages.AddUserToRecordTeamRequest> <br /> <xref:Microsoft.Crm.Sdk.Messages.RemoveUserFromRecordTeamRequest>|いいえ|1 レコードのみアクセスできます。|番号 レコードに対するアクセス権を付与します。|  
  
> [!NOTE]
>  所有者チームとアクセス チームでは、レコードおよび、取引先企業とその取引先企業に関連するすべての営業案件などの関連するレコードにアクセス権が付与されます。 レコード間の上位関係では、伝播規則が適用されます。 所有チームに対しては、ユーザーに割り当てられている役割に加えて、そのユーザーが属するチームに割り当てられている役割に基づいてエンティティにアクセスできます。 これにより、ユーザーは部署の外部に特権を持つことができます。 詳細: [エンティティ関係の動作](/dynamics365/customer-engagement/developer/entity-relationship-behavior)  
> 
> [!NOTE]
>  ユーザーは、アクセス チームに参加するために十分な特権が必要です。 たとえば、アクセス チームに取引先企業の削除アクセス権がある場合、このチームに参加するために、ユーザーに取引先企業エンティティの削除特権が必要です。 特権が十分でないユーザーを追加しようとすると、エラー メッセージ "You can’t add the user to the access team because the user doesn’t have sufficient privileges on the entity. (ユーザーにエンティティに対して十分な特権がないため、ユーザーをアクセス チームに追加できません。)" が表示されます。  
  
### <a name="see-also"></a>関連項目  
 [サンプル: アクセス チームを使用してレコードを共有](org-service/samples/share-record-using-access-team.md)   
 [チームの管理](https://technet.microsoft.com/library/dn531089.aspx)   
 [ホワイトペーパー: Microsoft Dynamics CRM 2013 を使用するアクセス チーム](http://download.microsoft.com/download/E/9/0/E9009308-CA01-4B37-B03C-435B8ACB49B4/Access%20Teams%20with%20Microsoft%20Dynamics%20CRM%202013.pdf)   
 [ホワイトペーパー: Microsoft Dynamics CRM による拡張できるセキュリティ モデリング](http://go.microsoft.com/fwlink/p/?LinkID=328757)   
 [ユーザーとチームのエンティティ](user-team-entities.md)   
 [チーム エンティティ](reference/entities/team.md)   
 [チーム テンプレート エンティティ](reference/entities/teamtemplate.md)   
 [Windows PowerShell を使用した展開の管理](https://technet.microsoft.com/library/dn531202.aspx)   
 [レコード ベースのセキュリティを使用してレコードへのアクセスをコントロールする](/dynamics365/customer-engagement/developer/security-dev/use-record-based-security-control-access-records)   
 [ロールベースのセキュリティを使用して Dynamics 365 におけるエンティティへのアクセスを制御する方法](/dynamics365/customer-engagement/developer/security-dev/how-role-based-security-control-access-entities)   
 [カスケード動作](/dynamics365/customer-engagement/developer/entity-relationship-behavior#BKMK_CascadingBehavior)

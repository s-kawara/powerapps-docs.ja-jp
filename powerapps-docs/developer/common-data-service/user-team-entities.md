---
title: ユーザーとチームのエンティティ (Common Data Service for Apps) | Microsoft Docs
description: ユーザー アカウントとプロファイルを作成および管理できるユーザーおよびチーム管理について説明します。
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
# <a name="user-and-team-entities"></a>ユーザーとチームのエンティティ

ユーザーおよびチーム管理は、ユーザー アカウントとプロファイルを作成および管理できるアプリ用 CDS の領域です。  

 *ユーザー*とは、アプリ用 CDS を使用し、各部署の作業を行う個人を指します。 各ユーザーにはユーザー アカウントがあります。 すべてのユーザーはそれぞれ 1 つの部署にのみ関連付けることができます。 この関連付けにより、ユーザーがアクセスできる顧客データを制御します。 ユーザー アカウントには、ユーザーの電話番号、電子メール アドレス、ユーザーの上司へのリンクなどの情報が含まれます。 各ユーザーには、各自の個人設定を管理するための特権と権限があります。 各ユーザーは、その組織の Azure Active Directory のユーザーと対応しています。 ユーザーを作成する際には、そのユーザーに少なくとも 1 つのセキュリティ ロールを割り当てる必要があります。 ユーザーがロールを割り当てられたチームのメンバーであっても、ユーザーにはロールを割り当てる必要があります。 アクセス レベルおよびロールの詳細については、「[ロールベースのセキュリティを使用して Dynamics 365 におけるエンティティへのアクセスを制御する方法](/dynamics365/customer-engagement/developer/security-dev/how-role-based-security-control-access-entities)」を参照してください。  

 *チーム* はユーザーのグループです。 チームにより、組織内のユーザーを連携し、情報を共有します。 チームの詳細については、「[共同作業と情報を共有するためにチームを使用する](use-access-teams-owner-teams-collaborate-share-information.md)」を参照してください。  

 レコードはユーザーまたはチーム単位で所有することができます。 <xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.OwnershipType> を <xref:Microsoft.Xrm.Sdk.Metadata.OwnershipTypes>.`UserOwned`  または <xref:Microsoft.Xrm.Sdk.Metadata.OwnershipTypes>.`TeamOwned`  に設定し、所有権を有効にします。 <xref:Microsoft.Crm.Sdk.Messages.ReassignObjectsOwnerRequest> メッセージまたは <xref:Microsoft.Crm.Sdk.Messages.ReassignObjectsSystemUserRequest> メッセージを使用して、所有者のすべてのレコードの一括再割り当てを実行できます。  

 次の図は、ユーザーとチームのエンティティ関係を示しています。  

 ![ユーザーとチームのエンティティの関連付けの図](media/crm-v5s-em-userteam.gif "ユーザーとチームのエンティティの関連付けの図")  

## <a name="users"></a>ユーザー  
 アプリ用 CDS では、ユーザーを無効化することはできますが、削除することはできません。 現在ログオンしているユーザーまたは偽装しているユーザーを調べるには、<xref:Microsoft.Crm.Sdk.Messages.WhoAmIRequest> メッセージを呼び出します。  

 次の表に、システム ユーザー エンティティの重要な属性についての詳細を示します。  


|   属性名    |                                                                                                                                                                                                                                                                                                                              内容                                                                                                                                                                                                                                                                                                                              |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     AccessMode      | このユーザーのアプリ用 CDS へのアクセスの種類を示します。 ユーザーの種類と呼ぶこともあります。<br /><br /> -   管理: [設定] 領域にアクセスできますが、[営業]、[マーケティング]、および [サービス] の領域にはアクセスできません。<br />-   非対話型: Web サービスからのみシステムにアクセスできます。<br />-   読み取り: 読み取り専用アクセスが許可されます。<br />-   読み取り/書き込み: 読み取りと書き込みの両方のアクセスが許可されます。<br />-   サポート ユーザー: アプリ用 CDS サポート チームによって作成されたユーザーです。 |
|       CalType       |                                                               ユーザーのライセンスの種類を示します。<br /><br /> -   管理: 管理ユーザー権限が付与されます。<br />-   デバイス フル: 読み取りと書き込みの両方のアクセスが、アプリ用 CDS を実行しているデバイスを使用するユーザーに許可されます。<br />-   デバイス制限あり: 読み取り専用アクセスが、アプリ用 CDS を実行しているデバイスを使用するユーザーに許可されます。<br />-   フル: 読み取りと書き込みの両方のアクセスが許可されます。<br />-   制限あり: 読み取り専用アクセスが許可されます。                                                                |
|     IsDisabled      |                                                                                                                                                                                                                                             ユーザーが無効になっているかどうかを示します。 有効にできるのは、ライセンスされているユーザーと、アクセス モードがサポートまたは非対話型のユーザーだけです。 サポート ユーザーを無効にすることはできません。                                                                                                                                                                                                                                              |
|     IsLicensed      |                                                                                                                                                                             ユーザーがライセンスされているかどうかを示します。 これは、Microsoft Online Services Environment でアプリ用 CDS にアクセスする顧客に適用されます。 この属性は読み取り専用であり、自動的に更新されます。                                                                                                                                                                              |
| IsSyncWithDirectory |                                                                                                                                 ユーザーが Office 365 のディレクトリと同期されているかどうかを示します。 これは、Microsoft Online Services Environment でアプリ用 CDS にアクセスする顧客に適用されます。 この属性は作成時にのみ設定が可能で、それ以降は読み取り専用です。                                                                                                                                 |
|       QueueId       |                                                                                                                                                                                                                                                                                                               ユーザーの既定のキューを示します。                                                                                                                                                                                                                                                                                                               |

 アクセス チェックを付加的に使用できます。 ユーザーに割り当てられている役割に加えて、そのユーザーが属するチームに割り当てられている役割に基づいてエンティティにアクセスできます。 これにより、ユーザーは部署の外部に特権を持つことができます。  

> [!NOTE]
>  ユーザーの特権セットは、ユーザーの役割による特権と、ユーザーが属するすべてのチームの役割による特権を合わせたものになります。  


 非対話型ユーザーは、1 つのライセンスで済むため、サービス間のコードを記述する場合によく使用されます。 アプリ用 CDS では 5 人の非対話型ユーザーが無料で使用することができます。 非対話型ユーザーを無効にするには、ユーザー レコードを更新して、`accessmode` の値を他のいずれかの値に変更します。 これにより、ユーザーが自動的に無効になります。

## <a name="community-tools"></a>コミュニティ ツール

**ユーザー設定ユーティリティ**は、アプリ用 CDS 向けに XrmToolbox コミュニティが開発したツールです。 コミュニティ開発ツールのトピック、[開発者ツール](developer-tools.md) を参照してください。

> [!NOTE]
> コミュニティ ツールはアプリ用 CDS の製品ではなく、コミュニティ ツールに対するサポートは提供されません。
> このツールに関するご質問は、その発行元にお問い合わせください。 詳細: [XrmToolBox](https://www.xrmtoolbox.com)。

### <a name="see-also"></a>関連項目  
 [管理およびセキュリティ エンティティ](/dynamics365/customer-engagement/developer/administration-security-entities)   
 [共同作業と情報を共有するためにチームを使用する](use-access-teams-owner-teams-collaborate-share-information.md)   
 [チーム エンティティ](reference/entities/team.md)   
 [ユーザーのタイム ゾーンの設定](specify-time-zone-settings-user.md)   
 [チーム テンプレート エンティティ](reference/entities/teamtemplate.md)   
 [SystemUser エンティティ](reference/entities/systemuser.md)   
 [UserSettings エンティティ](reference/entities/usersettings.md)   
 [サンプル: ユーザーを無効にする](/dynamics365/customer-engagement/developer/sample-disable-user)   
 [サンプル: GrantAccess、ModifyAccess、および RevokeAccess メッセージを使用したレコードの共有](org-service/samples/share-records-using-grantaccess-modifyaccess-revokeaccess-messages.md)   
 [サンプル: アクセス チームを使用してレコードを共有](org-service/samples/share-record-using-access-team.md)   
 [ブログ: Service Accounts – Non-Interactive Users (サービス アカウント – 非対話型ユーザー)](http://go.microsoft.com/fwlink/p/?LinkId=234350)   
 [特権およびロール エンティティ](/dynamics365/customer-engagement/developer/privilege-role-entities)

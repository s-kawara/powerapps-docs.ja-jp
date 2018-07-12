---
title: データ主体の権利 (DSR) による PowerApps 顧客データ エクスポート要求への応答 | Microsoft Docs
description: データ主体の権利 (DSR) による PowerApps 顧客データのエクスポート要求に応答する方法を説明します。
author: jamesol-msft
manager: kfile
ms.service: powerapps
ms.component: pa-admin
ms.topic: conceptual
ms.date: 05/23/2018
ms.author: jamesol
ms.openlocfilehash: 8eb651bcd4ad9320dc8995864249f619bb76ab77
ms.sourcegitcommit: 79b8842fb0f766a0476dae9a537a342c8d81d3b3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/07/2018
ms.locfileid: "37896859"
---
# <a name="responding-to-data-subject-rights-dsr-requests-to-export-powerapps-customer-data"></a>データ主体の権利 (DSR) による PowerApps 顧客データ エクスポート要求への応答
"データ ポータビリティの権利" では、データ主体は別のデータのコントローラーに送信できる電子形式 (つまり、構造化された、一般的に使用される、マシンが読み取り可能で相互運用可能な形式) で、個人データのコピーを要求できます。

* Web サイト アクセス: [PowerApps ポータル](https://web.powerapps.com)、[PowerApps 管理センター](https://admin.powerapps.com/)、[Office 365 Service Trust Portal](https://servicetrust.microsoft.com/)

* PowerShell アクセス: PowerApps [アプリ作成者コマンドレット](https://go.microsoft.com/fwlink/?linkid=871448)、[管理者コマンドレット](https://go.microsoft.com/fwlink/?linkid=871804)、および[オンプレミス ゲートウェイ コマンドレット](https://go.microsoft.com/fwlink/?linkid=872238)

PowerApps が特定のユーザーについて格納できる個人データの種類と、個人データの検索とエクスポートに使用できるエクスペリエンスの概要を以下に示します。

個人データが含まれるリソース | Web サイト アクセス |   PowerShell アクセス
--- | --- | --
環境 | PowerApps 管理センター |  PowerApps コマンドレット
環境のアクセス許可**   | PowerApps 管理センター    | PowerApps コマンドレット
キャンバス アプリ  | PowerApps 管理センター <br> PowerApps ポータル |    PowerApps コマンドレット
キャンバス アプリのアクセス許可  | PowerApps 管理センター <br> PowerApps ポータル  | PowerApps コマンドレット
ゲートウェイ | PowerApps ポータル***   | オンプレミス ゲートウェイ コマンドレット
ゲートウェイのアクセス許可 | PowerApps ポータル***   |
カスタム コネクタ | |    アプリ作成者: 使用可能 <br> 管理者: 使用可能
カスタム コネクタのアクセス許可 | |    アプリ作成者: 使用可能 <br> 管理者: 使用可能
接続 | | アプリ作成者: 使用可能 <br> 管理者: 使用可能
接続のアクセス許可  | | アプリ作成者: 使用可能 <br> 管理者: 使用可能
PowerApps のユーザー設定、ユーザー アプリの設定、通知 | | アプリ作成者: 使用可能 <br> 管理者: 使用可能

> ** Common Data Service for Apps (CDS) の導入により、環境内にデータベースを作成した場合、環境のアクセス許可とモデル駆動型アプリのアクセス許可は、CDS for Apps データベース インスタンス内のレコードとして格納されます。 CDS for Apps を使うユーザーに関する DSR 要求に応答する方法のガイダンスについては、「[Common Data Service for Apps での顧客データのデータ主体の権利 (DSR) 要求に対する対応](common-data-service-gdpr-dsr-guide.md)」をご覧ください。
> 
> *** 管理者は、リソースの所有者が明示的にアクセスを許可している場合にのみ、[PowerApps ポータル](https://web.powerapps.com)からこれらのリソースにアクセスできます。 管理者がアクセスを許可されていない場合は、[PowerApps 管理者 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871804)を利用する必要があります。

## <a name="prerequisites"></a>前提条件

### <a name="for-users"></a>ユーザーの場合
PowerApps の有効なライセンスを持つユーザーは、[PowerApps ポータル](https://web.powerapps.com)または[アプリ作成者用コマンドレット](https://go.microsoft.com/fwlink/?linkid=871448)を使って、このドキュメントに記載されているユーザー操作を実行できます。

### <a name="for-admins"></a>管理者の場合
PowerApps 管理センター、Microsoft Flow 管理センター、または [PowerApps 管理者 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871804)を使って、このドキュメントに記載されている管理操作を実行するには、次のものが必要です。

* 有料の PowerApps プラン 2 ライセンスまたは PowerApps プラン 2 無料試用版ライセンス。 [http://web.powerapps.com/trial](http://web.powerapps.com/trial) で、30 日間有効な無料試用版ライセンスにサインアップできます。 無料試用版ライセンスの有効期限が切れた場合は更新できます。

* 別のユーザーのリソースを検索する必要がある場合は、[Office 365 全体管理者](https://support.office.com/article/assign-admin-roles-in-office-365-for-business-eac4d046-1afd-4f1a-85fc-8219c79e1504)または [Azure Active Directory 全体管理者](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal)のアクセス許可 (環境管理者は、自分がアクセス許可を持っている環境および環境リソースにのみアクセスできることに注意してください)。

## <a name="step-1-export-personal-data-contained-within-environments-created-by-the-user"></a>ステップ 1: ユーザーによって作成された環境に含まれる個人データをエクスポートする

### <a name="powerapps-admin-center"></a>PowerApps 管理センター
管理者は、[PowerApps 管理センター](https://admin.powerapps.com/)で次の手順に従って、特定のユーザーによって作成されたすべての環境をエクスポートできます。

1. [PowerApps 管理センター](https://admin.powerapps.com/)で、組織内の各環境を選択します。

    ![管理センター ランディング ページ](./media/powerapps-gdpr-export-dsr/admin-center-landing.png)

2. 環境が DSR 要求からユーザーによって作成された場合は、**[詳細]** ページに移動し、詳細をコピーして、Microsoft Word などのドキュメント エディターに貼り付けます。

    ![環境の詳細](./media/powerapps-gdpr-export-dsr/environment-details.png)

### <a name="powershell-cmdlets-for-app-creators"></a>アプリ作成者用の PowerShell コマンドレット
ユーザーは、[PowerApps アプリ作成者 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871448)の **Get-PowerAppsEnvironment** 機能を使って、PowerApps 内でアクセス権のある環境をエクスポートできます。

~~~~
Add-PowerAppsAccount
Get-PowerAppsEnvironment | ConvertTo-Json | Out-File -FilePath "UserDetails.json"
~~~~

### <a name="powershell-cmdlets-for-admins"></a>管理者用の PowerShell コマンドレット
管理者は、[PowerApps 管理者 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871804)の **Get-AdminEnvironment** 機能を使って、ユーザーによって作成されたすべての環境をエクスポートできます。

~~~~
Add-PowerAppsAccount
$userId = "7557f390-5f70-4c93-8bc4-8c2faabd2ca0"
Get-AdminEnvironment -CreatedBy $userId | ConvertTo-Json | Out-File -FilePath "UserDetails.json"
~~~~
 
## <a name="step-2-export-the-users-environment-permissions"></a>ステップ 2: ユーザーの環境のアクセス許可をエクスポートする
ユーザーには環境内のアクセス許可 (環境管理者、環境作成者など) を割り当てることができ、アクセス許可は "*ロール割り当て*" として PowerApps に格納されます。 CDS for Apps の導入により、環境内にデータベースを作成した場合、ロールの割り当ては CDS for Apps データベース インスタンス内のレコードとして格納されます。 詳しくは、「[PowerApps での環境の管理](environments-administration.md)」をご覧ください。

### <a name="for-environments-without-a-cds-for-apps-database"></a>CDS for Apps データベースがない環境の場合

#### <a name="powerapps-admin-center"></a>PowerApps 管理センター
管理者は、次の手順に従って、[PowerApps 管理センター](https://admin.powerapps.com/)からユーザーの環境のアクセス許可をエクスポートできます。

1. [PowerApps 管理センター](https://admin.powerapps.com/)で、組織内の各環境を選択します。 組織内で作成されたすべての環境を確認するには、[Office 365 全体管理者](https://support.office.com/article/assign-admin-roles-in-office-365-for-business-eac4d046-1afd-4f1a-85fc-8219c79e1504)または [Azure Active Directory 全体管理者](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal)である必要があります。

    ![管理センター ランディング ページ](./media/powerapps-gdpr-export-dsr/admin-center-landing.png)

2. **[セキュリティ]** を選択します。

    環境に CDS For Apps データベースがない場合は、**[環境ロール]** のセクションが表示されます。

3. **[環境管理者]** と **[環境作成者]** の両方を個別に選択し、検索バーを使って、ユーザーの名前を検索します。

    ![[環境ロール] ページ](./media/powerapps-gdpr-export-dsr/admin-environment-role-share-page.png)

4. ユーザーにいずれかのロールへのアクセス権がある場合、**[ユーザー]** ページに移動し、詳細をコピーして、Microsoft Word などのドキュメント エディターに貼り付けます。

#### <a name="powershell-cmdlets-for-admins"></a>管理者用の PowerShell コマンドレット
管理者は、[PowerApps 管理者PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871804)の **Get-AdminEnvironmentRoleAssignment** 機能を使って、CDS for Apps データベースがないすべての環境でのユーザーに対するすべての環境ロール割り当てをエクスポートすることができます。

~~~~
Add-PowerAppsAccount
$userId = "0ecb1fcc-6782-4e46-a4c4-738c1d3accea"
Get-AdminEnvironmentRoleAssignment -UserId $userId | ConvertTo-Json | Out-File -FilePath "UserDetails.json"
~~~~

> [!IMPORTANT]
>  この機能は、CDS for Apps データベース インスタンスが存在しない環境においてのみ動作します。
>
>

### <a name="for-environments-with-a-cds-for-apps-database"></a>CDS for Apps データベースがある環境の場合
CDS for Apps の導入により、環境内にデータベースを作成した場合、ロール割り当ては、CDS for Apps データベース インスタンス内のレコードとして格納されます。 CDS for Apps データベース インスタンスから個人データを削除する方法については、[Common Data Service ユーザーの個人データの削除](https://go.microsoft.com/fwlink/?linkid=871886)に関するページをご覧ください。
 
## <a name="step-3-export-personal-data-contained-within-canvas-apps-created-by-the-user"></a>ステップ 3: ユーザーによって作成されたキャンバス アプリに含まれる個人データをエクスポートする

### <a name="powerapps-portal"></a>PowerApps ポータル
ユーザーは [PowerApps ポータル](https://web.powerapps.com)からアプリをエクスポートできます。 アプリをエクスポートする詳しい手順については、「[アプリのエクスポート](environment-and-tenant-migration.md#exporting-an-app)」をご覧ください。

### <a name="powerapps-admin-center"></a>PowerApps 管理センター
管理者は、[PowerApps 管理センター](https://admin.powerapps.com/)で次の手順に従って、ユーザーによって作成されたアプリをエクスポートできます。

1. [PowerApps 管理センター](https://admin.powerapps.com/)で、組織内の各環境を選択します。 組織内で作成されたすべての環境を確認するには、[Office 365 全体管理者](https://support.office.com/article/assign-admin-roles-in-office-365-for-business-eac4d046-1afd-4f1a-85fc-8219c79e1504)または [Azure Active Directory 全体管理者](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal)である必要があります。

    ![管理センター ランディング ページ](./media/powerapps-gdpr-export-dsr/admin-center-landing.png)

2. **[リソース]** を選んでから、**[アプリ]** を選びます。

3. 検索バーを使って、ユーザーの名前を検索します。そのユーザーがこの環境内で作成したすべてのアプリが表示されます。

    ![アプリの検索](./media/powerapps-gdpr-export-dsr/search-apps.png)

4. そのユーザーによって作成された各アプリの **[共有]** を選び、自分自身にアプリへの **[編集可能]** アクセス権を付与します。

    ![アプリの共有を選択する](./media/powerapps-gdpr-export-dsr/select-share.png)

    ![ユーザーにアクセス権を付与する](./media/powerapps-gdpr-export-dsr/grant-access.png)

5. ユーザーの各アプリへのアクセス権が付与されると、[PowerApps ポータル](https://web.powerapps.com)からアプリをエクスポートできます。 アプリをエクスポートする詳しい手順については、「[アプリのエクスポート](environment-and-tenant-migration.md#exporting-an-app)」をご覧ください。

### <a name="powershell-cmdlets-for-admins"></a>管理者用の PowerShell コマンドレット
管理者は、[PowerApps 管理者 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871804)の **Get-AdminApp** 機能を使って、ユーザーによって作成されたアプリをエクスポートできます。

~~~~
Add-PowerAppsAccount
$userId = "0ecb1fcc-6782-4e46-a4c4-738c1d3accea"
Get-AdminApp -Owner $userId | ConvertTo-Json | Out-File -FilePath "UserDetails.json"
~~~~

## <a name="step-4-export-the-users-permissions-to-canvas-apps"></a>ステップ 4: キャンバス アプリに対するユーザーのアクセス許可をエクスポートする
アプリがユーザーと共有されるたびに、PowerApps はアプリケーションに対するユーザーのアクセス許可 (CanEdit または CanUser) が記述されている "*ロール割り当て*" と呼ばれるレコードを格納します。 詳しくは、「[アプリを共有する](../maker/canvas-apps/share-app.md#share-an-app)」をご覧ください。

### <a name="powershell-cmdlets-for-app-creators"></a>アプリ作成者用の PowerShell コマンドレット
ユーザーは、[PowerApps アプリ作成者 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871448)の **Get-RoleAssignment** 機能を使って、自分がアクセス権を持っているすべてのアプリに対するアプリ ロール割り当てをエクスポートできます。

~~~~
Add-PowerAppsAccount
Get-AppRoleAssignment | ConvertTo-Json | Out-File -FilePath "UserDetails.json"
~~~~

### <a name="powerapps-admin-center"></a>PowerApps 管理センター
管理者は、次の手順に従って [PowerApps 管理センター](https://admin.powerapps.com/)から、ユーザーに対するアプリ ロール割り当てをエクスポートできます。

1. [PowerApps 管理センター](https://admin.powerapps.com/)で、組織内の各環境を選択します。 組織内で作成されたすべての環境を確認するには、[Office 365 全体管理者](https://support.office.com/article/assign-admin-roles-in-office-365-for-business-eac4d046-1afd-4f1a-85fc-8219c79e1504)または [Azure Active Directory 全体管理者](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal)である必要があります。

    ![管理センター ランディング ページ](./media/powerapps-gdpr-export-dsr/admin-center-landing.png)

2. 環境ごとに、**[リソース]** を選んでから **[アプリ]** を選びます。

3. 環境内の各アプリについて **[共有]** を選びます。

    ![アプリの共有を選択する](./media/powerapps-gdpr-export-dsr/select-admin-share-nofilter.png)

4. ユーザーがアプリへのアクセス権を持っている場合、アプリの **[共有]** ページに移動し、詳細をコピーして、Microsoft Word などのドキュメント エディターに貼り付けます。

    ![管理者のアプリ共有ページ](./media/powerapps-gdpr-export-dsr/admin-share-page.png)

### <a name="powershell-cmdlets-for-admins"></a>管理者用の PowerShell コマンドレット
管理者は、[PowerApps 管理者PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871804)の **Get-AdminAppRoleAssignment** 機能を使って、テナント内のすべてのアプリに対するユーザーのすべてのアプリ ロール割り当てをエクスポートすることができます。

~~~~
Add-PowerAppsAccount
$userId = "0ecb1fcc-6782-4e46-a4c4-738c1d3accea"
Get-AdminAppRoleAssignment -UserId $userId | ConvertTo-Json | Out-File -FilePath "UserDetails.json"
~~~~

## <a name="step-5-export-personal-data-contained-within-connections-created-by-the-user"></a>ステップ 5: ユーザーによって作成された接続に含まれる個人データをエクスポートする
接続は、他の API および SaaS システムとの接続を確立するときに、コネクタと組み合わせて使われます。 接続にはそれを作成したユーザーへの参照が含まれ、結果として、接続を削除することでユーザーへの参照を削除できます。

### <a name="powershell-cmdlets-for-app-creators"></a>アプリ作成者用の PowerShell コマンドレット
ユーザーは、[PowerApps アプリ作成者 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871448)の **Get-Connection** 機能を使って、アクセス権のあるすべての接続をエクスポートできます。

~~~~
Add-PowerAppsAccount
Get-Connection | ConvertTo-Json | out-file -FilePath "UserDetails.json"
~~~~

### <a name="powershell-cmdlets-for-admins"></a>管理者用の PowerShell コマンドレット
管理者は、[PowerApps 管理者 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871804)の **Get-AdminConnection** 機能を使って、ユーザーによって作成されたすべての接続をエクスポートできます。

~~~~
Add-PowerAppsAccount
$userId = "0ecb1fcc-6782-4e46-a4c4-738c1d3accea"
Get-AdminConnection -CreatedBy $userId | ConvertTo-Json | Out-File -FilePath "UserDetails.json"
~~~~
 
## <a name="step-6-export-the-users-permissions-to-shared-connections"></a>ステップ 6: 共有接続に対するユーザーのアクセス許可をエクスポートする

### <a name="powershell-cmdlets-for-app-creators"></a>アプリ作成者用の PowerShell コマンドレット
ユーザーは、[PowerApps アプリ作成者 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871448)の **Get-ConnectionRoleAssignment** 機能を使って、自分がアクセス権を持っているすべての接続に対する接続ロール割り当てをエクスポートできます。

~~~~
Add-PowerAppsAccount
Get-ConnectionRoleAssignment | ConvertTo-Json | Out-file -FilePath "UserDetails.json"
~~~~

### <a name="powershell-cmdlets-for-admins"></a>管理者用の PowerShell コマンドレット
管理者は、[PowerApps 管理者 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871804)の **Get-AdminConnectionRoleAssignment** 機能を使って、ユーザーのすべての接続ロールの割り当てをエクスポートすることができます。

~~~~
Add-PowerAppsAccount
$userId = "0ecb1fcc-6782-4e46-a4c4-738c1d3accea"
Get-AdminConnectionRoleAssignment -PrincipalObjectId $userId | ConvertTo-Json | Out-File -FilePath "UserDetails.json"
~~~~

## <a name="step-7-export-personal-data-contained-within-custom-connectors-created-by-the-user"></a>ステップ 7: ユーザーによって作成されたカスタム コネクタに含まれる個人データをエクスポートする
カスタム コネクタは、既存の既製のコネクタを補完し、他の API、SaaS、カスタム開発システムへの接続に対応します。

### <a name="powerapps-app-creator-powershell-cmdlets"></a>PowerApps アプリ作成者 PowerShell コマンドレット
ユーザーは、[PowerApps アプリ作成者 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871448)の **Get-Connector** 機能を使って、作成したすべてのカスタム コネクタをエクスポートできます。

~~~~
Add-PowerAppsAccount  
Get-Connector -FilterNonCustomConnectors | ConvertTo-Json | Out-File -FilePath "UserDetails.json"
~~~~

### <a name="powershell-cmdlets-for-admins"></a>管理者用の PowerShell コマンドレット
管理者は、[PowerApps 管理者 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871804)の **Get-AdminConnector** 機能を使って、ユーザーによって作成されたすべてのカスタム コネクタをエクスポートできます。

~~~~
Add-PowerAppsAccount
$userId = "0ecb1fcc-6782-4e46-a4c4-738c1d3accea"
Get-AdminConnector -CreatedBy $userId | ConvertTo-Json | Out-File -FilePath "UserDetails.json"
~~~~

## <a name="step-8-export-the-users-permissions-to-custom-connectors"></a>ステップ 8: カスタム コネクタに対するユーザーのアクセス許可をエクスポートする

### <a name="powershell-cmdlets-for-app-creators"></a>アプリ作成者用の PowerShell コマンドレット
ユーザーは、[PowerApps アプリ作成者 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871448)の **Get-ConnectorRoleAssignment** 機能を使って、自分がアクセス権を持っているカスタム コネクタに対するすべてのコネクタ ロール割り当てをエクスポートできます。

~~~~
Add-PowerAppsAccount  
Get-ConnectorRoleAssignment | ConvertTo-Json | Out-File -FilePath "UserDetails.json"
~~~~

### <a name="powershell-cmdlets-for-admins"></a>管理者用の PowerShell コマンドレット
管理者は、[PowerApps 管理者 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871804)の **Get-AdminConnectorRoleAssignment** 機能を使って、ユーザーのすべてのカスタム コネクタ ロール割り当てをエクスポートすることができます。

~~~~
Add-PowerAppsAccount
$userId = "0ecb1fcc-6782-4e46-a4c4-738c1d3accea"
Get-AdminConnectorRoleAssignment -PrincipalObjectId $userId | ConvertTo-Json | Out-File -FilePath "UserDetails.json"
~~~~
 
## <a name="step-9-export-powerapps-notifications-user-settings-and-user-app-settings"></a>ステップ 9: PowerApps の通知、ユーザー設定、ユーザー アプリの設定をエクスポートする
PowerApps は、アプリがユーザーと共有されたときや、CDS for Apps のエクスポート操作が完了したときなど、複数の種類の通知をユーザーに送信します。 ユーザーは、自分の通知履歴を [PowerApps ポータル](https://web.powerapps.com) で見ることができます。

また、PowerApps は、ユーザーが最後にアプリケーションを開いたときや、アプリをピン留めしたときなど、PowerApps ランタイムとポータル エクスペリエンスの提供に使用されるユーザーの複数の基本設定や設定も格納します。

### <a name="powershell-cmdlets-for-app-creators"></a>アプリ作成者用の PowerShell コマンドレット
ユーザーは、自分の PowerApps 通知、ユーザー設定、およびユーザー アプリ設定を、[PowerApps アプリ作成者 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871448)の **Get AdminPowerAppsUserDetails** 機能を使用してエクスポートできます。

~~~~
Add-PowerAppsAccount  
Get-AdminPowerAppsUserDetails -WriteToFile -OutputFilePath "UserDetails.json"
~~~~

### <a name="powershell-cmdlets-for-admins"></a>管理者用の PowerShell コマンドレット
管理者は、ユーザーの PowerApps 通知、ユーザー設定、およびユーザー アプリ設定を、[PowerApps 管理者 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871804)の **Get-AdminPowerAppsUserDetails** 機能を使用してエクスポートできます。

~~~~
Add-PowerAppsAccount
$userId = "0ecb1fcc-6782-4e46-a4c4-738c1d3accea"
Get-AdminPowerAppsUserDetails -WriteToFile -OutputFilePath "UserDetails.json" -UserPrincipalName foobar@microsoft.com
~~~~

## <a name="step-10-export-personal-data-contained-for-a-user-stored-gateway-or-in-the-users-gateway-permissions"></a>ステップ 10: ユーザーが格納したゲートウェイまたはユーザーのゲートウェイ アクセス許可に含まれる個人データをエクスポートする

### <a name="powerapps-portal"></a>PowerApps ポータル
ユーザーは、以下の手順に従って、ゲートウェイ サービス内に格納された個人データを [PowerApps ポータル](https://web.powerapps.com)からエクスポートできます。

1. テナントの既定の環境内で、[PowerApps ポータル](https://web.powerapps.com)から、**[ゲートウェイ]** を選び、アクセス権のある各ゲートウェイの **[詳細]** を選びます。

    ![ゲートウェイのランディング ページ](./media/powerapps-gdpr-export-dsr/gateway-select-details.png)

2. **[詳細]** ページで、ゲートウェイの詳細に個人データが含まれる場合は、詳細をコピーし、Microsoft Word などのドキュメント エディターに貼り付けます。

    ![ゲートウェイの詳細](./media/powerapps-gdpr-export-dsr/gateway-details-drillin.png)

3. **[共有]** を選び、ページの内容をコピーして、Microsoft Word などのドキュメント エディターに貼り付けます。

    ![ゲートウェイの詳細](./media/powerapps-gdpr-export-dsr/gateway-details-share.png)

### <a name="gateway-powershell-cmdlets"></a>ゲートウェイの PowerShell コマンドレット
パーソナル ゲートウェイを取得、管理、削除できる PowerShell コマンドレットもあります。 詳細については、「[オンプレミス ゲートウェイ コマンドレット](https://go.microsoft.com/fwlink/?linkid=872238)」をご覧ください。

### <a name="administrators"></a>管理者
組織のゲートウェイ管理の詳細については、「[Microsoft PowerApps のオンプレミス データ ゲートウェイについて](https://docs.microsoft.com/powerapps/maker/canvas-apps/gateway-reference#tenant-level-administration)」の**テナントの管理**に関する記事を参照してください。

## <a name="step-11-export-the-users-personal-data-in-microsoft-flow"></a>ステップ 11: Microsoft Flow に含まれるユーザーの個人データをエクスポートする
PowerApps ライセンスには、常に Microsoft Flow の機能が含まれています。 PowerApps ライセンスに含まれるだけでなく、Microsoft Flow はスタンドアロン サービスとして利用することもできます。 Microsoft Flow サービスを使うユーザーに関する DSR 要求への応答方法のガイダンスについては、「[Microsoft Flow に対する GDPR データ主体の要求への応答](https://go.microsoft.com/fwlink/?linkid=872250)」をご覧ください。

> [!IMPORTANT]
>  管理者は PowerApps ユーザーに対してこの手順を完了することをお勧めします。
>
>

## <a name="step-12-export-the-users-personal-data-in-cds-for-apps-instances"></a>ステップ 12: CDS for Apps インスタンスに含まれるユーザーの個人データをエクスポートする
特定の PowerApps ライセンスでは、組織内のユーザーは、CDS for Apps インスタンスを作成したり、CDS for Apps 上でアプリを作成してビルドしたりできます。これには、ユーザーが個人の環境で CDS for Apps 試すことのできる無料のライセンスである PowerApps Community Plan が含まれます。 各 PowerApps ライセンスに含まれる CDS for Apps の機能を確認するには、[PowerApps の価格ページ](https://powerapps.microsoft.com/pricing)をご覧ください。

CDS for Apps を使うユーザーに関する DSR 要求に応答する方法のガイダンスについては、「[Common Data Service for Apps での顧客データのデータ主体の権利 (DSR) 要求に対する対応](common-data-service-gdpr-dsr-guide.md)」をご覧ください。

> [!IMPORTANT]
>  管理者は PowerApps ユーザーに対してこの手順を完了することをお勧めします。
>
>

---
title: データ主体の権利 (DSR) による顧客データ削除要求への応答 | Microsoft Docs
description: データ主体の権利 (DSR) による PowerApps 顧客データの削除要求に応答する方法を説明します。
author: jamesol-msft
manager: kfile
ms.service: powerapps
ms.component: pa-admin
ms.topic: conceptual
ms.date: 05/23/2018
ms.author: jamesol
ms.openlocfilehash: 495d9976b1daa6e7adb20d97c0840b3a1ba90c4b
ms.sourcegitcommit: 68fc13fdc2c991c499ad6fe9ae1e0f8dab597139
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/04/2018
ms.locfileid: "34552693"
---
# <a name="responding-to-data-subject-rights-dsr-requests-to-delete-powerapps-customer-data"></a>データ主体の権利 (DSR) による PowerApps 顧客データの削除要求への応答

組織の顧客データから個人データを削除することによる "忘れられる権利" は、欧州連合 (EU) の一般データ保護規則 (GDPR: General Data Protection Regulation) での重要な保護です。 個人データの削除には、システムによって生成されたログの削除は含まれますが、監査ログ情報の削除は含まれません。

PowerApps では、組織の日常業務の重要な一部である基幹業務アプリケーションを構築できます。 ユーザーが組織を離れるときは、手作業で確認し、ユーザーが作成した特定のデータとリソースを削除するかどうかを判断する必要があります。 その他の個人データは、Azure Active Directory からユーザーのアカウントが削除されるとき常に自動的に削除されます。

自動的に削除される個人データと、手作業で確認して削除する必要があるデータの詳細を次に示します。

手作業で確認して削除する必要があるデータ |   ユーザーが Azure Active Directory から削除されると自動的に削除されるデータ
--- | ---
環境\** | ゲートウェイ
環境のアクセス許可\*** | ゲートウェイのアクセス許可
キャンバス アプリ\** | PowerApps の通知
キャンバス アプリのアクセス許可 | PowerApps のユーザー設定
接続\** | PowerApps のユーザー アプリ設定
接続のアクセス許可 |
カスタム コネクタ\** |
カスタム コネクタのアクセス許可 |  

\** これらの各リソースには、個人データを含む "作成者" および "変更者" のレコードが含まれます。 セキュリティ上の理由から、これらのレコードはリソースが削除されるまで保持されます。

\*** Common Data Service (CDS) for Apps データベースが含まれる環境では、環境のアクセス許可 (つまり、環境作成者および環境管理者のロールが割り当てられているユーザー) が、そのデータベース内のレコードとして格納します。 CDS for Apps のユーザーに対する DSR に応答する方法のガイダンスについては、「[Common Data Service for Apps での顧客データのデータ主体の権利 (DSR) 要求に対する対応](common-data-service-gdpr-dsr-guide.md)」をご覧ください。

手動での確認が必要なデータとリソースのために、PowerApps では特定のユーザーの個人データの再割り当て (必要な場合) または削除を行う以下のエクスペリエンスが提供されています。

* Web サイト アクセス: [PowerApps サイト](https://web.powerapps.com)、[PowerApps 管理センター](https://admin.powerapps.com/)、[Office 365 Service Trust Portal](https://servicetrust.microsoft.com/)

* PowerShell アクセス: [アプリ作成者](https://go.microsoft.com/fwlink/?linkid=871448)および[管理者](https://go.microsoft.com/fwlink/?linkid=871804)のための PowerApps コマンドレット、および[オンプレミス ゲートウェイ](https://go.microsoft.com/fwlink/?linkid=872238)のためのコマンドレット。

次に示すのは、個人データが含まれる可能性のあるリソースの種類ごとに使用可能な削除エクスペリエンスの詳細です。

個人データが含まれるリソース | Web サイト アクセス | PowerShell アクセス
--- | --- | ---
環境 | PowerApps 管理センター |  PowerApps コマンドレット
環境のアクセス許可**   | PowerApps 管理センター | PowerApps コマンドレット
キャンバス アプリ  | PowerApps 管理センター <br> PowerApps| PowerApps コマンドレット
キャンバス アプリのアクセス許可  | PowerApps 管理センター | PowerApps コマンドレット
接続 | | アプリ作成者: 使用可能 <br> 管理者: 使用可能
接続のアクセス許可 | | アプリ作成者: 使用可能 <br> 管理者: 使用可能
カスタム コネクタ | | アプリ作成者: 使用可能 <br> 管理者: 使用可能
カスタム コネクタのアクセス許可 | | アプリ作成者: 使用可能 <br> 管理者: 使用可能

\** CDS for Apps の導入により、環境内にデータベースを作成した場合、環境のアクセス許可とモデル駆動型アプリのアクセス許可は、そのデータベースのインスタンス内のレコードとして格納されます。 CDS for Apps のユーザーに対する DSR に応答する方法のガイダンスについては、「[Common Data Service for Apps での顧客データのデータ主体の権利 (DSR) 要求に対する対応](common-data-service-gdpr-dsr-guide.md)」をご覧ください。

## <a name="prerequisites"></a>前提条件

### <a name="for-users"></a>ユーザーの場合
PowerApps の有効なライセンスを持つユーザーは、[PowerApps](https://web.powerapps.com) または[アプリ作成者用 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871448)を使って、このドキュメントに記載されているユーザー操作を実行できます。

#### <a name="unmanaged-tenant"></a>アンマネージド テナント
[アンマネージド テナント](https://docs.microsoft.com/azure/active-directory/domains-admin-takeover)のメンバーである場合 (つまり、Azure AD テナントにグローバル管理者がいない場合) も、この記事で説明している手順に従い、ご自分の個人データを削除できます。  ただし、テナントにグローバル管理者がいないため、「[ステップ 11: Azure Active Directory からユーザーを削除する](#step-11-delete-the-user-from-azure-active-directory)」に従って、テナントから自分のアカウントを削除する必要があります。

アンマネージド テナントのメンバーであるか判断するには、次の手順に従います。

1. URL 内の電子メールを必ず自分のものに置き換え、ブラウザーで https://login.windows.net/common/userrealm/foobar@contoso.com?api-version=2.1 の URL を開きます。

2. **アンマネージド テナント**のメンバーである場合、応答に `"IsViral": true` が表示されます。
```
{
  ...
  "Login": "foobar@unmanagedcontoso.com",
  "DomainName": "unmanagedcontoso.com",
  "IsViral": true,
  ...
}
```

3. それ以外の場合は、**マネージド テナント**に属しています。

### <a name="for-administrators"></a>管理者の場合
[PowerApps 管理センター](https://admin.powerapps.com/)、Microsoft Flow 管理センター、または [PowerApps 管理者用 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871804)を使って、このドキュメントに記載されている管理操作を実行するには、次のものが必要です。

* 有料の PowerApps プラン 2 ライセンスまたは PowerApps プラン 2 無料試用版ライセンス。 [http://web.powerapps.com/trial](http://web.powerapps.com/trial) で、30 日間有効な無料試用版ライセンスにサインアップできます。 無料試用版ライセンスの有効期限が切れた場合は更新できます。

* 別のユーザーのリソースを検索する必要がある場合は、[Office 365 全体管理者](https://support.office.com/article/assign-admin-roles-in-office-365-for-business-eac4d046-1afd-4f1a-85fc-8219c79e1504)または [Azure Active Directory 全体管理者](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal)のアクセス許可 (環境管理者は、自分がアクセス許可を持っている環境および環境リソースにのみアクセスできることに注意してください)。

## <a name="step-1-delete-or-reassign-all-environments-created-by-the-user"></a>ステップ 1: ユーザーによって作成されたすべての環境の削除または再割り当てを行う
管理者は、ユーザーが作成した各環境の DSR 削除要求を処理するときに、2 つのことを決定します。

1. 環境が組織内のどのユーザーによっても使われていないことを確認した場合は、環境を削除できます。

2. 環境がまだ必要であると判断した場合は、環境を削除せず、自分自身 (または、組織内の別のユーザー) を環境管理者として追加できます。

> [!IMPORTANT]
> 環境を削除すると、すべてのアプリ、フロー、接続などを含む、環境内のすべてのリソースが完全に削除されます。したがって、削除する前に、環境の内容を確認してください。

### <a name="give-access-to-a-users-environments-from-the-powerapps-admin-center"></a>PowerApps 管理センターからユーザーの環境へのアクセス権を付与する
管理者は、[PowerApps 管理センター](https://admin.powerapps.com/)で次の手順に従って、特定のユーザーによって作成された環境への管理アクセス権を付与できます。

1. [PowerApps 管理センター](https://admin.powerapps.com/)で、組織内の各環境を選択します。

    ![管理センター ランディング ページ](./media/powerapps-gdpr-delete-dsr/admin-center-landing.png)

2. 環境が DSR 要求からユーザーによって作成されたものである場合は、**[セキュリティ]** を選び、「[環境の管理](environments-administration.md)」で説明されている手順に従って、自分自身または組織の他のユーザーに管理者特権を付与します。

    ![環境のセキュリティ](./media/powerapps-gdpr-delete-dsr/share-environment.png)

### <a name="delete-environments-created-by-a-user-from-the-powerapps-admin-center"></a>ユーザーによって作成された環境を PowerApps 管理センターから削除する
管理者は、[PowerApps 管理センター](https://admin.powerapps.com/)で次の手順に従って、特定のユーザーによって作成された環境を確認して削除できます。

1. [PowerApps 管理センター](https://admin.powerapps.com/)で、組織内の各環境を選択します。

    ![管理センター ランディング ページ](./media/powerapps-gdpr-delete-dsr/admin-center-landing.png)

2. 環境が DSR 要求からユーザーによって作成された場合は、**[削除]** を選んだ後、手順に従って環境を削除します。

    ![環境の削除](./media/powerapps-gdpr-delete-dsr/delete-environment.png)

### <a name="give-access-to-a-users-environments-using-powershell"></a>PowerShell を使用してユーザーの環境へのアクセス権を付与する
管理者は、[PowerApps 管理者用 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871804)の **Set-AdminEnvironmentRoleAssignment** 機能を使用して、ユーザーによって作成されたすべての環境へのアクセス権を自分自身 (または、組織内の別のユーザー) に割り当てることができます。

```
Add-PowerAppsAccount
$deleteDsrUserId = "0ecb1fcc-6782-4e46-a4c4-738c1d3accea"
$myUserId = $global:currentSession.UserId

#Assign yourself as an admin to each environment created by the user
Get-AdminEnvironment -CreatedBy $deleteDsrUserId | Set-AdminEnvironmentRoleAssignment -RoleName EnvironmentAdmin -PrincipalType User -PrincipalObjectId $myUserId

#Retrieve the environment role assignments to confirm
Get-AdminEnvironment -CreatedBy $deleteDsrUserId | Get-AdminEnvironmentRoleAssignment
```

> [!IMPORTANT]
> この機能は、CDS for Apps にデータベースのインスタンスが存在しない環境においてのみ動作します。

### <a name="delete-environments-created-by-a-user-using-powershell"></a>ユーザーによって作成された環境を PowerShell を使用して削除する
 管理者は、[PowerApps 管理者用 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871804)の **Remove-AdminEnvironment** 機能を使用して、ユーザーによって作成されたすべての環境を削除できます。

```
Add-PowerAppsAccount
$deleteDsrUserId = "0ecb1fcc-6782-4e46-a4c4-738c1d3accea"

# Retrieve all environments created by the user and then delete them
Get-AdminEnvironment -CreatedBy $deleteDsrUserId | Remove-AdminEnvironment
```

## <a name="step-2-delete-the-users-permissions-to-all-other-environments"></a>ステップ 2: 他のすべての環境に対するユーザーのアクセス許可を削除する
ユーザーには環境内のアクセス許可 (環境管理者、環境作成者など) を割り当てることができ、アクセス許可は "ロール割り当て" として PowerApps サービスに格納されます。
CDS for Apps の導入により、環境内にデータベースを作成した場合、これらのロール割り当ては、そのデータベースのインスタンス内のレコードとして格納されます。
詳しくは、「[環境の管理](environments-administration.md)」をご覧ください。

### <a name="for-environments-without-a-cds-for-apps-database"></a>CDS for Apps データベースがない環境の場合

#### <a name="powerapps-admin-center"></a>PowerApps 管理センター
管理者から、[PowerApps 管理センター](https://admin.powerapps.com/)から以下の手順に従って、ユーザーの環境のアクセス許可を削除できます。

1. [PowerApps 管理センター](https://admin.powerapps.com/)で、組織内の各環境を選択します。

    組織内で作成されたすべての環境を確認するには、[Office 365 全体管理者](https://support.office.com/article/assign-admin-roles-in-office-365-for-business-eac4d046-1afd-4f1a-85fc-8219c79e1504)または [Azure Active Directory 全体管理者](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal)である必要があります。

    ![管理センター ランディング ページ](./media/powerapps-gdpr-delete-dsr/admin-center-landing.png)

2. **[セキュリティ]** を選択します。

    環境に CDS for Apps データベースがない場合は、**[環境ロール]** のセクションが表示されます。

3. **[環境ロール]** で、**[環境管理者]** と **[環境作成者]** の両方を個別に選択し、検索バーを使って、ユーザーの名前を検索します。

    ![[環境ロール] ページ](./media/powerapps-gdpr-delete-dsr/admin-environment-role-share-page.png)

5.  ユーザーがいずれかのロールにアクセスできる場合は、**[ユーザー]** 画面内から、それらのアクセス許可を削除し、**[保存]** を選びます。

#### <a name="powershell"></a>PowerShell
管理者は、[PowerApps 管理者用 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871804)の **Remove-AdminEnvironmentRoleAssignment** 機能を使って、CDS for Apps データベースがないすべての環境でのユーザーに対するすべての環境ロール割り当てを削除することができます。

```
Add-PowerAppsAccount
$deleteDsrUserId = "0ecb1fcc-6782-4e46-a4c4-738c1d3accea"

#find all environment role assignments for the user for environments without a CDS for Apps instance and delete them
Get-AdminEnvironmentRoleAssignment -UserId $deleteDsrUserId | Remove-AdminEnvironmentRoleAssignment
```

> [!IMPORTANT]
> この機能は、CDS for Apps データベースのインスタンスがない環境においてのみ動作します。

### <a name="for-environments-with-a-cds-for-apps-database"></a>CDS for Apps データベースがある環境の場合
CDS for Apps の導入により、環境内にデータベースを作成した場合、これらのロール割り当ては、そのデータベースのインスタンス内のレコードとして格納されます。 CDS for Apps のデータベースのインスタンスから個人データを削除する方法については、Common Data Service ユーザーの個人データの削除に関するドキュメントをご覧ください。

## <a name="step-3-delete-or-reassign-all-canvas-apps-owned-by-a-user"></a>ステップ 3: ユーザーによって所有されるすべてのキャンバス アプリの削除または再割り当てを行う

### <a name="reassign-a-users-canvas-apps-using-the-powerapps-admin-powershell-cmdlets"></a>PowerApps 管理者 PowerShell コマンドレットを使用してユーザーのキャンバス アプリの再割り当てを行う
管理者は、ユーザーのキャンバス アプリを削除しない場合、[PowerApps 管理者用 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871804)の **Set-AdminAppOwner** 機能を使って、ユーザーによって所有されるアプリの再割り当てを行うことができます。

```
Add-PowerAppsAccount
$deleteDsrUserId = "0ecb1fcc-6782-4e46-a4c4-738c1d3accea"
$newAppOwnerUserId = "72c272b8-14c3-4f7a-95f7-a76f65c9ccd8"

#find all apps owned by the DSR user and assigns them a new owner
Get-AdminApp -Owner $deleteDsrUserId | Set-AdminAppOwner -AppOwner $newAppOwnerUserId
```

### <a name="delete-a-users-canvas-app-using-the-powerapps-site"></a>PowerApps サイトを使用してユーザーのキャンバス アプリを削除する
ユーザーは、[PowerApps サイト](https://web.powerapps.com)からアプリを削除できます。 アプリを削除する詳細な手順については、アプリの削除に関する記事をご覧ください。

### <a name="delete-a-users-canvas-app-using-the-powerapps-admin-center"></a>PowerApps 管理センターを使用してユーザーのキャンバス アプリを削除する
管理者は、[PowerApps 管理センター](https://admin.powerapps.com/)から以下の手順に従って、ユーザーが作成したアプリを削除できます。

1. [PowerApps 管理センター](https://admin.powerapps.com/)で、組織内の各環境を選択します。

    組織内で作成されたすべての環境を確認するには、[Office 365 全体管理者](https://support.office.com/article/assign-admin-roles-in-office-365-for-business-eac4d046-1afd-4f1a-85fc-8219c79e1504)または [Azure Active Directory 全体管理者](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal)である必要があります。

    ![管理センター ランディング ページ](./media/powerapps-gdpr-delete-dsr/admin-center-landing.png)

2. **[リソース]** > **[アプリ]** の順に選びます。

3. 検索バーを使って、ユーザーの名前を検索します。そのユーザーがこの環境内で作成したすべてのアプリが表示されます。

    ![アプリの検索](./media/powerapps-gdpr-delete-dsr/search-apps.png)

4. そのユーザーが所有する各アプリの **[詳細]** を選びます。

    ![アプリの詳細の選択](./media/powerapps-gdpr-delete-dsr/select-app-details.png)

5. **[削除]** を選んで各アプリを削除します。

### <a name="delete-a-users-canvas-app-using-the-powerapps-admin-powershell-cmdlets"></a>PowerApps 管理者 PowerShell コマンドレットを使用してユーザーのキャンバス アプリを削除する
管理者は、[PowerApps 管理者用 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871804)の **Remove-AdminApp** 機能を使って、ユーザーが所有するすべてのキャンバス アプリを削除できます。

```
Add-PowerAppsAccount
$deleteDsrUserId = "0ecb1fcc-6782-4e46-a4c4-738c1d3accea"

#find all apps owned by the DSR user and deletes them
Get-AdminApp -Owner "0ecb1fcc-6782-4e46-a4c4-738c1d3accea" | Remove-AdminApp
```

## <a name="step-4-delete-the-users-permissions-to-canvas-apps"></a>ステップ 4: キャンバス アプリに対するユーザーのアクセス許可を削除する
アプリがユーザーと共有されるたびに、PowerApps はアプリケーションに対するユーザーのアクセス許可 (CanEdit または CanUser) が記述されている "ロール割り当て" と呼ばれるレコードを格納します。 詳しくは、アプリの共有に関する記事をご覧ください。

> [!NOTE]
> アプリのロール割り当ては、アプリが削除されると削除されます。

> [!NOTE]
> アプリ所有者のロール割り当ては、アプリに新しい所有者を割り当てることによってのみ削除できます。

### <a name="powerapps-admin-center"></a>PowerApps 管理センター
管理者は、[PowerApps 管理センター](https://admin.powerapps.com/)から以下の手順に従って、ユーザーに対するアプリのロール割り当てを削除できます。

1. [PowerApps 管理センター](https://admin.powerapps.com/)で、組織内の各環境を選択します。

    組織内で作成されたすべての環境を確認するには、[Office 365 全体管理者](https://support.office.com/article/assign-admin-roles-in-office-365-for-business-eac4d046-1afd-4f1a-85fc-8219c79e1504)または [Azure Active Directory 全体管理者](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal)である必要があります。

    ![管理センター ランディング ページ](./media/powerapps-gdpr-delete-dsr/admin-center-landing.png)

2. 各環境について、**[リソース]** > **[アプリ]** を選びます。

3. 環境内の各アプリについて **[共有]** を選びます。

    ![アプリの共有を選択する](./media/powerapps-gdpr-delete-dsr/select-admin-share-nofilter.png)

4. ユーザーがアプリにアクセスできる場合は、アプリの **[共有]** 画面内から、それらのアクセス許可を削除し、**[保存]** を選びます。

    ![管理者のアプリ共有ページ](./media/powerapps-gdpr-delete-dsr/admin-share-page.png)

### <a name="powershell-cmdlets-for-admins"></a>管理者用の PowerShell コマンドレット
管理者は、[PowerApps 管理者用 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871804)の **Remove-AdminAppRoleAssignmnet** 機能を使って、ユーザーのキャンバス アプリのロール割り当てをすべて削除できます

```
Add-PowerAppsAccount
$deleteDsrUserId = "0ecb1fcc-6782-4e46-a4c4-738c1d3accea"

#find all app role assignments for the DSR user and deletes them
Get-AdminAppRoleAssignment -UserId $deleteDsrUserId | Remove-AdminAppRoleAssignment
```

## <a name="step-5-delete-connections-created-by-a-user"></a>ステップ 5: ユーザーによって作成された接続を削除する
接続は、他の API および SaaS システムとの接続を確立するときに、コネクタと組み合わせて使われます。  接続にはそれを作成したユーザーへの参照が含まれ、結果として、接続を削除することでユーザーへの参照を削除できます。

### <a name="powershell-cmdlets-for-app-creators"></a>アプリ作成者用の PowerShell コマンドレット
ユーザーは、[アプリ作成者用 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871448)の Remove-Connection 機能を使って、自分のすべての接続を削除できます。

```
Add-PowerAppsAccount

#Retrieves all connections for the calling user and deletes them
Get-Connection | Remove-Connection
```

### <a name="powershell-cmdlets-for-powerapps-administrators"></a>PowerApps 管理者用の PowerShell コマンドレット
管理者は、[PowerApps 管理者用 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871804)の **Remove-AdminConnection** 機能を使って、ユーザー接続をすべて削除できます。

```
Add-PowerAppsAccount
$deleteDsrUserId = "0ecb1fcc-6782-4e46-a4c4-738c1d3accea"

#Retrieves all connections for the DSR user and deletes them
Get-AdminConnection -CreatedBy $deleteDsrUserId | Remove-AdminConnection
```

## <a name="step-6-delete-the-users-permissions-to-shared-connections"></a>ステップ 6: 共有接続に対するユーザーのアクセス許可を削除する

### <a name="powershell-cmdlets-for-app-creators"></a>アプリ作成者用の PowerShell コマンドレット
ユーザーは、[アプリ作成者用 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871448)の Remove-ConnectionRoleAssignment 機能を使って、共有接続に対する自分のすべての接続ロール割り当てを削除できます。

```
Add-PowerAppsAccount

#Retrieves all connection role assignments for the calling users and deletes them
Get-ConnectionRoleAssignment | Remove-ConnectionRoleAssignment
```
> [!NOTE]
> 所有者のロール割り当ては、接続リソースを削除しない限り、削除できません。

### <a name="powershell-cmdlets-for-admins"></a>管理者用の PowerShell コマンドレット
管理者は、[PowerApps 管理者用 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871804)の **Remove-AdminConnectionRoleAssignment** 機能を使って、ユーザーの接続ロール割り当てをすべて削除できます。

```
Add-PowerAppsAccount
$deleteDsrUserId = "0ecb1fcc-6782-4e46-a4c4-738c1d3accea"

#Retrieves all connection role assignments for the DSR user and deletes them
Get-AdminConnectionRoleAssignment -PrincipalObjectId $deleteDsrUserId | Remove-AdminConnectionRoleAssignment
```

## <a name="step-7-delete-custom-connectors-created-by-the-user"></a>ステップ 7: ユーザーによって作成されたカスタム コネクタを削除する
カスタム コネクタは、既存の既製のコネクタを補完し、他の API、SaaS、カスタム開発システムへの接続に対応します。 カスタム コネクタの所有権を組織内の他のユーザーに譲渡するか、カスタム コネクタを削除することができます。

### <a name="powershell-cmdlets-for-app-creators"></a>アプリ作成者用の PowerShell コマンドレット
ユーザーは、[アプリ作成者用 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871448)の Remove-Connector 機能を使って、自分のすべてのカスタム コネクタを削除できます。

```
Add-PowerAppsAccount

#Retrieves all custom connectors for the calling user and deletes them
Get-Connector -FilterNonCustomConnectors | Remove-Connector
```

### <a name="powershell-cmdlets-for-admins"></a>管理者用の PowerShell コマンドレット
管理者は、[PowerApps 管理者用 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871804)の **Remove-AdminConnector** 機能を使って、ユーザーによって作成されたすべてのカスタム コネクタを削除できます。

```
Add-PowerAppsAccount
$deleteDsrUserId = "0ecb1fcc-6782-4e46-a4c4-738c1d3accea"

#Retrieves all custom connectors created by the DSR user and deletes them
Get-AdminConnector -CreatedBy $deleteDsrUserId | Remove-AdminConnector
```

## <a name="step-8-delete-the-users-permissions-to-shared-custom-connectors"></a>ステップ 8: 共有カスタム コネクタに対するユーザーのアクセス許可を削除する

### <a name="powershell-cmdlets-for-app-creators"></a>アプリ作成者用の PowerShell コマンドレット
ユーザーは、[アプリ作成者用 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871448)の Remove-ConnectorRoleAssignment 機能を使って、共有カスタム コネクタに対する自分のすべてのコネクタ ロール割り当てを削除できます。

```
Add-PowerAppsAccount

#Retrieves all connector role assignments for the calling users and deletes them
Get-ConnectorRoleAssignment | Remove-ConnectorRoleAssignment
```

> [!NOTE]
> 所有者のロール割り当ては、接続リソースを削除しない限り、削除できません。

### <a name="powershell-cmdlets-for-admins"></a>管理者用の PowerShell コマンドレット
管理者は、[PowerApps 管理者用 PowerShell コマンドレット](https://go.microsoft.com/fwlink/?linkid=871804)の **Remove-AdminConnectorRoleAssignment** 機能を使って、ユーザーのカスタム コネクタ ロール割り当てをすべて削除できます。

```
Add-PowerAppsAccount
$deleteDsrUserId = "0ecb1fcc-6782-4e46-a4c4-738c1d3accea"

#Retrieves all custom connector role assignments for the DSR user and deletes them
Get-AdminConnectorRoleAssignment -PrincipalObjectId $deleteDsrUserId | Remove-AdminConnectorRoleAssignment
```

## <a name="step-9-delete-the-users-personal-data-in-microsoft-flow"></a>ステップ 9: Microsoft Flow に含まれるユーザーの個人データを削除する
PowerApps ライセンスには、常に Microsoft Flow の機能が含まれています。 PowerApps ライセンスに含まれるだけでなく、Microsoft Flow はスタンドアロン サービスとして利用することもできます。 Microsoft Flow サービスを使うユーザーに関する DSR への応答方法のガイダンスについては、「[Microsoft Flow に対する GDPR データ主体の要求への応答](https://go.microsoft.com/fwlink/?linkid=872250)」をご覧ください。

> [!IMPORTANT]
> 管理者には、PowerApps ユーザーに対してこの手順を完了することをお勧めします。

## <a name="step-10-delete-the-users-personal-data-in-instances-of-cds-for-apps"></a>ステップ 10: CDS for Apps のインスタンスに含まれるユーザーの個人データを削除する
PowerApps Community Plan などの特定の PowerApps ライセンスを持つ組織内のユーザーは、CDS for Apps のインスタンスを作成し、CDS for Apps 上でアプリを作成して構築できます。 PowerApps Community Plan は無料のライセンスであり、ユーザーは個々の環境で CDS for Apps を試すことができます。 各 PowerApps ライセンスに含まれる機能については、PowerApps の価格ページをご覧ください。

CDS for Apps を使うユーザーに関する DSR に応答する方法のガイダンスについては、「[Common Data Service for Apps での顧客データのデータ主体の権利 (DSR) 要求に対する対応](common-data-service-gdpr-dsr-guide.md)」をご覧ください。

> [!IMPORTANT]
> 管理者には、PowerApps ユーザーに対してこの手順を完了することをお勧めします。

## <a name="step-11-delete-the-user-from-azure-active-directory"></a>ステップ 11: Azure Active Directory からユーザーを削除する
上記の手順を完了したら、最後に Azure Active Directory のユーザー アカウントを削除します。

### <a name="managed-tenant"></a>マネージド テナント
マネージド Azure AD テナントの管理者として、[Office 365 Service Trust Portal](https://servicetrust.microsoft.com/ViewPage/GDPRDSR) にある Azure でのデータ主体要求 GDPR に記載されている手順に従って、ユーザー アカウントを削除できます。

### <a name="unmanaged-tenant"></a>アンマネージド テナント
アンマネージド テナントのメンバーである場合、Azure AD テナントから自分のアカウントを削除するには、これらの手順に従う必要があります。

> [!NOTE]
> アンマネージドまたはマネージド テナントのどちらのメンバーであるかを判別するには、「[アンマネージド テナント](#unmanaged-tenant)」のセクションを参照してください。

1. [[Work and School privacy]](https://go.microsoft.com/fwlink/?linkid=87312)\(職場および学校のプライバシー\) ページに移動し、ご自分の Azure AD アカウントでサインインします。

2. **[アカウントの削除]** を選択し、Azure AD テナントからアカウントを削除する手順に従います。

    ![アプリの共有を選択する](./media/powerapps-gdpr-delete-dsr/close-account.png)

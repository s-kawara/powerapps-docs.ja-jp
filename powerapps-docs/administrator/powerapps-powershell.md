---
title: PowerShell のサポート (プレビュー) | Microsoft Docs
description: さまざまな PowerShell コマンドレットについて説明し、それらをでインストールして実行する方法のチュートリアルを示します。
author: jamesol-msft
manager: kfile
ms.service: powerapps
ms.component: pa-admin
ms.topic: reference
ms.date: 05/23/2018
ms.author: jamesol
ms.openlocfilehash: b6ee687fdfe6da8550d76193a7c9219aae5ae291
ms.sourcegitcommit: 0b051bba173353d7ceda3b60921e7e009eb00709
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2018
ms.locfileid: "39218834"
---
# <a name="powershell-support-for-powerapps-preview"></a>PowerApps 向け PowerShell のサポート (プレビュー)
アプリの作成者と管理者向けの PowerShell コマンドレットのプレビューが開始されたことで、現在は [PowerApps](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) または [PowerApps 管理センター](https://admin.powerapps.com)で手動によってのみ可能な監視および管理タスクの多くを自動化できます。

## <a name="installation"></a>インストール
アプリ作成者向けの PowerShell コマンドレットを実行するには、次のようにします。

1. [PowerShell スクリプト ファイル](https://go.microsoft.com/fwlink/?linkid=2006349)をダウンロードします。

2. フォルダーにファイルを解凍します。 

3. 同じフォルダーで (管理者として) PowerShell コマンド ウィンドウを開きます。

4. 次の 1 回限りの PowerShell コマンドを実行します (現在お使いのコンピューターで PowerShell コマンドを実行したことがないものとします)。

    ```
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Force
    ```

5. 次のコマンドを使って必要なモジュールをインポートします。

    ```
    Import-Module .\Microsoft.PowerApps.Administration.PowerShell.psm1 -Force
    Import-Module .\Microsoft.PowerApps.PowerShell.psm1 -Force
    ```

6.  現在、次のコマンドを使用して PowerShell ファイルを手動でブロック解除することが必要な場合がある[既知の問題](https://powerusers.microsoft.com/t5/Administering-PowerApps/Getting-errors-when-I-try-to-import-the-preview-powerapps/td-p/109036)があります。

    ```
    dir . | Unblock-File
    ```
7. コマンドにアクセスする前に、次のコマンドを使って資格情報を提供します。 これらの資格情報は約 8 時間以内に更新され、その後コマンドレットの使用を続けるには再度サインインする必要があります。

    ```
    # This call will open a prompt to collect the credentials (AAD account & password) that will be used by the commands
    Add-PowerAppsAccount
    ```

    ```
    # Here is how you can pass in credentials (avoiding opening a prompt)
    $pass = ConvertTo-SecureString "password" -AsPlainText -Force
    Add-PowerAppsAccount -Username foo@bar.com -Password $pass
    ```


## <a name="powerapps-cmdlets-for-app-creators-preview"></a>アプリ作成者向けの PowerApps コマンドレット (プレビュー)

### <a name="prerequisite"></a>前提条件
PowerApps の有効なライセンスを持つユーザーはコマンドレットで操作を実行することができますが、アクセスできるのは自分で作成したリソースまたは自分が共有を受けているリソース (アプリ、フローなど) のみです。

### <a name="cmdlet-list"></a>コマンドレット一覧
> [!NOTE]
> 適切なプレフィックスを追加して競合を回避するために、最新リリースでコマンドレットの関数名の一部を更新しました。 変更した内容の概要については、次の表を参照してください。

| 目的 | コマンドレット |
| --- | --- |
| 環境を読み取る | Get-PowerAppEnvironment *(以前の Get-PowerAppsEnvironment)* <br> Get-FlowEnvironment
| キャンバス アプリの読み取り、更新、削除を行う | Get-App <br> Remove-App <br> Publish-App <br> Set-AppDisplayName <br> Get-AppVersion <br> Restore-AppVersion
| キャンバス アプリのアクセス許可の読み取り、更新、削除を行う | Get-PowerAppRoleAssignment *(以前の Get-AppRoleAssignment)* <br> Set-PowerAppRoleAssignment *(以前の Set-AppRoleAssignment)* <br> Remove-PowerAppRoleAssignment *(以前の Remove-AppRoleAssignment)*
| フローの読み取り、更新、削除を行う | Get-Flow <br> Get-FlowRun <br> Enable-Flow <br> Disable-Flow <br> Remove-Flow
| フローのアクセス許可の読み取り、更新、削除を行う | Get-FlowOwnerRole <br> Set-FlowOwnerRole <br> Remove-FlowOwnerRole
| フローの承認の読み取り、応答を行う | Get-FlowApprovalRequest <br> Get-FlowApproval <br> RespondTo-FlowApprovalRequest
| 接続の読み取り、削除を行う | Get-PowerAppConnection *(以前の Get-Connection)* <br> Remove-PowerAppConnection *(以前の Remove-Connection)*
| 接続のアクセス許可の読み取り、更新、削除を行う | Get-PowerAppConnectionRoleAssignment *(以前の Get-ConnectionRoleAssignment)* <br> Set-PowerAppConnectionRoleAssignment *(以前の Set-ConnectionRoleAssignment)* <br> Remove-PowerAppConnectionRoleAssignment *(以前の Remove-ConnectionRoleAssignment)*
| コネクタの読み取り、削除を行う | Get-PowerAppConnector *(以前の Get-Connector)* <br> Remove-PowerAppConnector *(以前の Remove-Connector)*
| カスタム コネクタのアクセス許可の読み取り、更新、削除を行う | Get-PowerAppConnectorRoleAssignment *(以前の Get-ConnectorRoleAssignment)* <br> Set-PowerAppConnectorRoleAssignment *(以前の Set-ConnectorRoleAssignment)* <br> Remove-PowerAppConnectorRoleAssignment *(以前の Remove-ConnectorRoleAssignment)*


> [!NOTE]
> 各コマンドレットの構文を理解し、サンプルを見るには、次のコマンドを使います。
>```
>Get-Help Get-PowerAppEnvironment
>Get-Help Get-PowerAppEnvironment -Examples
>Get-Help Get-PowerAppEnvironment -Detailed
>```

## <a name="powerapps-cmdlets-for-administrators-preview"></a>管理者向けの PowerApps コマンドレット (プレビュー)

### <a name="prerequisite"></a>前提条件
管理コマンドレットで管理操作を実行するには、次のものが必要です。

* 有料の PowerApps プラン 2 ライセンスまたは PowerApps プラン 2 無料試用版ライセンス。 [http://web.powerapps.com/trial](http://web.powerapps.com/trial) で、30 日間有効な無料試用版ライセンスにサインアップできます。 無料試用版ライセンスの有効期限が切れた場合は更新できます。

* 別のユーザーのリソースを検索する必要がある場合は、[Office 365 全体管理者](https://support.office.com/article/assign-admin-roles-in-office-365-for-business-eac4d046-1afd-4f1a-85fc-8219c79e1504)または [Azure Active Directory 全体管理者](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal)のアクセス許可 (環境管理者は、自分がアクセス許可を持っている環境および環境リソースにのみアクセスできることに注意してください)。

### <a name="cmdlet-list"></a>コマンドレット一覧
> [!NOTE]
> 適切なプレフィックスを追加して競合を回避するために、最新リリースでコマンドレットの関数名の一部を更新しました。 変更した内容の概要については、次の表を参照してください。

| 目的 | コマンドレット
| --- | ---
| 環境と Common Data Service for Apps データベースの読み取り、更新、削除を行う | New-AdminPowerAppEnvironment **\*新規\*** <br> Set-AdminPowerAppEnvironmentDisplayName **\*新規\*** <br> Get-AdminPowerAppEnvironment *(以前の Get-AdminEnvironment)* <br> Remove-AdminPowerAppEnvironment *(以前の Remove-AdminEnvironment)* <br> New-AdminPowerAppCdsDatabase **\*新規\*** <br> Get-AdminPowerAppCdsDatabaseLanguages **\*新規\*** <br> Get-AdminPowerAppCdsDatabaseCurrencies **\*新規\*** <br> Get-AdminPowerAppEnvironmentLocations **\*新規\***
| 環境のアクセス許可の読み取り、更新、削除を行う <br><br> *現在、これらのコマンドレットは、Common Data Service (CDS) for Apps データベースがない環境でのみ動作します。* | Get-AdminPowerAppEnvironmentRoleAssignment *(以前の Get-AdminEnvironmentRoleAssignment)* <br> Set-AdminPowerAppEnvironmentRoleAssignment *(以前の Set-AdminEnvironmentRoleAssignment)* <br> Remove-AdminPowerAppEnvironmentRoleAssignment *(以前の Remove-AdminEnvironmentRoleAssignment)*
| キャンバス アプリの読み取り、更新、削除を行う | Get-AdminPowerApp *(以前の Get-AdminApp)* <br> Remove-AdminPowerApp *(以前の Remove-AdminApp)* <br> Get-AdminPowerAppConnectionReferences **\*新規\*** <br> Set-AdminPowerAppAsFeatured **\*新規\*** <br> Clear-AdminPowerAppAsFeatured **\*新規\*** <br> Set-AdminPowerAppAsHero **\*新規\*** <br> Clear-AdminPowerAppAsHero **\*新規\*** <br> Set-AdminPowerAppApisToBypassConsent **\*新規\*** <br> Clear-AdminPowerAppApisToBypassConsent **\*新規\***
| キャンバス アプリのアクセス許可の読み取り、更新、削除を行う | Get-AdminPowerAppRoleAssignment *(以前の Get-AdminAppRoleAssignment)* <br> Remove-AdminPowerAppRoleAssignment *(以前の Remove-AdminAppRoleAssignment)* <br> Set-AdminPowerAppRoleAssignment *(以前の Set-AdminAppRoleAssignment)* <br> Set-AdminPowerAppOwner *(以前の Set-AdminAppOwner)*
| フローの読み取り、更新、削除を行う | Get-AdminFlow <br> Enable-AdminFlow <br> Disable-AdminFlow <br> Remove-AdminFlow <br> Remove-AdminFlowApprovals **\*新規\***
| フローのアクセス許可の読み取り、更新、削除を行う | Get-AdminFlowOwnerRole <br> Set-AdminFlowOwnerRole <br> Remove-AdminFlowOwnerRole
| 接続の読み取り、削除を行う | Get-AdminPowerAppConnection *(以前の Get-AdminConnection)* <br> Remove-AdminPowerAppConnection *(以前の Remove-AdminConnection)*
| 接続のアクセス許可の読み取り、更新、削除を行う | Get-AdminPowerAppConnectionRoleAssignment *(以前の Get-AdminConnectionRoleAssignment)* <br> Set-AdminPowerAppEnvironmentConnectionRoleAssignment *(以前の Set-AdminConnectionRoleAssignment)* <br> Remove-AdminPowerAppConnectionRoleAssignment *(以前の Remove-AdminConnectionRoleAssignment)*
| カスタム コネクタの読み取り、削除を行う | Get-AdminPowerAppConnector *(以前の Get-AdminConnector)* <br> Remove-AdminPowerAppConnector *(以前の Remove-AdminConnector)*
| カスタム コネクタのアクセス許可の読み取り、更新、削除を行う | Get-AdminPowerAppConnectorRoleAssignment *(以前の Get-AdminConnectorRoleAssignment)*<br> Set-AdminPowerAppConnectorRoleAssignment *(以前の Set-AdminConnectorRoleAssignment)* <br> Remove-AdminPowerAppConnectorRoleAssignment *(以前の Remove-AdminConnectorRoleAssignment)*
| ユーザーの PowerApps ユーザー設定、ユーザー アプリ設定、通知の読み取りを行う | Get-AdminPowerAppsUserDetails
| ユーザーには表示されない、フローの実行をサポートする、ユーザーの Microsoft Flow 設定の読み取りおよび削除を行う | Get-AdminFlowUserDetails <br> Remove-AdminFlowUserDetails
| 組織のデータ損失防止ポリシーの作成、読み取り、更新、削除を行う | Get-AdminDlpPolicy *(以前の Get-AdminApiPolicy)* <br> Add-AdminDlpPolicy *(以前の Add-AdminApiPolicy)* <br> Remove-AdminDlpPolicy *(以前の Remove-AdminApiPolicy)* <br> Set-AdminDlpPolicy *(以前の Set-AdminApiPolicy)* <br> Add-ConnectorToBusinessDataGroup <br>  Remove-ConnectorFromBusinessDataGroup

> [!NOTE]
> 各コマンドレットの構文を理解し、サンプルを見るには、次のコマンドを使います。
>```
>Get-Help Get-AdminEnvironment
>Get-Help Get-AdminEnvironment -Examples
>Get-Help Get-AdminEnvironment -Detailed
>```

## <a name="questions"></a>ご質問

コメント、提案、または質問がある場合は、[Administering PowerApps Community Board](https://powerusers.microsoft.com/t5/Administering-PowerApps/bd-p/Admin_PowerApps) までお知らせください。

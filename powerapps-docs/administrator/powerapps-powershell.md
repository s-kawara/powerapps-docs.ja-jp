---
title: PowerShell のサポート (プレビュー) | Microsoft Docs
description: さまざまな PowerShell コマンドレットについて説明し、それらをでインストールして実行する方法のチュートリアルを示します。
author: jamesol-msft
manager: kfile
ms.service: powerapps
ms.component: pa-admin
ms.topic: reference
ms.date: 04/23/2018
ms.author: jamesol
ms.openlocfilehash: 953efbabcdce55ac58376f927d5e399e69a40974
ms.sourcegitcommit: b3b6118790d6b7b4285dbcb5736e55f6e450125c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/15/2018
---
# <a name="powershell-support-for-powerapps-preview"></a>PowerApps 向け PowerShell のサポート (プレビュー)
アプリの作成者と管理者向けの PowerShell コマンドレットのプレビューが開始されたことで、現在は [PowerApps](https://web.powerapps.com) または [PowerApps 管理センター](https://admin.powerapps.com)で手動によってのみ可能な監視および管理タスクの多くを自動化できます。

## <a name="installation"></a>インストール
アプリ作成者向けの PowerShell コマンドレットを実行するには、次のようにします。

1. [PowerShell スクリプト ファイル](https://go.microsoft.com/fwlink/?linkid=872358)をダウンロードします。

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

6. コマンドにアクセスする前に、次のコマンドを使って資格情報を提供します。 これらの資格情報は約 8 時間以内に更新され、その後コマンドレットの使用を続けるには再度サインインする必要があります。

    ```
    Add-PowerAppsAccount
    ```

7.  現在、次のコマンドを使用して PowerShell ファイルを手動でブロック解除することが必要な場合がある[既知の問題](https://powerusers.microsoft.com/t5/Administering-PowerApps/Getting-errors-when-I-try-to-import-the-preview-powerapps/td-p/109036)があります。

    ```
    dir . | Unblock-File
    ```

## <a name="powerapps-cmdlets-for-app-makers-preview"></a>アプリ開発者向けの PowerApps コマンドレット (プレビュー)

### <a name="prerequisite"></a>前提条件
PowerApps の有効なライセンスを持つユーザーはコマンドレットで操作を実行することができますが、アクセスできるのは自分で作成したリソースまたは自分が共有を受けているリソース (アプリ、フローなど) のみです。

### <a name="cmdlet-list"></a>コマンドレット一覧
| 目的 | コマンドレット |
| --- | --- |
| 環境を読み取る | Get-PowerAppsEnvironment <br> Get-FlowEnvironment
| キャンバス アプリの読み取り、更新、削除を行う | Get-App <br> Remove-App <br> Publish-App <br> Set-AppDisplayName <br> Get-AppVersion <br> Restore-AppVersion
| キャンバス アプリのアクセス許可の読み取り、更新、削除を行う | Get-AppRoleAssignment <br> Set-AppRoleAssignment <br> Remove-AppRoleAssignment
| フローの読み取り、更新、削除を行う | Get-Flow <br> Get-FlowRun <br> Enable-Flow <br> Disable-Flow <br> Remove-Flow
| フローのアクセス許可の読み取り、更新、削除を行う | Get-FlowOwnerRole <br> Set-FlowOwnerRole <br> Remove-FlowOwnerRole
| フローの承認の読み取り、応答を行う | Get-FlowApprovalRequest <br> Get-FlowApproval <br> RespondTo-FlowApprovalRequest
| 接続の読み取り、削除を行う | Get-Connection <br> Remove-Connection
| 接続のアクセス許可の読み取り、更新、削除を行う | Get-ConnectionRoleAssignment <br> Set-ConnectionRoleAssignment <br> Remove-ConnectionRoleAssignment
| コネクタの読み取り、削除を行う | Get-Connector <br> Remove-Connector
| カスタム コネクタのアクセス許可の読み取り、更新、削除を行う | Get-ConnectorRoleAssignment <br> Set-ConnectorRoleAssignment <br> Remove-ConnectorRoleAssignment

> [!NOTE]
> 各コマンドレットの構文を理解し、サンプルを見るには、次のコマンドを使います。
>```
>Get-Help Get-PowerAppsEnvironment
>Get-Help Get-PowerAppsEnvironment -Examples
>Get-Help Get-PowerAppsEnvironment -Detailed
>```

## <a name="powerapps-cmdlets-for-administrators-preview"></a>管理者向けの PowerApps コマンドレット (プレビュー)

### <a name="prerequisite"></a>前提条件
管理コマンドレットで管理操作を実行するには、次のものが必要です。

* 有料の PowerApps プラン 2 ライセンスまたは PowerApps プラン 2 無料試用版ライセンス。 [http://web.powerapps.com/trial](http://web.powerapps.com/trial) で、30 日間有効な無料試用版ライセンスにサインアップできます。 無料試用版ライセンスの有効期限が切れた場合は更新できます。

* 別のユーザーのリソースを検索する必要がある場合は、[Office 365 全体管理者](https://support.office.com/article/assign-admin-roles-in-office-365-for-business-eac4d046-1afd-4f1a-85fc-8219c79e1504)または [Azure Active Directory 全体管理者](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal)のアクセス許可 (環境管理者は、自分がアクセス許可を持っている環境および環境リソースにのみアクセスできることに注意してください)。

### <a name="cmdlet-list"></a>コマンドレット一覧
| 目的 | コマンドレット
| --- | ---
| 環境の読み取り、削除を行う | Get-AdminEnvironment <br> Remove-AdminEnvironment
| 環境のアクセス許可の読み取り、更新、削除を行う <br><br> *これらのコマンドレットは、Common Data Service (CDS) for Apps データベースがない環境でのみ動作します。* | Get-AdminEnvironmentRoleAssignment <br> Set-AdminEnvironmentRoleAssignment <br> Remove-AdminEnvironmentRoleAssignment
| キャンバス アプリの読み取り、削除を行う | Get-AdminApp <br> Remove-AdminApp
| キャンバス アプリのアクセス許可の読み取り、更新、削除を行う | Get-AdminAppRoleAssignment <br> Remove-AdminAppRoleAssignment <br> Set-AdminAppRoleAssignment <br> Set-AdminAppOwner
| フローの読み取り、更新、削除を行う | Get-AdminFlow <br> Enable-AdminFlow <br> Disable-AdminFlow <br> Remove-AdminFlow  <br> Remove-AdminFlowOwnerRole

> [!NOTE]
> 各コマンドレットの構文を理解し、サンプルを見るには、次のコマンドを使います。
>```
>Get-Help Get-AdminEnvironment
>Get-Help Get-AdminEnvironment -Examples
>Get-Help Get-AdminEnvironment -Detailed
>```

## <a name="questions"></a>ご質問

コメント、提案、または質問がある場合は、[Administering PowerApps Community Board](https://powerusers.microsoft.com/t5/Administering-PowerApps/bd-p/Admin_PowerApps) までお知らせください。

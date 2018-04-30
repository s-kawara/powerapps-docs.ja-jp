---
title: PowerShell のサポート | Microsoft Docs
description: PowerShell による PowerApps のサポートについて説明します
services: powerapps
suite: powerapps
documentationcenter: na
author: jamesol-msft
manager: kfile
editor: ''
tags: ''
ms-topic: article
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/17/2018
ms.author: jamesol
ms.openlocfilehash: 274d34ca56cc993ec26fa4f4ced77bb2aba9985f
ms.sourcegitcommit: e3a2819c14ad67cc4ca6640b9064550d0f553d8f
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/20/2018
---
# <a name="powershell-support-for-powerapps-preview"></a>PowerApps 向け PowerShell のサポート (プレビュー)

アプリの作成者と管理者向けの PowerShell コマンドレットのプレビューが開始されたことで、現在は [PowerApps サイト](https://web.powerapps.com)または [PowerApps 管理センター](https://admin.powerapps.com)で手動によってのみ可能な監視および管理タスクの多くを自動化できます。

## <a name="installation"></a>インストール
アプリ作成者向けの PowerShell コマンドレットを実行するには、まず、次の手順を実行する必要があります。

1. PowerShell スクリプト ファイルを[こちら](https://go.microsoft.com/fwlink/?linkid=872358)からダウンロードします

2. フォルダーにファイルを解凍します

3. 同じフォルダーにおいて、管理者として PowerShell コマンド ウィンドウを開きます

4. その後、次の 1 回限りの PowerShell コマンドを実行します (現在お使いのコンピューターで PowerShell コマンドを実行したことがないものとします)。

    ```
    Set-ExecutionPolicy -ExecutionPolicy Unrestricted -Force
    ```

5. 次のコマンドを使って必要なモジュールをインポートします。

    ```
    Import-Module .\Microsoft.PowerApps.Administration.PowerShell.psm1 -Force
    Import-Module .\Microsoft.PowerApps.PowerShell.psm1 -Force
    ```

6. 最後に、コマンドにアクセスする前に、次のコマンドを使って、資格情報を提供する必要があります。 これらの資格情報は約 8 時間以内に更新され、その後コマンドレットの使用を続けるには再度サインインする必要があります。

    ```
    Add-PowerAppsAccount
    ```

## <a name="powerapps-cmdlets-for-app-makers-preview"></a>アプリ開発者向けの PowerApps コマンドレット (プレビュー)

### <a name="prerequisite"></a>前提条件
PowerApps の有効なライセンスを持つすべてのユーザーは、以下のコマンドレットを使って操作を実行できます。 ただし、自分で作成したか、自分に共有されているリソース (例: アプリ、フローなど) に対してのみアクセスできます。

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
> 次のコマンドを使うと、各コマンドレットの構文を理解し、サンプルを見ることができます。
>```
>Get-Help Get-PowerAppsEnvironment
>Get-Help Get-PowerAppsEnvironment -Examples
>Get-Help Get-PowerAppsEnvironment -Detailed
>```

## <a name="powerapps-cmdlets-for-administrators-preview"></a>管理者向けの PowerApps コマンドレット (プレビュー)

### <a name="prerequisite"></a>前提条件
管理コマンドレットで管理操作を実行するには、次のアクセス許可を持つアカウントが必要です。

- 有料の PowerApps プラン 2 ライセンス、または PowerApps プラン 2 無料試用版ライセンス。 [http://web.powerapps.com/trial](http://web.powerapps.com/trial) で、30 日間有効な無料試用版ライセンスにサインアップできます。 無料試用版ライセンスの有効期限が切れた場合は更新できます。

- 別のユーザーのリソースを検索する必要がある場合は、[Office 365 全体管理者](https://support.office.com/article/assign-admin-roles-in-office-365-for-business-eac4d046-1afd-4f1a-85fc-8219c79e1504)または [Azure Active Directory 全体管理者](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal)の特権も必要です。 それ以外の場合は、自分が環境管理者特権を持っている環境および環境リソースにのみアクセスできます。

### <a name="cmdlet-list"></a>コマンドレット一覧
| 目的 | コマンドレット
| --- | ---
| 環境の読み取り、削除を行う | Get-AdminEnvironment <br> Remove-AdminEnvironment
| 環境の特権の読み取り、更新、削除を行う <br><br> *これらのコマンドレットは、Common Data Service for Apps データベースがない環境でのみ動作します。* | Get-AdminEnvironmentRoleAssignment <br> Set-AdminEnvironmentRoleAssignment <br> Remove-AdminEnvironmentRoleAssignment
| キャンバス アプリの読み取り、削除を行う | Get-AdminApp <br> Remove-AdminApp
| キャンバス アプリのアクセス許可の読み取り、更新、削除を行う | Get-AdminAppRoleAssignment <br> Remove-AdminAppRoleAssignment <br> Set-AdminAppRoleAssignment <br> Set-AdminAppOwner
| フローの読み取り、更新、削除を行う | Get-AdminFlow <br> Enable-AdminFlow <br> Disable-AdminFlow <br> Remove-AdminFlow  <br> Remove-AdminFlowOwnerRole

> [!NOTE]
> 次のコマンドを使うと、各コマンドレットの構文を理解し、サンプルを見ることができます。
>```
>Get-Help Get-AdminEnvironment
>Get-Help Get-AdminEnvironment -Examples
>Get-Help Get-AdminEnvironment -Detailed
>```

## <a name="questions"></a>ご質問

コメント、提案、または質問がある場合は、[Administering PowerApps Community Board](https://powerusers.microsoft.com/t5/Administering-PowerApps/bd-p/Admin_PowerApps) までお知らせください。

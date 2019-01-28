---
title: PowerShell のサポート (プレビュー) | Microsoft Docs
description: さまざまな PowerShell コマンドレットについて説明し、それらをでインストールして実行する方法のチュートリアルを示します。
author: jamesol-msft
manager: kvivek
ms.service: powerapps
ms.component: pa-admin
ms.topic: reference
ms.date: 01/18/2019
ms.author: jamesol
search.audienceType:
- admin
search.app:
- D365CE
- PowerApps
- Powerplatform
ms.openlocfilehash: 0152296adbe01abae2b831576c312a43d1f2a2b8
ms.sourcegitcommit: 3ce7c17f90f87756a072210c8abfbd93733a6d4c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/18/2019
ms.locfileid: "54397769"
---
# <a name="powershell-support-for-powerapps-preview"></a>PowerApps 向け PowerShell のサポート (プレビュー)
アプリの作成者と管理者向けの PowerShell コマンドレットのプレビューが開始されたことで、現在は [PowerApps](https://web.powerapps.com/?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) または [PowerApps 管理センター](https://admin.powerapps.com)で手動によってのみ可能な監視および管理タスクの多くを自動化できます。

## <a name="cmdlets"></a>コマンドレット
[コマンドレット](https://docs.microsoft.com/powershell/developer/cmdlet/writing-a-windows-powershell-cmdlet)は PowerShell スクリプト言語で記述された関数であり、Windows PowerShell 環境でコマンドを実行します。 この PowerApps コマンドレットを実行することで、Web ブラウザーで管理ポータルにアクセスすることなく、ビジネス アプリケーション プラットフォームとやりとりできます。 このコマンドレットを他の PowerShell 関数と組み合わせ、ワークフローを最適化できる複雑なスクリプトを記述できます。 テナントの管理者でなくてもコマンドレットを使用できますが、自分が所有しているリソースに制限されることにご留意ください。 "Admin" という言葉で始まるコマンドレットは管理者ユーザー アカウントで使うように設計されています。

コマンドレットは 2 つの別個のモジュールとして PowerShell ギャラリーで利用できます。 
- [Administrator](https://www.powershellgallery.com/packages/Microsoft.PowerApps.Administration.PowerShell/2.0.1)
- [Maker](https://www.powershellgallery.com/packages/Microsoft.PowerApps.PowerShell/1.0.1) 

## <a name="installation"></a>インストール
アプリ作成者向けの PowerShell コマンドレットを実行するには、次のようにします。

1. 管理者として PowerShell を実行します。

   > [!div class="mx-imgBorder"] 
   > ![管理者として PowerShell を実行する](media/open-powershell-as-admin75.png "管理者として PowerShell を実行する")

2. 次のコマンドを使って必要なモジュールをインポートします。

    ```
    Install-Module -Name Microsoft.PowerApps.Administration.PowerShell
    Install-Module -Name Microsoft.PowerApps.PowerShell -AllowClobber
    ```
3. レポジトリの *InstallationPolicy* 値の変更を承認するように求められたら、「A」と入力してモジュールごとに **Enter** を押し、すべてのモジュールに対して承認を選択します。

   ![InstallationPolicy 値を承認する](media/accept-installationpolicy-value75.png "InstallationPolicy 値を承認する")

4. コマンドにアクセスする前に、次のコマンドを使用して資格情報を指定できます。 これらの資格情報は約 8 時間以内に更新され、その後コマンドレットの使用を続けるには再度サインインする必要があります。

    ```
    # This call opens prompt to collect credentials (Azure Active Directory account and password) used by the commands 
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

### <a name="cmdlet-list---maker-cmdlets"></a>コマンドレットの一覧 - Maker コマンドレット
> [!NOTE]
> 適切なプレフィックスを追加して競合を回避するために、最新リリースでコマンドレットの関数名の一部を更新しました。 変更した内容の概要については、次の表を参照してください。

| 目的 | コマンドレット |
| --- | --- |
| 環境を読み取る | Get-PowerAppEnvironment *(以前の Get-PowerAppsEnvironment)* <br> Get-FlowEnvironment |
| キャンバス アプリの読み取り、更新、削除を行う | Get-PowerApp *(以前の Get-App)* <br> Remove-PowerApp *(以前の Remove-App)* <br> Publish-PowerApp *(以前の Publish-App)* <br> Set-AppDisplayName *(以前の Set-PowerAppDisplayName)*<br> Get-PowerAppVersion *(以前の Get-AppVersion)* <br> Restore-PowerAppVersion *(以前の Restore-AppVersion)* |
| キャンバス アプリのアクセス許可の読み取り、更新、削除を行う | Get-PowerAppRoleAssignment *(以前の Get-AppRoleAssignment)* <br> Set-PowerAppRoleAssignment *(以前の Set-AppRoleAssignment)* <br> Remove-PowerAppRoleAssignment *(以前の Remove-AppRoleAssignment)* |
| フローの読み取り、更新、削除を行う | Get-Flow <br> Get-FlowRun <br> Enable-Flow <br> Disable-Flow <br> Remove-Flow |
| フローのアクセス許可の読み取り、更新、削除を行う | Get-FlowOwnerRole <br> Set-FlowOwnerRole <br> Remove-FlowOwnerRole |
| フローの承認の読み取り、応答を行う | Get-FlowApprovalRequest <br> Get-FlowApproval <br> RespondTo-FlowApprovalRequest |
| 接続の読み取り、削除を行う | Get-PowerAppConnection *(以前の Get-Connection)* <br> Remove-PowerAppConnection *(以前の Remove-Connection)* |
| 接続のアクセス許可の読み取り、更新、削除を行う | Get-PowerAppConnectionRoleAssignment *(以前の Get-ConnectionRoleAssignment)* <br> Set-PowerAppConnectionRoleAssignment *(以前の Set-ConnectionRoleAssignment)* <br> Remove-PowerAppConnectionRoleAssignment *(以前の Remove-ConnectionRoleAssignment)* |
| コネクタの読み取り、削除を行う | Get-PowerAppConnector *(以前の Get-Connector)* <br> Remove-PowerAppConnector *(以前の Remove-Connector)* |
| カスタム コネクタのアクセス許可の読み取り、更新、削除を行う | Get-PowerAppConnectorRoleAssignment *(以前の Get-ConnectorRoleAssignment)* <br> Set-PowerAppConnectorRoleAssignment *(以前の Set-ConnectorRoleAssignment)* <br> Remove-PowerAppConnectorRoleAssignment *(以前の Remove-ConnectorRoleAssignment)* |

## <a name="powerapps-cmdlets-for-administrators-preview"></a>管理者向けの PowerApps コマンドレット (プレビュー)

### <a name="prerequisite"></a>前提条件
管理コマンドレットで管理操作を実行するには、次のものが必要です。

* 有料の PowerApps プラン 2 ライセンスまたは PowerApps プラン 2 無料試用版ライセンス。 [http://web.powerapps.com/trial](http://web.powerapps.com/trial) で、30 日間有効な無料試用版ライセンスにサインアップできます。 無料試用版ライセンスの有効期限が切れた場合は更新できます。

* 別のユーザーのリソースを検索する必要がある場合は、[Office 365 全体管理者](https://support.office.com/article/assign-admin-roles-in-office-365-for-business-eac4d046-1afd-4f1a-85fc-8219c79e1504)または [Azure Active Directory 全体管理者](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal)のアクセス許可 (環境管理者は、自分がアクセス許可を持っている環境および環境リソースにのみアクセスできることに注意してください)。

### <a name="cmdlet-list---admin-cmdlets"></a>コマンドレットの一覧 - Admin コマンドレット

| 目的 | コマンドレット
| --- | ---
| 環境と Common Data Service for Apps データベースの読み取り、更新、削除を行う | New-AdminPowerAppEnvironment <br> Set-AdminPowerAppEnvironmentDisplayName <br> Get-AdminPowerAppEnvironment *(以前の Get-AdminEnvironment)* <br> Remove-AdminPowerAppEnvironment *(以前の Remove-AdminEnvironment)* <br> New-AdminPowerAppCdsDatabase <br> Get-AdminPowerAppCdsDatabaseLanguages <br> Get-AdminPowerAppCdsDatabaseCurrencies <br> Get-AdminPowerAppEnvironmentLocations |
| CDS データベースの削除 | Remove-LegacyCDSDatabase **\*New\*** | 
| 環境のアクセス許可の読み取り、更新、削除を行う <br><br> *現在、これらのコマンドレットは、Common Data Service (CDS) for Apps データベースがない環境でのみ動作します。* | Get-AdminPowerAppEnvironmentRoleAssignment *(以前の Get-AdminEnvironmentRoleAssignment)* <br> Set-AdminPowerAppEnvironmentRoleAssignment *(以前の Set-AdminEnvironmentRoleAssignment)* <br> Remove-AdminPowerAppEnvironmentRoleAssignment *(以前の Remove-AdminEnvironmentRoleAssignment)* |
| キャンバス アプリの読み取り、更新、削除を行う | Get-AdminPowerApp *(以前の Get-AdminApp)* <br> Remove-AdminPowerApp *(以前の Remove-AdminApp)* <br> Get-AdminPowerAppConnectionReferences <br> Set-AdminPowerAppAsFeatured <br> Clear-AdminPowerAppAsFeatured <br> Set-AdminPowerAppAsHero <br> Clear-AdminPowerAppAsHero <br> Set-AdminPowerAppApisToBypassConsent <br> Clear-AdminPowerAppApisToBypassConsent |
| キャンバス アプリのアクセス許可の読み取り、更新、削除を行う | Get-AdminPowerAppRoleAssignment *(以前の Get-AdminAppRoleAssignment)* <br> Remove-AdminPowerAppRoleAssignment *(以前の Remove-AdminAppRoleAssignment)* <br> Set-AdminPowerAppRoleAssignment *(以前の Set-AdminAppRoleAssignment)* <br> Set-AdminPowerAppOwner *(以前の Set-AdminAppOwner)* |
| フローの読み取り、更新、削除を行う | Get-AdminFlow <br> Enable-AdminFlow <br> Disable-AdminFlow <br> Remove-AdminFlow <br> Remove-AdminFlowApprovals |
| フローのアクセス許可の読み取り、更新、削除を行う | Get-AdminFlowOwnerRole <br> Set-AdminFlowOwnerRole <br> Remove-AdminFlowOwnerRole |
| 接続の読み取り、削除を行う | Get-AdminPowerAppConnection *(以前の Get-AdminConnection)* <br> Remove-AdminPowerAppConnection *(以前の Remove-AdminConnection)* |
| 接続のアクセス許可の読み取り、更新、削除を行う | Get-AdminPowerAppConnectionRoleAssignment *(以前の Get-AdminConnectionRoleAssignment)* <br> Set-AdminPowerAppEnvironmentConnectionRoleAssignment *(以前の Set-AdminConnectionRoleAssignment)* <br> Remove-AdminPowerAppConnectionRoleAssignment *(以前の Remove-AdminConnectionRoleAssignment)* |
| カスタム コネクタの読み取り、削除を行う | Get-AdminPowerAppConnector *(以前の Get-AdminConnector)* <br> Remove-AdminPowerAppConnector *(以前の Remove-AdminConnector)* |
| カスタム コネクタのアクセス許可の読み取り、更新、削除を行う | Get-AdminPowerAppConnectorRoleAssignment *(以前の Get-AdminConnectorRoleAssignment)*<br> Set-AdminPowerAppConnectorRoleAssignment *(以前の Set-AdminConnectorRoleAssignment)* <br> Remove-AdminPowerAppConnectorRoleAssignment *(以前の Remove-AdminConnectorRoleAssignment)* |
| ユーザーの PowerApps ユーザー設定、ユーザー アプリ設定、通知の読み取りを行う | Get-AdminPowerAppsUserDetails |
| ユーザーには表示されない、フローの実行をサポートする、ユーザーの Microsoft Flow 設定の読み取りおよび削除を行う | Get-AdminFlowUserDetails <br> Remove-AdminFlowUserDetails |
| 組織のデータ損失防止ポリシーの作成、読み取り、更新、削除を行う | Get-AdminDlpPolicy *(以前の Get-AdminApiPolicy)* <br> New-AdminDlpPolicy *(以前の Add-AdminApiPolicy)* <br> Remove-AdminDlpPolicy *(以前の Remove-AdminApiPolicy)* <br> Set-AdminDlpPolicy *(以前の Set-AdminApiPolicy)* <br> Add-ConnectorToBusinessDataGroup <br>  Remove-ConnectorFromBusinessDataGroup <br/>Add-CustomConnectorToPolicy<br/> Remove-CustomConnectorFromPolicy|

## <a name="tips"></a>ヒント

- Get-Help ‘CmdletName’ を使用すると、サンプルの一覧を取得できます。

     ![Get-Help コマンド](media/get-help-cmdlet.png "Get-Help コマンド")

- 入力タグの選択肢を順番に表示するには、コマンドレット名の後にダッシュ (-) 文字を入力し、タブ キーをクリックします。

コマンドの例:

```
Get-Help Get-AdminPowerAppEnvironment
Get-Help Get-AdminPowerAppEnvironment -Examples
Get-Help Get-AdminPowerAppEnvironment -Detailed
```

## <a name="operation-examples"></a>操作の例

以下は、PowerApps の新規コマンドレットと既存コマンドレットの使用方法を示す一般的なシナリオをいくつか挙げたものです。

- [環境コマンド](#environments-commands)
- [PowerApps コマンド](#powerapps-commands)
- [フロー コマンド](#flow-commands)
- [API 接続コマンド](#api-connection-commands)
- [データ損失防止 (DLP) ポリシー コマンド](#data-loss-prevention-dlp-policy-commands)

### <a name="environments-commands"></a>環境コマンド

このコマンドを使用すると、テナントにおける環境の詳細を取得したり、更新したりできます。

#### <a name="display-a-list-of-all-environments"></a>すべての環境の一覧を表示する

```
Get-AdminPowerAppEnvironment
```

テナント全体を対象に各環境の一覧をその詳細 (環境名 (guid)、表示名、場所、作成者など) と共に返します。

#### <a name="display-details-of-your-default-environment"></a>既定の環境の詳細を表示する

```
Get-AdminPowerAppEnvironment –Default
```

テナントの既定の環境に関してのみ詳細を返します。

#### <a name="display-details-of-a-specific-environment"></a>特定の環境の詳細を表示する

```
Get-AdminPowerAppEnvironment –EnvironmentName ‘EnvironmentName’
```

**注**:*EnvironmentName* フィールドは一意の識別子であり、*DisplayName* とは異なります (次の画像にある出力の最初のフィールドと 2 つ目のフィールドをご覧ください)。

![Get-AdminEnvironment コマンド](media/get-adminenvironment.png "Get-AdminEnvironment コマンド")

### <a name="powerapps-commands"></a>PowerApps コマンド

テナントで PowerApps データを読み取ったり、変更したりするためにこの操作が利用されます。

#### <a name="display-a-list-of-all-powerapps"></a>すべての PowerApps の一覧を表示する

```
Get-AdminPowerApp
```

テナント全体を対象にすべての PowerApps の一覧とその詳細 (アプリケーション名 (guid)、表示名、作成者など) を返します。

#### <a name="display-a-list-of-all-powerapps-that-match-the-input-display-name"></a>入力された表示名に一致するすべての PowerApps の一覧を表示する

```
Get-AdminPowerApp 'DisplayName'
```

テナント内の PowerApps のうち、表示名に一致するもの全部を一覧にして返します。 

**注**:スペースを含む入力値は引用符文字 (”) で囲みます。

#### <a name="feature-an-application"></a>アプリケーションを推奨する

```
Set-AdminPowerAppAsFeatured –AppName 'AppName'
```

おすすめのアプリケーションがグループ化され、PowerApps モバイル プレーヤーの一覧の一番上に表示されます。

**注**:環境の場合と同様に、*AppName* フィールドは一意の識別子であり、*DisplayName* とは異なります。 表示名に基づいて操作を実行する場合、一部の機能ではパイプラインを使用できます (次の関数をご覧ください)。

#### <a name="make-an-application-a-hero-app-using-the-pipeline"></a>パイプラインを使用し、アプリケーションを Hero アプリにする

```
Get-AdminPowerApp 'DisplayName' | Set-AdminPowerAppAsHero
```

Hero アプリは PowerApps モバイル プレーヤーの一覧の一番上に表示されます。 Hero アプリに指定できるアプリは 1 つだけです。

パイプライン機能を収納するように関数が記述されている場合、パイプライン (2 つのコマンドレット間の "|" 文字として表される) は最初のコマンドレットの出力を受け取り、2 つ目のコマンドレットの入力値としてそれを渡します。

**注**: アプリを Hero に指定するには、おすすめアプリとして既に設定されている必要があります。

#### <a name="display-the-number-of-apps-each-user-owns"></a>各ユーザーが所有するアプリの数を表示する

```
Get-AdminPowerApp | Select –ExpandProperty Owner | Select –ExpandProperty displayname | Group
```

ネイティブ PowerShell 関数と PowerApps コマンドレットを組み合わせ、データをさらに操作できます。 ここでは Select 関数を使用し、Owner 属性 (オブジェクト) を Get-AdminApp オブジェクトから分離します。 その出力を別の Select 関数にパイプラインすることでオーナー オブジェクトの名前を分離します。 最後に、2 番目の Select 関数出力を Group 関数に渡すことで、各オーナーのアプリ数が含まれるテーブルを返します。

![Get-AdminPowerApp コマンド](media/get-adminpowerapp.png "Get-AdminPowerApp コマンド")

#### <a name="display-the-number-of-apps-in-each-environment"></a>各環境のアプリ数を表示する

```
Get-AdminPowerApp | Select -ExpandProperty EnvironmentName | Group | %{ New-Object -TypeName PSObject -Property @{ DisplayName = (Get-AdminPowerAppEnvironment -EnvironmentName $_.Name | Select -ExpandProperty displayName); Count = $_.Count } }
```

![Get-AdminPowerApp コマンド](media/get-adminpowerapp-environment.png "Get-AdminPowerApp コマンド")

#### <a name="download-powerapps-user-details"></a>PowerApps ユーザーの詳細をダウンロードする

```
Get-AdminPowerAppsUserDetails -OutputFilePath '.\adminUserDetails.txt' –UserPrincipalName ‘admin@bappartners.onmicrosoft.com’
```

上記のコマンドでは、指定されたテキスト ファイルに PowerApps ユーザーの詳細 (ユーザー プリンシパル名から指定されたユーザーの基本的な使用状況情報) が格納されます。 その名前のファイルがない場合、新しいファイルが作成されます。その名前でファイルが既に存在する場合、テキスト ファイルは上書きされます。

#### <a name="set-logged-in-user-as-the-owner-of-a-powerapp"></a>PowerApp のオーナーとしてログイン ユーザーを設定する

```
Set-AdminPowerAppOwner –AppName 'AppName' -AppOwner $Global:currentSession.userId –EnvironmentName 'EnvironmentName'
```

PowerApp のオーナー ロールを現在のユーザーに変更し、元のオーナーを "閲覧可能" タイプのロールに変更します。

**注**:AppName フィールドと EnvironmentName フィールドは一意の識別子 (guid) であり、表示名ではありません。

### <a name="flow-commands"></a>フロー コマンド

Microsoft Flow 関連のデータを表示したり、変更したりするときにこのコマンドを使用します。

#### <a name="display-all-flows"></a>すべてのフローを表示する

```
Get-AdminFlow
```

テナント内のすべてのフローを一覧で返します。

#### <a name="display-flow-owner-role-details"></a>フロー所有者ロールの詳細を表示する

```
Get-AdminFlowOwnerRole –EnvironmentName 'EnvironmentName' –FlowName ‘FlowName’
```

指定したフローのオーナー詳細を返します。

**注**:*環境*や *PowerApps* の場合と同様に、*FlowName* は一意の識別子 (guid) であり、フローの表示名とは異なります。

#### <a name="display-flow-user-details"></a>フロー ユーザー詳細を表示する

```
Get-AdminFlowUserDetails –UserId $Global:currentSession.userId
```

フローの使用状況に関するユーザー詳細を返します。 この例では、PowerShell セッションの現在のログイン ユーザーのユーザー ID を入力として使用しています。

#### <a name="remove-flow-user-details"></a>フロー ユーザー詳細を削除する

```
Remove-AdminFlowUserDetails –UserId 'UserId'
```

フロー ユーザーに関する詳細を Microsoft データベースから完全に削除します。 フロー ユーザー詳細を削除する前に、入力のユーザーが所有するすべてのフローを削除しておく必要があります。

**注**:UserId フィールドはユーザーの Azure Active Directory レコードのオブジェクト ID です。これは [Azure portal](https://portal.azure.com) で **[Azure Active Directory]**、**[ユーザー]**、**[プロファイル]**、**[オブジェクト ID]** の順に選択すると見つかります。 ここからこのデータにアクセスするには管理者でなければなりません。

#### <a name="export-all-flows-to-a-csv-file"></a>すべてのフローを CSV ファイルにエクスポートする

```
Get-AdminFlow | Export-Csv -Path '.\FlowExport.csv'
```

テナントにあるすべてのフローを表形式の .csv ファイルにエクスポートします。

### <a name="api-connection-commands"></a>API 接続コマンド

テナント内の API 接続を表示し、管理します。

#### <a name="display-all-native-connections-in-your-default-environment"></a>既定の環境にあるすべてのネイティブ接続を表示する

```
Get-AdminPowerAppEnvironment -Default | Get-AdminConnection
```

既定の環境にあるすべての API 接続を一覧表示します。 ネイティブ接続は Maker ポータルの **[データ]** の **[接続]** タブにあります。

#### <a name="display-all-custom-connectors-in-the-tenant"></a>テナント内のすべてのカスタム コネクタを表示する

```
Get-AdminPowerAppConnector
```

テナントにあるすべてのカスタム コネクタの詳細を一覧で返します。

### <a name="data-loss-prevention-dlp-policy-commands"></a>データ損失防止 (DLP) ポリシー コマンド

このコマンドレットによってテナントの DLP ポリシーが制御されます。

#### <a name="display-all-policies"></a>すべてのポリシーを表示する

```
Get-AdminDlpPolicy
```

すべてのポリシーの一覧を返します。

#### <a name="display-a-filtered-list-of-policies"></a>ポリシーの一覧にフィルターを適用して表示する

```
Get-AdminDlpPolicy 'DisplayName'
```

表示名でポリシーにフィルターを適用します。

#### <a name="display-all-business-data-only-api-connectors-in-a-policy"></a>ポリシーに含まれる "ビジネス データのみ" API コネクタをすべて表示する

```
Get-AdminDlpPolicy 'PolicyName' | Select –ExpandProperty BusinessDataGroup
```

入力されたポリシーの *[ビジネス データのみ]* (または *[BusinessDataGroup]*) フィールドにある API 接続を一覧表示します。

#### <a name="add-a-connector-to-the-business-data-only-group"></a>"ビジネス データのみ" グループにコネクタを追加する

```
Add-ConnectorToBusinessDataGroup -PolicyName 'PolicyName' –ConnectorName 'ConnectorName'
```

所与の DLP ポリシーの "ビジネス データのみ" グループにコネクタを追加します。 *DisplayName* および *ConnectorName* (入力として使用) 別のコネクタ一覧はここで確認します。

## <a name="version-history"></a>バージョン履歴
| バージョン | Date | 更新 |
| --- | --- | --- |
| 1.0 | 04/23/2018 | <ol> <li> Environments 承認、Apps 承認、Flows 承認、Flow 承認、Connections、Custom Connectors のための管理コマンドレットなど、アプリ作成者向けの PowerApps コマンドレット (プレビュー) の初回の起動 </li> <li> Environments、Apps、Flows のための管理コマンドレットなど、管理者向けの PowerApps コマンドレット (プレビュー) の初回の起動 </li></ol>|
| 2.0 | 05/24/2018 | <ol> <li> アプリ作成者向けコマンドレットと管理者向けコマンドレットの両方でマイナー バグ修正 </li> <li> 次の新しい管理者向けコマンドレットを追加: <br> Get-AdminConnection <br> Remove-AdminConnection <br> Get-AdminConnectionRoleAssignment <br> Set-AdminConnectionRoleAssignment <br>Remove-AdminConnectionRoleAssignment <br>Get-AdminConnector  <br>Remove-AdminConnector <br>Set-AdminConnectorRoleAssignment  <br>Get-AdminConnectorRoleAssignment  <br>Remove-AdminConnectorRoleAssignment <br>Get-AdminPowerAppsUserDetails <br>Get-AdminFlowUserDetails <br>Remove-AdminFlowUserDetails <br>Get-AdminApiPolicy  <br>Add-AdminApiPolicy <br>Remove-AdminApiPolicy <br>Set-AdminApiPolicy <br>Add-ConnectorToBusinessDataGroup  <br>Remove-ConnectorFromBusinessDataGroup </li> </ol>
| 3.0 | 07/30/2018 | <ol> <li> Add-PowerAppsAccount に資格情報を渡す機能を追加 (スクリプティングの繰り返しを可能にするため) </li> <li>  アプリ作成者向けコマンドレットと管理者向けコマンドレットの両方でマイナー バグ修正 </li> <li> アプリ作成者向けコマンドレットに "PowerApp" または "Flow" プレフィックスを追加 </li> <li>  管理者向けコマンドレットに "AdminPowerApp" または "AdminFlow" プレフィックスを追加 </li> <li> 次の新しい管理者向けコマンドレットを追加: <br> New-AdminPowerAppEnvironment <br> Set-AdminPowerAppEnvironmentDisplayName <br> New-AdminPowerAppCdsDatabase <br> Get-AdminPowerAppCdsDatabaseLanguages <br> Get-AdminPowerAppCdsDatabaseCurrencies <br> Get-AdminPowerAppEnvironmentLocations <br> Get-AdminPowerAppConnectionReferences <br> Set-AdminPowerAppAsFeatured <br> Clear-AdminPowerAppAsFeatured <br> Set-AdminPowerAppAsHero <br> Clear-AdminPowerAppAsHero <br> Set-AdminPowerAppApisToBypassConsent <br> Clear-AdminPowerAppApisToBypassConsent <br> Remove-AdminFlowApprovals </li></ol>
| 4.0 | 08/15/2018 | 既定で、関数を同期にする目的で (すなわち、データベースが正常にプロビジョニングされるまで返されません)、New-AdminPowerAppCdsDatabase にオプション パラメーターを追加
| 5.0 | 08/24/2018 | セキュリティ設定に基づいて使用される Flow 管理者コマンドレットの一部でデータが返されない問題を解決
| 6.0 | 01/09/2019 | <ol><li>コマンドレットを、Administrator と Maker という 2 つの別個のモジュールとして PowerShell ギャラリーで利用できるようになりました。</li> <li>次の管理コマンドレットを追加しました。Remove-LegacyCDSDatabase</li><li> 操作の例を追加しました</li><li>HTTP とカスタム コネクタを管理する機能をデータ損失防止 (DLP) に追加しました</li></ol>|

## <a name="questions"></a>ご質問

コメント、提案、または質問がある場合は、[Administering PowerApps Community Board](https://powerusers.microsoft.com/t5/Administering-PowerApps/bd-p/Admin_PowerApps) までお知らせください。

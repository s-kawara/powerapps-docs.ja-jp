---
title: XRM ツール用 PowerShell コマンドレットを使用してアプリ用 CDS に接続する (アプリ用 Common Data Service) | Microsoft Docs
description: Get-CrmConnection や Get-CrmOrganizations などの XRM ツール用 Powershell コマンドレットを使用してアプリ用 Common Data Service に接続し、現在のユーザーがアクセスできる組織を取得する方法について説明します
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: get-started-article
applies_to:
  - Dynamics 365 (online)
ms.assetid: 81816457-c963-46ca-b350-615fa75f56a7
caps.latest.revision: 27
author: MattB-msft
ms.author: kvivek
manager: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="use-powershell-cmdlets-for-xrm-tooling-to-connect-to-cds-for-apps"></a>XRM ツール用 PowerShell コマンドレットを使用してアプリ用 CDS に接続する

XRM ツールは、アプリ用 CDS に接続して現在のユーザーがアクセスできる組織を取得するために次に示す Windows PowerShell コマンドレットを提供します: `Get-CrmConnection` および `Get-CrmOrganizations`。  
  
<a name="Prereq"></a>   

## <a name="prerequisites"></a>前提条件  
  
-   XRM ツールのコマンドレットを使用するにはバージョン 3.0 以降の PowerShell が必要です。 バージョンを確認するには PowerShell のウィンドウを開き次のコマンドを実行します: `$Host`  
  
-   実行ポリシーを設定して署名済みの PowerShell スクリプトを実行します。 それには PowerShell ウィンドウを管理者として開き、次のコマンドを実行します: `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned`  
  
<a name="register"></a>   

## <a name="register-the-cmdlets"></a>コマンドレットの登録  

 PowerShell コマンドレットを使用する前にそれらを登録する必要があります。 XRM ツーリング PowerShell コマンドレットはここで NuGet パッケージとして使用できます: [https://www.nuget.org/packages/Microsoft.CrmSdk.XrmTooling.CrmConnector.PowerShell](https://www.nuget.org/packages/Microsoft.CrmSdk.XrmTooling.CrmConnector.PowerShell/)。 コマンドレットをダウンロードして登録するには: 
  
1. メモ帳を開いて、次のスクリプトをコピーします:

    ```powershell
    @PowerShell.exe -ExecutionPolicy RemoteSigned -Command "Invoke-Expression -Command ((Get-Content -Path '%~f0' | Select-Object -Skip 2) -join [environment]::NewLine)"
    @exit /b %Errorlevel%
    $currentFolder = Get-Location
    cd $currentFolder
    $sourceNugetExe = "https://dist.nuget.org/win-x86-commandline/latest/nuget.exe"
    $targetNugetExe = ".\nuget.exe"
    Remove-Item .\Tools -Force -Recurse -ErrorAction Ignore
    Invoke-WebRequest $sourceNugetExe -OutFile $targetNugetExe
    Set-Alias nuget $targetNugetExe -Scope Global -Verbose

    ##
    ##Specify the NuGet package source
    ##
    $nugetPackageSource = "https://api.nuget.org/v3/index.json"

    ##
    ##Download XRM Tooling PowerShell cmdlets
    ##
    ./nuget install -source $nugetPackageSource Microsoft.CrmSdk.XrmTooling.CrmConnector.PowerShell -O .\Tools
    md .\Tools\XRMToolingPowerShell
    $cmdletFolder = Get-ChildItem ./Tools | Where-Object {$_.Name -match 'Microsoft.CrmSdk.XrmTooling.CrmConnector.PowerShell.'}
    move .\Tools\$cmdletFolder\tools\*.* .\Tools\XRMToolingPowerShell
    Remove-Item .\Tools\$cmdletFolder -Force -Recurse

    ##
    ##Remove NuGet.exe
    ##
    Remove-Item nuget.exe
  
1. Save the notepad file as batch file on your computer: **GetTools.bat**.
1. Navigate to the folder where you saved the file, for example C:\SDK, and double-click the **GetTools.bat** file to run the script. This will create a Tools\XRMToolingPowerShell folder in the same location as your **GetTools.bat** file. The Tools\XRMToolingPowerShell folder contains the `RegisterXRMTooling.ps1` script to register the cmdlets, and other associated files.
1. Start PowerShell on your computer with elevated privileges (run as administrator).  
  
1.  At the prompt, change your directory to the folder that contains the PowerShell script for registering the cmdlets. For example:  
  
    ```powershell  
    cd c:\SDK\Tools\XRMToolingPowerShell  
    ```  
  
1.  `RegisterXRMTooling.ps1` スクリプトを実行して XRM ツール用 PowerShell コマンドレットを登録します。 次のコマンドを入力し、ENTER キーを押します。  
  
    ```powershell
    .\RegisterXRMTooling.ps1  
    ```
  
 これで PowerShell コマンドレットを使用する準備ができました。 登録済みのコマンドレットを一覧表示するには PowerShell ウィンドウで次のコマンドを実行します:  
  
```powershell
Get-Help “Crm”  
```  
  
<a name="RetrieveOrgs"></a>   

## <a name="use-the-cmdlet-to-retrieve-organizations-from-cds-for-apps"></a>コマンドレットを使用してアプリ用 CDS から組織を取得する  

`Get-CrmOrganizations` コマンドレットを使用して、アクセスできる組織を取得します。  
  
1.  アプリ用 CDS のインスタンスに接続する資格情報を入力します。 次のコマンドを実行するとアプリ用 CDS インスタンスに接続するためのユーザー名とパスワードの入力を要求され、それらは `$Cred` 変数に保存されます。  
  
    ```powershell  
    $Cred = Get-Credential  
    ```  
2.  次のコマンドを使用して組織を取得し、その情報を `$CRMOrgs` 変数に格納します。 

    - アプリ用 CDS のインスタンスに接続している場合:  
  
        ```powershell  
        $CRMOrgs = Get-CrmOrganizations -Credential $Cred -DeploymentRegion NorthAmerica –OnlineType Office365  
        ```  
  
        > [!NOTE]
        >  `DeploymentRegion` パラメーターの有効な値は、`NorthAmerica`、`EMEA`、`APAC`、`SouthAmerica`、`Oceania`、`JPN`、`CAN`、`IND`、および `NorthAmerica2` です。 `OnlineType` パラメーターの場合には、`Office365` を指定します。
<!--   
    -   If you’re connecting to the on-premises server:  
  
        ```powershell  
        $CRMOrgs = Get-CrmOrganizations –ServerUrl http://<CRM_Server_Host> –Credential $Cred  
        ```      
  
    -   If you’re connecting to the CDS for Apps server using the claims-based authentication against the specified Home realm:  
  
        ```powershell  
        $CRMOrgs = Get-CrmOrganizations –ServerUrl http://<CRM_Server_Host> –Credential $Cred –HomRealmURL http://<Identity_Provider_Address>  
        ```   -->
  
3.  手順 2 でコマンドを実行するときに、入力した資格情報が検証されます。 コマンドの実行が成功したら、次のコマンドを入力してから Enter キーを押し、アクセスできる組織を表示します。  
  
    ```powershell  
    $CRMOrgs  
    ```  
  
    <!-- TODO:
     ![CDS for Apps organization information](../media/xrmtooling-powershell-1.png)   -->
  
    > [!TIP]
    >  取得したアプリ用 CDS 組織を格納するために使用された変数 (この場合は `$CRMOrgs`) を `Get-CrmConnection` コマンドレットとともに使用してアプリ用 CDS に接続できます。 組織名を指定するには、コマンド `$CRMOrgs.UniqueName` を使用します。  
    >   
    >  `$CRMOrgs` 変数に格納されている組織の値が複数の場合は、コマンド `$CRMOrgs[n-1]` を使用して `nth` の組織を参照できます。 たとえば、`$CRMOrgs` 変数の 2 番目の組織の一意の名前を参照するには、コマンド `$CRMOrgs[1].UniqueName` を使用します。 詳細: [配列の値にアクセスする](/previous-versions/windows/it-pro/windows-powershell-1.0/ee692791\(v=technet.10\))  
  
<a name="ConnecttoCRM"></a>
   
## <a name="use-the-cmdlet-to-connect-to-cds-for-apps"></a>コマンドレットを使用してアプリ用 CDS に接続する  

`Get-CrmConnection` コマンドレットを使用してアプリ用 CDS のインスタンスに接続する このコマンドレットは XRM ツールの共通ログイン コントロールを使用して資格情報を指定し、アプリ用 CDS に接続します。または資格情報をインライン パラメーターとして指定することもできます。 詳細: [XRM ツールの共通ログイン コントロールを使用する](use-xrm-tooling-common-login-control-client-applications.md)

> [!IMPORTANT]
> `Get-CrmConnection` コマンドレットを使用する前に、次のコマンドを使用して Customer Engagement インスタンスに接続するための PowerShell による TLS 1.2 の使用の実施を確認してください:<br/>
> `[System.Net.ServicePointManager]::SecurityProtocol = [System.Net.SecurityProtocolType]::Tls12`<br/>
> Customer Engagement の接続のための TLS 1.2 の要件の詳細: [ブログの投稿: Dynamics 365 Customer Engagement の接続のセキュリティに予定されている更新](https://blogs.msdn.microsoft.com/crm/2017/09/28/updates-coming-to-dynamics-365-customer-engagement-connection-security/)   
  
### <a name="connect-to-cds-for-apps-by-using-the-common-login-control"></a>共通ログイン コントロールを使用してアプリ用 CDS に接続する  
  
1.  共通ログイン コントロールを使用して資格情報を提供しアプリ用 CDS に接続する場合、次のコマンドを使用します。 接続情報は、後で使用できるように、`$CRMConn` 変数に保存されます。  
  
    ```powershell  
    $CRMConn = Get-CrmConnection -InteractiveMode  
    ```  
  
2.  **LoginControl** ダイアログ ボックスが表示されます。 アプリ用 CDS のインスタンスに接続するための資格情報を入力して **Login**をクリックします。  
  
### <a name="connect-to-cds-for-apps-by-specifying-credentials-inline"></a>資格情報をインラインで指定してアプリ用 CDS に接続する  
  
1.  アプリ用 CDS に接続するには次のコマンドを使用します。 これらのコマンドは、先に作成した `$Cred` 変数を使用して、組織を取得すると同時に、資格情報を保存します。 接続情報は `$CRMConn` 変数に保存されます。

    <!-- -   If you’re connecting to a CDS for Apps instance:   -->
  
        ```powershell  
        $CRMConn = Get-CrmConnection -Credential $Cred -DeploymentRegion <Deployment region name> –OnlineType Office365 –OrganizationName <OrgName>  
        ```
  
        > [!NOTE]
        >  For the `DeploymentRegion` parameter, valid values are `NorthAmerica`, `EMEA`, `APAC`, `SouthAmerica`, `Oceania`, `JPN`, `CAN`, `IND` and `NorthAmerica2`. For the `OnlineType` parameter, specify `Office365`. 
  
    <!-- not available for this version at this time
     -   If you’re connecting to the on-premises server:  
  
        ```powershell  
        $CRMConn = Get-CrmConnection –ServerUrl http://<CRM_Server_Host> -Credential $Cred -OrganizationName <OrgName>  
        ```
  
    -   If you’re connecting to the CDS for Apps server using the claims-based authentication against the specified Home realm:  
  
        ```powershell  
        $CRMConn = Get-CrmConnection –ServerUrl http://<CRM_Server_Host> -Credential $Cred -OrganizationName <OrgName> –HomRealmURL http://<Identity_Provider_Address>  
        ```   -->
  
    > [!NOTE]
    > 前のすべてのコマンドの `OrganizationName` パラメーターについて、組織の一意の名前またはフレンドリ名を指定できます。 また、`Get-CrmOrganizations` コマンドレットを使用して取得して `$CRMOrgs` 変数に保存した、組織の一意の名前またはフレンドリ名も使用できます。 たとえば、`$CRMOrgs[x].UniqueName` または `$CRMOrgs[x].FriendlyName` を使用できます。  
  
2.  手順 1 でコマンドを実行するときに、入力した資格情報が検証されます。 コマンドレットの実行が成功したら、次のコマンドを入力してから Enter キーを押し、接続情報と状態を表示します。  
  
    ```powershell  
    $CRMConn  
    ```  
  
    <!--TODO:
     ![CDS for Apps connection information and status](../media/xrm-tooling-powershell-2.png "CDS for Apps connection information and status")   -->
  
### <a name="see-also"></a>関連項目
  
[XRM ツール API を使用してアプリ用 CDS に接続する](use-crmserviceclient-constructors-connect.md)<br />
[XRM ツールを使用して Windows のクライアント アプリケーションを作成する](build-windows-client-applications-xrm-tools.md)<br />
[ブログ: PowerShell module for performing data operations and manipulating user and system settings in CRM (CRM でデータ操作を実行し、ユーザーおよびシステム設定を操作するための PowerShell モジュール)](http://blogs.msdn.com/b/crm/archive/2015/09/25/powershell-module-for-performing-data-operations-and-manipulating-user-and-system-settings-in-crm.aspx)
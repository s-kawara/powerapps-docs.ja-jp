---
title: NuGet (Common Data Service for Apps) からツールをダウンロード | Microsoft Docs
description: Nuget からプラグイン登録、パッケージ展開、および他のコア ツールをダウンロードします。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: feb3e634-7c60-46fd-8b92-3f5682b1570b
author: shmcarth
ms.author: jdaly
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="download-tools-from-nuget"></a>NuGet からツールをダウンロード 

以下の powershell スクリプトを使用して、NuGet から開発で使用するツールをダウンロードすることができます。 これらのツールには以下の内容が含まれます。

|ツール|NuGet パッケージ|
|-|-|
|コード生成ツール `CrmSvcUtil.exe`|[Microsoft.CrmSdk.CoreTools](https://www.nuget.org/packages/Microsoft.CrmSdk.CoreTools)|
|Configuration Migration ツール `DataMigrationUtility.exe`|[Microsoft.CrmSdk.XrmTooling.ConfigurationMigration.Wpf](https://www.nuget.org/packages/Microsoft.CrmSdk.XrmTooling.ConfigurationMigration.Wpf)|
|Package Deployer `PackageDeployer.exe`|[Microsoft.CrmSdk.XrmTooling.PackageDeployment.WPF](https://www.nuget.org/packages/Microsoft.CrmSdk.XrmTooling.PackageDeployment.Wpf)|
|プラグイン登録ツール `PluginRegistration.exe` |[Microsoft.CrmSdk.XrmTooling.PluginRegistrationTool](https://www.nuget.org/packages/Microsoft.CrmSdk.XrmTooling.PluginRegistrationTool)|
|SolutionPackager ツール `SolutionPackager.exe`|[Microsoft.CrmSdk.CoreTools](https://www.nuget.org/packages/Microsoft.CrmSdk.CoreTools)|

## <a name="download-tools-using-powershell"></a>PowerShell を使用してツールをダウンロード

1. Windows の [スタート] メニューで、`Windows Powershell` と入力して開きます。
1. ツールをインストールするフォルダーに移動します。 たとえば、D ドライブの `devtools` フォルダーにインストールする場合は、`cd D:\devtools` と入力します。
1. 以下の PowerShell スクリプトを PowerShell ウィンドウにコピーして貼り付け、Enter キーを押します。

    ```powershell
    $sourceNugetExe = "https://dist.nuget.org/win-x86-commandline/latest/nuget.exe"
    $targetNugetExe = ".\nuget.exe"
    Remove-Item .\Tools -Force -Recurse -ErrorAction Ignore
    Invoke-WebRequest $sourceNugetExe -OutFile $targetNugetExe
    Set-Alias nuget $targetNugetExe -Scope Global -Verbose
        
    ##
    ##Download Plugin Registration Tool
    ##
    ./nuget install Microsoft.CrmSdk.XrmTooling.PluginRegistrationTool -O .\Tools
    md .\Tools\PluginRegistration
    $prtFolder = Get-ChildItem ./Tools | Where-Object {$_.Name -match 'Microsoft.CrmSdk.XrmTooling.PluginRegistrationTool.'}
    move .\Tools\$prtFolder\tools\*.* .\Tools\PluginRegistration
    Remove-Item .\Tools\$prtFolder -Force -Recurse
    
    ##
    ##Download CoreTools
    ##
    ./nuget install  Microsoft.CrmSdk.CoreTools -O .\Tools
    md .\Tools\CoreTools
    $coreToolsFolder = Get-ChildItem ./Tools | Where-Object {$_.Name -match 'Microsoft.CrmSdk.CoreTools.'}
    move .\Tools\$coreToolsFolder\content\bin\coretools\*.* .\Tools\CoreTools
    Remove-Item .\Tools\$coreToolsFolder -Force -Recurse

    ##
    ##Download Configuration Migration
    ##
    ./nuget install  Microsoft.CrmSdk.XrmTooling.ConfigurationMigration.Wpf -O .\Tools
    md .\Tools\ConfigurationMigration
    $configMigFolder = Get-ChildItem ./Tools | Where-Object {$_.Name -match 'Microsoft.CrmSdk.XrmTooling.ConfigurationMigration.Wpf.'}
    move .\Tools\$configMigFolder\tools\*.* .\Tools\ConfigurationMigration
    Remove-Item .\Tools\$configMigFolder -Force -Recurse
    
    ##
    ##Download Package Deployer 
    ##
    ./nuget install  Microsoft.CrmSdk.XrmTooling.PackageDeployment.WPF -O .\Tools
    md .\Tools\PackageDeployment
    $pdFolder = Get-ChildItem ./Tools | Where-Object {$_.Name -match 'Microsoft.CrmSdk.XrmTooling.PackageDeployment.Wpf.'}
    move .\Tools\$pdFolder\tools\*.* .\Tools\PackageDeployment
    Remove-Item .\Tools\$pdFolder -Force -Recurse

    ##
    ##Remove NuGet.exe
    ##
    Remove-Item nuget.exe    
    ```

1. 次のフォルダーにツールがあります。

- `[Your folder]\Tools\ConfigurationMigration`
- `[Your folder]\Tools\CoreTools`
- `[Your folder]\Tools\PackageDeployment`
- `[Your folder]\Tools\PluginRegistration`

これらのツールの最新バージョンを取得するには、これらの手順を繰り返します。

## <a name="see-also"></a>関連項目

[開発者ツール](developer-tools.md)<br />
[Visual Studio および .NET Framework](org-service/visual-studio-dot-net-framework.md)<br />
[事前バインド型エンティティ クラスの作成](/dynamics365/customer-engagement/developer/org-service/create-early-bound-entity-classes-code-generation-tool)<br />
[コード生成ツール用の拡張機能の作成](org-service/extend-code-generation-tool.md)<br />
[組織のメタデータの参照](browse-your-metadata.md)<br />
[Dynamics 365 Package Deployer および Windows PowerShell を使用してパッケージを展開する](/dynamics365/customer-engagement/admin/deploy-packages-using-package-deployer-windows-powershell)<br />
[プラグインの登録](register-plug-in.md)<br />

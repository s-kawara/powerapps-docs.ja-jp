---
title: <Topic Title> (アプリ用 Common Data Service) | Microsoft Docs
description: <Description>
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: shmcarth
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
<!-- The information about SDK assemblies should be found elsewhere
Perhaps this topic should call out the available tools at a high level?
Community tools should go here?
https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/developer-tools -->

# <a name="developer-tools-and-resources"></a>開発者のツールとリソース

開発者はアプリの Common Data Service で、ソリューションの作業時に、以下のツールとリソースを使用します。

## <a name="tools-available-for-download-from-nuget"></a>NuGet からダウンロードに利用可能なツール

次のツールは NuGet パッケージから除外されます。 [開発者ガイド: NuGet からツールをダウンロード](/dynamics365/customer-engagement/developer/download-tools-nuget) トピックには、ダウンロードおよびツールの最新バージョンをエクスポートに使用可能な PowerShell スクリプトがあります。

|ツール  |説明  |
|---------|---------|
|コード生成ツール `CrmSvcUtil.exe`|組織サービスで使われるエンティティ データ モデルを表す事前バインド .NET Framework クラスを生成する、コマンドライン コード生成ツールです。 <br />詳細: <br />[組織のサービス](work-with-data-cds.md#organization-service)<br />[コード生成ツールを使用して事前バインド型エンティティ クラスを作成する](/dynamics365/customer-engagement/developer/org-service/create-early-bound-entity-classes-code-generation-tool)|
|Configuration Migration ツール `DataMigrationUtility.exe`|環境間で構成データを移動するために使用します。 構成データは、カスタム機能を定義するために使用され、通常はユーザー定義エンティティに格納されます。 ツールはビジネス データを移動するために設計されていません。 <br /> 詳細: [アプリ管理者ガイドの Common Data Service: 構成移行ツールでインスタンスと組織間を移動する構成データを移動](/dynamics365/customer-engagement/admin/manage-configuration-data)|
|Package Deployer `PackageDeployer.exe`|Common Data Service for Apps インスタンスでパッケージを展開するために使されます。 パッケージは、ソリューションを含むインストール可能なユニットです。 <br /> 詳細: <br />[ソリューション パッケージの展開](introduction-solutions.md#deploy-solution-packages)<br />[Apps Package Deployer 用に CDS のパッケージを作成](/dynamics365/customer-engagement/developer/create-packages-package-deployer)|
|プラグイン登録ツール `PluginRegistration.exe`|.NET アセンブリのプラグイン クラスをサーバー イベントに登録するために使用されるツールです。 <br />詳細: <br />[プラグインの作成](apply-business-logic-with-code.md#create-a-plug-in)<br />[チュートリアル: プラグイン登録ツールを使用したプラグインの登録](/dynamics365/customer-engagement/developer/walkthrough-register-plugin-using-plugin-registration-tool)|
|SolutionPackager ツール `SolutionPackager.exe`|ソース制御システムによって容易に管理できるように、Common Data Service for Apps の圧縮されたソリューション ファイルを複数の XML ファイルに逆分解できるツールです。<br /> 詳細: <br />[ソリューションの開発チーム](introduction-solutions.md#team-development-of-solutions)<br />[SolutionPackager ツールを使用してソリューション ファイルを圧縮および解凍する](/dynamics365/customer-engagement/developer/compress-extract-solution-file-solutionpackager)|

## <a name="net-sdk-assemblies"></a>.NET SDK アセンブリ 

次は、.NET 開発者が使えるアセンブリです。 最新のバージョンは、NuGet パッケージ対応でダウンロードできます。

### <a name="work-with-data"></a>データに関する作業

組織サービスおよびディレクトリ サービスと対話するには、これらのアセンブリを使用します。

詳細: [Apps Organization サービス用 CDS を使用](/dynamics365/customer-engagement/developer/use-microsoft-dynamics-365-organization-service)

**NuGet Package**: [Microsoft.CrmSdk.CoreAssemblies](https://www.nuget.org/packages/Microsoft.CrmSdk.CoreAssemblies/)

|アセンブリ  |名前空間  |
|---------|---------|
|Microsoft.Crm.Sdk.Proxy.dll|[Microsoft.Crm.Sdk](/dotnet/api/microsoft.crm.sdk)<br />[Microsoft.Crm.Sdk.Messages](/dotnet/api/microsoft.crm.sdk.messages)|
|Microsoft.Xrm.Sdk.dll|[Microsoft.Xrm.Sdk](/dotnet/api/microsoft.xrm.sdk)<br />[Microsoft.Xrm.Sdk.Client](/dotnet/api/microsoft.xrm.sdk.client)<br />[Microsoft.Xrm.Sdk.Discovery](/dotnet/api/microsoft.xrm.sdk.discovery)<br />[Microsoft.Xrm.Sdk.Messages](/dotnet/api/microsoft.xrm.sdk.messages)<br />[Microsoft.Xrm.Sdk.Metadata](/dotnet/api/microsoft.xrm.sdk.metadata)<br />[Microsoft.Xrm.Sdk.Metadata.Query](/dotnet/api/microsoft.xrm.sdk.metadata.query)<br />[Microsoft.Xrm.Sdk.Organization](/dotnet/api/microsoft.xrm.sdk.organization)<br />[Microsoft.Xrm.Sdk.Query](/dotnet/api/microsoft.xrm.sdk.query)<br />[Microsoft.Xrm.Sdk.WebServiceClient](/dotnet/api/microsoft.xrm.sdk.webserviceclient)|

### <a name="create-process-designer-workflow-extensions"></a>Process Designer (ワークフロー) 拡張子を作成

アセンブリを使用して、ユーザー定義の活動を Process デザイナーに追加します。 

詳細については、[ユーザー定義のワークフロー活動 (ワークフロー アセンブリ)](/dynamics365/customer-engagement/developer/custom-workflow-activities-workflow-assemblies) を参照してください。

**NuGet Package**: [Microsoft.CrmSdk.Workflow](https://www.nuget.org/packages/Microsoft.CrmSdk.Workflow/) 

|アセンブリ|名前空間|
|---------|---------|
|Microsoft.Xrm.Sdk.Workflow.dll|[Microsoft.Xrm.Sdk.Workflow](/dotnet/api/microsoft.xrm.sdk.workflow)<br />[Microsoft.Xrm.Sdk.Workflow.Activities](/dotnet/api/microsoft.xrm.sdk.workflow.activities)<br />[Microsoft.Xrm.Sdk.Workflow.Designers](/dotnet/api/microsoft.xrm.sdk.workflow.designers)|

### <a name="build-windows-client-applications"></a>Windows のクライアント アプリケーションを作成

これらのアセンブリを使用して、組織サービスの接続を容易にし、Windows のクライアント アプリケーションを作成します。 

詳細については、[XRM ツールを使用して Windows のクライアント アプリケーションを作成](/dynamics365/customer-engagement/developer/build-windows-client-applications-xrm-tools) を参照

**NuGet Packages**:
- [Microsoft.CrmSdk.XrmTooling.CoreAssembly](https://www.nuget.org/packages/Microsoft.CrmSdk.XrmTooling.CoreAssembly/) (Microsoft.Xrm.Tooling.Connector.dll)
- [Microsoft.CrmSdk.XrmTooling.WpfControls](https://www.nuget.org/packages/Microsoft.CrmSdk.XrmTooling.WpfControls/) 

|アセンブリ|名前空間  |
|---------|---------|
|Microsoft.Xrm.Tooling.Connector.dll|[Microsoft.Xrm.Tooling.Connector](/dotnet/api/microsoft.xrm.tooling.connector)<br />[Microsoft.Xrm.Tooling.Connector.Model](/dotnet/api/microsoft.xrm.tooling.connector.model)|
|Microsoft.Xrm.Tooling.CrmConnectControl.dll|[Microsoft.Xrm.Tooling.CrmConnectControl](/dotnet/api/microsoft.xrm.tooling.crmconnectcontrol)<br />[Microsoft.Xrm.Tooling.CrmConnectControl.Model](/dotnet/api/microsoft.xrm.tooling.crmconnectcontrol.model)<br />[Microsoft.Xrm.Tooling.CrmConnectControl.Properties](/dotnet/api/microsoft.xrm.tooling.crmconnectcontrol.properties)<br />[Microsoft.Xrm.Tooling.CrmConnectControl.Utility](/dotnet/api/microsoft.xrm.tooling.crmconnectcontrol.utility)|
|Microsoft.Xrm.Tooling.WebResourceUtility.dll|[Microsoft.Xrm.Tooling.WebResourceUtility](/dotnet/api/microsoft.xrm.tooling.webresourceutility)|

### <a name="create-packages"></a>パッケージを作成

これらのアセンブリを使用して、Package Deployer 用のパッケージを作成します。

詳細: [CDS for Apps Package Deployer のパッケージを作成](/dynamics365/customer-engagement/developer/create-packages-package-deployer)

**NuGet Package**: [Microsoft.CrmSdk.XrmTooling.PackageDeployment](https://www.nuget.org/packages/Microsoft.CrmSdk.XrmTooling.PackageDeployment/)

|アセンブリ|名前空間  |
|---------|---------|
|Microsoft.Xrm.Tooling.PackageDeployment.CrmPackageExtentionBase.dll|[Microsoft.Xrm.Tooling.PackageDeployment.CrmPackageExtentionBase](/dotnet/api/microsoft.xrm.tooling.packagedeployment.crmpackageextentionbase)|

### <a name="create-custom-virtual-entity-data-providers"></a>カスタム仮想エンティティ データ プロバイダーを作成

これらのアセンブリを使用して、カスタム仮想エンティティ データ プロバイダーを作成します。 

詳細: [仮想エンティティで開始](/dynamics365/customer-engagement/developer/virtual-entities/get-started-ve)

**NuGet Package**: [Microsoft.CrmSdk.Data](https://www.nuget.org/packages/Microsoft.CrmSdk.Data/)

|アセンブリ  |名前空間  |
|---------|---------|
|Microsoft.Xrm.Sdk.Data.dll|[Microsoft.Xrm.Sdk.Data](/dotnet/api/microsoft.xrm.sdk.data)<br />[Microsoft.Xrm.Sdk.Data.CodeGen](/api/microsoft.xrm.sdk.data.codegen)<br />[Microsoft.Xrm.Sdk.Data.Converters](/dotnet/api/microsoft.xrm.sdk.data.converters)<br />[Microsoft.Xrm.Sdk.Data.Exceptions](/dotnet/api/microsoft.xrm.sdk.data.exceptions)<br />[Microsoft.Xrm.Sdk.Data.Expressions](/dotnet/api/microsoft.xrm.sdk.data.expressions)<br />[Microsoft.Xrm.Sdk.Data.Infra](/dotnet/api/microsoft.xrm.sdk.data.infra)<br />[Microsoft.Xrm.Sdk.Data.Mappings](/dotnet/api/microsoft.xrm.sdk.data.mappings)|

### <a name="extend-outlook-client"></a>Outlook Client の拡張

アセンブリを使用して、オフライン アクセス対応の Microsoft Dynamics 365 for Outlook および Apps for Microsoft Office Outlook 用 Microsoft CDS と相互作用します。 

詳細: [Dynamics 365 for Outlook の拡張](/dynamics365/customer-engagement/developer/extend-customer-engagement-outlook)

**NuGet Package**: [Microsoft.CrmSdk.Outlook](https://www.nuget.org/packages/Microsoft.CrmSdk.Outlook/)

|アセンブリ|名前空間|
|---------|---------|
|Microsoft.Crm.Outlook.Sdk.dll|[Microsoft.Crm.Outlook.Sdk](/dotnet/api/microsoft.crm.outlook.sdk)|


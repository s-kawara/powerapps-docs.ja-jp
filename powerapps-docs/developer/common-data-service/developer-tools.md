---
title: 開発者ツールとリソース(Common Data Service) | Microsoft Docs
description: ソリューションの操作時に使用できるツールとリソースについて説明します。
ms.custom: ''
ms.date: 1/31/2019
ms.reviewer: pehecke
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

# <a name="developer-tools-and-resources"></a>開発者のツールとリソース

開発者は Common Data Serviceを使用してソリューションを操作する際に、以下のツールとリソースを使用します。

## <a name="tools-available-for-download-from-nuget"></a>ツールは NuGet からダウンロードすることができます。

以下のツールは NuGet パッケージで配布されています。 [開発者ガイド: NuGetからツールをダウンロードする](/dynamics365/customer-engagement/developer/download-tools-nuget) のトピックには、ダウンロードして使用することができるPowerShellスクリプトの最新バージョンが含まれています。

|ツール  |説明  |
|---------|---------|
|コード生成ツール `CrmSvcUtil.exe`|組織サービスで使われるエンティティ データ モデルを表す事前バインド .NET Framework クラスを生成する、コマンドライン コード生成ツールです。 <br />詳細: <br />[組織のサービス](work-with-data-cds.md#organization-service)<br />[コード生成ツールを使用して事前バインド型エンティティ クラスを作成する](/dynamics365/customer-engagement/developer/org-service/create-early-bound-entity-classes-code-generation-tool)|
|Configuration Migration ツール `DataMigrationUtility.exe`|環境間で構成データを移動するために使用します。 構成データは、カスタム機能を定義するために使用され、通常はユーザー定義エンティティに格納されます。 ツールはビジネス データを移動するために設計されていません。 <br /> 詳細については次を参照してください: [Common Data Service 管理者ガイド: 設定移行ツールを使用して、インスタンス間および組織間で構成データを移動する](/dynamics365/customer-engagement/admin/manage-configuration-data)|
|Package Deployer `PackageDeployer.exe`|Common Data Service インスタンスにパッケージを展開するために使用します。 パッケージは、ソリューションを含むインストール可能なユニットです。 <br /> 詳細: <br />[ソリューション パッケージの展開](introduction-solutions.md#deploy-solution-packages)<br />[Common Data Service のパッケージを作成する Package Deployer](/dynamics365/customer-engagement/developer/create-packages-package-deployer)|
|プラグイン登録ツール `PluginRegistration.exe`|.NET アセンブリのプラグイン クラスをサーバー イベントに登録するために使用されるツールです。 <br />詳細: <br />[プラグインの作成](apply-business-logic-with-code.md#create-a-plug-in)<br />[プラグインの登録](register-plug-in.md)|
|SolutionPackager ツール `SolutionPackager.exe`|Common Data Service 圧縮ソリューションファイルを複数のXMLファイルおよびその他のファイルに可逆的に分解処理を行い、これらのファイルをソースコントロールシステムで簡単に管理するツールです。<br /> 詳細: <br />[ソリューションの開発チーム](introduction-solutions.md#team-development-of-solutions)<br />[SolutionPackager ツールを使用してソリューション ファイルを圧縮および解凍する](/dynamics365/customer-engagement/developer/compress-extract-solution-file-solutionpackager)|

## <a name="net-sdk-assemblies"></a>.NET SDK アセンブリ 

次は、.NET 開発者が使えるアセンブリです。 最新バージョンは、対応する NuGet パッケージからダウンロードすることができます。

### <a name="work-with-data"></a>データに関する作業

組織サービスおよびディレクトリ サービスと対話するには、これらのアセンブリを使用します。

詳細については次を参照してください: [ Common Data Service 組織サービスを使用する](/dynamics365/customer-engagement/developer/use-microsoft-dynamics-365-organization-service)

**NuGet パッケージ**: [Microsoft.CrmSdk.CoreAssemblies](https://www.nuget.org/packages/Microsoft.CrmSdk.CoreAssemblies/)

|アセンブリ  |名前空間  |
|---------|---------|
|Microsoft.Crm.Sdk.Proxy.dll|[Microsoft.Crm.Sdk](/dotnet/api/microsoft.crm.sdk)<br />[Microsoft.Crm.Sdk.Messages](/dotnet/api/microsoft.crm.sdk.messages)|
|Microsoft.Xrm.Sdk.dll|[Microsoft.Xrm.Sdk](/dotnet/api/microsoft.xrm.sdk)<br />[Microsoft.Xrm.Sdk.Client](/dotnet/api/microsoft.xrm.sdk.client)<br />[Microsoft.Xrm.Sdk.Discovery](/dotnet/api/microsoft.xrm.sdk.discovery)<br />[Microsoft.Xrm.Sdk.Messages](/dotnet/api/microsoft.xrm.sdk.messages)<br />[Microsoft.Xrm.Sdk.Metadata](/dotnet/api/microsoft.xrm.sdk.metadata)<br />[Microsoft.Xrm.Sdk.Metadata.Query](/dotnet/api/microsoft.xrm.sdk.metadata.query)<br />[Microsoft.Xrm.Sdk.Organization](/dotnet/api/microsoft.xrm.sdk.organization)<br />[Microsoft.Xrm.Sdk.Query](/dotnet/api/microsoft.xrm.sdk.query)<br />[Microsoft.Xrm.Sdk.WebServiceClient](/dotnet/api/microsoft.xrm.sdk.webserviceclient)|

### <a name="create-process-designer-workflow-extensions"></a>Process Designer (ワークフロー) 拡張子を作成

アセンブリを使用して、ユーザー定義の活動を Process デザイナーに追加します。 

詳細については、[ユーザー定義のワークフロー活動 (ワークフロー アセンブリ)](/dynamics365/customer-engagement/developer/custom-workflow-activities-workflow-assemblies) を参照してください。

**NuGet パッケージ**: [Microsoft.CrmSdk.Workflow](https://www.nuget.org/packages/Microsoft.CrmSdk.Workflow/) 

|アセンブリ|名前空間|
|---------|---------|
|Microsoft.Xrm.Sdk.Workflow.dll|[Microsoft.Xrm.Sdk.Workflow](/dotnet/api/microsoft.xrm.sdk.workflow)<br />[Microsoft.Xrm.Sdk.Workflow.Activities](/dotnet/api/microsoft.xrm.sdk.workflow.activities)<br />[Microsoft.Xrm.Sdk.Workflow.Designers](/dotnet/api/microsoft.xrm.sdk.workflow.designers)|

### <a name="build-windows-client-applications"></a>Windows のクライアント アプリケーションを作成

これらのアセンブリを使用して、組織サービスの接続を容易にし、Windows のクライアント アプリケーションを作成します。 

詳細については、[XRM ツールを使用して Windows のクライアント アプリケーションを作成](/dynamics365/customer-engagement/developer/build-windows-client-applications-xrm-tools) を参照

**NuGet パッケージ**:
- [Microsoft.CrmSdk.XrmTooling.CoreAssembly](https://www.nuget.org/packages/Microsoft.CrmSdk.XrmTooling.CoreAssembly/) (Microsoft.Xrm.Tooling.Connector.dll)
- [Microsoft.CrmSdk.XrmTooling.WpfControls](https://www.nuget.org/packages/Microsoft.CrmSdk.XrmTooling.WpfControls/) 

|アセンブリ|名前空間  |
|---------|---------|
|Microsoft.Xrm.Tooling.Connector.dll|[Microsoft.Xrm.Tooling.Connector](/dotnet/api/microsoft.xrm.tooling.connector)<br />[Microsoft.Xrm.Tooling.Connector.Model](/dotnet/api/microsoft.xrm.tooling.connector.model)|
|Microsoft.Xrm.Tooling.CrmConnectControl.dll|[Microsoft.Xrm.Tooling.CrmConnectControl](/dotnet/api/microsoft.xrm.tooling.crmconnectcontrol)<br />[Microsoft.Xrm.Tooling.CrmConnectControl.Model](/dotnet/api/microsoft.xrm.tooling.crmconnectcontrol.model)<br />[Microsoft.Xrm.Tooling.CrmConnectControl.Properties](/dotnet/api/microsoft.xrm.tooling.crmconnectcontrol.properties)<br />[Microsoft.Xrm.Tooling.CrmConnectControl.Utility](/dotnet/api/microsoft.xrm.tooling.crmconnectcontrol.utility)|
|Microsoft.Xrm.Tooling.WebResourceUtility.dll|[Microsoft.Xrm.Tooling.WebResourceUtility](/dotnet/api/microsoft.xrm.tooling.webresourceutility)|

### <a name="create-packages"></a>パッケージを作成

これらのアセンブリを使用して Package Deployerのパッケージを作成します。

詳細情報については次を参照してください: [Common Data Service Package Deployerにパッケージを作成する](/dynamics365/customer-engagement/developer/create-packages-package-deployer)

**NuGet パッケージ**: [Microsoft.CrmSdk.XrmTooling.PackageDeployment](https://www.nuget.org/packages/Microsoft.CrmSdk.XrmTooling.PackageDeployment/)

|アセンブリ|名前空間  |
|---------|---------|
|Microsoft.Xrm.Tooling.PackageDeployment.CrmPackageExtentionBase.dll|[Microsoft.Xrm.Tooling.PackageDeployment.CrmPackageExtentionBase](/dotnet/api/microsoft.xrm.tooling.packagedeployment.crmpackageextentionbase)|

### <a name="create-custom-virtual-entity-data-providers"></a>カスタム仮想エンティティ データ プロバイダーを作成

これらのアセンブリを使用して、カスタム仮想エンティティ データ プロバイダーを作成します。 

詳細: [仮想エンティティで開始](/dynamics365/customer-engagement/developer/virtual-entities/get-started-ve)

**NuGet パッケージ**: [Microsoft.CrmSdk.Data](https://www.nuget.org/packages/Microsoft.CrmSdk.Data/)

|アセンブリ  |名前空間  |
|---------|---------|
|Microsoft.Xrm.Sdk.Data.dll|[Microsoft.Xrm.Sdk.Data](/dotnet/api/microsoft.xrm.sdk.data)<br />[Microsoft.Xrm.Sdk.Data.CodeGen](/api/microsoft.xrm.sdk.data.codegen)<br />[Microsoft.Xrm.Sdk.Data.Converters](/dotnet/api/microsoft.xrm.sdk.data.converters)<br />[Microsoft.Xrm.Sdk.Data.Exceptions](/dotnet/api/microsoft.xrm.sdk.data.exceptions)<br />[Microsoft.Xrm.Sdk.Data.Expressions](/dotnet/api/microsoft.xrm.sdk.data.expressions)<br />[Microsoft.Xrm.Sdk.Data.Infra](/dotnet/api/microsoft.xrm.sdk.data.infra)<br />[Microsoft.Xrm.Sdk.Data.Mappings](/dotnet/api/microsoft.xrm.sdk.data.mappings)|

### <a name="extend-outlook-client"></a>Outlook Client の拡張

このアセンブリを使用すると、Microsoft Dynamics 365 for Outlook および Microsoft Common Data Service ffor Microsoft Office Outlook とOffline Accessを連携して使用することができます。 

詳細情報については次を参照してください: [Dynamics 365 for Outlookを拡張する](/dynamics365/customer-engagement/developer/extend-customer-engagement-outlook)

**NuGet パッケージ**: [Microsoft.CrmSdk.Outlook](https://www.nuget.org/packages/Microsoft.CrmSdk.Outlook/)

|アセンブリ|名前空間|
|---------|---------|
|Microsoft.Crm.Outlook.Sdk.dll|[Microsoft.Crm.Outlook.Sdk](/dotnet/api/microsoft.crm.outlook.sdk)|


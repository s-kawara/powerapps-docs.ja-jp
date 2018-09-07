---
title: Common Data Service for Apps Developer の概要 | Microsoft Docs
description: 開発者が Common Data Service for Apps を使用して、価値を高める方法について説明します。
services: ''
suite: powerapps
documentationcenter: na
author: JimDaly
manager: faisalmo
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/19/2018
ms.author: jdaly
search.audienceType:
- developer
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: 3b0e2d70a9295bdf1a8a6d6a71cb6075677bb991
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "42844056"
---
# <a name="common-data-service-for-apps-developer-overview"></a>Common Data Service for Apps Developer の概要

PowerApps は、ユーザー、企業、独立系ソフトウェア ベンダー (ISV)、システム インテグレーター (SI) に基幹業務アプリを構築するための強力なプラットフォームを提供します。 このリリースでは、Common Data Service for Apps と呼ばれる Common Data Service の拡張が PowerApps に新しく追加されています。これには Dynamics 365 for Sales、Marketing、Customer Service に機能を供給する Dynamic 365 プラットフォームのコア機能が含まれています。


## <a name="get-started"></a>はじめる

Dynamics 365 for Sales、Marketing、Customer Service アプリを既に使用したことがある場合、その経験を Common Data Service for Apps のカスタマイズと拡張に活かすことができます。

以下のトピックでは、Dynamics 365 for Sales、Marketing、Customer Service アプリを初めて使用する開発者に、Common Data Service for Apps で作業を開始する際に役立つ重要な概念の概要を説明します。

> [!NOTE]
> - モデル駆動型アプリは Common Data Service for Apps に接続されます。 アプリケーション レベルで開発者がどのように価値を高められるかについては、「[開発者向けのモデル駆動型アプリの概要](../model-driven-apps/overview.md)」を参照してください。 このセクションの内容は、開発者がサービス レベルで実行できる拡張機能のみに関するものです。 
> - Common Data Service for Apps と Dynamics 365 for Sales、Marketing、Customer Service アプリは同じプラットフォームを利用しているため、開発者向けのより詳細な情報については、「[Dynamics 365 Customer Engagement の開発者ガイド](/dynamics365/customer-engagement/developer/developer-guide)」を参照してください。 これらのトピックには、概要と、より詳細な開発者ガイドおよびその他のガイドへのリンクがあります。


## <a name="tools-and-resources-for-developers"></a>開発者向けツールとリソース

開発者は、Common Data Service for Apps を使用してソリューションを操作する際に、次のツールとリソースを使用します。

### <a name="tools-available-for-download-from-nuget"></a>NuGet からダウンロード可能なツール

次のツールは NuGet パッケージで配布されます。 「[開発者ガイド: NuGet からツールをダウンロード](/dynamics365/customer-engagement/developer/download-tools-nuget)」トピックには、これらの最新バージョンのツールをダウンロードして抽出するために使用できる PowerShell スクリプトが含まれています。

|ツール  |説明  |
|---------|---------|
|コード生成ツール `CrmSvcUtil.exe`|組織のサービスで使用されるエンティティ データ モデルを表す、事前バインド .NET Framework クラスを生成するコマンドライン コード生成ツールです。 <br />詳細情報: <br />[組織のサービス](use-web-services.md#organization-service)<br />[Dynamics 365 Customer Engagement の開発者ガイド: コード生成ツール (CrmSvcUtil.exe) を使用して事前バインド型エンティティ クラスを作成する](/dynamics365/customer-engagement/developer/org-service/create-early-bound-entity-classes-code-generation-tool)|
|Configuration Migration ツール `DataMigrationUtility.exe`|環境間で構成データを移動するために使用します。 構成データはカスタム機能を定義するために使用され、通常はカスタム エンティティに格納されます。 このツールは、ビジネス データを移動するためのものではありません。 <br /> 詳細情報: [Dynamics 365 Customer Engagement の管理者ガイド: Configuration Migration ツールを使用して構成データをインスタンスおよび組織間で移動する](/dynamics365/customer-engagement/admin/manage-configuration-data)|
|Package Deployer `PackageDeployer.exe`|Common Data Service for Apps インスタンスでパッケージを配置するために使用します。 パッケージは、ソリューションを含むインストール可能な単位です。 <br /> 詳細情報: <br />[ソリューション パッケージの配置](introduction-solutions.md#deploy-solution-packages)<br />[Dynamics 365 Customer Engagement の開発者ガイド: Dynamics 365 Package Deployer 用のパッケージを作成する](/dynamics365/customer-engagement/developer/create-packages-package-deployer)|
|プラグイン登録ツール `PluginRegistration.exe`|サーバー イベントに .NET アセンブリ プラグイン クラスをサブスクライブするために使用されるツールです。 <br />詳細情報: <br />[プラグインの作成](apply-business-logic-with-code.md#create-a-plug-in)<br />[Dynamics 365 Customer Engagement の開発者ガイド: チュートリアル: プラグイン登録ツールを使用したプラグインの登録](/dynamics365/customer-engagement/developer/walkthrough-register-plugin-using-plugin-registration-tool)|
|SolutionPackager ツール `SolutionPackager.exe`|Common Data Service for Apps の圧縮ソリューション ファイルを複数の XML ファイルとその他のファイルに可逆的に分解して、それらのファイルをソース管理システムで簡単に管理できるようにするツールです。<br /> 詳細情報: <br />[ソリューションのチーム開発](introduction-solutions.md#team-development-of-solutions)<br />[Dynamics 365 Customer Engagement の開発者ガイド: SolutionPackager ツールを使用して、ソリューション ファイルを圧縮および抽出する](/dynamics365/customer-engagement/developer/compress-extract-solution-file-solutionpackager)|

### <a name="net-sdk-assemblies"></a>.NET SDK アセンブリ

.NET 開発者が使用できるアセンブリを以下に示します。 最新バージョンは、対応する NuGet パッケージでダウンロードできます。

#### <a name="work-with-data"></a>データの処理

これらのアセンブリを使用して、組織のサービスおよび探索サービスと対話します。

詳細情報: [Dynamics 365 Customer Engagement の開発者ガイド: Dynamics 365 組織サービスを使用](/dynamics365/customer-engagement/developer/use-microsoft-dynamics-365-organization-service)

**NuGet パッケージ**: [Microsoft.CrmSdk.CoreAssemblies](https://www.nuget.org/packages/Microsoft.CrmSdk.CoreAssemblies/)

|アセンブリ  |名前空間  |
|---------|---------|
|Microsoft.Crm.Sdk.Proxy.dll|[Microsoft.Crm.Sdk](/dotnet/api/microsoft.crm.sdk)<br />[Microsoft.Crm.Sdk.Messages](/dotnet/api/microsoft.crm.sdk.messages)|
|Microsoft.Xrm.Sdk.dll|[Microsoft.Xrm.Sdk](/dotnet/api/microsoft.xrm.sdk)<br />[Microsoft.Xrm.Sdk.Client](/dotnet/api/microsoft.xrm.sdk.client)<br />[Microsoft.Xrm.Sdk.Discovery](/dotnet/api/microsoft.xrm.sdk.discovery)<br />[Microsoft.Xrm.Sdk.Messages](/dotnet/api/microsoft.xrm.sdk.messages)<br />[Microsoft.Xrm.Sdk.Metadata](/dotnet/api/microsoft.xrm.sdk.metadata)<br />[Microsoft.Xrm.Sdk.Metadata.Query](/dotnet/api/microsoft.xrm.sdk.metadata.query)<br />[Microsoft.Xrm.Sdk.Organization](/dotnet/api/microsoft.xrm.sdk.organization)<br />[Microsoft.Xrm.Sdk.Query](/dotnet/api/microsoft.xrm.sdk.query)<br />[Microsoft.Xrm.Sdk.WebServiceClient](/dotnet/api/microsoft.xrm.sdk.webserviceclient)|

#### <a name="create-process-designer-workflow-extensions"></a>プロセス デザイナー (ワークフロー) の拡張機能を作成する

このアセンブリを使用して、プロセス デザイナーにカスタム アクティビティを追加します。 

詳細情報: [Dynamics 365 Customer Engagement 開発者ドキュメント: ユーザー定義ワークフロー活動 (ワークフロー アセンブリ)](/dynamics365/customer-engagement/developer/custom-workflow-activities-workflow-assemblies)

**NuGet パッケージ**: [Microsoft.CrmSdk.Workflow](https://www.nuget.org/packages/Microsoft.CrmSdk.Workflow/) 

|アセンブリ|名前空間|
|---------|---------|
|Microsoft.Xrm.Sdk.Workflow.dll|[Microsoft.Xrm.Sdk.Workflow](/dotnet/api/microsoft.xrm.sdk.workflow)<br />[Microsoft.Xrm.Sdk.Workflow.Activities](/dotnet/api/microsoft.xrm.sdk.workflow.activities)<br />[Microsoft.Xrm.Sdk.Workflow.Designers](/dotnet/api/microsoft.xrm.sdk.workflow.designers)|

#### <a name="build-windows-client-applications"></a>Windows クライアント アプリケーションをビルドする

これらのアセンブリを使用して、組織のサービスへの接続を容易にし、Windows クライアント アプリケーションをビルドします。 

詳細情報: [Dynamics 365 Customer Engagement の開発者ガイド: XRM ツールを使用して Windows クライアント アプリケーションを作成する](/dynamics365/customer-engagement/developer/build-windows-client-applications-xrm-tools)

**NuGet パッケージ**:
- [Microsoft.CrmSdk.XrmTooling.CoreAssembly](https://www.nuget.org/packages/Microsoft.CrmSdk.XrmTooling.CoreAssembly/) (Microsoft.Xrm.Tooling.Connector.dll)
- [Microsoft.CrmSdk.XrmTooling.WpfControls](https://www.nuget.org/packages/Microsoft.CrmSdk.XrmTooling.WpfControls/) 

|アセンブリ|名前空間  |
|---------|---------|
|Microsoft.Xrm.Tooling.Connector.dll|[Microsoft.Xrm.Tooling.Connector](/dotnet/api/microsoft.xrm.tooling.connector)<br />[Microsoft.Xrm.Tooling.Connector.Model](/dotnet/api/microsoft.xrm.tooling.connector.model)|
|Microsoft.Xrm.Tooling.CrmConnectControl.dll|[Microsoft.Xrm.Tooling.CrmConnectControl](/dotnet/api/microsoft.xrm.tooling.crmconnectcontrol)<br />[Microsoft.Xrm.Tooling.CrmConnectControl.Model](/dotnet/api/microsoft.xrm.tooling.crmconnectcontrol.model)<br />[Microsoft.Xrm.Tooling.CrmConnectControl.Properties](/dotnet/api/microsoft.xrm.tooling.crmconnectcontrol.properties)<br />[Microsoft.Xrm.Tooling.CrmConnectControl.Utility](/dotnet/api/microsoft.xrm.tooling.crmconnectcontrol.utility)|
|Microsoft.Xrm.Tooling.WebResourceUtility.dll|[Microsoft.Xrm.Tooling.WebResourceUtility](/dotnet/api/microsoft.xrm.tooling.webresourceutility)|

#### <a name="create-packages"></a>パッケージを作成する

これらのアセンブリを使用して、Package Deployer 用のパッケージを作成します。

詳細情報: [Dynamics 365 Customer Engagement の開発者ガイド: Dynamics 365 Package Deployer 用のパッケージを作成する](/dynamics365/customer-engagement/developer/create-packages-package-deployer)

**NuGet パッケージ**: [Microsoft.CrmSdk.XrmTooling.PackageDeployment](https://www.nuget.org/packages/Microsoft.CrmSdk.XrmTooling.PackageDeployment/)

|アセンブリ|名前空間  |
|---------|---------|
|Microsoft.Xrm.Tooling.PackageDeployment.CrmPackageExtentionBase.dll|[Microsoft.Xrm.Tooling.PackageDeployment.CrmPackageExtentionBase](/dotnet/api/microsoft.xrm.tooling.packagedeployment.crmpackageextentionbase)|

#### <a name="create-custom-virtual-entity-data-providers"></a>カスタムの仮想エンティティ データ プロバイダーを作成する

このアセンブリを使用して、カスタムの仮想エンティティ データ プロバイダーを作成します。 

詳細情報: [Dynamics 365 Customer Engagement の開発者ガイド: 仮想エンティティに関する入門情報](/dynamics365/customer-engagement/developer/virtual-entities/get-started-ve)

**NuGet パッケージ**: [Microsoft.CrmSdk.Data](https://www.nuget.org/packages/Microsoft.CrmSdk.Data/)

|アセンブリ  |名前空間  |
|---------|---------|
|Microsoft.Xrm.Sdk.Data.dll|[Microsoft.Xrm.Sdk.Data](/dotnet/api/microsoft.xrm.sdk.data)<br />[Microsoft.Xrm.Sdk.Data.CodeGen](/api/microsoft.xrm.sdk.data.codegen)<br />[Microsoft.Xrm.Sdk.Data.Converters](/dotnet/api/microsoft.xrm.sdk.data.converters)<br />[Microsoft.Xrm.Sdk.Data.Exceptions](/dotnet/api/microsoft.xrm.sdk.data.exceptions)<br />[Microsoft.Xrm.Sdk.Data.Expressions](/dotnet/api/microsoft.xrm.sdk.data.expressions)<br />[Microsoft.Xrm.Sdk.Data.Infra](/dotnet/api/microsoft.xrm.sdk.data.infra)<br />[Microsoft.Xrm.Sdk.Data.Mappings](/dotnet/api/microsoft.xrm.sdk.data.mappings)|

#### <a name="extend-outlook-client"></a>Outlook クライアントを拡張する

このアセンブリを使用して、Outlook 用 Microsoft Dynamics 365 およびオフライン アクセス対応 Microsoft Office Outlook 用 Microsoft Dynamics 365 と対話します。 

詳細情報: [Dynamics 365 Customer Engagement の開発者ガイド: Outlook 用 Dynamics 365 Customer Engagement の拡張](/dynamics365/customer-engagement/developer/extend-customer-engagement-outlook)

**NuGet パッケージ**: [Microsoft.CrmSdk.Outlook](https://www.nuget.org/packages/Microsoft.CrmSdk.Outlook/)

|アセンブリ|名前空間|
|---------|---------|
|Microsoft.Crm.Outlook.Sdk.dll|[Microsoft.Crm.Outlook.Sdk](/dotnet/api/microsoft.crm.outlook.sdk)|



## <a name="community-tools-for-common-data-service-for-apps"></a>Common Data Service for Apps 用のコミュニティ ツール

Dynamics 365 コミュニティではツールを作成しています。 人気が高いツールの多くは、[XrmToolBox](https://www.xrmtoolbox.com/) で配布されています。 XrmToolBox は、カスタマイズ、構成、操作タスクを容易にするツールを提供する、Common Data Service for Apps に接続する、Windows アプリケーションです。 これには、管理、カスタマイズまたは構成タスクを簡単に、またより短い時間で行えるようにする 30 を超えるプラグインが付属しています。

Common Data Service for Apps で使用できる、XrmToolBox から配布される厳選されたコミュニティ ツールの一覧を以下に示します。

|ツール  |説明  |
|---------|---------|
|[Attribute Manager](https://www.xrmtoolbox.com/plugins/DLaB.Xrm.AttributeManager/)|属性の型の名前変更、削除、または変更を行う場合に使用します。|
|[Early Bound Generator](https://www.xrmtoolbox.com/plugins/DLaB.Xrm.EarlyBoundGenerator/)|事前バインド エンティティ/オプション セット/アクションを生成します。 SDK の CrmSvcUtil を使用し、クラスの作成に使用されるコマンド ラインを示します。|
|[Excel にエクスポート](https://www.xrmtoolbox.com/plugins/Ryr.XrmToolBox.ExportToExcel/)|レコードを選択されたビュー/fetchxml から Excel に簡単にエクスポートできます。|
|[FetchXML Builder](https://www.xrmtoolbox.com/plugins/Cinteros.Xrm.FetchXmlBuilder/)|FetchXml クエリを作成してテストします。|
|[メタデータ ブラウザー](https://www.xrmtoolbox.com/plugins/MsCrmTools.MetadataBrowser/)|Dynamics CRM 組織からのメタデータを参照します。|
|[プラグイン トレース ビューアー](https://www.xrmtoolbox.com/plugins/Cinteros.XrmToolBox.PluginTraceViewer/)|簡単なフィルター処理でプラグイン トレース ログを調べ、可能性を示します。|
|[ユーザー設定ユーティリティ](https://www.xrmtoolbox.com/plugins/MsCrmTools.UserSettingsUtility/)|ユーザーの個人用設定を一括管理します。|

> [!NOTE]
> コミュニティで作成されるツールは、Microsoft ではサポートされません。 コミュニティ ツールに関するご質問や問題については、そのツールの発行元にお問い合わせください。

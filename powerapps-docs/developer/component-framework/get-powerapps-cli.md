---
title: PowerApps component framework ツールの入手 | Microsoft Docs
description: PowerApps component framework を使用してユーザー定義コンポーネントを作成、デバッグ、展開するために Microsoft PowerApps CLIを取得します。
keywords: PowerApps コンポーネント フレームワーク、カスタム コンポーネント、コンポーネント フレームワーク
ms.author: nabuthuk
manager: kvivek
ms.date: 06/18/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f393f227-7a88-4f25-9036-780b3bf14070
---

# <a name="get-tooling-for-powerapps-component-framework"></a>PowerApps component framework ツールを入手します。

[!INCLUDE[cc-beta-prerelease-disclaimer](../../includes/cc-beta-prerelease-disclaimer.md)]

PowerApps component framework を使用して、ユーザー定義コンポーネントを作成、デバッグ、および展開するには、 **Microsoft PowerApps CLI** (コマンド ライン インターフェイス) を使用します。 PowerApps CLI により開発者は PowerApps component framework コンポーネントを迅速に作成できます。そして将来的には追加の開発やアプリケーション ライフサイクル管理 (ALM) のエクスペリエンスに対するサポートを含むように拡張されます。 

## <a name="what-is-microsoft-powerapps-cli"></a>Microsoft PowerApps CLI とは 

Microsoft PowerApps CLI はユーザー定義コンポーネントを作成するための、シンプルでワンストップな開発者向けコマンド ライン インターフェイスです。 PowerApps CLI は、エンタープライズ開発者と ISV が PowerApp、Dynamics 365 for Customer Engagement アプリ 拡張機能、そしてカスタマイズを、すばやく効率的に作成、構築、デバッグ、および公開できる、包括的な ALM ストーリーの最初のステップです。  

> [!IMPORTANT]
> - Microsoft PowerApps CLI ツールはプレリリース版であり、製品版とは異なる場合があります。
> - [!INCLUDE[cc_preview_features_definition](../../includes/cc-preview-features-definition.md)] 
> - ソフトウェアに関するフィードバックを Microsoft に提供する場合、お客様は、フィードバックを使用、共有、および商品化する権利をいかなる方法および目的にもかかわらず Microsoft に無償で与えるものとします。 
> - Microsoft はこのプレビュー機能のサポートを提供しません。 Microsoft テクニカル サポートは問題や質問への対応を致しかねます。

## <a name="install-microsoft-powerapps-cli"></a>Microsoft PowerApps CLI のインストール

Microsoft PowerApps CLI を使用するには、次の手順を実行します。

1. [Npm](https://www.npmjs.com/get-npm)(Node.js に含まれる) または [Node.js](https://nodejs.org/en/) (npm に含まれる) をインストールします。 最も安定している LTS (長期サポート) バージョン 10.15.3 LTS をお勧めします。

1. [.NET Framework4.6.2開発者パック](https://dotnet.microsoft.com/download/dotnet-framework/net462) をインストールします 。 

1. Visual Studio 2017 以降をお持ちでない場合、以下のいずれかの方法に従ってください:
   - オプション1: [Visual Studio 2017](https://docs.microsoft.com/visualstudio/install/install-visual-studio?view=vs-2017)以降をインストールします。
   - オプション 2: [.NET Core 2.2 SDK](https://dotnet.microsoft.com/download/dotnet-core/2.2) をインストールしてから、 [Visual Studioコード](https://code.visualstudio.com/Download) をインストールします。

1. [Microsoft PowerApps CLI](https://aka.ms/PowerAppsCLI) のインストール



> [!NOTE]
> - PowerApps CLI を使用してユーザー定義コンポーネントを展開するには、システム管理者またはシステム カスタマイザー特権を持つ Common Data Service 環境が必要です。
> - 現在、PowerApps CLI は Windows 10 でのみサポートされています。

## <a name="update-microsoft-powerapps-cli-to-the-latest-version"></a>最新バージョンに Microsoft PowerApps CLIを更新します。

Microsoft PowerApps CLI を最新バージョンに更新し、最新機能をすべて利用して、VS 2017 の開発者コマンド プロンプトで次のコマンドを実行します。

```CLI
pac install latest
```

### <a name="what-else-do-i-need-to-know"></a>ほかに知る必要があることは？

ソリューション プロジェクトまたは PowerApps component frameworkプロジェクトをすでに作成している場合は、必ずこれらのプロジェクトを最新のパッケージに更新してください。 これにより、既存のプロジェクトで新しく追加された機能を利用できます。 新しく作成されたプロジェクトには、すでにこれらの設定が含まれます。

- PowerApps component framework プロジェクト フォルダにある `pcfproj` の バージョン タグを更新します:

   ```XML
   <PackageReference Include="Microsoft.PowerApps.MSBuild.Pcf" Version="0.*"/>
   ```
- ソリューション プロジェクト フォルダにある `cdsproj` の バージョン タグを更新します:

   ```XML
   <PackageReference Include="Microsoft.PowerApps.MSBuild.Solution" Version="0.*"/>
   ```

    > [!NOTE] 
    > 上記の変更を行った後、正しいバージョン `msbuild /t:restore` でプロジェクトを作成するコマンドを実行します。


- PowerApps component framework プロジェクト フォルダにある `package.json` ファイル の バージョン タグを更新します:

  ```JSON
  "devDependencies":{
   "pcf-scripts": "^0",
   "pcf-start": "^0"
    }
  ```
   > [!NOTE]
   > 上記の変更を行った後、コマンド プロンプトで 'npm 更新プログラム' を使用すると、常にプロジェクトが正しいバージョンに更新されます。

## <a name="microsoft-powerapps-cli-telemetry"></a>Microsoft PowerApps CLI テレメトリ

PowerApps CLI ツールのどの機能が開発者によって最も頻繁に使用されるかを理解するために、この機能のチームは匿名化したテレメトリを集約しています。 集計データは本当に重要なことに焦点を合わせて、顧客に最高のエクスペリエンスを提供することを可能にします。

> [!NOTE]
> テレメトリ収集を無効にするには、次のコマンド `pac telemetry --enable false` を実行します。 テレメトリを元に戻すには、次のコマンド `pac telemetry --enable true` を使用します。

## <a name="uninstall-microsoft-powerapps-cli"></a>Microsoft PowerApps CLI をアンインストールします。

PowerApps CLI ツールをアンインストールするには [ここ](https://aka.ms/PowerAppsCLI) から MSI を実行してください。 

プライベート プレビューの参加者の方で、CLI の古いバージョンをお持ちの場合は、以下の手順を実行します:

1. PowerApps CLI がインストールされた場所を調べるには、コマンド プロンプトを開いて `where pac` と入力します。
1. PowerAppsCLI フォルダを削除します。
1. コマンド プロンプトでコマンド `rundll32 sysdm.cpl,EditEnvironmentVariables` を実行して、環境変数ツールを開きます。
1. `User variable for...` セクションの `Path` をダブルクリックします。
1. PowerAppsCLI のパスを含む行を選択して、右側の削除ボタンをクリックします。
1. **OK** を 2 回クリックします。

### <a name="see-also"></a>関連項目

[TypeScript でコンポーネントを実装する](implementing-controls-using-typescript.md)<br/>


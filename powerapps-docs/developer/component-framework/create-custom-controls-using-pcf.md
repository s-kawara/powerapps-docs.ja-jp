---
title: PowerApp コンポーネントのフレームワーク ツールを使用してカスタム コンポーネントを作成する | Microsoft Docs
description: PowerApps コンポーネントのフレームワーク ツールを使用してコンポーネントの作成を開始する
keywords: PowerApps コンポーネント フレームワーク、カスタム コンポーネント、コンポーネント フレームワーク
ms.author: nabuthuk
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d2cbf58a-9112-45c2-b823-2c07a310714c
---

# <a name="create-debug-and-deploy-a-component-using--microsoft-powerapps-cli"></a>Microsoft PowerApps CLI を使用してコンポーネントを作成、デバッグ、および展開する

PowerApps コマンド ライン インターフェイス (CLI) を使用して、カスタム PowerApps コンポーネント フレームワーク コンポーネントを作成、デバッグ、および展開する。 PowerApps CLI により開発者は PowerApps コンポーネント フレームワーク コンポーネントを迅速に作成できます。そして将来的に追加の開発やアプリケーション ライフサイクル管理 (ALM) のエクスペリエンスのサポートを含むように拡張されます。 

## <a name="what-is-microsoft-powerapps-cli"></a>Microsoft PowerApps CLI とは 

Microsoft PowerApps CLI はカスタム コンポーネントを作成するための、シンプルでワンストップな開発者向けコマンド ライン インターフェイスです。 PowerApps CLI は、エンタープライズ開発者と ISV が PowerApp、Dynamics 365 for Customer Engagement アプリ 拡張機能、そしてカスタマイズを、すばやく効率的に作成、構築、デバッグ、および公開できる、包括的な ALM ストーリーの最初のステップです。  

## <a name="prerequisites-to-use-powerapps-cli"></a>PowerApps CLI を使用する前提条件

PowerApps CLI を使用するために以下が必要です:

- [Npm](https://www.npmjs.com/get-npm)(Node.js に含まれる) または [Node.js](https://nodejs.org/en/) (npm に含まれる) をインストールします。 最も安定している LTS (長期サポート) バージョン 10.15.3 LTS をお勧めします。
- まだ Visual Studio 2017 以降をお持ちでない場合、以下のいずれかの方法に従ってください:
   - オプション 1: Visual Studio 2017 以降をインストールします。
   - オプション 2: .NET Core 2.2 SDK と Visual Studio Code をインストールします。
- Microsoft PowerApps CLI を [ここ](http://download.microsoft.com/download/D/B/E/DBE69906-B4DA-471C-8960-092AB955C681/powerapps-cli-0.1.51.msi) からインストールします

> [!IMPORTANT]
> - Microsoft PowerApps CLI ツールはプレリリース版であり、製品版とは異なる場合があります。
> - [!INCLUDE[cc_preview_features_definition](../../includes/cc-preview-features-definition.md)] 
> - ソフトウェアに関するフィードバックを Microsoft に提供する場合、お客様は、フィードバックを使用、共有、および商品化する権利をいかなる方法および目的にもかかわらず Microsoft に無償で与えるものとします。 
> - Microsoft はこのプレビュー機能のサポートを提供しません。 Microsoft テクニカル サポートは問題や質問への対応を致しかねます。

> [!NOTE]
> カスタム コンポーネントを展開するには、システム管理者またはシステム カスタマイザー権限を持つ Common Data Service 環境が必要です。

> [!NOTE]
> 現在、PowerApps CLI は Windows 10 でのみサポートされます。

## <a name="creating-a-new-powerapps-component-framework-component"></a>新しい PowerApps コンポーネントのフレームワーク コンポーネントの作成

開始するには、PowerApps CLI をインストールした後で VS 2017 の新しい開発者コマンド プロンプトを開きます。

1. VS 2017 の開発者コマンド プロンプトで、ローカル ハードドライブにたとえば `C:\Users\<your name>\Documents\My_PCF_Control` のように新しいフォルダを作成します。
2. コマンド `cd <specify your new folder path>` を使用して、新しく作成したフォルダに移動します。
3. 次のコマンドを実行して、いくつかの基本パラメータを渡すことで新しいコンポーネント プロジェクトを作成します `pac pcf init --namespace <specify your namespace here> --name <put component name here> --template <component type>`
 
   > [!NOTE]
   > 今回は 2 種類のコンポーネント **フィールド** と **データセット** をご提供します。

4. 必要なプロジェクトの依存関係をすべて取得するには、コマンド `npm install` を実行します。
5. 任意の開発者環境でプロジェクト フォルダ (`C:\Users\<your name>\Documents\My_PCF_Control\<component name>`) を開き、カスタム コンポーネント開発を始めます。 段階的なチュートリアルに従いたい場合は、下にスクロールしてサンプルの線形コンポーネントの実装方法を確認してください。

## <a name="building-your-components"></a>コンポーネントの構築

コンポーネントを構築するには Visual Studio Code でフォルダを開き、コマンド (Ctrl-Shift-B) を使用してビルド オプションを選択します。 あるいは、VS 2017 ウィンドウの開発者コマンド プロンプトで `npm run build` コマンドを使用して、素早くコントロールを構築できます。

## <a name="debugging-your-powerapps-component-framework-component"></a>PowerApps コンポーネントのフレームワーク コンポーネントのデバッグ

カスタム コンポーネント ロジックの実装が完了したら、次のコマンドを実行してデバッグ処理を開始します `npm start`

> [!NOTE]
> 現在はフィールド コンポーネントの視覚化しかできませんが、データセットのサポートがすぐに開始されます。 単なる例として、以下の画像は以下のチュートリアルで実装されたサンプル コンポーネントを示します。 

> [!div class="mx-imgBorder"]
> ![ローカルホスト](media/local-host.png "ローカルホスト")

上の画像で示すように、ブラウズ ウィンドウは 3 つのセクションで開きます。 右側のウィンドウは **入力** と **出力** セクションで構成されており、独自のコンポーネントは左側のウィンドウに表示されます

  - **入力** セクションは、manifest.xml で定義されたすべてのプロパティと、その種類 / 種類グループを表示する対話型の UI です。 それは各プロパティの模擬データを入力することを可能にします。 
  - **出力** セクションはコンポーネントの `getOutputs` メソッドが呼ばれるたびに出力を表示します。  
 
> [!NOTE]
> `manifest.xml` を修正するか追加のプロパティを作成する場合は、それらが入力セクションに表示される前にデバッグ プロセスを再起動する必要があります。

模擬データを入力している間、ブラウザのデバッグ機能を使用してコンポーネントの動作を確認できます。 各ブラウザには、ブラウザでコードをネイティブにデバッグするための、デバッグ ツールが用意されています。 通常は **F12** キーを押すことでブラウザのデバッグを有効にでき、デバッグに使用されるネイティブ開発者ツールを表示します。 現在、Chrome と Edge の両方のブラウザがサポートされています。

たとえば、**Microsoft Edge** で、

- **F12** を押してインスペクターを開きます。
- コンポーネントをクリックします
- 上部のバーで **デバッガー** に移動し、検索バーのマニフェスト ファイルに記述されたコンポーネント名の検索を開始します。 たとえば、コンポーネント名を `Hello World component` のように入力します。

     > [!div class="mx-imgBorder"]
     > ![デバッグ コンポーネント](media/debug-control.png "デバッグ コンポーネント")

> [!NOTE]
> `init` と `updateView` のようなコンポーネントのライフ サイクル メソッドに、ブレークポイントを設定するのは常に良い方法です

次のようにソース タブにブレークポイントを設定することで、ローカルでリアルタイムにコンポーネントを操作したり、DOM の要素を確認することもできます:

> [!div class="mx-imgBorder"]
> ![ローカルホスト](media/local-host.png "ローカルホスト")

> [!div class="mx-imgBorder"]
> ![デバッグ コンポーネント](media/debug-control-1.png "デバッグ コンポーネント 1")


 > [!NOTE]
 > 以下の手順を使用して、fiddler を使用した外部ループ デバッグを実行することもできます。
 >    1. [Fiddler](https://www.telerik.com/download/fiddler) のインストール
 >    2. [AutoResponder](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/streamline-javascript-development-fiddler-autoresponder) を設定するにはステップに従って下さい

## <a name="deploying-your-powerapps-component-framework-components"></a>PowerApps コンポーネントのフレームワーク コンポーネントの展開

デバッグと開発が終了したら、残りは 1 ステップです - 新しいコンポーネントのデプロイ。  

[ソリューション](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/customize/solutions-overview) ファイルを作成してインポートするには、次の手順に従います。

1. 新しいディレクトリを作成して、そこに移動します 'cd <new directory name>'
2. `cd <your new folder>` の後で `pac solution init --publisherName <enter your publisher name> --customizationPrefix <enter your publisher name>` コマンドを使用して、選択したディレクトリに新しいソリューション プロジェクトを作成します。

   > [!NOTE]
   > [publisherName](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/reference/entities/publisher) と [cutomizationPrefix](https://docs.microsoft.com/en-us/powerapps/maker/common-data-service/change-solution-publisher-prefix) の値は環境に固有である必要があります。
 
3. 新しいソリューション プロジェクトを作成したら、その作成したコンポーネントが配置される場所を参照する必要があります。 コマンド `pac solution add-reference --path <path or relative path of your PowerApps component framework project on disk>` を使用して参照を追加できます
4. ソリューション プロジェクトから zip ファイルを生成するには、ソリューション プロジェクト ディレクトリに `cd` してから `msbuild /t:restore` そして `msbuild` コマンドを使ってプロジェクトをビルドする必要があります

    > [!NOTE]
    > msbuild 15 がパスにない場合は、Vs 2017 の開発者コマンド プロンプトを開いて `msbuild` コマンドを実行します。

    > [!NOTE]
    > デバッグ構成でソリューションをビルドして、アンマネージド ソリューション パッケージを生成します。 管理ソリューション パッケージは、リリース構成でソリューションを構築することにより生成されます。 これらの設定は `cdsproj` ファイルで SolutionPackageType プロパティを指定することでオーバーライドできます。
    
    > [!NOTE]
    > プロジェクトが管理ソリューションまたはマネージドとアンマネージドの両方を発行するようにビルドしたい場合は、ソリューションプロジェクトを作成したフォルダを開いて `cdsproj` ファイルを編集し、以下のプロパティ グループのコメントを外します:
      ```XML
         <PropertyGroup>
          <SolutionPackageType>Managed</SolutionPackageType>
           </PropertyGroup>
      ```

    > [!NOTE]
    > また、以下のプロパティ グループ要素を追加して、追加のソリューション パッケージ [機能](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/compress-extract-solution-file-solutionpackager) を有効にもできます:

     ```XML
       <PropertyGroup>
         <SolutionPackageErrorLevel />
         <SolutionPackageEnableLocalization />
        <SolutionPackagerWorkingDirectory />
        <SolutionPackageLogFilePath />
        <SolutionPackageZipFilePath />
        <SolutionPackageMapFilePath />
       </PropertyGroup>
     ```

5. 生成されたソリューションの zip ファイルは `\bin\debug\` にあります。
6. zip ファイルの準備ができたら Web ポータルを使用して、手動で [ソリューションをインポート](https://docs.microsoft.com/en-us/dynamics365/customer-engagement/customize/import-update-export-solutions) する必要があります。

## <a name="adding-custom-controls-to-entity-or-a-field"></a>エンティティやフィールドにカスタム コントロールを追加する

データセット コンポーネントや単純なテーブル コンポーネントなど、カスタム コンポーネントをグリッドやビューに追加するには、トピック [フィールドやエンティティにコントロールを追加する](add-custom-controls-to-a-field-or-entity.md) で説明する手順に従います。 

## <a name="telemetry"></a>テレメトリ

PowerApps CLI ツールのどの機能が開発者によって最も頻繁に使用されるかを理解するために、この機能のチームは匿名化したテレメトリを集約しています。 集計データは本当に重要なことに焦点を合わせて、顧客に最高のエクスペリエンスを提供することを可能にします。

> [!NOTE]
> テレメトリ収集を無効にするには、次のコマンド `pac telemetry --enable false` を実行します。 テレメトリを元に戻すには、次のコマンド `pac telemetry --enable true` を使用します。

## <a name="how-to-uninstall-microsoft-powerapps-cli"></a>Microsoft PowerApps CLI をアンインストールする方法

CLI ツールをアンインストールするには [ここ](http://download.microsoft.com/download/D/B/E/DBE69906-B4DA-471C-8960-092AB955C681/powerapps-cli-0.1.51.msi) から MSI を実行してください。 プライベート プレビューの参加者の方で、CLI の古いバージョンをお持ちの場合は、以下の手動の手順に従ってください:

1. PowerApps CLI がインストールされた場所を調べるには、コマンド プロンプトを開いて `where pac` と入力します。
1. PowerAppsCLI フォルダを削除します。
1. コマンド プロンプトでコマンド `rundll32 sysdm.cpl,EditEnvironmentVariables` を実行して、環境変数ツールを開きます。
1. `User variable for...` セクションの `Path` をダブルクリックします。
1. PowerAppsCLI のパスを含む行を選択して、右側の削除ボタンをクリックします。
1. [OK] を 2 回クリックします。

## <a name="known-configuration-issues-and-workarounds"></a>既知の構成に関する問題と対応策

**Msbuild エラー MSB4036:**

1. プロジェクト ファイルのタスク名はタスク クラスの名前と同じです。
2. タスク クラスはパブリックで Microsoft.Build.Framework.ITask インターフェイスを実装しています。
3. タスクは、プロジェクト ファイルまたは <path> ディレクトリにある *.tasks ファイルの <UsingTask> で正しく宣言されます

**解決方法:**

1. Visual Studio インストーラーを開きます。 
1. VS 2017 で変更をクリックします。 
1. 個別のコンポーネントをクリックします
1. コード ツールの **NuGet ターゲットとビルド タスク** を参照してください。

### <a name="see-also"></a>関連項目

[TypeScript でコンポーネントを実装する](implementing-controls-using-typescript.md)<br/>
[既存のコンポーネントを新しいツールの形式に更新する](updating-existing-controls.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](overview.md)

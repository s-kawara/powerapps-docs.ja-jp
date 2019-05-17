---
title: インポート コントロール | Microsoft Docs
description: カスタム コントロールのインポート処理
keywords: null
ms.author: nabuthuk
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.topic: article
---

# <a name="deploying-controls-into-common-data-service"></a>Common Data Service にコントロールを展開する

このトピックはカスタム コントロールを Common Data Service にインポートする方法を示します。 PowerApps CLI でカスタム コントロールを開発した後、次のステップはそれらのコントロールをインポートすることで、これで実行時にコントロールを表示できます。

ソリューション ファイルを作成してインポートする手順を示します:

1. `cd <your new folder>` の後で `pac solution init --publisherName <enter your publisher name> --customizationPrefix <enter your publisher name>` コマンドを使用して、選択したディレクトリに新しいソリューション プロジェクトを作成します。

   > [!NOTE]
   > `publisherName` と `cutomizationPrefix` の値は環境に固有である必要があります。
 
2. 新しいソリューション プロジェクトを作成したら、その作成したコントロールが配置される場所を参照する必要があります。 コマンド `pac solution add-reference --<path of your PowerApps component framework project on disk>` を使用して参照を追加できます
3. ソリューション プロジェクトから zip ファイルを生成するには、ソリューション プロジェクト ディレクトリに `cd` してから `msbuild/t:restore` と `msbuild` コマンドを使ってプロジェクトをビルドする必要があります

    > [!NOTE]
    > msbuild 15 がパスにない場合は、Vs 2017 の開発者コマンド プロンプトを開いて msbuild コマンドを実行します。

    > [!NOTE]
    > デバッグ構成でソリューションをビルドして、アンマネージド ソリューション パッケージを生成します。 管理ソリューション パッケージは、リリース構成でソリューションを構築することにより生成されます。 これらの設定は、cdsproj ファイルで SolutionPackageType プロパティを指定することでオーバーライドできます。

4. 生成されたソリューション ファイルは `\bin\debug\` にあります。
5. Webポータルを使用して手動でソリューションをインポートする必要があります。

## <a name="telemetry"></a>テレメトリ

PowerApps CLI ツールのどの機能が開発者によって最も頻繁に使用されるかを理解するために、この機能のチームは匿名化したテレメトリを集約しています。 集計データは本当に重要なことに焦点を合わせて、顧客に最高のエクスペリエンスを提供することを可能にします。

テレメトリ収集を無効にするには、次のコマンド `pac telemetry - -enabled false` を実行します。 テレメトリを元に戻すには、次のコマンド `pac telemetry- -enabled true` を使用します。

### <a name="see-also"></a>関連項目

[エンティティやフィールドにコントロールを追加](add-custom-controls-to-a-field-or-entity.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](overview.md)
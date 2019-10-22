---
title: PowerApps component framework | のツールを入手するMicrosoft Docs
description: Microsoft PowerApps CLI を取得して、PowerApps コンポーネントフレームワークを使用してコードコンポーネントを作成、デバッグ、および配置します。
keywords: PowerApps コンポーネントフレームワーク、コードコンポーネント、コンポーネントフレームワーク
ms.author: nabuthuk
author: Nkrb
manager: kvivek
ms.date: 10/01/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: f393f227-7a88-4f25-9036-780b3bf14070
ms.openlocfilehash: 496b7d443775da075dd8da52ac4b0a754121bf28
ms.sourcegitcommit: 4c35aedde46380d5438687ae6f61a3b0cc7e7e2f
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/05/2019
ms.locfileid: "72340025"
---
# <a name="get-tooling-for-powerapps-component-framework"></a>PowerApps コンポーネントフレームワークのツールを入手する

**MICROSOFT POWERAPPS CLI** (コマンドラインインターフェイス) を使用して、PowerApps コンポーネントフレームワークを使用してコードコンポーネントを作成、デバッグ、および配置します。 PowerApps CLI を使用すると、開発者はコードコンポーネントをすばやく作成できます。 今後、開発およびアプリケーションライフサイクル管理 (ALM) の追加のエクスペリエンスをサポートするように拡張される予定です。 

## <a name="what-is-microsoft-powerapps-cli"></a>Microsoft PowerApps CLI とは 

Microsoft PowerApps CLI は、開発者とアプリの開発者がコードコンポーネントを作成できるようにする、単純な単一ストップの開発者コマンドラインインターフェイスです。 PowerApps CLI ツールは、企業の開発者や Isv が拡張機能とカスタマイズを迅速かつ効率的に作成、ビルド、デバッグ、公開できる包括的な ALM に向けた第一歩です。  

## <a name="install-microsoft-powerapps-cli"></a>Microsoft PowerApps CLI のインストール

CLI Microsoft PowerApps を取得するには、次の手順を実行します。

1. [Npm](https://www.npmjs.com/get-npm) (node.js 付属) または[node.js](https://nodejs.org/en/) (npm 付属) をインストールします。 LTS (長期的なサポート) バージョン 10.15.3 LTS をお勧めします。これは、最も安定しているように見えます。

1. [.NET Framework 4.6.2 Developer Pack](https://dotnet.microsoft.com/download/dotnet-framework/net462)をインストールします。 

1. Visual Studio 2017 以降をまだ持っていない場合は、次のいずれかのオプションを実行します。
   - オプション 1: [Visual Studio 2017](https://docs.microsoft.com/visualstudio/install/install-visual-studio?view=vs-2017)以降をインストールします。
   - オプション 2: [.Net Core 2.2 SDK](https://dotnet.microsoft.com/download/dotnet-core/2.2)をインストールし、 [Visual Studio Code](https://code.visualstudio.com/Download)をインストールします。

1. [MICROSOFT POWERAPPS CLI](https://aka.ms/PowerAppsCLI)をインストールします。
1. 最新の機能をすべて活用するには、次のコマンドを使用して PowerApps CLI ツールを最新バージョンに更新します。

    ```CLI
    pac install latest
    ```

> [!NOTE]
> - PowerApps CLI を使用してコードコンポーネントを配置するには、システム管理者またはシステムカスタマイザーの特権を持つ Common Data Service 環境が必要です。
> - 現在、PowerApps CLI は Windows 10 でのみサポートされています。

## <a name="microsoft-powerapps-cli-telemetry"></a>CLI テレメトリの Microsoft PowerApps

機能チームはテレメトリを集計して、PowerApps CLI ツールで最も頻繁に使用される機能や機能を理解します。 集計データを使用すると、重要なものに焦点を当てることによって、顧客に最適なエクスペリエンスを提供できます。

> [!NOTE]
> テレメトリの収集を無効にするには、コマンド `pac telemetry disable` を実行します。 テレメトリを再び有効にするには、コマンド `pac telemetry enable` を使用します。


## <a name="uninstall-microsoft-powerapps-cli"></a>Microsoft PowerApps CLI のアンインストール

PowerApps CLI ツールをアンインストールするには、[ここ](https://aka.ms/PowerAppsCLI)から MSI を実行します。 

プライベートプレビュー参加要素で、古いバージョンの CLI を使用している場合は、次の手順を実行します。

1. PowerApps CLI がインストールされている場所を確認するには、コマンドプロンプトを開き、「`where pac`」と入力します。
1. PowerAppsCLI フォルダーを削除します。
1. コマンドプロンプトで `rundll32 sysdm.cpl,EditEnvironmentVariables` コマンドを実行して、環境変数ツールを開きます。
1. [@No__t_1] セクションの `Path` をダブルクリックします。
1. PowerAppsCLI パスを含む行を選択し、右側にある **[削除]** ボタンを選択します。
1. [ **OK]** を2回選択します。

### <a name="see-also"></a>関連項目

[TypeScript を使用してコンポーネントを実装する](implementing-controls-using-typescript.md)<br/>

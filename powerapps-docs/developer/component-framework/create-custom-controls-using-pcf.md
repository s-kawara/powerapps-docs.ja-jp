---
title: カスタムコンポーネントの作成と構築 | Microsoft Docs
description: PowerApps コンポーネントのフレームワーク ツールを使用してコンポーネントの作成を開始する
keywords: PowerApps コンポーネント フレームワーク、カスタム コンポーネント、コンポーネント フレームワーク
ms.author: nabuthuk
author: Nkrb
manager: kvivek
ms.date: 06/20/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d2cbf58a-9112-45c2-b823-2c07a310714c
---

# <a name="create-and-build-a-custom-component"></a>カスタムコンポーネントを作成、構築する

[!INCLUDE[cc-beta-prerelease-disclaimer](../../includes/cc-beta-prerelease-disclaimer.md)]

このトピックでは、PowerApps component frameworkを使用して、カスタム コンポーネントの作成、展開方法について説明します。

Microsoft PowerApps CLI がインストールされていることが前提となります。

## <a name="create-a-new-component"></a>新しいコンポーネントの作成

開始するには、PowerApps CLI をインストールした後で VS 2017 の新しい開発者コマンド プロンプトを開きます。

1. VS 2017 の開発者コマンド プロンプトでは、ローカルのハードディスクに新規フォルダを作成します。作成例としては、*C:\Users\<your name>\Documents\My_PCF_Control*です。
2. `cd <specify your new folder path>`のコマンドを使用して、新規作成されたフォルダに移動します。
3. 以下のコマンドを実行し、いくつかの基本パラメータを渡して新しいコンポーネントプロジェクトを作成します:

    `pac pcf init --namespace <specify your namespace here> --name <put component name here> --template <component type>`
 
   > [!NOTE]
   > 現在は、次の2つのコンポーネントを提供しています: **フィールド** 、 **データセット**.

4. 必要なプロジェクトの依存関係をすべて取得するには、コマンド `npm install` を実行します。
5. 任意の開発者環境でプロジェクト フォルダ (`C:\Users\<your name>\Documents\My_PCF_Control\<component name>`) を開き、カスタム コンポーネント開発を始めます。

## <a name="build-your-component"></a>コンポーネントを構築する

コンポーネントを構築するには、Visual Studio コードのフォルダを開き、(Ctrl-Shift-B) コマンドを使用し、構築のオプションを選択します。 あるいは、VS 2017 ウィンドウの開発者コマンド プロンプトで  `npm run build` コマンドを使用することで、簡単にコンポーネントを構築することができます。

> [!TIP]
> コンポーネントのデバッグを構築中、または構築完了後に行うには、 [カスタムコンポーネントのデバッグ](debugging-custom-controls.md) を参照してください。

## <a name="known-configuration-issues-and-workarounds"></a>設定に関する既知の問題と回避策

**Msbuild エラー MSB4036:**

1. プロジェクト ファイルのタスク名はタスク クラスの名前と同じです。
2. タスク クラスはパブリックで Microsoft.Build.Framework.ITask インターフェイスを実装しています。
3. タスクは、プロジェクト ファイルの \<UsingTask> または、 <path> ディレクトリに格納されている、 *.tasks ファイルにて正しく宣言されています。

**解決方法:**

1. Visual Studio インストーラーを開きます。 
1. For VS 2017 では、 **修正** を選択します。 
1. 個々のコンポーネント をクリックします。
1. コード ツール配下の **NuGet ターゲットと構築タスク** を確認します。

### <a name="see-also"></a>関連項目

[カスタムコンポーネントのデバッグ](debugging-custom-controls.md)<br/>
[カスタムコンポーネントのパッケージ化](import-custom-controls.md)<br/>
[カスタム コンポーネントをフィールドやエンティティに追加する](add-custom-controls-to-a-field-or-entity.md)<br/>
[既存のカスタムコンポーネントを更新する](updating-existing-controls.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](overview.md)

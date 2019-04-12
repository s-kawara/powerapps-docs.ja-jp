---
title: 'チュートリアル: プラグインのデバッグ (Common Data Service) | Microsoft Docs'
description: 'このチュートリアルは、プラグインの使用方法を説明するシリーズの 2 番目のチュートリアルです。 '
ms.custom: ''
ms.date: 1/28/2019
ms.reviewer: pehecke
ms.service: powerapps
ms.topic: article
author: JimDaly
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="tutorial-debug-a-plug-in"></a>チュートリアル: プラグインをデバッグする

このチュートリアルは、プラグインの使用方法を説明するシリーズの 2 番目のチュートリアルです。 

- [チュートリアル: プラグインを書き込み登録する](tutorial-write-plug-in.md)
- チュートリアル: プラグインをデバッグする (このチュートリアル)
- [チュートリアル: プラグインを更新する](tutorial-update-plug-in.md)

関連する概念と技術的詳細については、以下を参照してください。

- [ビジネス プロセスを拡張するためのプラグインの使用](plug-ins.md)
- [プラグインを記述する](write-plug-in.md)
- [プラグインの登録](register-plug-in.md)
- [プラグインのデバッグ](debug-plug-in.md)


## <a name="goal"></a>目標

プラグインはリモート サーバーで実行されるため、プロセスにデバッガーを追加できません。 プラグイン プロファイラーは、実行中のプラグインのプロファイルをキャプチャし、Visual Studio ローカルで使用してプラグインの実行を再現できるようにします。



## <a name="prerequisites"></a>前提条件

- [チュートリアル: プラグインを作成して登録する](tutorial-write-plug-in.md) のすべての前提条件が適用されます。 [前提条件](tutorial-write-plug-in.md#prerequisites)を参照してください。
- 前のチュートリアルを完了していない場合、別の登録されているプラグインで以下の一般的な手順を使用できます。

## <a name="install-plug-in-profiler"></a>プラグイン プロファイラーをインストールする

1. プラグイン登録ツールがまだインストールされて開かれていない場合、[チュートリアル: プラグインを作成して登録する](tutorial-write-plug-in.md)の手順に従って開きます。 [プラグイン登録ツールを使用して接続する](tutorial-write-plug-in.md#connect-using-the-plug-in-registration-tool)セクションを完了します。
1. プラグイン登録ツールで、**プロファイラーのインストール** をクリックします。

    ![プロファイラーをインストールする](media/tutorial-debug-plug-in-install-profiler.md.png)

1. これにより、Common Data Service 環境のプラグイン プロファイラーという新しいマネージド ソリューションがインストールされます。 これは完了するまで 1、2 分要します。

## <a name="start-profiling"></a>プロファイリングの開始

1. プラグイン登録ツールで、先に登録した **(ステップ) BasicPlugin.FollowupPlugin: 取引先企業を作成する** ステップを選択し、**プロファイリングの開始** を選択します。

    ![プロファイリングの開始](media/tutorial-debug-plug-in-start-profiling.png)

1. **プロファイラーの設定** ダイアログで、既定の設定内容を受け入れて、**OK** をクリックしてダイアログを閉じます。

    ![foo](media/tutorial-debug-plug-in-profiler-settings.png)


プロファイラーの実行に関する詳細については、[コマンド プロンプト ウィンドウからプラグイン プロファイラーを起動する](#run-profiler-standalone) をご覧ください。

## <a name="capture-a-profile"></a>プロファイルを取り込む

1. モデル駆動型のアプリケーションでは、プラグインをトリガーするように新しい取引先企業を作成します。 これにより、プラグイン実行のインスタンスが取り込まれ、システムのプロファイル レコードとして保持されます。
1. プラグイン登録ツールで、**デバッグ**をクリックします。

    ![デバッグのクリック](media/tutorial-debug-plug-in-capture-profile-debug.png)

1. **プラグイン実行の再生** ダイアログの **セットアップ** タブで、![プロファイル コマンドを選択](media/tutorial-debug-plug-in-select-profile-command.png) アイコンをクリックして、**CRM からプロファイルを選択する** ダイアログを開きます。
1. **CRM からプロファイルを選択**  ダイアログで、**型名** が **BasicPlugin.FollowupPlugin** と等しく、前回プラグインをトリガーしたときに取り込んだプロファイルを表すプロファイルを選択します。

    ![[CRM からプロファイルを選択] ダイアログ](media/tutorial-debug-plug-in-select-profile-dialog.png)

## <a name="debug-your-plug-in"></a>プラグインをデバッグ

1. **プラグイン実行の再生**  ダイアログの **セットアップ** タブにある **アセンブリの指定** で、省略記号 (**…**) ボタンをクリックした後、`BasicPlugin.dll` の場所を選択します 。

    ![プラグイン実行の再生](media/tutorial-debug-plug-in-replay-plug-in-execution.png)

1. Visual Studio プロジェクトでは、プラグイン クラスのブレークポイントを設定します。

    ![ブレークポイントの設定](media/tutorial-debug-plug-in-set-break-point.png)

1. Visual Studio プロジェクトで、**デバッグ** > **プロセスにアタッチ…** を選択します。

    ![プロセスにアタッチ コマンド](media/tutorial-debug-plug-in-attach-to-process.png)

1. **PluginRegistration.exe** プロセスを選択し、**追加** をクリックします。

    ![[プロセスにアタッチ] ダイアログ](media/tutorial-debug-plug-in-attach-to-process-dialog.png)

    > [!NOTE]
    > プラグイン登録ツールがデバッグ モードで実行されていることがわかります。

1. **プラグイン実行の再生** ダイアログで、**実行の開始** をクリックします。

    ![実行の開始](media/tutorial-debug-plug-in-replay-plug-in-execution-debug.png)

1. Visual Studio プロジェクトで、コードが先に設定したブレークポイントで一時停止していることがわかります。 

    ![ブレークポイント ヒット](media/tutorial-debug-plug-in-breakpoint-hit.png)

1. デバッグするためにコードを進めることができるようになりました。


## <a name="repeat"></a>繰り返し

繰り返すには、Visual Studio プロジェクトで **デバッグ** > **再アタッチ** を選択して処理し、**プラグイン実行の再生** ダイアログで **実行の開始** をもう一度クリックします。

## <a name="stop-profiling"></a>プロファイリングの停止

1. **プラグイン実行の再生ダイアログ** ダイアログを閉じる
1. プラグイン登録ツールで、**プロファイリングの停止** をクリックします。

    ![プロファイリングの停止](media/tutorial-debug-plug-in-stop-profiling.png)

## <a name="next-steps"></a>次のステップ

プラグインで行う一般的な操作の詳細については、[チュートリアル: プラグインを更新する](tutorial-update-plug-in.md)に進みます。

次のチュートリアルに進まない場合、この手順で作成した BasicPlugin アセンブリの登録を解除する必要があります。 手順については、[アセンブリ、プラグイン、ステップの登録解除](tutorial-update-plug-in.md#unregister-assembly-plug-in-and-step)を参照してください。

<a name="run-profiler-standalone"></a>

## <a name="run-the-plug-in-profiler-from-a-command-prompt-window"></a>プラグイン プロファイラーをコマンド プロンプト ウィンドウから実行する

 プラグイン登録ツールから対話的にプロファイラーを実行することがしばしば望ましい一方で、プロファイラーはツールから独立しているコマンド プロンプト ウィンドウから実行することができます。 この方法は、顧客の [!INCLUDE[pn_dynamics_crm](../../includes/pn-dynamics-crm.md)] アプリ サーバーからプラグイン プロファイル ログを取得して、失敗したプラグインをデバッグするのに便利です。 開発者は、そのログを使用してプラグイン登録ツールでプラグインの実行を再生し、[!INCLUDE[pn_Visual_Studio](../../includes/pn-visual-studio.md)] を使用してプラグインをデバッグすることができます。

### <a name="procedure-run-the-plug-in-profiler-from-a-command-prompt"></a>手順: プラグイン プロファイラーをコマンド プロンプトから実行する

1. コマンド プロンプト ウィンドウを開き、作業ディレクトリを プラグイン登録ツール `PluginRegistration.exe` をダウンロードしたフォルダーに設定します。
2. 利用可能な実行時パラメータを見るためにこのコマンドを入力してください:  `PluginProfiler.Debugger.exe /?`  
3. サポートされているパラメーターの一覧を確認し、適切なパラメーターで PluginProfiler.Debugger.exe プログラムを再実行します。 
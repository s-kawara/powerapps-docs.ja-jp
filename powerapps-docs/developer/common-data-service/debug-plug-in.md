---
title: プラグインのデバッグ (アプリ用 Common Data Service) | Microsoft Docs
description: プラグイン登録ツールを使用して、プラグインをデバッグする方法を説明します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: brandonsimons
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="debug-plug-ins"></a>プラグインのデバッグ

書き込み、登録、およびプラグインをデバッグするプロセスは次のとおりです:

1. Visual Studio に .NET Framework クラス ライブラリ プロジェクトを作成します。
1. `Microsoft.CrmSdk.CoreAssemblies` NuGet パッケージをプロジェクトに追加します。
1. ステップとして登録されるクラスの <xref:Microsoft.Xrm.Sdk.IPlugin> インターフェイスを実装します。
1. インターフェイスに必要な <xref:Microsoft.Xrm.Sdk.IPlugin.Execute*> メソッドにコードを追加する
    1. 必要なサービスへの参照を取得する
    1. ビジネス ロジックの追加
1. アセンブリにサインし、ビルドする
1. アセンブリをテストする
    1. テスト環境でアセンブリを登録する
    1. アンマネージド ソリューションに、登録されたアセンブリとステップを追加する
    1. **アセンブリの動作をテストする**
    1. **想定されたトレース ログが書き込まれたことを確認する**
    1. **必要に応じてアセンブリをデバッグする**

このトピックの内容は上記**太字**のステップをカバーし、次のチュートリアルをサポートしています:

- [チュートリアル: プラグインを書き込み登録する](tutorial-write-plug-in.md)
- [チュートリアル: プラグインをデバッグする](tutorial-debug-plug-in.md)
- [チュートリアル: プラグインを更新する](tutorial-update-plug-in.md)

## <a name="test-your-assembly"></a>アセンブリをテストする

アセンブリをテストする最も簡単な方法は、アプリを使用して手動で操作を実行することです。 ただし、プラグインを実行させるイベントは、ワークフローや Web サービスから作成されたエンティティなど、複数の方法で開始できます。

属性の値または他の実行コンテキスト情報は、アクションの実行方法によって異なる場合があります。 プラグインを書き込むときは、防御プログラミング プラクティスを実行し、すべての期待値がそこにあると想定しないようにしてください。

プラグインを起動させる操作の自動化を行うプログラムを作成し、可能なバリエーションの数を含めることができます。

テスト自動ワークフローを使用したい場合、コミュニティがこのために作成したいくつかのツールがあります。 詳細については、[サーバー側開発のためのテスト ツール](testing-tools-server.md)を参照してください。


## <a name="use-tracing"></a>トレースを使用する

[トレース サービスの使用](write-plug-in.md#use-the-tracing-service)でも説明されているように、 <xref:Microsoft.Xrm.Sdk.ITracingService>、<xref:Microsoft.Xrm.Sdk.ITracingService.Trace*> を使用してプラグインのコード内で [PluginTraceLog エンティティ](reference/entities/plugintracelog.md)にメッセージを書き込めます。 メソッド。

このサービスを使用する前に、アプリ用 CDS 環境でトレースを有効にする必要があります。 [トレース ログを表示](tutorial-write-plug-in.md#view-trace-logs)で手順を詳しく説明します。

> [!NOTE]
> トレース ログは、特に多数のトレースと例外が生成されたときは、組織の保存領域を占有します。 トレースログは、デバッグとトラブルシューティングの場合にのみオンにして、調査の完了後はオフにする必要があります。

デバッグ中は、ブラウザーの Web API を使用して、特定のプラグイン クラスのトレース ログを簡単にクエリできます。 アセンブリの名前が `BasicPlugin.FollowUpPlugin` である場合、ブラウザーのアドレス フィールドでこのクエリを使用できます。

`GET <your org uri>/api/data/v9.0/plugintracelogs?$select=messageblock&$filter=typename eq 'BasicPlugin.FollowUpPlugin'`

JSON 結果はブラウザーに次のように返されます:


```json
{
    "@odata.context": "<your org uri>/api/data/v9.0/$metadata#plugintracelogs(messageblock)",
    "value": [{
        "messageblock": "FollowupPlugin: Creating the task activity.",
        "plugintracelogid": "f0c221d1-7f84-4f89-acdb-bbf8f7ce9f6c"
    }]
}
```

> [!TIP]
> これは、返された JSON をフォーマットするブラウザー プラグインをインストールする場合に最適です。 または、Postman を使用することもできます。 詳細については、[Postman を Web API と共に使用する](/dynamics365/customer-engagement/developer/webapi/use-postman-web-api)を参照してください。
> 
> [XrmToolbox プラグイン追跡ビューア](https://www.xrmtoolbox.com/plugins/Cinteros.XrmToolBox.PluginTraceViewer/)を使用する方が適している場合があります。 このコミュニティ ツールは Microsoft ではサポートされていません。 このツールに関するご質問は、その発行元にお問い合わせください。

同期プラグインまたはカスタム ワークフロー アセンブリが、ユーザーへのエラー ダイアログの表示につながるエラーをスローした場合、トレース メッセージはダウンロード可能なログ ファイルの中にあります。 ユーザーは、**ログ ファイルのダウンロード** ボタンを選択して、例外とトレース出力を格納しているログを表示することができます。

例外を返す、非同期の登録済みプラグインおよびワークフロー アセンブリの場合、トレース情報は Web アプリケーションの **システム ジョブ** フォームの詳細領域に表示されます。

> [!NOTE]
> ユーザー定義コードがデータベース トランザクション内で実行され、トランザクションのロールバックを引き起こす例外が発生した場合、コードによるすべてのエンティティ データの変更は取り消されます。 ただし、`PluginTraceLog` エンティティ レコードは、ロールバックが完了しても残ります。

## <a name="use-plug-in-profiler"></a>プラグイン プロファイラーを使用する

プラグイン プロファイラーは、自分の環境にインストールできるソリューションで、プラグインの実行コンテキストを取り込み、そのデータを使用してデバッグ中に Visual Studio 内でイベントを再生することができます。

プラグイン プロファイラーのインストールおよび使用方法については、[チュートリアル: プラグインのデバッグ](tutorial-debug-plug-in.md)を参照してください。 [プラグイン プロファイラーのインストール](tutorial-debug-plug-in.md#install-plug-in-profiler)および[プラグインのデバッグ](tutorial-debug-plug-in.md#debug-your-plug-in)を参照してください。

### <a name="view-plug-in-profile-data"></a>プラグイン プロファイラーを表示する

プラグイン プロファイラーをインストールしていくつかのプロファイルを取得すると、デバッグ時に使用されるイベント コンテキストと再生データを表示できます。 このデータを表示すると、プラグインが使用できる実行コンテキスト データを理解するのに役立ちます。

プラグイン登録ツールを使用してこのデータを表示するには、**プラグイン プロファイルの表示**コマンドを選択します。 これにより、プラグイン プロファイル ダイアログが開きます。

![プラグイン プロファイルを開く](media/view-plug-in-profile.png)

![ダウンロード アイコン](media/prt-down-arrow-icon.png)のアイコンを選択し、**CRM からプロファイルを選択する**ダイアログで、使用するログ アイテムを指定します。

![CRM からプロファイルを選択する](media/prt-select-profile-from-crm.png)

そして、**プラグイン プロファイル** ダイアログの**表示**を選択します。

これにより、プロファイル情報を含む開いている XML ファイルがダウンロードされます。 `Context` 要素は、プラグインに渡される実行コンテキストを表します。

![エクスポート プロファイル データ](media/prt-example-profile-data.png)

### <a name="more-information"></a>詳細

[サーバ側開発のためのテスト ツール](testing-tools-server.md)
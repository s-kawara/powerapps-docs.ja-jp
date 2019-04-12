---
title: 'サンプル: プラグインからの Web アクセス (Common Data Service) | Microsoft Docs'
description: このサンプルは、 Web 上にあるリソースにアクセスできるプラグインの書き込み方法を示します。
ms.custom: ''
ms.date: 1/16/2019
ms.reviewer: ''
ms.service: powerapps
ms.topic: samples
author: JimDaly
ms.author: pehecke
manager: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="sample-web-access-from-a-plug-in"></a>サンプル: プラグインからの Web アクセス

このサンプルは、 Web サービスもしくはフィードのようなリソースにアクセスできるプラグインの書き込み方法を示します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/WebAccessPlugin) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

1. [サンプル](https://github.com/Microsoft/PowerApps-Samples) リポジトリをダウンロードまたは複製して、ローカル コピーを用意します。 このサンプルは PowerApps-Samples-master\cds\orgsvc\C#\WebAccessPlugin にあります。
2. Visual Studio でサンプル ソリューションを開き、プロジェクトのプロパティに移動して、ビルド中にアセンブリが署名されることを確認します。 サンプルのアセンブリ (WebAccessPlugin.dll) をビルドするには F6 を押します。
3. プラグイン登録ツールを実行して D365 サーバーのサンドボックスおよびデータベースにサンプルのアセンブリを登録します。 ステップを登録するときは、セキュリティ保護されていない設定フィールドに Web URI 文字列 (例: http://www.microsoft.com) を指定します。
4. D365 アプリ を使用して適切な操作を実行して、メッセージとプラグインを登録したエンティティの要求を呼び出します。
5. プラグインを実行すると、63 行目のコードで例外がスローされます。 これにより、D365 アプリに ISV エラー ダイアログが表示されます。 そのダイアログで、**ダウンロード ファイル** を選択して、Web サービスの応答を含むプラグインの出力があるエラーログを表示します。
6. テストを完了したらアセンブリとステップの登録を解除します。

## <a name="what-this-sample-does"></a>このサンプルの概要

実行されると、プラグインは指定された Web サービスのアドレス (またはデフォルトのアドレス) から Web ページのデータをダウンロードし、そのデータをエラーログ ファイルまたはトレースサービスに書き込みます。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. Web アドレス値について、コンストラクタの安全でない設定パラメータをチェックします。それ以外の場合は、既定値が使用されます。
2. `System.Net.WebClient` クラスは Web ページ データをダウンロードするためにプラグインの `Execute` メソッドによって使用されます。
3. テスト目的でエラーログ ダウンロード ファイルを介して Web サービスの応答を利用可能にするために例外がスローされます。

### <a name="demonstrate"></a>使用方法

1. `WebClient.DownloadData` メソッドは Web サービス要求を使って Web ページ データをダウンロードします。
2. その応答データは、後で D365 アプリで表示するために、例外エラーログまたは（オプションで）トレース サービスに書き込まれます。
3. プラグイン コードは、Web サービスから WebException をキャッチし処理する方法を説明します。

### <a name="see-also"></a>関連項目
[外部 Web リソースにアクセスする](../../access-web-services.md)<br/>
[プラグインの登録](../../register-plug-in.md)
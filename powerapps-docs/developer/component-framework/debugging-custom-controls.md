---
title: カスタム コンポーネントのデバッグ | MicrosoftDocs
description: Fiddler とネイティブ デバッグを使用してカスタム コンポーネントをデバッグする方法
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.topic: article
ms.assetid: 18e88d702-3349-4022-a7d8-a9adf52cd34f
ms.author: nabuthuk
author: Nkrb
---
# <a name="debug-custom-components"></a>カスタムコンポーネントのデバッグ

カスタム コンポーネント ロジックの実装が完了したら、 `npm start` コマンドを使用してカスタム コンポーネントのテストとデバッグを開始します。 これにより、カスタムコンポーネントが構築され、ローカル テスト ハーネスで開きます。

> [!div class="mx-imgBorder"]
> ![テスト ハーネス 1](media/test-harness-1.png "テスト ハーネス 1")

上記の図に示されているように、ブラウザ ウィンドウが4つのセクションで開きます。 カスタム コンポーネントは左側のウィンドウで表示されますが、右側のウィンドウには **コンテキストの入力**、 **データの入力** 、 **データの出力** セクションが表示されます。

- **コンテキストの入力** セクションでは、フォームファクターを指定する方法、および各フォームファクター(Web、タブレット、電話) でカスタムコンポーネントをテストする方法が記載されています。 これは、カスタムコンポーネントが特定のフォームファクター機能に依存している場合に特に有用です。 次期リリースでは、高さと幅を指定する機能が実装されます。
- **データの入力** セクションは、マニフェスト ファイルで定義されている、すべてのプロパティと種別あるいは種別グループを表示する対話型の UI です。 これにより、各プロパティの模擬データを入力することができます。 
- **出力** セクションはコンポーネントの `getOutputs` メソッドが呼ばれるたびに出力を表示します。  

     > [!div class="mx-imgBorder"]
     > ![テスト ハーネス 2](media/test-harness-2.png "テスト ハーネス 2")

> [!NOTE]
> `manifest.xml` ファイルの修正または新規プロパティを作成する場合は、それらを入力セクションに表示させるにはデバッグ プロセスを再起動する必要があります。

## <a name="test-custom-components-with-mock-data"></a>擬似データを使用してカスタム コンポーネントをテストします。

- フィールド コンポーネントの場合、以下に示すように **ControlManifest.Input.xml** に定義されている各プロパティの値とタイプを入力することができます。

   > [!div class="mx-imgBorder"]
   > ![テスト ハーネス 2.5](media/test-harness-2.5.png "テスト ハーネス 2.5")

- データセットの場合は、テストデータを含むCSVファイルを読み込むことができます。 これは手動で作成することも可能ですが、ご利用の環境から.csv形式のファイルを直接エクスポートすることもできます。 有効なCSVファイルが使用可能になると、以下の図のように読み込むことができます。

   > [!div class="mx-imgBorder"]
   > ![テスト ハーネス 3](media/test-harness-3.png "テスト ハーネス 3")

- CSVファイルの読み込みが完了すると、 **ControlManifest.Input.xml** に定義されている各プロパティーをCSVの列にバインドします。 これを行うには、以下のように各プロパティの列を選択します:

    > [!div class="mx-imgBorder"]
    > ![テスト ハーネス 4](media/test-harness-4.png "テスト ハーネス 4")

- **ControlManifest.Input.xml**にプロパティが定義されていない場合は、すべての列が自動的にハーネスに読み込まれます。

   > [!div class="mx-imgBorder"]
   > ![テスト ハーネス 5](media/test-harness-5.png "テスト ハーネス 5")

## <a name="debug-custom-components-using-native-browsers"></a>ネイティブ ブラウザーを使用してカスタム コンポーネントをデバッグする

ブラウザのデバッグ機能を使用して、コンポーネントの動作を観察することができます。 各ブラウザには、ブラウザでコードをネイティブにデバッグするための、デバッグ ツールが用意されています。 通常は **F12** キーを押すことでブラウザのデバッグを有効にでき、デバッグに使用されるネイティブ開発者ツールを表示します。

たとえば、**Microsoft Edge** です。

- **F12** を押下してインスペクターを開きます。
- コンポーネントをクリックします
- 上部のバーで **デバッガー** に移動し、検索バーでマニフェスト ファイルに記述されているコンポーネント名の検索を開始します。 たとえば、コンポーネント名を `Hello World component` のように入力します。

     > [!div class="mx-imgBorder"]
     > ![デバッグ コンポーネント](media/debug-control.png "デバッグ コンポーネント")

> [!NOTE]
> `init` と `updateView` のようなコンポーネントのライフ サイクル メソッドにブレークポイントを設定することを推奨します。

以下のようにソース タブにブレークポイントを設定することで、ローカルでリアルタイムにコンポーネントを操作したり、DOM の要素を確認することもできます

> [!div class="mx-imgBorder"]
> ![デバッグ コンポーネント](media/debug-control-1.png "デバッグ コンポーネント 1")

## <a name="fiddler-autoresponder"></a>Fiddler AutoResponder

Fiddler AutoResponder を使用することで、迅速にカスタムコンポーネントのデバッグをおこないます。 [Fiddler](https://www.telerik.com/download/fiddler) をインストールして [AutoResponder](https://docs.microsoft.com/dynamics365/customer-engagement/developer/streamline-javascript-development-fiddler-autoresponder) を構成するには以下の手順に従います。

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークの API リファレンス](reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](overview.md)

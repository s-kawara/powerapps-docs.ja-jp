---
title: カスタム コンポーネントのデバッグ | MicrosoftDocs
description: Fiddler とネイティブ デバッグを使用してカスタム コントロールをデバッグする方法
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.topic: article
ms.assetid: 18e88d702-3349-4022-a7d8-a9adf52cd34f
ms.author: nabuthuk
---
# <a name="debug-custom-components"></a>カスタムコンポーネントのデバッグ

カスタム コントロール ロジックの実装が完了したら、次のコマンドを実行してデバッグ処理を開始します `npm start`

> [!NOTE]
> 現在のところ、フィールド コントロールを表示することしかできませんが、近い将来にデータセットに対応を行う予定です。

> [!div class="mx-imgBorder"]
> ![ローカルホスト](media/local-host.png "ローカルホスト")

上の画像で示すように、ブラウズ ウィンドウは 3 つのセクションで開きます。 右側のウィンドウは **入力** と **出力** セクションで構成されており、独自のコントロールは左側のウィンドウに表示されます

  - **入力** セクションは、manifest.xml で定義されたすべてのプロパティと、その種類 / 種類グループを表示する対話型の UI です。 それは各プロパティの模擬データを入力することを可能にします。 
  - **出力** セクションはコントロールの `getOutputs` メソッドが呼ばれるたびに出力を表示します。  
 
> [!NOTE]
> `manifest.xml` を修正するか追加のプロパティを作成する場合は、それらが入力セクションに表示される前にデバッグ プロセスを再起動する必要があります。

模擬データを入力している間、ブラウザのデバッグ機能を使用してコントロールの動作を確認できます。 各ブラウザには、ブラウザでコードをネイティブにデバッグするための、デバッグ ツールが用意されています。 通常は **F12** キーを押すことでブラウザのデバッグを有効にでき、デバッグに使用されるネイティブ開発者ツールを表示します。

たとえば、**Microsoft Edge** です。

- **F12** を押してインスペクターを開きます。
- コントロールをクリックします
- 上部のバーで **デバッガー** に移動し、検索バーのマニフェスト ファイルに記述されたコントロール名の検索を開始します。 たとえば、コントロール名を `Hello World Control` のように入力します。

     > [!div class="mx-imgBorder"]
     > ![デバッグ コントロール](media/debug-control.png "デバッグ コントロール")

> [!NOTE]
> `init` と `updateView` のようなコントロールのライフ サイクル メソッドに、ブレークポイントを設定するのは常に良い方法です

次のようにソース タブにブレークポイントを設定することで、ローカルでリアルタイムにコントロールを操作したり、DOM の要素を確認することもできます

> [!div class="mx-imgBorder"]
> ![ローカルホスト](media/local-host.png "ローカルホスト")

> [!div class="mx-imgBorder"]
> ![デバッグ コントロール](media/debug-control-1.png "デバッグ コントロール 1")

## <a name="fiddler-autoresponder"></a>Fiddler AutoResponder

カスタム コンポーネントを素早くデバッグするには、Fiddler AutoResponder を使用します。 [Fiddler](https://www.telerik.com/download/fiddler) をインストールして [AutoResponder](https://docs.microsoft.com/dynamics365/customer-engagement/developer/streamline-javascript-development-fiddler-autoresponder) を構成するには以下の手順に従います。

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークの API リファレンス](reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](overview.md)
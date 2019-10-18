---
title: コードコンポーネントのデバッグ |MicrosoftDocs
description: Fiddler とネイティブデバッグを使用してコードコンポーネントをデバッグする方法
manager: kvivek
ms.date: 10/01/2019
ms.service: powerapps
ms.topic: article
ms.assetid: 18e88d702-3349-4022-a7d8-a9adf52cd34f
ms.author: nabuthuk
author: Nkrb
ms.openlocfilehash: 088792a32f401ddaf7d3a3cd4fd4d5aa9fa472ff
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72346925"
---
# <a name="debug-code-components"></a>コードコンポーネントのデバッグ

コードコンポーネントロジックの実装が完了したら、`npm start` コマンドを使用して、コードコンポーネントのテストとデバッグを開始できます。 これにより、コードコンポーネントがビルドされ、ローカルのテストハーネスで開かれます。

> [!div class="mx-imgBorder"]
> ![テストハーネス 1](media/test-harness-1.png "テストハーネス 1")

上の図に示すように、ブラウザーウィンドウには4つのセクションが表示されます。 コードコンポーネントは左ペインに表示され、右ペインには**コンテキスト入力**、**データ入力**、および**出力**セクションがあります。

- **コンテキスト入力**は、フォームファクターを指定し、各フォームファクター (web、タブレット、電話) を使用してコードコンポーネントをテストする方法を提供します。 これは、コードコンポーネントが特定のフォームファクターの機能に依存している場合に便利です。
- **データ入力**は、[マニフェスト](manifest-schema-reference/manifest.md)ファイルで定義されているすべてのプロパティとその[型](manifest-schema-reference/types.md)または[型グループ](manifest-schema-reference/type-group.md)を表示する対話型 UI です。 これにより、各プロパティのモックデータ内でキーを使用できるようになります。 
- **出力は**、コンポーネントの[getoutputs](reference/control/getoutputs.md)メソッドが呼び出されるたびに出力をレンダリングします。  

     > [!div class="mx-imgBorder"]
     > ![テストハーネス 2](media/test-harness-2.png "テストハーネス 2")

> [!NOTE]
> @No__t_0 ファイルを変更するか、追加のプロパティを作成する場合は、デバッグプロセスを再起動してから [入力] セクションに表示する必要があります。

## <a name="test-code-components-with-mock-data"></a>モックデータを使用してコードコンポーネントをテストする

- *フィールド*型のコンポーネントの場合は、次に示すように、 **controlmanifest**に定義されているすべてのプロパティに対して、値と型を入力できます。

   > [!div class="mx-imgBorder"]
   > ![テストハーネス 2.5](media/test-harness-2.5.png "テストハーネス 2.5")

- *データセット*の種類のコンポーネントでは、テストデータを含む CSV ファイルを読み込むことができます。 お使いの環境から直接、.csv 形式で手動で作成またはエクスポートします。 有効な CSV ファイルが使用可能になると、次に示すように、そのファイルを読み込むことができます。

   > [!div class="mx-imgBorder"]
   > ![テストハーネス 3](media/test-harness-3.png "テストハーネス 3")

- CSV ファイルを読み込んだ後、 **Controlmanifest. .xml**に定義されている各プロパティを csv ファイルの列にバインドします。 これを行うには、次に示すように、各プロパティの列を選択します。

    > [!div class="mx-imgBorder"]
    > ![テストハーネス 4](media/test-harness-4.png "テストハーネス 4")

- **Controlmanifest .xml**ファイルにプロパティが定義されていない場合は、すべての列が自動的にテストハーネスに読み込まれます。

   > [!div class="mx-imgBorder"]
   > ![テストハーネス 5](media/test-harness-5.png "テストハーネス 5")


## <a name="watch-mode-in-test-harness"></a>テストハーネスのウォッチモード

テストハーネスは `watch` モードをサポートしており、PowerApps component framework プロジェクトで利用できます。 @No__t_0 モードを有効にするには、コマンド `npm start watch` を使用してテストハーネスを起動します。 @No__t_0 モードでは、次のコンポーネントアセットに加えられた変更は、再起動しなくても、テストハーネスに自動的に反映されます。

1.  `index.ts` ファイル。
2.  `ControlManifest.Input.xml` ファイル。
3.  @No__t_0 にインポートされたライブラリ。
4.  マニフェストファイルに一覧表示されているすべてのリソース。

## <a name="debug-code-components-using-native-browsers"></a>ネイティブブラウザーを使用してコードコンポーネントをデバッグする

ブラウザーのデバッグ機能を使用して、コンポーネントの動作を確認できます。 各ブラウザーには、ブラウザーでネイティブにコードをデバッグするのに役立つデバッグツールが用意されています。 通常、デバッグに使用するネイティブ開発者ツールを表示するには、 **F12**キーを押して、ブラウザーでデバッグをアクティブ化します。

たとえば、 **Microsoft Edge**の場合は、次のようになります。

- **F12**キーを押して、インスペクターを開きます。
- コンポーネントを選択します。
- 上部のバーで **[デバッガー]** にアクセスし、検索バーのマニフェストファイルで説明されているコンポーネント名を検索します。 たとえば、`Hello World component` のようなコンポーネント名を入力します。

     > [!div class="mx-imgBorder"]
     > ![デバッグ]コンポーネント(media/debug-control.png "デバッグコンポーネント")

> [!NOTE]
> [Init](reference/control/init.md)や[updateview](reference/control/updateview.md)などのコンポーネントのライフサイクルメソッドにブレークポイントを設定することを常にお勧めします。

また、次に示すように、[*ソース*] タブでブレークポイントを設定することにより、コンポーネントとローカルでリアルタイムで対話し、DOM 内の要素を観察することもできます。

> [!div class="mx-imgBorder"]
> ![デバッグ]コンポーネント(media/debug-control-1.png "デバッグコンポーネント 1")

## <a name="fiddler-autoresponder"></a>Fiddler AutoResponder

Fiddler AutoResponder を使用して、コードコンポーネントをすばやくデバッグします。 [Fiddler](https://www.telerik.com/download/fiddler)をインストールし、手順に従って[AutoResponder](https://docs.microsoft.com/dynamics365/customer-engagement/developer/streamline-javascript-development-fiddler-autoresponder)を構成します。

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネントフレームワーク API リファレンス](reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](overview.md)

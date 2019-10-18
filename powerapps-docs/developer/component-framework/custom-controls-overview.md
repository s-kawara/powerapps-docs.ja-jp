---
title: コードコンポーネントとは |MicrosoftDocs
description: PowerApps コンポーネントフレームワークを使用すると、ユーザーがフォーム、ビュー、およびダッシュボードのデータを表示および操作するための拡張ユーザーエクスペリエンスを提供するコードコンポーネントを作成できます。
manager: kvivek
ms.date: 09/05/2019
ms.service: powerapps
ms.topic: article
ms.assetid: 135481cd-4583-4e49-8f58-02f32a9b054a
ms.author: nabuthuk
author: Nkrb
ms.openlocfilehash: 08a2043dfb92634837c367e664306d9c100632d6
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72346971"
---
# <a name="what-are-code-components"></a>コードコンポーネントとは

コードコンポーネントはソリューションコンポーネントの一種であり、ソリューションファイルに含めて、別の環境にインストールすることができます。 詳細につい[ては、「ソリューションを使用して拡張機能をパッケージ化して配布する](https://docs.microsoft.com/dynamics365/customer-engagement/developer/package-distribute-extensions-use-solutions)

コードコンポーネントは、ソリューションに追加してから Common Data Service にインポートすることによって追加します。 コンポーネントが Common Data Service になると、システム管理者およびシステムカスタマイザーは、既定のコンポーネントの代わりに使用するフィールド、サブグリッド、ビュー、およびダッシュボードサブグリッドを構成できます。 これらのコードコンポーネントは、キャンバスアプリで追加することもできます。 

コードコンポーネントは、次の3つの要素で構成されます。

1. [マニフェスト](#manifest)
2. [コンポーネント実装ライブラリ](#component-implementation-library)
3. [リソース](#resources)

## <a name="manifest"></a>マニフェスト

マニフェストは、コンポーネントを定義するメタデータ ファイルです。 これは次のような XML ドキュメントです。

- コンポーネントの名前。
- 構成できるデータの種類 (フィールドまたはデータセット)。
- コンポーネントを追加するときにアプリケーションで構成できるすべてのプロパティ。
- コンポーネントが必要とするリソースファイルの一覧。 
- 必須コンポーネントインターフェイスを適用するオブジェクトを返す、コンポーネント実装ライブラリ内の TypeScript 関数の名前。

ユーザーがコードコンポーネントを構成すると、マニフェストファイル内のデータによって、使用可能なコンポーネントが除外され、コンテキストの有効なコンポーネントのみが構成に使用できるようになります。 コンポーネントのマニフェストファイルで定義されているプロパティは、構成フィールドとして表示されます。これにより、コンポーネントを構成するユーザーが値を指定できるようになります。 これらのプロパティ値は、実行時にコンポーネントで使用できます。 詳細情報:[マニフェストスキーマリファレンス](manifest-schema-reference/index.md)

## <a name="component-implementation-library"></a>コンポーネント実装ライブラリ

コンポーネントライブラリの実装は、PowerApps コンポーネントフレームワークを使用してコードコンポーネントを開発する場合の主要な手順の1つです。 開発者は、TypeScript を使用してコンポーネントライブラリを実装できます。 各コードコンポーネントには、関数の定義を含むライブラリが必要です。このライブラリは、コードコンポーネントインターフェイスに記述されているメソッドを実装するオブジェクトを返します。 

オブジェクトは、次のメソッドを実装します。

- [init](reference/control/init.md) (必須)
- [Updateview](reference/control/updateview.md) (必須)
- [Getoutputs](reference/control/getoutputs.md) (省略可能)
- [破棄](reference/control/destroy.md)(必須)

これらのメソッドは、コードコンポーネントのライフサイクルを制御します。

### <a name="page-load"></a>ページの読み込み

ページが読み込まれると、アプリケーションはオブジェクトを処理する必要があります。 マニフェストファイルのデータを使用して、コードはを呼び出してオブジェクトを取得します。

```js
var obj =  new <"namespace on manifest">.<"constructor on manifest">();
```

マニフェストの名前空間とコンストラクターの値がそれぞれ `SampleNameSpace`、`LinearInputComponent` 場合、オブジェクトをインスタンス化するコードは次のようになります。

```js
var controlObj = new SampleNameSpace.LinearInputComponent();
```

ページの準備が整うと、パラメーターのセットを使用して[init](reference/control/init.md)メソッドを呼び出すことによってコンポーネントが初期化されます。

```js
controlObj.init(context,notifyOutputChanged,state,container);
```

|パラメーター|Description|
|---|---|
|関連| コンポーネントがどのように構成されているか、および[PowerApps component Framework api](reference/index.md)と共にコンポーネント内で使用できるすべてのパラメーターについての情報が含まれています。 たとえば、`context.parameters.<"property name from manifest">` は、入力プロパティにアクセスするために使用できます。|
|notifyOutputChanged |コードコンポーネントの新しい出力を非同期に取得する準備ができたときに、フレームワークに通知します。|
|状態|コンポーネントが[Setcontrolstate](reference/mode/setcontrolstate.md)メソッドを使用して以前に明示的に格納した場合に、現在のセッションの前のページの読み込みからのコンポーネントデータを格納します。|
|コンテナー|コンポーネントを定義する UI の HTML 要素を開発者とアプリメーカーが追加できる HTML div 要素。|

### <a name="user-changes-data"></a>ユーザーによるデータの変更

ページが読み込まれると、ユーザーがコンポーネントと対話してデータを変更するまで、コンポーネントにデータが表示されます。 このエラーが発生した場合は、 [init](reference/control/init.md)メソッドで*notifyOutputChanged*パラメーターとして渡されたメソッドを呼び出す必要があります。 このメソッドを使用すると、プラットフォームは[Getoutputs](reference/control/getoutputs.md)メソッドを呼び出すことによって応答します。 [Getoutputs](reference/control/getoutputs.md)メソッドは、ユーザーによって行われた変更を含む値を返します。 フィールドコンポーネントの場合は、通常、コンポーネントの新しい値になります。

### <a name="app-changes-data"></a>アプリの変更データ

プラットフォームによってデータが変更されると、コンポーネントの[Updateview](reference/control/updateview.md)メソッドが呼び出され、新しいコンテキストオブジェクトがパラメーターとして渡されます。 コンポーネントに表示される値を更新するには、このメソッドを実装する必要があります。

### <a name="page-close"></a>ページを閉じる

ユーザーがページから移動するたびに、コードコンポーネントによってスコープが失われ、そのページでオブジェクトに割り当てられたすべてのメモリがクリアされます。 ただし、ブラウザー実装機構に基づく一部のメソッドは、メモリを維持して使用する場合があります。 通常、これらはイベントハンドラーです。 ユーザーがこの情報を格納する場合は、同じセッション内で情報が次に指定されるように[Setcontrolstate](reference/mode/setcontrolstate.md)メソッドを実装する必要があります。

開発者は、ページを閉じるときに呼び出される[destroy](reference/control/destroy.md)メソッドを実装して、イベントハンドラーなどのクリーンアップコードを削除する必要があります。

## <a name="resources"></a>リソース

各コードコンポーネントには、その視覚化を構築するためのリソースファイルが必要です。 マニフェストには、リソースファイルを定義できます。 マニフェストファイルのリソースノードは、コンポーネントが視覚化を実装するために必要なリソースを参照します。 詳細情報: [resources 要素](manifest-schema-reference/resources.md)

### <a name="related-topics"></a>関連トピック

[コードコンポーネントの作成とビルド](create-custom-controls-using-pcf.md)

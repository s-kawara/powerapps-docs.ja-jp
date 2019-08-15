---
title: カスタム コンポーネントとは | MicrosoftDocs
description: PowerApps コンポーネント フレームワークを使用してカスタム コンポーネントを作成し、フォーム、ビュー、ダッシュボードでデータを表示して作業する高度なユーザー エクスペリエンスを提供します。
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.topic: article
ms.assetid: 135481cd-4583-4e49-8f58-02f32a9b054a
ms.author: nabuthuk
---

# <a name="what-are-custom-components"></a>カスタム コンポーネントとは

[!INCLUDE[cc-beta-prerelease-disclaimer](../../includes/cc-beta-prerelease-disclaimer.md)]

カスタム コンポーネントはソリューション コンポーネントの一種です。つまり、カスタム コンポーネントをソリューションに含めて異なる環境にインストールできます。 詳細: [ソリューションを使用した拡張機能のパッケージ化および配布](https://docs.microsoft.com/dynamics365/customer-engagement/developer/package-distribute-extensions-use-solutions).

カスタム コンポーネントをソリューションに含めて追加し、そしてシステムにインポートします。 システムに組み込まれたら、管理者およびシステム カスタマイザーは既定のコンポーネントの代わりにそれらを使用するよう、フォーム フィールド、サブグリッド、ビュー、ダッシュボード サブグリッドを構成できます。

カスタム コンポーネントは 3 つのコンポーネントに含まれます:

1. マニフェスト
2. コンポーネント実装ライブラリ
3. リソース

## <a name="manifest"></a>マニフェスト

マニフェストはコンポーネントを定義するメタデータ ファイルです。 それは次を記述する XML 文書です:

- コンポーネントの名前空間と名前。
- 構成が可能なデータの種類、フィールドまたはデータセット。
- コンポーネントが追加されたときにアプリケーションで構成できる任意のプロパティ。
- コンポーネントが必要とするリソース ファイルの一覧。 
- 必要なコンポーネント インタフェースを適用するオブジェクトを返す、コンポーネント実装ライブラリの TypeScript 関数名。

誰かがアプリケーションのコンポーネントを設定したときに、マニフェストのデータは利用可能なコンポーネントを除外して、コンテキストに有効なコンポーネントのみ構成に使用できるようにします。 コンポーネントのマニフェストで定義されたプロパティは、コンポーネントの設定時に値を指定できるよう構成フィールドとして表示されます。 これらのプロパティ値は、実行時にコンポーネント関数で利用可能になります。 詳細: [マニフェスト ファイルの参照](manifest-schema-reference/index.md)

## <a name="component-implementation-library"></a>コンポーネント実装ライブラリ

[!INCLUDE [component-implementation-library](control-implementation-library.md)]

### <a name="page-load"></a>ページの読み込み

ページを読み込む時にアプリケーションは作業するオブジェクトを必要とします。 マニフェストからのデータを使用して、コードは呼び出しによってオブジェクトを取得します

```js
var obj =  new ["namespace on manifest"].["constructor on manifest"]();
```

マニフェストの名前空間とコンストラクタの値がそれぞれ `MyNameSpace` と `LinearInputControl` だった場合、オブジェクトをインスタンス化するコードはこれになります:

```js
var controlObj = new MyNameSpace.LinearInputControl();
```

ページの準備ができたら、一連のパラメーターとともに [init](reference/control/init.md) 関数を呼び出してコンポーネントを初期化します。

```js
controlObj.init(context,notifyOutputChanged,state,container);
```

|パラメーター|説明|
|---|---|
|コンテキスト| コンポーネントの構成方法に関するすべての情報と、コンポーネントとともに [フレームワーク API](reference/index.md) で使用できるすべてのパラメータを含みます。 たとえば、`context.parameters.["property name from manifest"]` を入力プロパティへのアクセスに使用できます。|
|notifyOutputChanged |コンポーネントが非同期に取得できる新しい出力があることをフレームワークに警告する機能。|
|状態|制御が `setControlState API` を使用して以前に明示的に保存した場合は、現在のセッションの前のページ読み込みのコンポーネント データが含まれます。|
|コンテナ|コンポーネントを定義する UI の HTML 要素を追加する HTML div 要素。 UI に値を表示するには `context.parameters.controlValue object` からデータを取得する必要があります。|

### <a name="user-changes-data"></a>ユーザーがデータを変更する

ページが読み込まれると、ユーザーがデータを変更するためにコンポーネントを操作するまで、コンポーネントはデータを表示します。 これが起こるとき、それを好きなように管理できますが、[init](reference/control/init.md) 関数で **notifyOutputChanged** パラメータとして渡される関数を呼び出す必要があります。 この関数を使うとき、プラットフォームは実装が必須の [getOutputs](reference/control/getoutputs.md) メソッドを呼び出すことで応答します。 [getOutputs](reference/control/getoutputs.md) メソッドはユーザーが行った変更を表す値を返します。 フィールド コンポーネントの場合、通常これはコンポーネントの新しい値になります。

### <a name="app-changes-data"></a>アプリがデータを変更する

プラットフォームによってデータが変更された場合は、コンポーネント オブジェクトの [updateView](reference/control/updateview.md) メソッドを呼び出し、新しいコンテキスト オブジェクトをパラメータとして渡します。 このメソッドを実装し、それを使用してコンポーネントに表示される値を更新する必要があります。

### <a name="page-close"></a>ページを閉じる

ユーザーがページから離れると、コンポーネントはスコープを失い、通常そのページに割り当てられたコンポーネント内のオブジェクトのメモリはすべて消去されます。 ただし、ブラウザの実装メカニズムに基づくいくつかの項目は、消えずにメモリを消費し続ける可能性があります。 通常、これらはイベント ハンドラーです。 ユーザーが情報を保存する必要がある場合は、同じセッション内で次回に情報が渡されるように `setControlState` メソッドを実装する必要があります。
オブジェクトに [destroy](reference/control/destroy.md) メソッドを定義する必要があります。 これはページが閉じるときに呼び出され、イベント ハンドラーの削除などコードを削除してクリーンアップするために使用する必要があります。

## <a name="resources"></a>リソース

各カスタム コンポーネントは視覚化を構築するためのリソース ファイルが必要です。 マニフェストでリソース ファイルを定義できます。 マニフェスト ファイルのリソース ノードは、コンポーネントが視覚化を実装するのに必要なリソースを参照します。 詳細: [リソース](manifest-schema-reference/resources.md)

### <a name="related-topics"></a>関連トピック

[カスタム コンポーネントの作成](create-custom-controls-using-pcf.md)

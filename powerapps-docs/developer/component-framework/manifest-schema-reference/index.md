---
title: PowerApps コンポーネント フレームワークのマニフェスト スキーマ リファレンス | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
manager: null
ms.date: 06/4/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 045a395b-4475-48dd-8f67-6bc2b33cd89c
---

# <a name="manifest-schema-reference"></a>マニフェスト スキーマ リファレンス

[!INCLUDE[cc-beta-prerelease-disclaimer](../../../includes/cc-beta-prerelease-disclaimer.md)]

このセクションは PowerApps CLI を使用して生成されたマニフェスト スキーマの参照ドキュメントを含みます。

|Element|説明|
|----|-----------|
|[コード](code.md)|[!INCLUDE [code-description](includes/code-description.md)]|
|[コントロール](control.md)|[!INCLUDE [control-description](includes/control-description.md)]|
|[css](css.md)|[!INCLUDE [css-description](includes/css-description.md)]|
|[データセット](data-set.md)|[!INCLUDE [data-set-description](includes/data-set-description.md)]|
|[HTML](html.md)|[!INCLUDE [html-description](includes/html-description.md)]|
|[img](img.md)|[!INCLUDE [img-description](includes/img-description.md)]|
|[マニフェスト](manifest.md)|マニフェストはコンポーネントを定義するメタデータ ファイルです。 説明する XML ドキュメントです<br/> - コンポーネントの名前空間です。<br/> - 構成が可能なデータの種類、フィールドまたはデータセット。<br/> - コンポーネントが追加されたときにアプリケーションで構成できる任意のプロパティ。<br/> - コンポーネントが必要とするリソース ファイルの一覧。<br/> - そのうちひとつは JavaScript Web リソースでなければいけません。 この JavaScript はオブジェクトをインスタンス化する関数を含む必要があります。 これはコンポーネントが動作するのに必要なメソッドを公開するインターフェースを実装します。 これはコンポーネント実装ライブラリと呼ばれます。<br/> - 必要なインタフェースを適用するオブジェクトを返す、コンポーネント実装ライブラリの JavaScript 関数名。<br/> 誰かがアプリケーションのコンポーネントを設定したときに、マニフェストのデータは利用可能なコンポーネントを除外して、コンテキストに有効なコンポーネントのみ構成に使用できるようにします。 コンポーネントのマニフェストで定義されたプロパティは、コントロールの設定時に値を指定できるよう構成フィールドとして表示されます。 これらのプロパティ値は、実行時にコンポーネント関数で利用可能になります。|
|[プロパティ](property.md)|[!INCLUDE [property-description](includes/property-description.md)]|
|[プロパティ セット](property-set.md)|[!INCLUDE [property-set-description](includes/property-set-description.md)]|
|[リソース](resources.md)|[!INCLUDE [resources-description](includes/resources-description.md)]|
|[resx](resx.md)|[!INCLUDE [resx-description](includes/resx-description.md)]|
|[種類のグループ](type-group.md)|[!INCLUDE [type-group-description](includes/type-group-description.md)]|


### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークのマニフェスト スキーマ リファレンス](index.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../overview.md)
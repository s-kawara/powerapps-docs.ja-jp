---
title: PowerApps コンポーネントフレームワークマニフェストスキーマリファレンス |Microsoft Docs
description: ''
keywords: ''
ms.author: nabuthuk
author: Nkrb
manager: kvivek
ms.date: 06/4/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 045a395b-4475-48dd-8f67-6bc2b33cd89c
ms.openlocfilehash: 8f58f10f6a3695615ddc3b58b540c59240af9641
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72346373"
---
# <a name="manifest-schema-reference"></a>マニフェスト スキーマ リファレンス

このセクションには、PowerApps CLI で生成されるマニフェスト スキーマの参照文書が含まれています。

> [!IMPORTANT]
> **[使用可能]** タブには、モデル駆動型アプリとキャンバスアプリでサポートされている要素が表示されます (試験段階プレビュー)。 サポートされているかどうかにかかわらず、各プロパティの **[使用可能]** セクションを確認することをお勧めします。 たとえば、**コード**要素は、モデル駆動型アプリとキャンバスアプリの両方でサポートされていますが、**コード**要素内の**html**および**img**プロパティはキャンバスアプリをサポートしていません。 

|要素|Description|利用可能な対象|
|----|-----------|-----|
|[コード](code.md)|[!INCLUDE [code-description](includes/code-description.md)]|モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー)|
|[コントロール](control.md)|[!INCLUDE [control-description](includes/control-description.md)]|モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー)|
|[css](css.md)|[!INCLUDE [css-description](includes/css-description.md)]|モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー)|
|[data-set](data-set.md)|[!INCLUDE [data-set-description](includes/data-set-description.md)]|モデル駆動型アプリ|
|[html](html.md)|[!INCLUDE [html-description](includes/html-description.md)]|モデル駆動型アプリ|
|[img](img.md)|[!INCLUDE [img-description](includes/img-description.md)]|モデル駆動型アプリ|
|[マニフェスト](manifest.md)|マニフェストは、コンポーネントを定義するメタデータ ファイルです。 次を表現する XML ドキュメントです。<br/> - コンポーネントの名前空間。<br/> - 構成できるデータの種類。フィールドかデータセット。<br/> - コンポーネントの追加時、アプリケーションで構成できるプロパティ。<br/> - コンポーネントに必要なリソース ファイルの一覧。<br/> - そのうちの 1 つは JavaScript Web リソースにする必要があります。 この JavaScript には、オブジェクトをインスタンス化する関数を含める必要があります。 それにより、コンポーネントが動作するために必要なメソッドを公開するインターフェイスが実装されます。 これはコンポーネント実装ライブラリと呼ばれています。<br/> - 必須のインターフェイスを適用するオブジェクトを返すコンポーネント実装ライブラリにある JavaScript 関数の名前。<br/> 誰かがアプリケーションでコンポーネントを構成するとき、そのコンテキストで有効なコンポーネントのみが公正に利用できるよう、マニフェストのデータによって利用可能なコンポーネントが除外されます。 コンポーネントのマニフェストに定義されているプロパティは、コントロールを構成している人が値を指定できるよう、構成フィールドとしてレンダリングされます。 このプロパティ値はその後、実行時にコンポーネント関数で利用できます。|モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー)|
|[プロパティ](property.md)|[!INCLUDE [property-description](includes/property-description.md)]|モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー)|
|[property-set](property-set.md)|[!INCLUDE [property-set-description](includes/property-set-description.md)]|モデル駆動型アプリ|
|[リソース](resources.md)|[!INCLUDE [resources-description](includes/resources-description.md)]|モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー)|
|[resx](resx.md)|[!INCLUDE [resx-description](includes/resx-description.md)]|モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー)|
|[type-group](type-group.md)|[!INCLUDE [type-group-description](includes/type-group-description.md)]|モデル駆動型アプリとキャンバスアプリ (試験段階プレビュー)|
|[機能-使用法](feature-usage.md)|機能使用量要素は `uses-feature` 要素のラッパーとして機能します。これにより、開発者は、コンポーネントが使用する機能を宣言できます。 使用する機能の要素が定義されていない場合、機能の使用に関する要素は必要ありません。|モデル駆動型アプリ|

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネントフレームワークマニフェストスキーマリファレンス](index.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../overview.md)
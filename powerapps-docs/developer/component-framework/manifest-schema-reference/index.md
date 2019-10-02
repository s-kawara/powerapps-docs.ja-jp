---
title: PowerApps コンポーネント フレームワークのマニフェスト スキーマ リファレンス | Microsoft Docs
description: ''
keywords: ''
ms.author: nabuthuk
manager: ''
ms.date: 06/4/2018
ms.reviewer: ''
ms.service: crm-online
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 045a395b-4475-48dd-8f67-6bc2b33cd89c
ms.openlocfilehash: 88e9d35792d86e279b9af4a19eaff288643412ca
ms.sourcegitcommit: c52c1869510a9a37d9f7b127e06f07583529588b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2019
ms.locfileid: "64524321"
---
# <a name="manifest-schema-reference"></a>マニフェスト スキーマ リファレンス

[!INCLUDE[cc-beta-prerelease-disclaimer](../../../includes/cc-beta-prerelease-disclaimer.md)]

このセクションには、PowerApps CLI で生成されるマニフェスト スキーマの参照文書が含まれています。

|要素|説明|
|----|-----------|
|[コード](code.md)|[!INCLUDE [code-description](includes/code-description.md)]|
|[コントロール](control.md)|[!INCLUDE [control-description](includes/control-description.md)]|
|[css](css.md)|[!INCLUDE [css-description](includes/css-description.md)]|
|[data-set](data-set.md)|[!INCLUDE [data-set-description](includes/data-set-description.md)]|
|[html](html.md)|[!INCLUDE [html-description](includes/html-description.md)]|
|[img](img.md)|[!INCLUDE [img-description](includes/img-description.md)]|
|[マニフェスト](manifest.md)|マニフェストは、コンポーネントを定義するメタデータ ファイルです。 次を表現する XML ドキュメントです。<br/> - コンポーネントの名前空間。<br/> - 構成できるデータの種類。フィールドかデータセット。<br/> - コンポーネントの追加時、アプリケーションで構成できるプロパティ。<br/> - コンポーネントに必要なリソース ファイルの一覧。<br/> - そのうちの 1 つは JavaScript Web リソースにする必要があります。 この JavaScript には、オブジェクトをインスタンス化する関数を含める必要があります。 それにより、コンポーネントが動作するために必要なメソッドを公開するインターフェイスが実装されます。 これはコンポーネント実装ライブラリと呼ばれています。<br/> - 必須のインターフェイスを適用するオブジェクトを返すコンポーネント実装ライブラリにある JavaScript 関数の名前。<br/> 誰かがアプリケーションでコンポーネントを構成するとき、そのコンテキストで有効なコンポーネントのみが公正に利用できるよう、マニフェストのデータによって利用可能なコンポーネントが除外されます。 コンポーネントのマニフェストに定義されているプロパティは、コントロールを構成している人が値を指定できるよう、構成フィールドとしてレンダリングされます。 このプロパティ値はその後、実行時にコンポーネント関数で利用できます。|
|[プロパティ](property.md)|[!INCLUDE [property-description](includes/property-description.md)]|
|[property-set](property-set.md)|[!INCLUDE [property-set-description](includes/property-set-description.md)]|
|[リソース](resources.md)|[!INCLUDE [resources-description](includes/resources-description.md)]|
|[resx](resx.md)|[!INCLUDE [resx-description](includes/resx-description.md)]|
|[type-group](type-group.md)|[!INCLUDE [type-group-description](includes/type-group-description.md)]|


### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークのマニフェスト スキーマ リファレンス](index.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../overview.md)
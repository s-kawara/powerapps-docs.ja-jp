---
title: DataSet | Microsoft Docs
description: ''
keywords: ''
ms.author: nabuthuk
author: Nkrb
manager: kvivek
ms.date: 10/01/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0202d51f-e9a9-4a2e-b3e9-0bfd7f6afb86
ms.openlocfilehash: 5e9408c81fc9587b9dec30f18fc68c3112ba6125
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72345315"
---
# <a name="dataset"></a>DataSet

[!INCLUDE [dataset-description](includes/dataset-description.md)]

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリ

## <a name="properties"></a>プロパティ

### <a name="addcolumn"></a>addColumn ()

Columnset に列を追加します。

### <a name="remarks"></a>」

このメソッドは、2つのパラメーターを受け取ります。

|名前|種類|必須|Description|
|------|-----|------|-----|
|指定|`string`|はい|データセットに追加する列の名前。|
|entityAlias|`string`|いいえ| 列名を追加する必要があるエンティティの別名。|

### <a name="columns"></a>欄

このデータセットで使用可能な列のセット。

**型**: [Column](column.md)[]

### <a name="error"></a>エラー

データの取得中にエラーが発生したかどうか。

**種類**: `boolean`

### <a name="errormessage"></a>errorMessage

該当する場合は、最後に検出されたエラーに関連付けられたエラーメッセージ。

**種類**: `string`

### <a name="filtering"></a>除外

現在のクエリの列フィルター処理。

**種類**:[フィルター処理](filtering.md)

### <a name="linking"></a>結び付ける

リンクされたエンティティ情報を定義します。

**種類**:[リンク](linking.md)

### <a name="loading"></a>読み込み

データセットが読み込み中かどうかを示します。

**種類**: `boolean`

### <a name="paging"></a>ベル

改ページ位置の自動修正の状態とアクション。

**種類**:[ページング](paging.md)

### <a name="records"></a>レコード

完全なレコードオブジェクトへの Id のマップ。

**型**: [entityrecord](entityrecord.md)

### <a name="sortedrecordids"></a>sortedRecordIds

データセット内のレコードの Id。クエリ応答の結果によって並べ替えられます。

**種類**: `string[]`

### <a name="sorting"></a>'83'5c

現在のクエリの並べ替え状態。

**種類**: [sortstatus](sortstatus.md)

## <a name="methods"></a>メソッド

|B | Description | 
| ------------- |-------------|
|[clearSelectedRecordIds](dataset/clearselectedrecordids.md)|[!INCLUDE [clearselectedrecordids-description](dataset/includes/clearselectedrecordids-description.md)]| 
|[getSelectedRecordIds](dataset/getselectedrecordids.md)|[!INCLUDE [getselectedrecordids-description](dataset/includes/getselectedrecordids-description.md)]| 
|[getTargetEntityType](dataset/gettargetentitytype.md)|[!INCLUDE [gettargetentitytype-description](dataset/includes/gettargetentitytype-description.md)]| 
|[getTitle](dataset/gettitle.md)|[!INCLUDE [gettitle-description](dataset/includes/gettitle-description.md)]| 
|[getViewId](dataset/getviewid.md)|[!INCLUDE [getviewid-description](dataset/includes/getviewid-description.md)]| 
|[openDatasetItem](dataset/opendatasetitem.md)|[!INCLUDE [opendatasetitem-description](dataset/includes/opendatasetitem-description.md)]| 
|[更新](dataset/refresh.md)|[!INCLUDE [refresh-description](dataset/includes/refresh-description.md)]| 
|[setSelectedRecordIds](dataset/setselectedrecordids.md)|[!INCLUDE [setselectedrecordids-description](dataset/includes/setselectedrecordids-description.md)]| 

## <a name="example"></a>例

データセットメソッドの実装方法の詳細については、「[データセットグリッドコンポーネント](../sample-controls/data-set-grid-control.md)」を参照してください。

### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネントフレームワーク API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../overview.md)
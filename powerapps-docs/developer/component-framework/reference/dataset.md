---
title: データセット | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
author: Nkrb
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 0202d51f-e9a9-4a2e-b3e9-0bfd7f6afb86
---

# <a name="dataset"></a>データセット

[!INCLUDE[cc-beta-prerelease-disclaimer](../../../includes/cc-beta-prerelease-disclaimer.md)]

[!INCLUDE [dataset-description](includes/dataset-description.md)]

## <a name="properties"></a>プロパティ

## <a name="addcolumn"></a>addColumn

データセットに列を追加する機能

**種類**: `function`<br />
**任意出席者**

### <a name="remarks"></a>備考

この関数はふたつのパラメータを受け取る必要があります。

|Name|型|必須出席者|説明|
|-|-|-|-|
|名前|文字列|あり|データセットに追加される列の名前|
|entityalias|文字列|なし| 列名を追加する必要があるエイリアス|

## <a name="columns"></a>列

このデータセットで利用可能な一連の列。

**種類**: [列](column.md)[]

## <a name="error"></a>error

データ取得中にエラーが発生したか。

**種類**: `boolean`

## <a name="errormessage"></a>errorMessage

最後に発生したエラーに関連付けられてたエラー メッセージ。

**種類**: `string`

## <a name="filtering"></a>フィルター処理

プレースホルダーの説明: IDataSetExposedParameter.name
<!-- 
QUESTION: This description doesn't seem right
'The column sorting for the current query.' 
-->

**種類**: [フィルター処理](filtering.md)

## <a name="linking"></a>リンク

プレースホルダーの説明: IDataSetExposedParameter.name

**種類**: [リンク](linking.md)

## <a name="loading"></a>読み込み中

データセットが読み込まれているか。

**種類**: `boolean`

## <a name="paging"></a>ページング

改ページの状態とアクション。

**種類**: [ページング](paging.md)

## <a name="records"></a>レコード

完全なレコード オブジェクトへの ID のマップ。

**種類**: `object`

## <a name="sortedrecordids"></a>sortedRecordIds

順番に並んだデータセット内のレコードの ID。

**種類**: `string[]`

## <a name="sorting"></a>並べ替え

現在のクエリの列の並べ替え。

**種類**: [並べ替え](sortstatus.md)

## <a name="methods"></a>メソッド

|方法 | 説明 | 
| ------------- |-------------|
|[clearSelectedRecordIds](dataset/clearselectedrecordids.md)|[!INCLUDE [clearselectedrecordids-description](dataset/includes/clearselectedrecordids-description.md)]| 
|[getSelectedRecordIds](dataset/getselectedrecordids.md)|[!INCLUDE [getselectedrecordids-description](dataset/includes/getselectedrecordids-description.md)]| 
|[getTargetEntityType](dataset/gettargetentitytype.md)|[!INCLUDE [gettargetentitytype-description](dataset/includes/gettargetentitytype-description.md)]| 
|[getTitle](dataset/gettitle.md)|[!INCLUDE [gettitle-description](dataset/includes/gettitle-description.md)]| 
|[getViewId](dataset/getviewid.md)|[!INCLUDE [getviewid-description](dataset/includes/getviewid-description.md)]| 
|[openDatasetItem](dataset/opendatasetitem.md)|[!INCLUDE [opendatasetitem-description](dataset/includes/opendatasetitem-description.md)]| 
|[最新の情報に更新](dataset/refresh.md)|[!INCLUDE [refresh-description](dataset/includes/refresh-description.md)]| 
|[setSelectedRecordIds](dataset/setselectedrecordids.md)|[!INCLUDE [setselectedrecordids-description](dataset/includes/setselectedrecordids-description.md)]| 


### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークの API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../overview.md)
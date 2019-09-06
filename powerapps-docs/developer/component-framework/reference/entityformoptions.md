---
title: EntityFormOptions | Microsoft Docs
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
ms.assetid: 418871c0-59dc-4a7c-a8f9-9364a19f7662
---
# <a name="entityformoptions"></a>EntityFormOptions

[!INCLUDE[cc-beta-prerelease-disclaimer](../../../includes/cc-beta-prerelease-disclaimer.md)]

## <a name="properties"></a>プロパティ

## <a name="createfromentity-entityreference"></a>createFromEntity: EntityReference

マップした属性値に基づいて既定値を提供するレコードを指定します。 検索オブジェクトには次のプロパティがあります: エンティティの種類、ID、および名前。

## <a name="entity"></a>entity

フォームを表示するエンティティ レコードの一意の ID。 

**種類**: `string`

## <a name="entityname"></a>entityName

フォームを表示するエンティティの論理名。 

**種類**: `string`

## <a name="formid"></a>formId

表示するフォーム インスタンスの ID。

**種類**: `string`

## <a name="height"></a>height

表示するフォーム ウィンドウの高さ (ピクセル単位)。

**種類**: `number`

## <a name="openinnewwindow"></a>openInNewWindow

新しいウィンドウでフォームを表示するかどうか

**種類**: `boolean`

## <a name="usequickcreateform"></a>useQuickCreateForm

簡易作成フォームを開くかどうか。 これを指定しない場合、既定で false が渡されます。 

**種類**: `boolean`

## <a name="width"></a>width

表示するフォーム ウィンドウの幅 (ピクセル単位)。

**種類**: `boolean`

## <a name="windowposition"></a>windowPosition

画面上のウィンドウの場所を指定します。

**種類**: `number`

windowPosition 値は以下の可能な値の数値です

|Value|位置|
|---|---|
|1|中央揃え|
|2|側|


### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークの API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../overview.md)
---
title: openForm | Microsoft Docs
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
ms.assetid: bea56947-d976-4974-9ac7-2d5f5c7b6732
---

# <a name="openform"></a>openForm

[!INCLUDE [openform-description](includes/openform-description.md)]

## <a name="syntax"></a>構文

`openForm(options, parameters)`

## <a name="parameters"></a>パラメーター

| パラメーター名|型|必須出席者|説明|
| ------------- |----|--------|-----------|
|オプション|`EntityFormOptions`|はい|EntityFormOptions は以下の属性を持ちます:<br/>- **createFromEntity**: [EntityReference](../entityreference.md)。 マップした属性値に基づいて既定値を提供するレコードを指定します。 検索オブジェクトには以下の文字列プロパティがあります: entityType、ID、そして名前。 <br/>- **entityId**: `string`。 フォームを表示するエンティティ レコードの ID。<br/>- **entityName**: `string`。 フォームを表示するエンティティの論理名。<br/>- **formId**: `string`。 表示するフォーム インスタンスの ID。<br/>- **高さ**: `number`。 表示するフォーム ウィンドウの高さ (ピクセル単位)。<br/>- **openInNewWindow**: `boolean`。 新しいウィンドウでフォームを表示するか。<br/>- **useQuickCreateForm**: `boolean`。 簡易作成フォームを開くか。 これを指定しない場合、既定で `false` が渡されます。<br/>- **幅**: `number`。 表示するフォーム ウィンドウの幅 (ピクセル単位)。<br/>- **windowPosition**: `number`。 画面でのフォームのウィンドウ位置に対して次のいずれかの値を指定します: `1:center` <br/> `2:side`|
|パラメーター|`key`|はい|エンティティ フォーム パラメーター。|

## <a name="return-value"></a>戻り値

種類: `Promise`

## <a name="remarks"></a>備考

[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise) と [ファイル](https://developer.mozilla.org/docs/Web/API/File) を参照してください。


### <a name="related-topics"></a>関連トピック

[ナビゲーション](../navigation.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../../overview.md)
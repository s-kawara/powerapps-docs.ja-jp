---
title: openForm |Microsoft Docs
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
ms.assetid: bea56947-d976-4974-9ac7-2d5f5c7b6732
ms.openlocfilehash: d0754030de4880f0ad693105e96b47d785f1561b
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72342371"
---
# <a name="openform"></a>openForm

[!INCLUDE [openform-description](includes/openform-description.md)]

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリ

## <a name="syntax"></a>構文

`context.navigation.openForm(options, parameters)`

## <a name="parameters"></a>パラメーター

| パラメーター名|種類|必須|Description|
| ------------- |----|--------|-----------|
|オプション|`EntityFormOptions`|はい|フォームを開くためのエンティティフォームオプション。 EntityFormOptions には、次の属性があります。<br/>- **Createfromentity**: `Lookup`。 マップされた属性値に基づいて既定値を提供するレコードを指定します。 Lookup オブジェクトには、`entityType`、`id`、および `name` の文字列プロパティがあります。 <br/>- **entityId**: `String`。 フォームを表示するエンティティレコードの ID。<br/>- **entityName**: `String`。 フォームを表示するエンティティの論理名。<br/>- **formId**: `String`。 表示するフォームインスタンスの ID。<br/>-  の**高さ**: `Number` します。 表示するフォームウィンドウの高さ (ピクセル単位)。<br/>**Openinnewwindow**: `boolean` を -  します。 フォームを新しいウィンドウに表示するかどうかを指定します。<br/>- **useQuickCreateForm**: `Boolean`。 簡易作成フォームを開くかどうかを指定します。 この値を指定しない場合、既定で `false` が渡されます。<br/>- **幅**: `Number`。 表示するフォームウィンドウの幅 (ピクセル単位)。<br/>- **Windowposition**: `Number`。 画面上のフォームのウィンドウ位置に対して、次のいずれかの値を指定します。 `1:center` <br/> `2:side`|
|パラメータ|`Object`|いいえ|追加のパラメーターをフォームに渡すディクショナリオブジェクト。 パラメーターが無効な場合、エラーが発生します。 詳細につい[ては、「フォームに渡されるパラメーターを使用したフィールド値」と「](https://docs.microsoft.com/en-us/powerapps/developer/model-driven-apps/set-field-values-using-parameters-passed-form) [カスタムクエリ文字列パラメーターを受け入れるようにフォームを構成](https://docs.microsoft.com/en-us/powerapps/developer/component-framework/sample-controls/navigation-api-control)する」を参照してください。|

## <a name="return-value"></a>戻り値

種類: `Promise<OpenFormSuccessResponse>`

## <a name="remarks"></a>」

[Promise](https://developer.mozilla.org/docs/Web/JavaScript/reference/Global_Objects/Promise)を見る

### <a name="related-topics"></a>関連トピック

[ナビゲーション](../navigation.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../../overview.md)
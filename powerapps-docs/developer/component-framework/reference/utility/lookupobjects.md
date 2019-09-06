---
title: lookupObjects | Microsoft Docs
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
ms.assetid: d213b401-cfc4-44df-b55c-f040fb6d7072
---

# <a name="lookupobjects"></a>lookupObjects

[!INCLUDE [lookupobjects-description](includes/lookupobjects-description.md)]

## <a name="syntax"></a>構文

`lookupObjects(lookupOptions)`

## <a name="parameters"></a>パラメーター

| パラメーター名|型|必須出席者|説明|
| ------------- |----|--------|-----------|
|lookupOptions|`UtilityApi.LookupOptions`|はい|検索ダイアログを開くオプション。 LookupOptions は以下の属性を持ちます:<br/>- **allowMultiSelect**: `boolean`。 検索で複数のアイテムを選択できるかどうか。<br/>- **defaultEntityType**: `string`. 既定のエンティティの種類。<br/>- **defaultViewId**: `string`。 使用する既定のビュー。<br/>- **entityTypes**: `string[]`。 表示するエンティティの種類。<br/>- **viewIds**: `string[]`。 ビュー ピッカーで使用できるビュー。 システム ビューのみがサポートされます (ユーザー ビューはサポートされません)|

## <a name="return-value"></a>戻り値

種類: `Promise`

[Promise](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Promise) と [ファイル](https://developer.mozilla.org/docs/Web/API/File) を参照してください。


### <a name="related-topics"></a>関連トピック

[Utility](../utility.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../../overview.md)
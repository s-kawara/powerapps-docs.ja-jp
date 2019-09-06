---
title: getResource | Microsoft Docs
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
ms.assetid: 5c04ba7c-acfe-4375-8dd8-6c537ded9352
---

# <a name="getresource"></a>getResource

[!INCLUDE [getresource-description](includes/getresource-description.md)]

## <a name="syntax"></a>構文

`getResource(id, success, failure)`

## <a name="parameters"></a>パラメーター

| パラメーター名|型|必須出席者|説明|
| ------------- |----|--------|-----------|
|id|`string`|はい|リソースの文字列の識別子。|
|success|`string`|いいえ|成功コールバック。 リソースのデータは Base 64 エンコード形式で返されます。|
|失敗|`string`|いいえ|失敗コールバック。|


### <a name="related-topics"></a>関連トピック

[リソース](../resources.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../../overview.md)
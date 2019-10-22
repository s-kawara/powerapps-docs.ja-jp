---
title: hasEntityPrivilege |Microsoft Docs
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
applies_to:
- Dynamics 365 (online)
- Dynamics 365 Version 9.x
ms.assetid: f22723f0-c606-465c-abba-0a8c46a10e32
ms.openlocfilehash: f370d14f0b978d7ac4b6e6535677e06e7cf3f86e
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72340899"
---
# <a name="hasentityprivilege"></a>hasEntityPrivilege

[!INCLUDE [hasentityprivilege-description](includes/hasentityprivilege-description.md)]

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリ

## <a name="syntax"></a>構文

`context.utils.hasEntityPrivilege(entityTypeName, privilegeType, privilegeDepth)`

## <a name="parameters"></a>パラメーター

| パラメーター名|種類|必須|Description|
| ------------- |----|--------|-----------|
|entityTypeName|`string`|はい|エンティティ型の名前|
|privilegeType|`enum`|いいえ|エンティティ特権の種類。 次の属性があります。<br/>- `None = 0`<br/>- `Create = 1` <br/>- `Read = 2`<br/>- `Write = 3`<br/>- `Delete = 4`<br/>- `Assign =5`<br/>- `Share =6`<br/>- `Append =7`<br/>- `AppendTo =8`|
|privilegeDepth|`enum`|いいえ|エンティティ特権の深さ。 次の属性があります。 <br/>- `None = -1`<br/>- `Basic = 0`<br/>- `Local = 1`<br/>- `Deep = 2`<br/>- `Global = 3`|

## <a name="return-value"></a>戻り値

**種類**: `boolean`

### <a name="related-topics"></a>関連トピック

[ユーティリティ](../utility.md)<br/>
[PowerApps コンポーネントフレームワーク API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../../overview.md)
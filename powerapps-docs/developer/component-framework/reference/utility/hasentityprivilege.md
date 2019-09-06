---
title: hasEntityPrivilege | Microsoft Docs
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
applies_to:
  - Dynamics 365 (online)
  - Dynamics 365 Version 9.x
ms.assetid: f22723f0-c606-465c-abba-0a8c46a10e32
---

# <a name="hasentityprivilege"></a>hasEntityPrivilege

[!INCLUDE [hasentityprivilege-description](includes/hasentityprivilege-description.md)]

## <a name="syntax"></a>構文

`hasEntityPrivilege(entityTypeName, privilegeType, privilegeDepth)`

## <a name="parameters"></a>パラメーター

| パラメーター名|型|必須出席者|説明|
| ------------- |----|--------|-----------|
|entityTypeName|`string`|はい|エンティティの種類の名前|
|特権の種類|`enum`|いいえ|エンティティの特権の種類。 次の属性があります:<br/>- `None =1`<br/>- `Create =1` <br/>- `Read =2`<br/>- `Write =3`<br/>- `Delete =4`<br/>- `Assign =5`<br/>- `Share =6`<br/>- `Append =7`<br/>- `AppendTo =8`|
|privilegeDepth|`enum`|いいえ|エンティティの特権の深さ。 次の属性があります: <br/>- `None =-1`<br/>- `Basic =0`<br/>- `Local =1`<br/>- `Deep =2`<br/>- `Global =3`|

## <a name="return-value"></a>戻り値

**種類**: `boolean`

### <a name="related-topics"></a>関連トピック

[Utility](../utility.md)<br/>
[PowerApps コンポーネント フレームワークの API リファレンス](../../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../../overview.md)
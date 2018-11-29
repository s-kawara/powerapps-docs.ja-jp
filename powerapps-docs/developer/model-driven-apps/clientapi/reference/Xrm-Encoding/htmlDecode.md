---
title: htmlDecode| MicrosoftDocs
description: クライアント API メソッドはデコードされた文字列に HTMLエンコードされた文字列を変換します。
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 4ef7160b-ac01-4d08-8a98-f8e3012ef20b
author: KumarVivek
ms.author: kvivek
manager: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="htmldecode-client-api-reference"></a>htmlDecode (クライアント API 参照)



[!INCLUDE[./includes/htmlDecode-description.md](./includes/htmlDecode-description.md)] 

## <a name="syntax"></a>構文

`Xrm.Encoding.htmlDecode(arg)`

## <a name="parameters"></a>パラメーター

|パラメーター名        | 種類           | 必須出席者  |説明  |
| ------------- |-------------| -----|-----|
|引数        | String           | 必須出席者  |デコードされる HTMLエンコードされた文字列。  |


## <a name="return-value"></a>戻り値

**種類**: 文字列

**説明**: デコードされた文字列。

## <a name="related-topics"></a>関連トピック

[htmlEncode](htmlEncode.md)

[htmlAttributeEncode](htmlAttributeEncode.md)

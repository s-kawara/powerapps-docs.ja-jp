---
title: getMaxLength (クライアント API 参照)| MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 67a96fc4-4d65-4858-90da-f41eeba0365a
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getmaxlength-client-api-reference"></a>getMaxLength (クライアント API 参照)



文字列属性またはメモ属性の最大長を示す数を返します。 

## <a name="attribute-types-supported"></a>サポートされる属性の種類

文字列、メモ

## <a name="syntax"></a>構文

`formContext.getAttribute(arg).getMaxLength()`

## <a name="return-value"></a>戻り値

**種類**: 数値。 

**説明**: この属性の文字列の最大長さです。

> [!NOTE]
> 電子メール フォーム を定義する属性はメモ属性ですが、`getMaxLength` メソッドがありません。
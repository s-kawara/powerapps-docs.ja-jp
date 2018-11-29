---
title: getOption (クライアント API 参照)| MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: e334d2d9-91c0-4953-956d-444a84dc9da2
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getoption-client-api-reference"></a>getOption (クライアント API 参照)



メソッドに引数として渡された値 (ラベル値または列挙値) と一致する値を持つオプション オブジェクトを返します。 

## <a name="attribute-types-supported"></a>サポートされる属性の種類

OptionSet、MultiSelectOptionSet

## <a name="syntax"></a>構文

`formContext.getAttribute(arg).getOption(value)`

## <a name="parameters"></a>パラメーター

**文字列** (オプションのラベル) または**数値** (オプションの列挙値)。

## <a name="return-value"></a>戻り値

**種類**: オプション オブジェクト。 

**説明**: 属性の論理名。


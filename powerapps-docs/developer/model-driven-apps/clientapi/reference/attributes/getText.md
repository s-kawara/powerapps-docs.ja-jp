---
title: モデル駆動型アプリの getText (クライアント API 参照)| MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 649fe7b0-016d-409f-ba3c-b14e0f1953e0
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="gettext-client-api-reference"></a>getText (クライアント API 参照)



**optionset** または **multiselectoptionset** 属性に現在選択しているオプション用テ キストの文字列値を取得します。 

## <a name="attribute-types-supported"></a>サポートされる属性の種類

optionset、multiselectoptionset

## <a name="syntax"></a>構文

`formContext.getAttribute(arg).getText()`

## <a name="return-value"></a>戻り値

**種類**: 文字列。 

**説明**: 選択したオプションの **テキスト** 値。

### <a name="related-topics"></a>関連トピック
[getInitialValue (クライアント API 参照)](getInitialValue.md)

[getOption (クライアント API 参照)](getOption.md)

[getOptions (クライアント API 参照)](getOptions.md)

[getSelectedOption (クライアント API 参照)](getSelectedOption.md) 



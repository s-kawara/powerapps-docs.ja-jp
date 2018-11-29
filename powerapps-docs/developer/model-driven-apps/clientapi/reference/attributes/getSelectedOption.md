---
title: Xrm.Device| MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: ce572df6-aae6-431a-aa95-73eee544c7e9
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getselectedoption-client-api-reference"></a>getSelectedOption (クライアント API 参照)



それぞれ **optionset** または **multiselectoptionset** 属性で選択されたオプション オブジェクトまたはオプション オブジェクトの配列を返します。 

## <a name="attribute-types-supported"></a>サポートされる属性の種類

optionset、multiselectoptionset

## <a name="syntax"></a>構文

`formContext.getAttribute(arg).getSelectedOption()`

## <a name="return-value"></a>戻り値

**種類**: optionset に対してオプション オブジェクト。multiselectoptionset に対してオプション オブジェクトの配列。 

**説明**: テキストおよび値のプロパティを持つオブジェクトを返します。

### <a name="related-topics"></a>関連トピック
[getInitialValue (クライアント API 参照)](getInitialValue.md)

[getOption (クライアント API 参照)](getOption.md)

[getOptions (クライアント API 参照)](getOptions.md)

[getText (クライアント API 参照)](getText.md)


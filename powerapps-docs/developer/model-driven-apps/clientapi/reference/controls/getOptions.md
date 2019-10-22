---
title: getOptions (クライアント API 参照)| MicrosoftDocs
ms.date: 08/13/2019
ms.service: powerapps
ms.topic: reference
ms.assetid: 83347491-68d2-4844-bda4-0cd0abde2edf
author: nkrb
ms.author: kvivek
manager: annbe
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getoptions-client-api-reference"></a>getOptions (クライアント API 参照)

空白のオプションや、 [removeOption](removeOption.md) によってコントロールから削除されたオプションなど、コントロールで使用することができる有効なオプションを表す、オプション オブジェクトの配列を返します。 

## <a name="control-types-supported"></a>サポートされているコントロールの種類

OptionSet、MultiSelectOptionSet

## <a name="syntax"></a>構文

`formContext.getControl(arg).getOptions()`

## <a name="return-value"></a>戻り値

**種類**: オプション オブジェクトの配列。 

**説明**: 有効なオプションを表すオプションオブジェクトの配列です。各オプション オブジェクトには以下の属性があります:
- **テキスト**: 文字列 オプションのラベル
- **値**: 数値 オプションの列挙値


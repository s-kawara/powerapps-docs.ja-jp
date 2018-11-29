---
title: モデル駆動型アプリにおける addOption (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 9798f168-7b94-411d-9aed-6471042ff11a
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="addoption-client-api-reference"></a>addOption (クライアント AIP 参照)



コントロールにオプションを追加します。 

## <a name="control-types-supported"></a>サポートされているコントロールの種類

OptionSet、MultiSelectOptionSet

## <a name="syntax"></a>構文

`formContext.getControl(arg).addOption(option, index);`

## <a name="parameters"></a>パラメーター

|Name | 種類​​ | 必須出席者 | 内容|
|--|--|--|--|
|option |オブジェクト |あり|追加するオプション。 オブジェクトには、次の属性が含まれています。<br/>**- テキスト**: 文字列。 オプションのラベル。<br/>**- 値**: 数字。 オプションの値。|
|インデックス |数値 |No|新しいオプションを配置するインデックスの位置。 指定されていない場合、オプションは末尾に追加されます。|

### <a name="related-topics"></a>関連トピック

[clearOptions](clearOptions.md)

[removeOption](removeOption.md)
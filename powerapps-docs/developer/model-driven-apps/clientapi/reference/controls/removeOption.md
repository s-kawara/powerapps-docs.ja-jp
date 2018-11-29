---
title: モデル駆動型アプリの removeOption (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 09fd288c-d687-4976-b708-29a466fc35b1
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="removeoption-client-api-reference"></a>removeOption (クライアント API 参照)



コントロールからオプションを削除します。 

## <a name="control-types-supported"></a>サポートされているコントロールの種類

optionset、multiselectoptionset

## <a name="syntax"></a>構文

`formContext.getControl(arg).removeOption(value);`

## <a name="parameters"></a>パラメーター

|Name | 種類​​ | 必須出席者 | 内容|
|--|--|--|--|
|値 |数値 |はい|削除するオプションの値。|

### <a name="related-topics"></a>関連トピック

[addOption](addOption.md)

[clearOptions](clearOptions.md)

 



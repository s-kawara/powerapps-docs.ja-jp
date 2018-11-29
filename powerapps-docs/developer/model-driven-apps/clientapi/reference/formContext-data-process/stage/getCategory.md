---
title: モデル駆動型アプリの getCategory (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 2849a9e1-b2fb-464c-8fc7-90b0df027c86
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getcategory-client-api-reference"></a>getCategory (クライアント API 参照)



[!INCLUDE[./includes/getCategory-description.md](./includes/getCategory-description.md)]

## <a name="syntax"></a>構文

`var stageCategoryNumber = stageObj.getCategory().getValue();`

## <a name="return-value"></a>戻り値

**種類**: 数値。 

**説明**: 可能な値のリストを次に示します。

|Value |内容|
|--|--|
|0|見込みありと評価|
|1|提案作成|
|2|提案|
|3|クローズ|
|4|特定|
|5|調査|
|6|解決|

### <a name="related-topics"></a>関連トピック

[formContext.data.process](../../formContext-data-process.md)
 



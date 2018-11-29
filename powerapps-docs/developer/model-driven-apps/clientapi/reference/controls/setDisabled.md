---
title: モデル駆動型アプリにおける setDisabled (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 86383cb1-c4c8-4e82-9f60-1dc4588b519d
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="setdisabled-client-api-reference"></a>setDisabled (クライアント API 参照)



コントロールが無効かどうかを設定します。

## <a name="control-types-supported"></a>サポートされているコントロールの種類

**kbsearch** コントロールを除くすべての種類

## <a name="syntax"></a>構文

`formContext.getControl(arg).setDisabled(bool);`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|bool|Boolean|あり|コントロールを無効または有効にするには、**true** または **false** を指定します。|

### <a name="related-topics"></a>関連トピック

[getDisabled](getDisabled.md)




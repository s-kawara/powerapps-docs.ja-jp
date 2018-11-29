---
title: モデル駆動型アプリの clearFormNotification (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 6c57db71-a76d-404c-852e-9c36a1c549ee
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="clearformnotification-client-api-reference"></a>clearFormNotification (クライアントAPI参照)



[!INCLUDE[./includes/clearFormNotification-description.md](./includes/clearFormNotification-description.md)]

## <a name="syntax"></a>構文

`formContext.ui.clearFormNotification(uniqueId)`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|uniqueId|String|あり|[setFormNotification](setFormNotification.md)メソッドを使用して設定された、クリアされるメッセージの一意な識別子。|

## <a name="return-value"></a>戻り値

**種類** :ブール値

**概要**: メソッドが成功すると True、それ以外の場合は False です。 


### <a name="related-topics"></a>関連トピック

[setFormNotification](setFormNotification.md)

[formContext.ui](../formContext-ui.md)

[formContext](../../clientapi-form-context.md)


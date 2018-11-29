---
title: モデル駆動型アプリにおける clearNotification (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 4d025f92-db16-440c-9f82-e40d71e09862
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="clearnotification-client-api-reference"></a>clearNotification (クライアントAPI参照)



コントロールに対して既に表示されているメッセージを削除。

## <a name="control-types-supported"></a>サポートされているコントロールの種類

すべて

## <a name="syntax"></a>構文

`formContext.getControl(arg).clearNotification(uniqueId);`

## <a name="parameters"></a>パラメーター

|Name | 種類​​ | 必須出席者 | 内容|
|--|--|--|--|
|uniqueId |String |No|**setNotification** または **addNotification** を使用して特定のメッセージ セットをクリアするために使用する ID。 **uniqueId** パラメーターが指定されない場合、現在表示されている通知はクリアされます。| 


## <a name="return-value"></a>戻り値

**種類** :ブール値 

**説明** :メソッドが成功したかどうかを示します。 

### <a name="related-topics"></a>関連トピック

[addNotification](addNotification.md)

[setNotification](setNotification.md)
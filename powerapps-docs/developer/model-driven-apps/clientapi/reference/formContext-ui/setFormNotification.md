---
title: モデル駆動型アプリの setFormNotification (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 48749e32-8490-4c8f-917c-3f1f8b9c028b
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="setformnotification-client-api-reference"></a>setFormNotification (クライアントAPI参照)



[!INCLUDE[./includes/setFormNotification-description.md](./includes/setFormNotification-description.md)]

任意の数の通知を表示できます。また、それらの通知は [clearFormNotification](clearFormNotification.md) を使用して削除するまで表示されます。 通知領域の高さは限られていますので、各新しいメッセージは、上部に追加されます。 ユーザーは、削除されていない以前のメッセージを見るにはスクロールする必要がある場合があります。

## <a name="syntax"></a>構文

`formContext.ui.setFormNotification(message, level, uniqueId);`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|メッセージ|String|あり|メッセージのテキスト。|
|レベル|String|あり|メッセージのレベルは、メッセージがどのように表示されるかを定義します。 次のいずれかの値を指定します。<br>`ERROR` : 通知はシステム エラーアイコンを使用します。<br/>`WARNING` : 通知はシステム警告アイコンを使用します。<br/>`INFO` : 通知はシステム情報アイコンを使用します。|
|uniqueId|String|あり|通知を削除する [clearFormNotification](clearFormNotification.md) で後に使用されるメッセージの一意識別子です。|

## <a name="return-value"></a>戻り値

**種類**: ブール値

**概要**: メソッドが成功すると True、それ以外の場合は False です。 


### <a name="related-topics"></a>関連トピック

[clearFormNotification](clearFormNotification.md)

[formContext.ui](../formContext-ui.md)

[formContext](../../clientapi-form-context.md)


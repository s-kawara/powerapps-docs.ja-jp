---
title: モデル駆動型アプリにおける保存イベント引数 (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: dff20ae0-c9ec-4413-9cd1-0ff77639ad91
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="save-event-arguments-client-api-reference"></a>イベント引数の保存 (Client API 参照)



フォーム [OnSave](events/form-onsave.md) イベントが発生したら、実行コンテキスト オブジェクトの [getEventArgs](executioncontext/getEventArgs.md) メソッドを使用して、保存イベントを管理するために使用できるメソッドを格納したオブジェクトを取得できます。

|メソッド|内容|
|--|--|
|[getSaveMode](save-event-arguments/getSaveMode.md)|[!INCLUDE[save-event-arguments/includes/getSaveMode-description.md](save-event-arguments/includes/getSaveMode-description.md)]|
|[isDefaultPrevented](save-event-arguments/isDefaultPrevented.md)|[!INCLUDE[save-event-arguments/includes/isDefaultPrevented-description.md](save-event-arguments/includes/isDefaultPrevented-description.md)]|
|[preventDefault](save-event-arguments/preventDefault.md)|[!INCLUDE[save-event-arguments/includes/preventDefault-description.md](save-event-arguments/includes/preventDefault-description.md)]|


## <a name="related-topics"></a>関連トピック

[クライアント API 実行コンテキスト](../clientapi-execution-context.md)

[実行コンテキストのメソッド](execution-context.md)


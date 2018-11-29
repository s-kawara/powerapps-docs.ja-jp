---
title: モデル駆動型アプリにおける TabStateChange イベント (Client API リファレンス) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 89123cde-7c66-4c7d-94e4-e287285019f8
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="tabstatechange-event-client-api-reference"></a>TabStateChange イベント (クライアント API 参照)



このイベントは、ユーザーの操作によってタブの **DisplayState** が変更されたか、[setDisplayState](../formContext-ui-tabs/setDisplayState.md) メソッドがコードに適用されたときに発生します。 

このイベントは、タブ内の IFRAME の **src** プロパティを変更する場合に使用します。縮小されたタブ内の IFRAME の OnLoad イベントで IFrame.**src** プロパティを設定すると、タブが展開されたときに値が上書きされます。

[addTabStateChange](../formContext-ui-tabs/addTabStateChange.md) メソッドを使用してこのイベント ハンドラーを追加し、[removeTabStateChange](../formContext-ui-tabs/removeTabStateChange.md) メソッドを使用して削除します。




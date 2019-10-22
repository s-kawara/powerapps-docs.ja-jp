---
title: Dynamics 365 for Customer Engagement における onPreProcessStatusChange イベント (クライアント API 参照) | MicrosoftDocs
ms.date: 06/30/2019
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 for Customer Engagement (online)
ms.assetid: null
author: MSFTMan
ms.author: Deonhe
manager: KVivek
search.audienceType:
  - developer
search.app:
  - D365CE
---
# <a name="onpreprocessstatuschange-event-client-api-reference"></a>onPreProcessStatusChange イベント (クライアント API 参照)

[!INCLUDE[](../../../../../includes/cc_applies_to_update_9_0_0.md)]

このイベントはプロセスのインスタンスの状態が変化する **前** に発生します。 

**formContext.data.process**.[addOnPreProcessStatusChange](../formContext-data-process/eventhandlers/addOnPreProcessStatusChange.md) メソッドを使用して、このイベントのイベント ハンドラを追加し、 **formContext.data.process**.[removeOnPreProcessStatusChange](../formContext-data-process/eventhandlers/removeOnPreProcessStatusChange.md) メソッドを使用してイベント ハンドラを削除します。 

開発者は、onPreProcessStatusChange イベントに登録されたWebリソース スクリプト内から、Webリソース スクリプトに渡された executionContext オブジェクトで以下を起動することができます: 

`executionContext.getEventArgs().preventDefault();` 

`preventDefault`を呼び出したとき:

- 状態の変更はされません。 プロセス インスタンスは当初の状態で当初のステージに残ります。
- メインフォームの保存はされません。 メインフォームが処理途中の状態である場合、状態の変更はされません。
- onProcessStatusChange の登録を行ったWebリソースは呼び出されません。

このクライアントAPIは、統合クライアントでのみサポートされます。 従来WebクライアントではこのクライアントAPIはサポートされていません。

## <a name="methods-supported-for-this-event"></a>このイベントをサポートする方法
- **formContext.data.process**、[addOnPreProcessStatusChange](../formcontext-data-process/eventhandlers/addOnPreProcessStatusChange.md) メソッドはこのイヴェントにイベント ハンドラを追加します。
- **formContext.data.process**、[removeOnPreProcessStatusChange](../formcontext-data-process/eventhandlers/removeOnPreProcessStatusChange.md) メソッドはこのイヴェントからイベント ハンドラを削除します。 

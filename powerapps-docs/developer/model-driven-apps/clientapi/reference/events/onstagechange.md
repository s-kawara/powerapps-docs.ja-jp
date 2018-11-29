---
title: モデル駆動型アプリにおける OnStageChange イベント (Client API リファレンス) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 0c85fe34-1368-4d0d-87eb-4109206ce4f7
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="onstagechange-event-client-api-reference"></a>OnStageChange イベント (クライアント API 参照)



このイベントは、業務プロセス フロー コントロールのステージが変更されると発生します。 このイベントは、ユーザーがユーザー インターフェイスで**次のステージ**または**前のステージに移動**ボタンをクリックするか、開発者が `formContext.data.process.moveNext` または `formContext.data.process.movePrevious` メソッドを使用すると発生します。 このイベントのハンドラーでコードを使用してステージを変更すると、キャンセルできません。

実行コンテキスト オブジェクトは、このイベントのイベント ハンドラーに渡されます。 [getEventArgs](../executioncontext/getEventArgs.md) メソッドを使用して、次のメソッドを持つオブジェクトを取得できます。
- **getDirection**: ステージ変更の方向を示す "次へ" または "前へ" のいずれかの文字列を返します。
- **getStage**: ステージ オブジェクトを返します。 ナビゲーションが新規エンティティに移動する場合を除き、戻されたステージは目的のステージ オブジェクトつまりアクティブ ステージを表します。 ナビゲーションが新規エンティティに移動する場合は、ステージは移動元のステージつまり以前のアクティブ ステージ オブジェクトを表します。 詳細: [ステージ メソッド](../formContext-data-process.md#stage-methods)。

## <a name="methods-supported-for-this-event"></a>このイベントをサポートするメソッド
- このイベントのイベント ハンドラを追加する **formContext.data.process**.[addOnStageChange](../formcontext-data-process/eventhandlers/addOnStageChange.md) メソッド。
- このイベントのイベント ハンドラーを取り外す **formContext.data.process**.[removeOnStageChange](../formcontext-data-process/eventhandlers/removeOnStageChange.md) メソッド。 




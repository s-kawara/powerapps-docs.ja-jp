---
title: モデル駆動型アプリにおける OnStageSelected イベント (Client API リファレンス) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 1ef0f11c-6188-4492-ae61-260a402223b8
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="onstageselected-event-client-api-reference"></a>OnStageSelected イベント (クライアント API 参照)



このイベントは、業務プロセス フロー コントロールのステージが選択されると発生します。 このイベントのハンドラーでコードを使用してステージを選択すると、キャンセルできません。

[getEventArgs](../executioncontext/getEventArgs.md) メソッドを使用して、次のメソッドを持つオブジェクトを取得できます。

**getStage**: 選択されたステージを表すステージ オブジェクトを返します。 詳細: [ステージ メソッド](../formContext-data-process.md#stage-methods)。

## <a name="methods-supported-for-this-event"></a>このイベントをサポートするメソッド
- このイベントのイベント ハンドラを追加する **formContext.data.process**.[addOnStageSelected](../formcontext-data-process/eventhandlers/addOnStageSelected.md) メソッド。
- このイベントのイベント ハンドラーを取り外す **formContext.data.process**.[removeOnStageSelected](../formcontext-data-process/eventhandlers/addOnStageSelected.md) メソッド。 




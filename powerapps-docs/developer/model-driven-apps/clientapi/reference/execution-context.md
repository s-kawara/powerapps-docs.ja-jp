---
title: モデル駆動型アプリにおけるクライアント API 実行コンテキスト | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: conceptual
applies_to:
  - Dynamics 365 (online)
ms.assetid: 1fcbf0fd-4e47-4352-a555-9315f7e57331
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="execution-context-client-api-reference"></a>実行コンテキスト (クライアント API 参照)



実行コンテキストは、コードを実行するイベントコンテキストを定義します。 詳細については、[クライアント API 実行コンテキスト](../clientapi-execution-context.md) を参照してください。

実行コンテキスト オブジェクトには以下のメソッドが用意されています。

|メソッド |内容 |
|---|---|
|[getDepth](executioncontext/getDepth.md)|このハンドラーの実行順序を示す値を返します。|
|[getEventArgs](executioncontext/getEventArgs.md)|**OnSave** イベントを管理するメソッドを持つオブジェクトを返します。|
|[getEventSource](executioncontext/getEventSource.md)|イベントが発生したオブジェクトへの参照を返します。|
|[getFormContext](executioncontext/getFormContext.md)|呼び出された場所によってフォーム上のフォームまたはアイテムへの参照を返します。|
|[getSharedVariable](executioncontext/getSharedVariable.md)|[setSharedVariable](executioncontext/setSharedVariable.md) メソッドを使用して変数セットを取得します。|
|[setSharedVariable](executioncontext/setSharedVariable.md)|現在のハンドラーの終了後に別のハンドラーから使用できる変数の値を設定します。|

### <a name="related-topics"></a>関連トピック

[クライアント API 実行コンテキスト](../clientapi-execution-context.md)

[イベント引数の保存](save-event-arguments.md)

[クライアント API オブジェクト モデルについて](../understand-clientapi-object-model.md) 


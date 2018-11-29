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
# <a name="client-api-execution-context"></a>クライアントAPI実行コンテキスト



実行コンテキストは、コードを実行するイベントコンテキストを定義します。 フォームまたはグリッドでイベントが発生する際に実行コンテキストが渡されます。イベント ハンドラーで[formContext](clientapi-form-context.md) あるいは [gridContext](clientapi-grid-context.md)を判断する、または保存イベントを管理するなどのさまざまなタスクを実行するのに使用することができます。 

実行コンテキストは、次に示す方法のいずれかで渡されます:

- **UIを使用したイベント ハンドラーの定義**: 実行コンテキストは、イベント ハンドラーによってJavaScriptライブラリ関数に渡すことのできる *[オプション]* パラメーターです。 イベント実行コンテキストを渡す関数名を指定する際に、**ハンドラーのプロパティ**ダイアログの**最初のパラメーターとして実行コンテキストを渡す**オプションを使用します。 実行コンテキストは、この関数に渡される最初のパラメーターです。<br/><br/>
![実行コンテキストを渡す](../media/ClientAPI-PassExecutionContext.png)<br/><br/>

- **コードを使用してイベント ハンドラーを定義**: 実行コンテキストは、コードを使用する関数セットに渡す最初のパラメーターとして自動的に渡されます。 コードのイベント ハンドラーを定義するために使用可能なメソッドの一覧については、 [コードを使用してイベントに関数を追加、または削除](events-forms-grids.md#add-or-remove-event-handler-function-to-event-using-code)を参照してください。 

実行コンテキストのオブジェクトにより、コンテキストとさらに連動するためのいくつかの方法が提供されます。 詳細については、[実行コンテキスト (クライアントAPI参照)](reference/execution-context.md) を参照してください。


### <a name="related-topics"></a>関連トピック

 [クライアントAPIフォームコンテキスト](clientapi-form-context.md)<br>
 [クライアントAPIグリッドコンテキスト](clientapi-grid-context.md)<br>
 [リボン アクションのフォームとグリッドのコンテキスト](../pass-data-page-parameter-ribbon-actions.md#form-and-grid-context-in-ribbon-actions)



---
title: Dynamics 365 for Customer Engagement の OnPreStageChange イベント (クライアント API 参照) | MicrosoftDocs
ms.date: 07/20/2019
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 for Customer Engagement (online)
ms.assetid: null
author: msftman
ms.author: deonhe
manager: kvivek
search.audienceType:
  - developer
search.app:
  - D365CE
---
# <a name="onprestagechange-event-client-api-reference"></a>OnPreStageChange イベント (クライアント API 参照)

このイベントは、ビジネスプロセスフローの制御が変更される **前** に発生します。 このイベントが発生するのは、ユーザー インターフェイスで **次のステージ**、 **前のステージに戻る** 、 **有効なステージを設定する** ボタンを選択した後、あるいは開発者が `formContext.data.process.moveNext`、 `formContext.data.process.movePrevious`、`formContext.data.process.setActiveStage` メソッドを使用した時です。

開発者は、onPreStageChange イベントに登録されたWebリソース スクリプト内から、Webリソース スクリプトに渡された executionContext オブジェクトで以下を起動することができます: 

`executionContext.getEventArgs().preventDefault();` 

`preventDefault`を呼び出したとき:

- 状態の変更はされません。 プロセス インスタンスは当初のステージに残ります。
- メインフォームの保存はされません。 メインフォームが処理途中の状態である場合、状態の変更はされません。
- onStageChange の登録を行ったWebリソースは呼び出されません。


実行コンテキスト オブジェクトは、このイベントのイベント ハンドラーに渡されます。 [getEventArgs](../executioncontext/getEventArgs.md) メソッドを使用して、次のメソッドを持つオブジェクトを取得できます。
- **getDirection**: ステージ変更の方向を示す "次へ" または "前へ" のいずれかの文字列を返します。
- **getStage**: ステージ オブジェクトを返します。 ナビゲーションが新規エンティティに移動する場合を除き、戻されたステージは目的のステージ オブジェクトつまりアクティブ ステージを表します。 ナビゲーションが新規エンティティに移動する場合は、ステージは移動元のステージつまり以前のアクティブ ステージ オブジェクトを表します。 詳細: [ステージ メソッド](../formContext-data-process.md#stage-methods)。

このクライアントAPIは、統合クライアントでのみサポートされます。 従来WebクライアントではこのクライアントAPIはサポートされていません。

## <a name="methods-supported-for-this-event"></a>このイベントをサポートする方法
- **formContext.data.process**.[addOnPreStageChange](../formcontext-data-process/eventhandlers/addOnPreStageChange.md) メソッドは、このイベントのイベント ハンドラを追加します。
- **formContext.data.process**.[removeOnPreStageChange](../formcontext-data-process/eventhandlers/removeOnPreStageChange.md) メソッドは、このイベントのイベント ハンドラを削除します。 




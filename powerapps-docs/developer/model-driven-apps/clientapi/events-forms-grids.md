---
title: モデル駆動型アプリのフォームとグリッド内のイベント| MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 9fb38429-55ef-45ce-a3a3-e649e1be89d0
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="events-in-forms-and-grids-in-model-driven-apps"></a>モデル駆動型アプリのフォームとグリッド内のイベント



すべてのクライアント側のコードは、イベントによって開始されます。 モデル駆動型アプリでは、イベント発生時に実行されるように JavaScript ライブラリ ([スクリプト Web リソース](../script-jscript-web-resources.md)) 内の特定の機能を関連付けます。 この機能は [*イベント ハンドラー*] と呼ばれます。 各イベント ハンドラーは、単一の関数を JavaScript ライブラリおよび関数が渡されるパラメータに指定します。

イベント ハンドラーは UI を使用する一部のイベントにのみ関連付けることができます。 UI を介して関連付けることができないイベントの場合、クライアント API にはこの様なイベントにイベント ハンドラーをアタッチするために使用可能なメソッドが用意されています。 

## <a name="add-or-remove-event-handler-function-to-event-using-ui"></a>UI を使用するイベントに対してイベント ハンドラー機能を追加または削除する

**フォームのプロパティ**ダイアログボックスの**イベント ハンドラー**セクションを使用して、スクリプトをフォームおよびフィールドのイベントに関連付けます。

![フォーム プロパティ内のイベント ハンドラー セクション](../media/Form-EventHandlers.png)

## <a name="add-or-remove-event-handler-function-to-event-using-code"></a>コードを使用するイベントに対してイベント ハンドラー機能を追加または削除する

UI を介して関連付けることができないイベントに対してイベント ハンドラーを追加および削除する、次のメソッドを使用する

|イベント |イベント ハンドラー|
|-------|-------|
|属性 [OnChange](reference/events/attribute-onchange.md) | [addOnChange](reference/attributes/addonchange.md) および [removeOnChange](reference/attributes/removeOnchange.md) メソッド|
|フォーム [OnLoad](reference/events/form-onload.md)| formContext.ui [addOnLoad](reference/formcontext-ui/addonload.md) および [removeOnLoad](reference/formcontext-ui/removeonload.md) メソッド|
|フォーム データ [OnLoad](reference/events/form-data-onload.md)| formContext.data [addOnLoad](reference/formcontext-data/addonload.md) および [removeOnLoad](reference/formcontext-data/removeonload.md) メソッド|
|フォーム [OnSave](reference/events/form-onsave.md)| [addOnSave](reference/formcontext-data-entity/addonsave.md) および [removeOnSave](reference/formcontext-data-entity/removeonsave.md) メソッド|
|検索コントロール [PreSearch](reference/events/presearch.md)| [addPreSearch](reference/controls/addpresearch.md) および [removePreSearch](reference/controls/removepresearch.md) メソッド|
|kbsearch コントロール [OnResultOpened](reference/events/onresultopened.md)|[addOnResultOpened](reference/controls/addOnResultOpened.md) および [removeOnResultOpened](reference/controls/removeOnResultOpened.md) メソッド|
|kbsearch コントロール [OnSelection](reference/events/onselection.md)|[addOnSelection](reference/controls/addOnSelection.md) および [removeOnSelection](reference/controls/removeOnSelection.md) メソッド|
|kbsearch コントロール [PostSearch](reference/events/postsearch.md)|[addOnPostSearch](reference/controls/addOnPostSearch.md) および [removeOnPostSearch](reference/controls/removeOnPostSearch.md) メソッド|

>[!IMPORTANT]
>実行コンテキストは、コードを使用してセットする関数に最初のパラメーターとして自動的に渡されます。 詳細: [クライアント API 実行コンテキスト](clientapi-execution-context.md) 

## <a name="form-event-pipeline"></a>フォーム イベント パイプライン
各イベントに最大 50 個のイベント ハンドラーを定義することができます。 各イベント ハンドラーは、**フォームのプロパティ**ダイアログボックスの**イベント**タブの**イベント ハンドラー**セクションに表示される順番に実行されます。

[setSharedVariable](reference/executioncontext/setSharedVariable.md) および [getSharedVariable](reference/executioncontext/getSharedVariable.md) メソッドを使用して、イベント ハンドラー間の共通変数 (関数) を渡します。 実行コンテキスト [getDepth](reference/executioncontext/getDepth.md) メソッドを使用すると、あるイベント ハンドラーが他のイベント ハンドラーとの関係でどの順序で実行されるかを知ることができます。 

### <a name="related-topics"></a>関連トピック

[クライアント API オブジェクト モデルについて](understand-clientapi-object-model.md)<br/>
[クライアント API 実行コンテキスト](clientapi-execution-context.md)<br/>
[イベント (クライアント API 参照)](reference/events.md)<br/>


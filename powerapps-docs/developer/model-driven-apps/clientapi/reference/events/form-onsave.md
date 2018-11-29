---
title: モデル駆動型アプリのフォーム OnSave イベント (クライアント API 参照) | Microsoft Docs
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
# <a name="form-onsave-event-client-api-reference-in-model-driven-apps"></a>モデル駆動型アプリのフォーム OnSave イベント (クライアント API 参照)



`OnSave` イベントは、次のタイミングで発生します。
- 保存する変更済みデータがない時でも、ユーザーがフォームの右下隅の**保存**アイコンをクリックする。
- 保存する変更済みデータがない時でも、コードが [formContext.data.entity.save](../formContext-data-entity/save.md) メソッドを実行する。
- ユーザーがフォームから移動し、フォームに保存されていないデータがある。
- オートセーブ オプションが有効で、データ変更の 30 秒後にフォームに保存されていないデータがある。
- コードが [formContext.data.save](../formContext-data/save.md) メソッドを実行し、フォームに保存されていないデータがある。
- コードが [formContext.data.refresh](../formContext-data/refresh.md) メソッドを実行して true 値を最初のパラメーターとして渡し、フォームに保存されていないデータがある。

保存を実行するのにクリックされるボタンを確認するには、getSaveMode メソッドを使用します。

イベント引数オブジェクトの preventDefault メソッドを使用して、保存操作をキャンセルできます。 実行コンテキストの一部である getEventArgs メソッドを使用してアクセスできる preventDefault メソッド。 実行コンテキストは自動的にフォーム イベント ハンドラーに渡されます。

### <a name="related-topic"></a>関連項目
[グリッド OnSave イベント](grid-onsave.md)  




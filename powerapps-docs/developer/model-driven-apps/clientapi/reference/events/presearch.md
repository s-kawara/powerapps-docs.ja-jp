---
title: モデル駆動型アプリにおける 検索コントロール PreSearch イベント (Client API リファレンス) | Microsoft Docs
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
# <a name="lookup-control-presearch-event-client-api-reference"></a>検索コントロール PreSearch イベント (クライアント API 参照)



このイベントは、レコードを検索するのに検索コントロールがダイアログを起動する直前に発生します。 このイベントに対するイベント ハンドラーに設定する UI はありません。 検索コントロールで [addPreSearch](../controls/addpresearch.md) と [removePreSearch](../controls/removepresearch.md) メソッドを使用して、このイベントのイベント ハンドラーの追加と削除をする必要があります。

このイベントを他の検索コントロール メソッドと共に使用して、ユーザーが選択する検索結果を検索コントロールが表示する直前に、フォーム データに基づく検索に表示される結果を最新のものに変更します。 

## <a name="related-topics"></a>関連トピック

[addCustomFilter](../controls/addCustomFilter.md)




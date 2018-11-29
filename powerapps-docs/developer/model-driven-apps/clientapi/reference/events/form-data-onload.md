---
title: モデル駆動型アプリのフォーム データ OnLoad イベント (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: fb13c0a1-0e00-4592-8e58-3c2412141fbd
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="form-data-onload-event-client-api-reference"></a>フォーム データ OnLoad イベント (クライアント API 参照)



このイベントは、フォーム データが読み込まれるたびに、特に以下の場合に発生します。

- 最初のページ読み込み時
- formContext.data.[refresh](../formContext-data/refresh.md) メソッドを使用して、ページ データが明示的に更新されるとき。
- 変更がある場合に、レコードの保存時にページでデータが更新されるとき。
 
このイベントに対するイベント ハンドラーを管理するには、formContext.data.[addOnLoad](../formContext-data/addOnLoad.md) および formContext.data.[removeOnLoad](../formContext-data/removeOnLoad.md) メソッドを使用します。 




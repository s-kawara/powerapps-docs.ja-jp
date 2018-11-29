---
title: モデル駆動型アプリにおけるクライアント API グリッド コンテキスト | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: conceptual
applies_to:
  - Dynamics 365 (online)
ms.assetid: f884d7d4-31e6-4080-acd9-493e81e6b278
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="client-api-grid-context"></a>クライアントAPIグリッドコンテキスト

グリッドではデータを表形式で表示します。 グリッドは、フォーム全体にまたがることも、フォーム上のアイテムの 1 つになることもできます。後者は **サブグリッド** と呼ばれます。

クライアント API グリッドコンテキストオブジェクトは、現在のコードが実行されるフォームのサブグリッドへの参照を提供します。 

> [!NOTE]
> グリッドのコンテキストの取得 (フォーム全体に渡る) はリボン コマンドでのみサポートされます。 詳細情報 [リボン アクションのフォームとグリッドのコンテキスト](/powerapps/developer/model-driven-apps/pass-data-page-parameter-ribbon-actions#form-and-grid-context-in-ribbon-actions)

[formContext](clientapi-form-context.md) オブジェクトを使用して、コードが実行される場所のフォームのインスタンスを取得してから、フォーム上のサブグリッド コントロールを取り込みます。 たとえば、サブグリッド コントロールの名前を認識しているとき(例として、既定の取引先企業フォーム内の**取引先担当者**サブグリッド)、次のコードを使用してそのコントロールにアクセスできます。

```JavaScript
function doSomething(executionContext) {
   var formContext = executionContext.getFormContext(); // get the form Context
   var gridContext = formContext.getControl("Contacts"); // get the grid context

   // Perform operations on the subgrid
}
```

## <a name="related-topics"></a>関連トピック

[クライアントAPIフォームコンテキスト](clientapi-form-context.md)<br/>
[クライアント API 実行コンテキスト](clientapi-execution-context.md)<br/>
[クライアント API オブジェクト モデルについて](understand-clientapi-object-model.md)<br/>
[グリッドおよびサブグリッド](reference/grids.md)


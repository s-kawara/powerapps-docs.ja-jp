---
title: モデル駆動型アプリの ViewSelector メソッド (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 37fbabaf-e2ce-4e46-a54e-e46bd884197b
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="viewselector-methods-client-api-reference"></a>ViewSelector メソッド (クライアント API 参照)



サブグリッド コントロールのビュー セレクターに関する情報を取得または設定するメソッドを提供します。 ビュー セレクターを表示するようにサブグリッド コントロールが構成されていない場合、**ViewSelector** メソッドを呼び出すと、エラーがスローされます。

ViewSelector は読み取り専用グリッドでのみ使用できます。 ViewSelector は **gridContext**.[getViewSelector](gridcontrol/getViewSelector.md) メソッドによって返されます。

```JavaScript
var viewSelector = gridContext.getViewSelector();
```

メソッド

|Name|内容|以下に使用できます|
|--|--|--|
|[getCurrentView](viewselector/getCurrentView.md)|[!INCLUDE[viewselector/includes/getCurrentView-description.md](viewselector/includes/getCurrentView-description.md)]|読み取り専用グリッド|
|[isVisible](viewselector/isVisible.md)|[!INCLUDE[viewselector/includes/isVisible-description.md](viewselector/includes/isVisible-description.md)]|読み取り専用グリッド|
|[setCurrentView](viewselector/setCurrentView.md)|[!INCLUDE[viewselector/includes/setCurrentView-description.md](viewselector/includes/setCurrentView-description.md)]|読み取り専用グリッド|


### <a name="related-topics"></a>関連トピック

[gridContext](../grids.md#bkmk_gridcontext)

[モデル駆動型アプリにおけるグリッドおよびサブグリッド](../grids.md)



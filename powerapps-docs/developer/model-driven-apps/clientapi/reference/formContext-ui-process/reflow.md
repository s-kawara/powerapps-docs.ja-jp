---
title: モデル駆動型アプリにおける reflow (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 6833e4ea-70fc-4ee0-8aab-68cc55e21444
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="reflow-client-api-reference"></a>reflow (クライアント API 参照)



[!INCLUDE[./includes/reflow-description.md](./includes/reflow-description.md)]

## <a name="syntax"></a>構文

`formContext.ui.process.reflow(updateUI, parentStage, nextStage);`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|updateUI|Boolean|あり|プロセス コントロールの UI を更新するには **true** を指定し、そうでない場合は **false** を指定します。|
|parentStage|String|あり|GUID フォーマットでは、親ステージの ID を指定します。|
|nextStage|String|あり|GUID フォーマットでは、次のステージの ID を指定します。|

### <a name="related-topics"></a>関連トピック

[formContext.ui.process](../formContext-ui-process.md)




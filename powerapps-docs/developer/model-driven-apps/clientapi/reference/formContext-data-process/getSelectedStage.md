---
title: モデル駆動型アプリの getSelectedStage (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: ac9a8c97-ad4d-4ed8-8eb0-51b2693253dc
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getselectedstage-client-api-reference"></a>getSelectedStage (クライアント API 参照)



[!INCLUDE[./includes/getSelectedStage-description.md](./includes/getSelectedStage-description.md)]

## <a name="syntax"></a>構文

`formContext.data.process.getSelectedStage();`

## <a name="return-value"></a>戻り値

**種類**: ステージ。 

**説明**: 現在選択されているステージ。 返されるステージのプロパティにアクセスするメソッドについては、「[ステージ メソッド](../formContext-data-process.md#stage-methods)」を参照してください。

### <a name="related-topics"></a>関連トピック

[getActiveStage (Client API reference)](activestage/getActiveStage.md)

[formContext.data.process](../formContext-data-process.md)
 



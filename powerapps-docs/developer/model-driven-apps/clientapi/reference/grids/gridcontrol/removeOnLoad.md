---
title: モデル駆動型アプリにおける removeOnLoad (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 4d025f92-db16-440c-9f82-e40d71e09862
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="removeonload-client-api-reference"></a>removeOnLoad (クライアント API 参照)



[!INCLUDE[./includes/removeOnLoad-description.md](./includes/removeOnLoad-description.md)]

## <a name="grid-types-supported"></a>サポートされるグリッドの種類

読み取り専用グリッド

## <a name="syntax"></a>構文

`gridContext.removeOnLoad(myFunction);`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|myFunction|関数リファレンス|あり|**OnLoad** イベントから削除する関数。

## <a name="remarks"></a>備考

`gridContext` を取得するには、「[グリッド コンテキストの取得](../../grids.md#bkmk_gridcontext)」を参照してください。

### <a name="related-topics"></a>関連トピック

[addOnLoad](addOnLoad.md) 



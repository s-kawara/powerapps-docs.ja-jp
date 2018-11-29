---
title: モデル駆動型アプリにおける setStatus (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 649fe7b0-016d-409f-ba3c-b14e0f1953e0
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="setstatus-client-api-reference"></a>setStatus (クライアント API 参照)



[!INCLUDE[./includes/setStatus-description.md](./includes/setStatus-description.md)]

## <a name="syntax"></a>構文

`formContext.data.process.setStatus(status, callbackFunction);`

## <a name="parameters"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|状態|String|あり|新しい状態。 値は**アクティブ**、**中止**、または**完了**のいずれかです。|
|callbackFunction|関数|No|操作が完了したときに呼び出す関数。 このコールバック関数は、文字列値として新しい状態に渡されます。|

**種類**: 文字列。 

**説明**: **アクティブ**、**中断**、または**完了**のいずれかの値を返します。

### <a name="related-topics"></a>関連トピック

[formContext.data.process](../../formContext-data-process.md)
 



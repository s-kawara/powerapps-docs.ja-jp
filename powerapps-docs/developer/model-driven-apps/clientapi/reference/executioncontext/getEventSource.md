---
title: モデル駆動型アプリの getEventSource (クライアント API 参照) | MicrosoftDocs
description: イベントが発生したオブジェクトへの参照を返す getEventSource メソッドについて説明します。
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 9f3b2fed-fde5-46e4-8c59-43aa51aa82df
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="geteventsource-client-api-reference"></a>getEventSource (クライアント API 参照)



イベントが発生したオブジェクトへの参照を返します。

## <a name="syntax"></a>構文

`ExecutionContextObj.getEventSource()`

## <a name="return-value"></a>戻り値

**種類**: オブジェクト

**説明**: HTML DOM オブジェクトではなく、イベントのソースである **Xrm** オブジェクト モデルからのオブジェクトを返します。 たとえば [OnChange](../events/attribute-onchange.md) イベントの場合、このメソッドは、変更された属性を表す **formContext.data.entity** 属性オブジェクトを返します。


### <a name="related-topics"></a>関連トピック
[実行コンテキスト](../execution-context.md)






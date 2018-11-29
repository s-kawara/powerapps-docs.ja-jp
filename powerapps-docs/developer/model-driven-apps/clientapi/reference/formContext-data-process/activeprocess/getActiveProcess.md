---
title: モデル駆動型アプリの getActiveProcess (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: a977a250-b79f-4c88-a6af-776350b110f7
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getactiveprocess-client-api-reference"></a>getActiveProcess (クライアント API 参照)



[!INCLUDE[./includes/getActiveProcess-description.md](./includes/getActiveProcess-description.md)]

## <a name="syntax"></a>構文

`var activeProcess = formContext.data.process.getActiveProcess();`

## <a name="return-value"></a>戻り値

**種類**: プロセス。 

**説明**: 現在アクティブなプロセス。 返されるプロセスのプロパティにアクセスするメソッドについては、「[プロセス メソッド](../../formContext-data-process.md#process-methods)」を参照してください。

### <a name="related-topics"></a>関連トピック

[setActiveProcess)](setActiveProcess.md)

[formContext.data.process](../../formContext-data-process.md)
 



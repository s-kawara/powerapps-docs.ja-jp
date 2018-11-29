---
title: モデル駆動型アプリの setActiveProcessInstance (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: c01a9445-00b6-4152-a482-df830f91a3ea
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="setactiveprocessinstance-client-api-reference"></a>setActiveProcessInstance (クライアント API 参照)



[!INCLUDE[./includes/setActiveProcessInstance-description.md](./includes/setActiveProcessInstance-description.md)]

## <a name="syntax"></a>構文

`formContext.data.process.setActiveProcessInstance(processInstanceId, callbackFunction);`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|processInstanceId|String|あり|アクティブなインスタンスとして設定するプロセス インスタンスの ID。|
|callbackFunction|関数|No|操作が完了したときに呼び出す関数。 このコールバック関数に、操作が成功したかどうかを示すために次のいずれかの文字列値が渡されます。<br/>- **success**: 操作が成功しました。<br/>- **invalid**: processInstanceId が有効でないか、またはプロセスが有効な状態になっていません。|

### <a name="related-topics"></a>関連トピック

[getProcessInstances](getProcessInstances.md)

[formContext.data.process](../formContext-data-process.md)
 



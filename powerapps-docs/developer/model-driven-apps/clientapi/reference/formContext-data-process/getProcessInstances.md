---
title: モデル駆動型アプリの getProcessInstances (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: powerapps
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 4ed6c991-59c9-4a69-90d4-635f3f1d397b
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getprocessinstances-client-api-reference"></a>getProcessInstances (クライアント API 参照)



[!INCLUDE[./includes/getProcessInstances-description.md](./includes/getProcessInstances-description.md)]

## <a name="syntax"></a>構文

`formContext.data.process.getProcessInstances(callbackFunction(object));`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|callbackFunction|関数|あり|コールバック関数は、キー : 値のペアとして次の属性および対応する値を持つオブジェクトに渡されます。 すべての戻り値は文字列型です。ただし、[日付](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Date) 型の **CreatedOnDate** を除きます。 <br/>- CreatedOn (廃止)<br/>- CreatedOnDate<br/>- ProcessDefinitionID<br/>- ProcessDefinitionName<br/>- ProcessInstanceID<br/>- ProcessInstanceName<br/>- StatusCodeName<br/><br/>プロセス インスタンスは、ユーザーの特権に基づいてフィルター処理されます。|

### <a name="related-topics"></a>関連トピック

[setActiveProcessInstance](setActiveProcessInstance.md)

[formContext.data.process](../formContext-data-process.md)
 



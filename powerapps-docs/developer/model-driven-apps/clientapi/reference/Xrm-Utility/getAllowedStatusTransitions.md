---
title: モデル駆動型アプリの getAllowedStatusTransitions (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 28c36741-0070-435c-a42f-49f4dda2ef7f
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="getallowedstatustransitions-client-api-reference"></a>getAllowedStatusTransitions (クライアント API 参照)



[!INCLUDE[./includes/getAllowedStatusTransitions-description.md](./includes/getAllowedStatusTransitions-description.md)] 

## <a name="syntax"></a>構文

`Xrm.Utility.getAllowedStatusTransitions(entityName,stateCode).then(successCallback, errorCallback)`

## <a name="parameters"></a>パラメーター

|Name |種類​​ |必須出席者 |内容 |
|---|---|---|---|
|entityName|String|あり|エンティティの論理名。|
|stateCode|数値|あり|許可された状態遷移値を調べる状態コード。|
|successCallback|関数|No|処理が成功したときに実行する関数。|
|errorCallback|関数|No|処理が失敗したときに実行する関数。|


### <a name="related-topics"></a>関連トピック

[Xrm.Utility](../xrm-utility.md)




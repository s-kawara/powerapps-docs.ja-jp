---
title: モデル駆動型アプリにおける invokeProcessAction (Client API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: e71012ba-249d-4ae7-8891-f7d3ae16a20a
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="invokeprocessaction-client-api-reference"></a>invokeProcessAction (クライアント API 参照)



[!INCLUDE[./includes/invokeProcessAction-description.md](./includes/invokeProcessAction-description.md)] 

操作の詳細については、[アクションの使用](/flow/actions)を参照してください。

## <a name="syntax"></a>構文

`Xrm.Utility.invokeProcessAction(name,parameters).then(successCallback, errorCallback)`

## <a name="parameters"></a>パラメーター

|Name |型 |必須出席者 |説明 |
|---|---|---|---|
|名前|String|あり|呼び出すプロセス アクションの名前。|
|パラメーター|object|No|アクションの入力パラメータを含むオブジェクト。 項目の `key:value` ペアを使用してオブジェクトを定義します。ここで、`key` は**文字列**型です。|
|successCallback |関数 |あり |アクションが呼び出された場合に呼び出す関数。  |
|errorCallback |関数 |あり |処理が失敗したときに呼び出す関数。  |

## <a name="returns"></a>戻り値

成功時に、アクション出力と共に Web API 結果を返します。

### <a name="related-topics"></a>関連トピック

[アクションの使用](/flow/actions)

[Xrm.Utility](../xrm-utility.md)



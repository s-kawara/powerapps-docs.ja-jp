---
title: モデル駆動型アプリの getCurrentAppName (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: a8f83718-41a4-4958-a5ac-9b28cc2f8dba
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getcurrentappname-client-api-reference"></a>getCurrentAppName (クライアント API 参照)



モデル駆動型アプリで現在のビジネス アプリの名前を返します。

## <a name="syntax"></a>構文

```JavaScript
var globalContext = Xrm.Utility.getGlobalContext();
globalContext.getCurrentAppName().then(successCallback, errorCallback);
``` 

## <a name="parameters"></a>パラメーター

|Name |型 |必須出席者 |説明 |
|---|---|---|---|
|successCallback |関数 |あり |ビジネス アプリ名が返される場合に呼び出す関数。  |
|errorCallback |関数 |あり |処理が失敗したときに呼び出す関数。  |

## <a name="return-value"></a>戻り値

このメソッドがビジネス アプリのコンテキストで呼び出された場合、ビジネス アプリの名前を返します。 それ以外の場合は、エラーによって失敗します。

### <a name="related-topics"></a>関連トピック

[コードを使用してモデル駆動型アプリを作成、管理、公開する](../../../../create-manage-model-driven-apps-using-code.md)

[Xrm.Utility.getGlobalContext](../getGlobalContext.md)



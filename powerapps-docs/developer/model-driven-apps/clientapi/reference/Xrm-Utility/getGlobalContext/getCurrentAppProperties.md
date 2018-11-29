---
title: モデル駆動型アプリの getCurrentAppProperties (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 5f8d91ff-ba0d-4e90-a79a-18e32d09baa3
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getcurrentappproperties-client-api-reference"></a>getCurrentAppProperties (クライアント API 参照)



モデル駆動型アプリで現在のビジネス アプリのプロパティを返します。

## <a name="syntax"></a>構文

```JavaScript
var globalContext = Xrm.Utility.getGlobalContext();
globalContext.getCurrentAppProperties().then(successCallback, errorCallback);
``` 

## <a name="parameters"></a>パラメーター

|Name |型 |必須出席者 |説明 |
|---|---|---|---|
|successCallback |関数 |あり |ビジネス アプリのプロパティ情報が返される場合に呼び出す関数。 次の属性 (アプリ プロパティ) のオブジェクトは関数に渡されます。<br/>- **appId**<br/>- **displayName**<br/>- **uniqueName**<br/>- **url**<br/>- **webResourceId**<br/>- **webResourceName**<br/>- **welcomePageId**<br/>- **welcomePageName**|
|errorCallback |関数 |あり |処理が失敗したときに呼び出す関数。  |

## <a name="return-value"></a>戻り値

このメソッドがビジネス アプリのコンテキストで呼び出された場合、ビジネス アプリのプロパティを返します。 それ以外の場合は、エラーによって失敗します。

### <a name="related-topics"></a>関連トピック

[コードを使用してモデル駆動型アプリのアプリを作成、管理、公開する](../../../../create-manage-model-driven-apps-using-code.md)

[Xrm.Utility.getGlobalContext](../getGlobalContext.md) 




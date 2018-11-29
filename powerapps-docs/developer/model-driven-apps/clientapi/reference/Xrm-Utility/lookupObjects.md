---
title: モデル駆動型アプリの lookupObjects (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 89123cde-7c66-4c7d-94e4-e287285019f8
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="lookupobjects-client-api-reference"></a>lookupObjects (クライアント API 参照)



[!INCLUDE[./includes/lookupObjects-description.md](./includes/lookupObjects-description.md)] 

## <a name="syntax"></a>構文

`Xrm.Utility.lookupObjects(lookupOptions).then(successCallback, cancelCallback)`

## <a name="parameters"></a>パラメーター

**lookupOptions**: オブジェクト。 検索ダイアログを開くためのオプションを定義します。 次のプロパティがあります。

|プロパティ名 |種類​​ |必須出席者 |内容 |
|---|---|---|---|
|allowMultiSelect|Boolean|No|検索で複数のアイテムを選択できるかどうかを指定します。|
|defaultEntityType|String|No|使用する既定のエンティティの種類。|
|defaultViewId|String|No|使用する既定のビュー。|
|entityTypes|Array|No|表示するエンティティの種類。|
|showBarcodeScanner|Boolean|No|検索コントロールがモバイル クライアントでバーコード スキャナーを表示するかどうかを示します。|
|viewIds|Array|No|ビュー ピッカーで使用できるビュー。 システム ビューのみサポートされます。|
|successCallback |関数 |あり |検索コントロールが呼び出された場合に呼び出す関数。 次のプロパティを持つオブジェクトが渡されます。<br/>- **entityType**: 文字列。 検索コントロールで選択されたレコードのエンティティの種類。<br/>- **id**: 文字列。 検索コントロールで選択されたレコードの ID。<br/>- **name**: 文字列。 検索コントロールで選択されたレコードの名前。|
|errorCallback |関数 |あり |検索コントロールをキャンセルしたか、または処理が失敗したときに呼び出す関数。  |


### <a name="related-topics"></a>関連トピック

[Xrm.Utility](../xrm-utility.md)
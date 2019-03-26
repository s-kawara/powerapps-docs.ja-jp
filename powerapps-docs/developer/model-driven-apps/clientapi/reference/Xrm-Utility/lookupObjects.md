---
title: モデル駆動型アプリの lookupObjects (クライアント API 参照) | MicrosoftDocs
ms.date: 01/24/2019
ms.service: powerapps
ms.topic: reference
ms.assetid: 89123cde-7c66-4c7d-94e4-e287285019f8
author: KumarVivek
ms.author: kvivek
manager: annbe
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="lookupobjects-client-api-reference"></a>lookupObjects (クライアント API 参照)



[!INCLUDE[./includes/lookupObjects-description.md](./includes/lookupObjects-description.md)] 

## <a name="syntax"></a>構文

`Xrm.Utility.lookupObjects(lookupOptions).then(successCallback, errorCallback)`

## <a name="parameters"></a>パラメーター

**lookupOptions**: オブジェクト。 検索ダイアログを開くためのオプションを定義します。 次のプロパティがあります。

|プロパティ名 |種類​​ |必須出席者 |内容 |
|---|---|---|---|
|allowMultiSelect|Boolean|No|検索で複数のアイテムを選択できるかどうかを指定します。|
|defaultEntityType|String|No|使用する既定のエンティティの種類。|
|defaultViewId|String|なし|使用する既定のビュー。|
|disableMru|Boolean|なし|最近使用した (MRU) アイテムを表示するかどうかを判断します。<br />統一インターフェイスでのみ使用できます。|
|entityTypes|Array|なし|表示するエンティティの種類。|
|フィルター|オブジェクトの配列|なし|結果をフィルター処理するのに使用します。 配列内の各オブジェクトには、次の属性が含まれています。<br /><ul><li>**filterXml**: 文字列。 適用する FetchXML フィルター要素。</li><li>**entityLogicalName**: 文字列。 このフィルターを適用するエンティティの種類。</li></ul>|
|showBarcodeScanner|Boolean|なし|検索コントロールがモバイル クライアントでバーコード スキャナーを表示するかどうかを示します。|
|viewIds|Array|No|ビュー ピッカーで使用できるビュー。 システム ビューのみサポートされます。|
|successCallback |関数 |あり |検索コントロールが呼び出された場合に呼び出す関数。 次のプロパティを持つオブジェクトの配列が渡されます。<br/><ul><li>**entityType**: 文字列。 検索コントロールで選択されたレコードのエンティティの種類。</li><li>**id**: 文字列。 検索コントロールで選択されたレコードの ID。</li><li>**name**: 文字列。 検索コントロールで選択されたレコードの名前。</li>|
|errorCallback |関数 |あり |検索コントロールをキャンセルしたか、または処理が失敗したときに呼び出す関数。  |


### <a name="related-topics"></a>関連トピック

[Xrm.Utility](../xrm-utility.md)

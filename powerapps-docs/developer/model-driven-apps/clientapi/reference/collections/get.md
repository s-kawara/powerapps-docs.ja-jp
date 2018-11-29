---
title: モデル駆動型アプリでコレクション (クライアント API 参照) のメソッドを取得する | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 4d025f92-db16-440c-9f82-e40d71e09862
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="get-method-for-collections-client-api-reference"></a>コレクションに対する get メソッド (Client API 参照)



[!INCLUDE[./includes/get-description.md](./includes/get-description.md)]

## <a name="syntax"></a>構文

`collection.get([String][Number][delegate function(attribute, index)])`

## <a name="parameters"></a>パラメーター

|パラメーター  |戻り値 |返り値の種類  |
|---------|------|-------|
|なし​​  |コレクション内のすべてのオブジェクト  |Array|
|String  |名前が引数と一致するオブジェクト<br/><br/>**formContext.data.process** 名前空間で返されるオブジェクトには名前が含まれていません。 その、このメソッドで文字列パラメーターを使用してもオブジェクトは返されません。  |オブジェクト|
|数値  |インデックスが数字と一致するオブジェクト  |オブジェクト|
|デリゲート関数(属性, インデックス)  |戻り値 デリゲート関数が **true** を返す任意のオブジェクト。  |Array|


### <a name="related-topics"></a>関連トピック
[クライアント API のコレクション](../collections.md)

[forEach](forEach.md)

[getLength](getLength.md)


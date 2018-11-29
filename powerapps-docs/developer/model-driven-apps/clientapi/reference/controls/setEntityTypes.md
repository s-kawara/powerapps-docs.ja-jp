---
title: モデル駆動型アプリにおける setEntityTypes (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 93154168-1e9f-4849-b4bb-be8804f86f81
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="setentitytypes-client-api-reference"></a>setEntityTypes (クライアント API 参照)



検索コントロールで使用できるエンティティの種類を設定します。

## <a name="control-types-supported"></a>サポートされているコントロールの種類

検索コントロール

## <a name="syntax"></a>構文

`formContext.getControl(arg).setEntityTypes([entityLogicalNames]);`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|entityLogicalNames|文字列の配列|あり|検索コントロールで使用できるエンティティの論理名を指定します。|

### <a name="related-topics"></a>関連トピック

[getEntityTypes](getEntityTypes.md)

 



---
title: モデル駆動型アプリの getEntityTypes (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: c20ba958-821f-4168-a518-e39431603b28
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getentitytypes-client-api-reference"></a>getEntityTypes (クライアント API 参照)



検索コントロールで使用できるエンティティの種類を取得します。 

## <a name="control-types-supported"></a>サポートされているコントロールの種類

検索コントロール

## <a name="syntax"></a>構文

`formContext.getControl(arg).getEntityTypes();`

## <a name="return-value"></a>戻り値

**種類**: 文字列の配列

**説明**: このコントロールで使用できるエンティティの論理名。

### <a name="related-topics"></a>関連トピック

[setEntityTypes](setEntityTypes.md)

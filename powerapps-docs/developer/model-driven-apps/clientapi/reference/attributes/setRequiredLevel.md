---
title: setRequiredLevel (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 67a96fc4-4d65-4858-90da-f41eeba0365a
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="setrequiredlevel-client-api-reference"></a>setRequiredLevel (クライアント API 参照)



レコードを保存するために、属性のデータが必須であるかまたは推奨であるか設定します。

> [!IMPORTANT]
> 属性の要求レベルを減らすと、ページの保存時にエラーが発生することがあります。 サーバーが属性を必要とする場合、属性の値がないとエラーが発生します。 

## <a name="attribute-types-supported"></a>サポートされる属性の種類

すべて

## <a name="syntax"></a>構文

`formContext.getAttribute(arg).setRequiredLevel(requirementLevel)`

## <a name="parameters"></a>パラメーター

**種類**: 文字列。 

**説明**: レベルを以下のいずれかの値に設定します。
- なし
- 必須
- 推奨

### <a name="related-topic"></a>関連項目
[getRequiredLevel (クライアント API 参照)](getRequiredLevel.md)



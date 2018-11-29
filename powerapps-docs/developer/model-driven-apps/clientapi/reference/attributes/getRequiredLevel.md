---
title: getRequiredLevel (クライアント API 参照)| MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: c0b6ea26-2a11-4a49-8ecf-fe700e782bf3
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getrequiredlevel-client-api-reference"></a>getRequiredLevel (クライアント API 参照)



属性の値が必要または推奨かどうかを示す値を文字列を返します。 

## <a name="attribute-types-supported"></a>サポートされる属性の種類

すべて

## <a name="syntax"></a>構文

`formContext.getAttribute(arg).getRequiredLevel()`

## <a name="return-value"></a>戻り値

**種類**: 文字列。 

**説明**: 次のいずれかの値を返します。
- なし
- 必須
- 推奨

### <a name="related-topic"></a>関連項目
[setRequiredLevel (クライアント API 参照)](setRequiredLevel.md)

---
title: モデル駆動型アプリの getEntityReference (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: b8e23eee-f20f-4db9-9cc6-7fa5dd7ce2bb
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getentityreference-client-api-reference"></a>getEntityReference (クライアント API 参照)



[!INCLUDE[./includes/getEntityReference-description.md](./includes/getEntityReference-description.md)]

## <a name="grid-types-supported"></a>サポートされるグリッドの種類

読み取り専用および編集可能なグリッド

## <a name="syntax"></a>構文

`gridEntity.getEntityReference();`

## <a name="return-value"></a>戻り値

**種類**: 検索

**説明**: 行内のレコードを参照する検索オブジェクトです。 オブジェクトには次の属性があります。
- **entityType**: 文字列。 行内のレコードの論理名。 **GridEntity**.[getEntityName](getEntityName.md) メソッドによって返される同じデータ。
- **id**: 文字列。 行内のレコードの ID。 **GridEntity**.[getId](getId.md) メソッドによって返される同じデータ。
- **name**: 文字列。 行内のレコードの主属性の値。 **GridEntity**.[getPrimaryAttributeValue](getPrimaryAttributeValue.md) メソッドによって返される同じデータ。

## <a name="remarks"></a>備考

`gridEntity` オブジェクトを取得するには、「[GridEntity](../gridentity.md)」を参照してください。 


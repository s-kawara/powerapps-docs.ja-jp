---
title: モデル駆動型アプリの getIsDirty (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 93908c95-c813-4f55-9d19-8fd27a0126d7
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getisdirty-client-api-reference"></a>getIsDirty (クライアント API 参照)



[!INCLUDE[./includes/getIsDirty-description.md](./includes/getIsDirty-description.md)]

## <a name="syntax"></a>構文

`formContext.data.entity.getIsDirty();`

## <a name="return-type"></a>返り値の種類

**種類:** ブール値

**説明**: フォーム内のフィールドが変更されている場合は true、そうでない場合は false です。

### <a name="related-topics"></a>関連トピック

[formContext.data.getIsDirty](../formContext-data/getIsDirty.md)

[formContext](../../clientapi-form-context.md)


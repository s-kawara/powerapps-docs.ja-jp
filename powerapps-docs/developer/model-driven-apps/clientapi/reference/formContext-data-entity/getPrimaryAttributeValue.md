---
title: モデル駆動型アプリの getPrimaryAttributeValue (クライアント API 参照) | Microsoft Docs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 1a66f93d-a47c-4316-91f1-dcf5d09f9d19
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getprimaryattributevalue-client-api-reference"></a>getPrimaryAttributeValue (クライアント API 参照)



[!INCLUDE[./includes/getPrimaryAttributeValue-description.md](./includes/getPrimaryAttributeValue-description.md)]

## <a name="syntax"></a>構文

`formContext.data.entity.getPrimaryAttributeValue();`

## <a name="return-value"></a>戻り値

**種類**: 文字列。

**説明**: エンティティの名前。

## <a name="remarks"></a>備考

各エンティティは、<xref:Microsoft.Xrm.Sdk.Metadata.EntityMetadata.PrimaryNameAttribute>として設計された 1 つの文字列属性があります。 この属性の値は、レコードへのリンクが表示されるときに使用されます。




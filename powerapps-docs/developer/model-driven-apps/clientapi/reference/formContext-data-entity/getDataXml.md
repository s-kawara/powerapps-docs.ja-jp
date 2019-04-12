---
title: モデル駆動型アプリの getDataXml (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: powerapps
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
# <a name="getdataxml-client-api-reference"></a>getDataXml (クライアント API 参照)



[!INCLUDE[./includes/getDataXml-description.md](./includes/getDataXml-description.md)]

## <a name="syntax"></a>構文

`formContext.data.entity.getDataXml();`

## <a name="return-value"></a>戻り値

**種類**: 文字列。

**説明**: この例では、取引先企業レコードの次の 3 つのフィールドが更新されました。name、accountnumber、telephone2。

```"<account><name>Contoso</name><accountnumber>55555</accountnumber><telephone2>425 555-1234</telephone2></account>"```

## <a name="remarks"></a>備考

このメソッドはタブレット PC 用 Microsoft Dynamics 365 では使用できません。




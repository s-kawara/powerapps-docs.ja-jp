---
title: モデル駆動型アプリの getData (クライアント API 参照) | MicrosoftDocs
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
# <a name="getdata-client-api-reference"></a>getData (クライアント API 参照)



[!INCLUDE[./includes/getData-description.md](./includes/getData-description.md)]

これは廃止されたので、**GridRow.data** を使用する必要があります。

## <a name="grid-types-supported"></a>サポートされるグリッドの種類

読み取り専用および編集可能なグリッド

## <a name="syntax"></a>構文

`gridRow.getData();`

## <a name="return-value"></a>戻り値

**種類**: [GridRowData](../gridrowdata.md)

## <a name="remarks"></a>備考

`gridRow` オブジェクトを取得するには、「[GridRow](../gridrow.md)」を参照してください。 


---
title: モデル駆動型アプリの getEntity (クライアント API 参照) | MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 1672c213-d315-48fb-b49c-47cc19d23c28
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getentity-client-api-reference"></a>getEntity (クライアント API 参照)



[!INCLUDE[./includes/getEntity-description.md](./includes/getEntity-description.md)]

これは廃止されたので、**GridRowData.entity** を使用する必要があります。

## <a name="grid-types-supported"></a>サポートされるグリッドの種類

読み取り専用および編集可能なグリッド

## <a name="syntax"></a>構文

`gridRowData.getEntity();`

## <a name="return-value"></a>戻り値

**種類**: [GridEntity](../gridentity.md)

## <a name="remarks"></a>備考

`gridRowData` オブジェクトを取得するには、「[GridRowData](../gridrowdata.md)」を参照してください。 


---
title: モデル駆動型アプリの getTotalRecordCount (クライアント API 参照)| MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: 8305f0cb-9959-4429-a721-a864ade4cd35
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="gettotalrecordcount-client-api-reference"></a>getTotalRecordCount (クライアント API 参照)



[!INCLUDE[./includes/getTotalRecordCount-description.md](./includes/getTotalRecordCount-description.md)]

- Outlook 用 Dynamics 365 クライアントがサーバーに接続していないときは、この値は、ユーザーがオフラインで取得したレコードに限定されます。
- Dynamics 365 モバイル クライアントの場合、このメソッドは、サブグリッド内のレコードの数を返します。

## <a name="grid-types-supported"></a>サポートされるグリッドの種類

読み取り専用および編集可能なグリッド

## <a name="syntax"></a>構文

`var filteredRecordCount = gridContext.getGrid().getTotalRecordCount();`

## <a name="return-value"></a>戻り値

**種類**: 数値

**説明**: ビューのフィルター条件と一致するレコードの総数。

## <a name="remarks"></a>備考

`gridContext` を取得するには、「 [グリッド コンテキストの取得](../../grids.md#bkmk_gridcontext)」 を参照してください。

コレクション内のデータにアクセスするために使用できるメソッドの詳細については、「 [コレクション (クライアント API 参照)](../../collections.md) 」 を参照してください。


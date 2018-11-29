---
title: モデル駆動型アプリの getUrl (クライアント API 参照)| MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: f2023d7d-5877-4436-abe6-e81ca68b8ec0
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="geturl-client-api-reference"></a>getUrl (クライアント API 参照)



[!INCLUDE[./includes/getUrl-description.md](./includes/getUrl-description.md)]

## <a name="grid-types-supported"></a>サポートされるグリッドの種類

読み取り専用および編集可能なグリッド

## <a name="syntax"></a>構文

`gridContext.getUrl(client);`

## <a name="parameter"></a>パラメーター

|Name|種類​​|必須出席者|内容|
|--|--|--|--|
|クライアント|数値|No|クライアントの種類を示します。 次のいずれかの値を指定できます。<br/>0: ブラウザー<br/>1: モバイル アプリケーション|

## <a name="return-value"></a>戻り値

**種類**: 文字列

**説明**: 現在のグリッド コントロール の URL。

## <a name="remarks"></a>備考

 `gridContext`を取得するには、 [グリッド コンテキストの取得](../../grids.md#bkmk_gridcontext)を参照してください。




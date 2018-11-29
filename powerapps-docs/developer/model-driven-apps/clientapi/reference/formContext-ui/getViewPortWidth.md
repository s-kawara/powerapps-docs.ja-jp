---
title: モデル駆動型アプリの getViewPortWidth (クライアント API 参照)| MicrosoftDocs
ms.date: 10/31/2018
ms.service: crm-online
ms.topic: reference
applies_to: Dynamics 365 (online)
ms.assetid: e19af732-01e8-4853-b81c-40d79192cea2
author: KumarVivek
ms.author: kvivek
manager: amyla
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="getviewportwidth-client-api-reference"></a>getViewPortWidth (クライアント API 参照)



[!INCLUDE[./includes/getViewPortWidth-description.md](./includes/getViewPortWidth-description.md)]

ビューポートは、フォームデータが含まれているページの領域です。 これは、フォームの本文に対応し、ページのナビゲーション、ヘッダー、フッター、フォーム アシスタント領域は含みません。

## <a name="syntax"></a>構文

`formContext.ui.getViewPortWidth();`

## <a name="return-value"></a>戻り値

**種類**: 数値

**説明**: ビューポートのピクセル単位の幅。 


### <a name="related-topics"></a>関連トピック

[getViewPortHeight](getViewPortHeight.md)

[formContext.ui](../formContext-ui.md)

[formContext](../../clientapi-form-context.md)


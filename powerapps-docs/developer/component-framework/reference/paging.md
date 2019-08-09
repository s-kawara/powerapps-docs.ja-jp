---
title: ページング | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 12891e96-972c-4289-bbde-2bc261cd1f12
---

# <a name="paging"></a>ページング

[!INCLUDE[cc-beta-prerelease-disclaimer](../../../includes/cc-beta-prerelease-disclaimer.md)]

[!INCLUDE [paging-description](includes/paging-description.md)]

## <a name="properties"></a>プロパティ

## <a name="totalresultcount"></a>totalResultCount

現在のクエリに対するサーバー上の結果の合計。

**種類**: `number`

## <a name="hasnextpage"></a>hasNextPage

結果セットを後方にページングできるかどうか。

**種類**: `boolean`

## <a name="haspreviouspage"></a>hasPreviousPage

結果セットを後方にページングできるかどうか。

**種類**: `boolean`

## <a name="methods"></a>メソッド

|方法 | 説明 |
| ------|-------------|
|[loadNextPage](paging/loadnextpage.md)|[!INCLUDE [loadnextpage-description](paging/includes/loadnextpage-description.md)]|
|[loadPreviousPage](paging/loadpreviouspage.md)|[!INCLUDE [loadpreviouspage-description](paging/includes/loadpreviouspage-description.md)]|
|[リセット](paging/reset.md)|[!INCLUDE [reset-description](paging/includes/reset-description.md)]|
|[setPageSize](paging/setpagesize.md)|[!INCLUDE [setpagesize-description](paging/includes/setpagesize-description.md)]|


### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークの API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../overview.md)
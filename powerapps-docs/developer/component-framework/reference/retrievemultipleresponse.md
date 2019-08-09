---
title: RetrieveMultipleResponse | Microsoft Docs
description: null
keywords: null
ms.author: nabuthuk
manager: kvivek
ms.date: 04/23/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 08ea66d3-b4af-44af-a3ae-cb2ebad043e8
---

# <a name="retrievemultipleresponse"></a>RetrieveMultipleResponse

[!INCLUDE[cc-beta-prerelease-disclaimer](../../../includes/cc-beta-prerelease-disclaimer.md)]

## <a name="properties"></a>プロパティ

## <a name="entities"></a>エンティティ

各オブジェクトが属性とその値を含む取得されたエンティティレコードを表す、JSON オブジェクトの配列。

**種類**: `Entity[]`

## <a name="nextlink"></a>nextLink

取得されるレコードの件数が、要求内の 'maxPageSize' パラメーターで指定された値より多い場合、この属性はレコードの次のセットを返す URL を返します。

**種類**: `string`


### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネント フレームワークの API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネント フレームワークの概要](../overview.md)
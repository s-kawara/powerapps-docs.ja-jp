---
title: RetrieveMultipleResponse |Microsoft Docs
description: ''
keywords: ''
ms.author: nabuthuk
author: Nkrb
manager: kvivek
ms.date: 10/01/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 08ea66d3-b4af-44af-a3ae-cb2ebad043e8
ms.openlocfilehash: 0e5b2cad047bcf91b0c63e27c4a7ceb35c1ed538
ms.sourcegitcommit: 2a3430bb1b56dbf6c444afe2b8eecd0e499db0c3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/12/2019
ms.locfileid: "72341313"
---
# <a name="retrievemultipleresponse"></a>RetrieveMultipleResponse

## <a name="available-for"></a>利用可能な対象 

モデル駆動型アプリ

## <a name="properties"></a>プロパティ

### <a name="entities"></a>事業

JSON オブジェクトの配列。各オブジェクトは、属性とその値を含む取得されたエンティティレコードを表します。

**種類**: `Entity[]`

### <a name="nextlink"></a>nextLink

取得されるレコードの数が要求の `maxPageSize` パラメーターで指定された値を超える場合、この属性は、次のレコードのセットを返す URL を返します。

**種類**: `string`


### <a name="related-topics"></a>関連トピック

[PowerApps コンポーネントフレームワーク API リファレンス](../reference/index.md)<br/>
[PowerApps コンポーネントフレームワークの概要](../overview.md)
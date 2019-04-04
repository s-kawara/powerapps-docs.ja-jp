---
title: 開発者:Common Data Service でメタデータを使用する場合のベスト プラクティスとガイダンス | Microsoft Docs
description: PowerApps の Common Data Service でメタデータを使用する場合の開発者向けベスト プラクティスとガイダンスです。
services: ''
suite: powerapps
documentationcenter: na
author: jowells
manager: austinj
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/12/2018
ms.author: jowells
search.audienceType:
- developer
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: 35e07c87e515759a6e61a0c0a027c190b11bef53
ms.sourcegitcommit: 5b2b70c3fc7bcba5647d505a79276bbaad31c610
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/22/2019
ms.locfileid: "58358014"
---
# <a name="best-practices-and-guidance-while-working-with-metadata-for-the-common-data-service"></a>Common Data Service でメタデータを使用する場合のベスト プラクティスとガイダンス

以下の一覧には、Common Data Service 内のメタデータのやり取りと使用に関するガイダンスとベスト プラクティスがすべて含まれています。


|ベスト プラクティス  |説明  |
|---------|---------|
|[公開済みのメタデータを取得する](retrieve-published-metadata.md)     |公開されていないメタデータを取得すると、要求自体の処理にオーバーヘッドが追加され、パフォーマンスが低下するだけでなく、要求元が予期しないメタデータが返される可能性もあります。         |
|[クエリ API 経由でエンティティに対して特定の列を取得する](retrieve-specific-columns-entity-via-query-apis.md)     |データを取得するために送信するクエリには、"すべての列" ではなく、クエリに関連する ColumnSet インスタンス内の特定の列を含めるようにします。         |

# <a name="see-also"></a>関連項目
[コードを使用してメタデータを操作する](../../metadata-services.md)<br />
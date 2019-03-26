---
title: '開発者: アプリ用 Common Data Service のメタデータに関する作業のベスト プラクティスおよびガイダンス | Microsoft Docs'
description: PowerApps のアプリ用 Common Data Service の開発者のための、メタデータに関する作業のベスト プラクティスおよびガイダンス
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
---

# <a name="best-practices-and-guidance-while-working-with-metadata-for-the-common-data-service-for-apps"></a>アプリ用 Common Data Service のメタデータに関する作業のベスト プラクティスおよびガイダンス

下の一覧では、アプリ用 Common Data Service 内でのメタデータとの対話および使用に関するすべてのガイダンスとベスト プラクティスを示しています。


|ベスト プラクティス  |説明  |
|---------|---------|
|[公開メタデータの取得](retrieve-published-metadata.md)     |非公開メタデータを取得すると、要求自体の処理にオーバーヘッドが追加され、処理が遅くなるだけでなく、要求者が予期しないメタデータを返す可能性もあります。         |
|[クエリ API によってエンティティの特定の列を取得](retrieve-specific-columns-entity-via-query-apis.md)     |データを取得するために送信されたクエリには、All Columns ではなく、クエリに関連付けられている ColumnSet のインスタンス内の特定の列を含める必要があります。         |

# <a name="see-also"></a>関連項目
[コードを使用してメタデータを扱う](../../metadata-services.md)<br />
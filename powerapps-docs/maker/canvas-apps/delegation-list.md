---
title: キャンバス アプリ内の委任可能なデータ ソース | Microsoft Docs
description: キャンバス アプリ内でサポートされるすべての委任可能なデータ ソースの一覧
author: lancedMicrosoft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: anneta
ms.date: 08/15/2017
ms.author: lanced
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 98931d4692a61839e0530682bd2d40258c07b7df
ms.sourcegitcommit: 429b83aaa5a91d5868e1fbc169bed1bac0c709ea
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/24/2018
ms.locfileid: "42825765"
---
# <a name="delegable-data-sources-in-canvas-apps"></a>キャンバス アプリ内の委任可能なデータ ソース
[委任](delegation-overview.md)に関する記事で詳しく説明しているように、委任とは、データをキャンバス アプリに移動してローカルで処理するのではなく、PowerApps からデータ ソースにデータの処理が委任されることです。

委任は、表形式のデータ ソースでのみサポートされています。 次の一覧には、表形式のデータ ソースと委任がサポートされているかどうかを示しています。詳細については、次のセクションを参照してください。

* Common Data Service - **サポート**
* SharePoint - **サポート**
* SQL Server - **サポート**
* Dynamics 365 - **サポート**
* Salesforce - **サポート**
* Dynamics 365 for Operations - 未サポート
* Dynamics 365 for Financials - 未サポート
* Dynamics NAV - 未サポート
* Google シート - 未サポート

その他の表形式のデータ ソースと委任のサポートについては、継続的に追加されます。

このドキュメントでは、データ ソースごとにサポートされている委任の現在の状態を示します。

## <a name="prerequisites"></a>前提条件

* 「[委任について](delegation-overview.md)」の内容を理解しておく

## <a name="list-of-data-sources-and-supported-delegation"></a>データ ソースとサポートされる委任の一覧
このデータ ソースおよび委任可能な関数と述語の一覧は、PowerApps における現在の委任のサポート状態を反映するために定期的に更新されます。

### <a name="top-level-delegable-functions"></a>最上位の委任可能な関数

| &nbsp; | Common Data Service | SharePoint | SQL Server | Dynamics 365 | Salesforce |
| --- | --- | --- | --- | --- | --- |
| Average |いいえ |いいえ |はい |いいえ |いいえ |
| フィルター |はい |はい |はい |はい |はい |
| LookUp |はい |はい |はい |はい |はい |
| 最大 |いいえ |いいえ |はい |いいえ |いいえ |
| Min |いいえ |いいえ |はい |いいえ |いいえ |
| Search |はい<sup>1</sup> |いいえ |はい |はい |はい |
| 並べ替え |はい |はい |はい |はい |はい |
| SortByColumns |はい |はい |はい |はい |はい |
| Sum |いいえ |いいえ |はい |いいえ |いいえ |

<sup>1</sup>文字列フィールドのみ

### <a name="filter-and-lookup-delegable-predicates"></a>Filter および LookUp の委任可能な述語

| &nbsp; | Common Data Service | SharePoint | SQL Server | Dynamics 365 | Salesforce |
| --- | --- | --- | --- | --- | --- |
| Not |はい |いいえ |はい |はい |はい |
| IsBlank |いいえ |いいえ |はい |はい |いいえ |
| TrimEnds |いいえ |いいえ |はい |いいえ |いいえ |
| Len |いいえ |いいえ |はい |いいえ |いいえ |
| +、- |いいえ |いいえ |はい |いいえ |いいえ |
| <、<=、=、<>、>、>= |はい |はい (= のみ) |はい |はい |はい |
| And (&&)、Or (&#124;&#124;)、Not (!) |はい<sup>2</sup> |はい (Not(!) 以外) |はい |はい |はい |
| in |いいえ |いいえ |はい |いいえ |はい |
| StartsWith |いいえ |はい |いいえ |いいえ |いいえ |

<sup>2</sup>演算子のみ。 And/Or/Not 関数は委任されません。

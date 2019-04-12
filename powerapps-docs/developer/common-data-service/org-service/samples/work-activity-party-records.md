---
title: 'サンプル: 活動関係者レコードの操作方法 (Common Data Service) | Microsoft Docs'
description: このサンプルは、活動関係者レコードの使用方法を示します。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: samples
author: brandonsimons
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="sample-work-with-activity-party-records"></a>サンプル: 活動関係者レコードの操作方法

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/sample-work-activity-party-records -->

このサンプル コードは、活動関係者レコードの使用方法を示します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/ActivityPartyRecords) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

このサンプルでは、活動関係者レコードを操作するためにいくつかのサンプル データを作成します。 

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
1. このサンプルに必要となる 3 つの取引先担当者レコードを作成します。


### <a name="demonstrate"></a>使用方法

1. [セットアップ](#setup) で作成された取引先担当者レコードを取得します。 
2. 各取引先担当者の活動関係者レコードを作成します。
3. さらにレター活動を作成し、それぞれの活動関係者エンティティに**から**および**へ**フィールドを設定します。

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) 中に作成されたレコードを削除するオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。

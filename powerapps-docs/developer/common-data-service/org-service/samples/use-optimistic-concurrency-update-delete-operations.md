---
title: 'サンプル: 更新および削除の操作でオプティミスティック同時実行を使用する (Common Data Service) | Microsoft Docs'
description: このサンプルは、オペレーションの更新プログラムおよび削除でオプティミスティック同時実行を使用する方法を示します。
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
# <a name="sample-use-optimistic-concurrency-with-update-and-delete-operations"></a>サンプル: オペレーションの更新プログラムおよび削除でオプティミスティック同時実行を使用する

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/org-service/sample-use-optimistic-concurrency-update-delete-operations -->

このサンプルは、オペレーションの更新プログラムおよび削除でオプティミスティック同時実行を使用する方法を示します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/OptimisticConcurrency) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]


## <a name="what-this-sample-does"></a>このサンプルの概要

`UpdateRequest` クラスは、既存のレコードを更新する必要があるデータが含まれているシナリオで使用するためのものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルは何をするか](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います:

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
1. `Account` メソッドは取引先企業のレコードを作成します。

### <a name="demonstrate"></a>使用方法

1. [セットアップ](#setup)で作成された取引先企業レコードを取得します。
1. `creditlimit` 属性を増加して取引先企業レコードを更新します。
1. `UpdateRequest` メソッドは、行バージョンの一致を確認してリクエストの同時実行の動作を設定します。

### <a name="clean-up"></a>クリーンアップ

1. サンプルで作成されたすべてのデータを削除するためのオプションを表示します。

サンプルで作成されるデータを検証する場合、削除は任意です。 手動でデータを削除することで同じ結果を得られます。

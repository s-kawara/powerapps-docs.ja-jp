---
title: 'サンプル: 目標を追跡するユーザー ロールアップ クエリ (Common Data Service) | Microsoft Docs'
description: このサンプルはロールアップ クエリを使用して目標を追跡する方法を示します。
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
# <a name="sample-use-rollup-queries-to-track-goals"></a>サンプル: ロールアップ クエリを使用して目標を追跡する

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/sample-use-rollup-queries-track-goals -->

このサンプルは、ロールアップ クエリを使用して目標を追跡する方法を示します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/QueriesTrackGoals) からダウンロードできます。

このサンプルではシステムに存在しない追加のユーザーが 3 人必要です。 次に **そのまま** 示すように、必要になった 3 人のユーザーを **Office 365**で手動で作成します。 `yourorg` を組織名で置換します。

**名**: Nancy<br/>
**姓**: Anderson<br/>
**セキュリティ ロール**: Salesperson<br/>
**ユーザー名**: nanderson@yourorg.onmicrosoft.com<br/>

**名**: David<br/>
**姓**: Bristol<br/>
**セキュリティ ロール**: Salesperson<br/>
**ユーザー名**: dbristol@yourorg.onmicrosoft.com<br/>

**名**: Kevin<br/>
**姓**: Cook<br/>
**セキュリティ ロール**: SalesManager<br/>
**ユーザー名**: kcook@yourorg.onmicrosoft.com<br/>

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

このサンプルは、ロールアップ クエリを使用して目標を追跡する方法を示します。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルは何をするか](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います:

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
2. **Office 365**で手動で作成された、セールス マネージャーおよび2名のセールス担当者を取得します。
3. `SalesOrder` レコードをサポートするためにレコードを作成します。
4. サンプルの新しい出荷単位一覧を作成します。
5. 新しい出荷単位一覧を作成した際に自動的に作成される、既定の出荷単位 ID を取得します。
6. `Product` はサンプルに必要ないくつかの製品を作成します。
7. `PriceLevel` は新しい価格表を作成します。
8. `ProductPriceLevel` は最初の製品の価格表品目を作成して大口値引きを適用します。
9. 受注の潜在顧客 ID に対する取引先企業レコードを作成します。 
10. `SalesOrderDetails` は負の値で上書きされた価格とともに受注に製品を追加します。

### <a name="demonstrate"></a>使用方法

1. 指標を作成し、指標の種類を `Amount` に設定します。そして金額データの種類を `Money` に設定します。
2. `RollupField` は実際の合計の目標であるロールアップ フィールドを作成します。
3. `GoalRollupQuery` は、最初のセールス担当者が受け持つエリア (郵便番号: 60661) での受注のうち $1000 を超える値を検索するロールアップ クエリを作成します。 
4. 2 つの目標を作成します。1 つの親目標と、1 つの子目標です。
5. `RecalculateRequest` は目標のロールアップを計算します。 

### <a name="clean-up"></a>クリーンアップ

1. [セットアップ](#setup)で作成されたサンプル データを削除するオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。

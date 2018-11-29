---
title: 'サンプル: ターゲット収益に対するカスタム期間の目標データのロールアップ (Common Data Service for Apps) | Microsoft Docs'
description: このサンプルは、対象の売り上げに対するカスタム期間の目標のデータをロールアップする方法を示します。
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
# <a name="sample-rollup-goal-data-for-a-custom-period-against-the-target-revenue"></a>サンプル: カスタム期間の目標データを、対象の売上に対してロールアップする

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/sample-rollup-goal-data-custom-period-target-revenue -->

このサンプルは、対象の売り上げに対するカスタム期間の目標のデータをロールアップする方法を示します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/RollupGoalData) からダウンロードできます。

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

このサンプルは、対象の売り上げに対するカスタム期間の目標のデータをロールアップする方法を示します。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織のバージョンをチェックします。
2. **Office 365** で手動で作成された、セールス マネージャーおよび 2 名のセールス担当者を取得します。
3. 抜き取り出荷単位一覧を作成し、既定の出荷単位 ID を取得します。 
4. いくつかの製品および新しい値引き表を作成します。
5. `PriceLevel` は、価格表を作成します。
6. `ProductPriceLevel` は最初の製品の価格表品目を作成して大口値引きを適用します。
7. 営業案件の潜在顧客 ID に対する取引先企業レコードを作成します。
8. ユーザーが指定した売上見込みと共に新しい営業案件を作成します。
9. カタログ製品を作成して、価格表を上書きします。
10. 調整値引きが適用された新しいリスト外提案製品を作成します。

### <a name="demonstrate"></a>使用方法

1. 指標を作成し、金額のデータの種類を `Money` に設定します。
2. 予想される値と実績値を対象にするロールアップ フィールドを作成します。
3. `GoalRollupQuery` は、目標ロールアップ クエリを作成し、営業担当者の領域で営業案件を見つけます。 
4. 3 つの目標を作成します。1 つの親目標と、2 つの子目標です。
5. `RecalculateRequest` は目標のロールアップを計算します。 

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup)で作成されたサンプル データを削除するオプションを表示します。

    サンプルで作成されたエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除しても同じ結果を得られます。

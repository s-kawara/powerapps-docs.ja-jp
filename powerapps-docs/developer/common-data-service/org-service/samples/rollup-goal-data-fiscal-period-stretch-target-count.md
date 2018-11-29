---
title: 'サンプル: 件数の拡大対象に対する会計期間の目標の合計のロールアップ (Common Data Service for Apps) | Microsoft Docs'
description: このサンプルでは、件数の拡大対象に対する会計期間の目標データのロールアップ方法を示します。
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
# <a name="sample-rollup-goal-data-for-a-fiscal-period-against-the-stretch-target-count"></a>サンプル: 件数の拡大対象に対する会計期間の目標データのロールアップ

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/sample-rollup-goal-data-fiscal-period-stretch-target-count -->

このサンプルでは、完了した電話の件数を表す拡大対象件数に対して会計期間の目標データをロールアップする方法を示しています。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/GoalDataForFiscalYear) からダウンロードできます。

このサンプルでは、システムに存在しない追加のユーザーが必要です。 次に **そのまま** 示すように、必要になった 3 人のユーザーを **Office 365**で手動で作成します。 `yourorg` を組織名で置換します。

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

このサンプルでは、完了した電話の件数を表す拡大対象件数に対して会計期間の目標データをロールアップする方法を示しています。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織のバージョンをチェックします。
2. **Office 365**で手動で作成された、セールス マネージャーおよび2名のセールス担当者を取得します。
3. サンプル用に `PhoneCall` のレコードおよびサポートする取引先企業レコードを作成します。
4. 電話の**差出人**フィールドの ActivityParty を作成します。
5. オープンな電話を作成します。
6. 最初の電話をクローズし、2 番目の電話を作成します。
7. 2 番目の電話をクローズします。

### <a name="demonstrate"></a>使用方法

1. 指標を作成し、指標の種類を **カウント** に設定して、拡大追跡を有効にします。
2. 完了した (受信した) 電話の目標であるロールアップ フィールドを作成します。
3. `GoalRollupQuery` は目標ロールアップ クエリを作成し、受信および送信されるクローズな電話を検索します。 
4. 3 つの目標を作成します。1 つの親目標と、2 つの子目標です。
5. `RecalculateRequest` は目標のロールアップを計算します。 

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup)で作成されたサンプル データを削除するオプションを表示します。

    サンプルで作成されたエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除しても同じ結果を得られます。

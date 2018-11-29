---
title: 'サンプル: 目標の合計件数を上書きして目標をクローズする (アプリ用Common Data Service) | Microsoft Docs'
description: このサンプルは、目標の合計件数を上書きして目標をクローズする方法を示します。
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
# <a name="sample-override-goal-total-count-and-close-the-goal"></a>サンプル: 目標の合計件数を上書きして目標をクローズする

このサンプルは、目標の合計件数を上書きして目標をクローズする方法を示します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/OverrideGoalTotal) からダウンロードできます。

このサンプルでは、システムに存在しない追加のユーザーが必要です。 次に**示したとおりに**、必要になったユーザーを **Office 365**で手動で作成します。 `yourorg` を組織の `OrgName` で置換します。

**名**: Samantha<br/>
**姓**: Smith<br/>
**セキュリティ ロール**: マーケティング マネージャー<br/>
**ユーザー名**: ssmith@yourorg.onmicrosoft.com<br/>

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要


このサンプルは、目標の合計件数を上書きして目標をクローズする方法を示します。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織のバージョンをチェックします。
2. **Office 365**で手動で作成された、セールス マネージャー ユーザーを取得します。
3. サンプル用に `PhoneCall` のレコードおよびサポートする取引先企業レコードを作成します。
4. 電話の差出人フィールドの ActivityParty を作成します。
5. オープンな電話を作成します。
6. 最初の電話をクローズし、2 番目の電話を作成します。
7. 2 番目の電話をクローズします。

### <a name="demonstrate"></a>使用方法

1. 指標を作成し、指標の種類を `count` に設定します。そして `IsAmount` を false に設定します。
2. `RollupFields` は完了した (受信した) 電話の目標であるロールアップ フィールドを作成します。
3. `GoalRollupQuery` は目標ロールアップ クエリを作成し、受信および送信されるクローズな電話を検索します。 
4. 目標を作成してオープンな受信される電話を追跡します。
5. `RecalculateRequest` は目標のロールアップを計算します。 
6. 目標の実績値と進行中の値を上書きします。
7. `goal.IsOverridden =true` と設定すると、ロールアップ値が次回の再計算操作時にシステムが計算した値で上書きされるのを防ぐことができます。

### <a name="clean-up"></a>クリーンアップ

1. [セットアップ](#setup)で作成されたサンプル データを削除するオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。

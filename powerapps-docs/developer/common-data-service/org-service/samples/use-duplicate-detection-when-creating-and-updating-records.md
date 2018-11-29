---
title: 'サンプル: レコードを作成および更新する際に重複データ検出を使用する (アプリ用 Common Data Service) | Microsoft Docs'
description: このサンプルではエンティティ レコードの作成および更新のために、重複データ検出を呼び出す方法を説明します。
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
# <a name="sample-use-duplicate-detection-when-creating-and-updating-records"></a>サンプル: レコードの作成および更新時の重複データ検出の使用

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/org-service/sample-use-duplicate-detection-when-creating-and-updating-records --> このサンプルではエンティティ レコードの作成および更新のために、重複データ検出を呼び出す方法を説明します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/UseDuplicatedetectionforCRUD) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]


## <a name="what-this-sample-does"></a>このサンプルの概要

`DuplicateRule` メソッドは重複データ検出ルールを作成する必要があるデータが含まれているシナリオで使用するためのものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルは何をするか](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います:

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
1. `Account` メソッドは取引先企業のレコードを作成します。 
1. `DuplicateRule` メソッドは重複データ検出ルールを作成します。
1. `DuplicateRuleCondition` メソッドは重複データ検出ルールの条件を作成します。
1. `PublishDuplicateRuleRequest` メソッドは既に作成された重複データ検出ルールを発行します。 発行操作が完了するまで待機する必要があるため、ルールの状態を `Published` になるまでポーリングし続けます。

### <a name="demonstrate"></a>実際にやってみます
1. `Account` メソッドは取引先企業のレコードを作成します。 
1. `CreateRequest` メソッドは重複データ検出の回避により操作を作成します。
1. `UpdateRequest` メソッドは新しい取引先企業番号で取得した取引先企業レコードを更新します。

### <a name="clean-up"></a>クリーンアップ

1. サンプルで作成されたすべてのデータを削除するためのオプションを表示します。

サンプルで作成されるデータを検証する場合、削除は任意です。 手動でデータを削除することで同じ結果を得られます。

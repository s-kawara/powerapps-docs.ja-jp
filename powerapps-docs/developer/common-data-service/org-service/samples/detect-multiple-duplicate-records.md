---
title: 'サンプル: 複数の重複レコードを検出する (Common Data Service) | Microsoft Docs'
description: このサンプルでは、特定のエンティティの種類の複数の重複レコードを検出および記録する方法を説明します。
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
# <a name="sample-detect-multiple-duplicate-records"></a>サンプル: 複数の重複レコードを検出する

このサンプルでは、特定のエンティティの種類の複数の重複レコードを検出および記録する方法を説明します。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`BulkDetectDuplicatesRequest` メッセージは、複数の重複レコードを検出して記録する非同期のシステム ジョブを送信するために必要なデータを含むシナリオで使用するためのものです。 サンプルは[ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/DetectMultipleDuplicateRecords) からダウンロードできます。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
1. `CreateRequiredRecords` クラスはサンプルの重複エンティティ レコードを作成します。
1. `DuplicateRule` メソッドは重複データ検出ルールを作成します。
1. `DuplicateRuleCondition` メソッドは、重複レコードの検出の重複データ検出レコードの条件を作成します。
1. `PublishDuplicateRuleRequest` メソッドは重複データ検出ルールを公開します。
1. 公開が完了する前に `PublishDuplicateRuleRequest` が返されるので、非同期ジョブの状態を `Completed` になるまで取得し続けます。

### <a name="demonstrate"></a>使用方法

1. `BulkDetectDuplicatesRequest` メソッドは BulkDetectDuplicatesRequest オブジェクトを作成する

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) で作成されたレコードを削除するオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。


---
title: 'サンプル: 監査エンティティのデータ変更 (アプリ用 Common Data Service) | MicrosoftDocs'
description: このサンプルでは、エンティティ データの変更を監査する方法を紹介します
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
# <a name="sample-audit-entity-data-changes"></a>サンプル: エンティティのデータ変更を監査する

このサンプルでは、エンティティとその属性に対する監査を有効または無効にする方法、監査対象エンティティのデータ変更履歴を取得する方法、および監査レコードを削除する方法を説明します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/AuditEntityData) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法
[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`RetrieveRecordChangeHistoryRequest` メッセージは、エンティティに関する監査履歴を検出する必要があるデータが含まれているシナリオで使用するためのものです。


## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
2. サンプルの取引先企業エンティティを作成します。

### <a name="demonstrate"></a>使用方法

1. システム ユーザー レコードからの組織の ID を取得します。
2. 組織での監査およびサンプルの取引先企業エンティティでの監査を有効化します。
3. `RetrieveRecordChangeHistoryRequest` では、取引先企業エンティティに対する監査履歴が取得され、結果が表示されます。

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) で作成されたサンプル データを削除するためのオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。

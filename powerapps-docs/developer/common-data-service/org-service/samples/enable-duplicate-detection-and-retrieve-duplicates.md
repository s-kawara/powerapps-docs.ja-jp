---
title: 'サンプル: 重複データ検出の有効化および重複データの取得 (Common Data Service) | Microsoft Docs'
description: このサンプルでは、重複データ検出機能を有効にして重複レコードを取得する方法を示します。
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
# <a name="sample-enable-duplicate-detection-and-retrieve-duplicates"></a>サンプル: 重複データ検出を有効にし、重複を取得する

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/org-service/sample-enable-duplicate-detection-and-retrieve-duplicates -->

このサンプルでは、重複データ検出機能を有効にして重複レコードを取得する方法を示します。 サンプルは、[こちら](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/EnableDuplicateDetection) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`IsDuplicateDetectionEnabled` プロパティは、組織およびエンティティの重複データ検出ルールを有効にするシナリオで使用するものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
1. `Account` メソッドでは、重複レコードを取得するためにアカウント レコードを作成します。
1. `RetrieveDuplicateRequest` メソッドは、重複レコードを取得します。 
1. `EnableDuplicateDetectionForOrg` クラスでは、組織の重複データ検出を有効にします。 
1. 重複データ検出を有効にするには、`IsDuplicateDetectionEnabled = true` と設定します。
1. `RetrieveEntityRequest` メソッドは、エンティティ メタデータを取得します。 
1. `IsDuplicateDetectionEnabled = true` と設定して、重複データ検出フラグを更新します。
1. `UpdateEntityRequest` にて、重複データ検出を使用してエンティティを更新し、`true` と設定します。

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) で作成されたレコードを削除するオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。

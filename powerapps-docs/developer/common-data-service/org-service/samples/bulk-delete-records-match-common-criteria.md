---
title: 'サンプル: 共通の条件に合致するレコードを一括して削除する (Common Data Service) | Microsoft Docs'
description: このサンプルは、共通の条件に一致するレコードを一括削除する方法を示します
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: brandonsimons
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="sample-bulk-delete-records-that-match-common-criteria"></a>サンプル: 共通の条件に合致するレコードを一括して削除する

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/sample-bulk-delete-records-match-common-criteria -->

このサンプルは、一般的な条件に一致するレコードを一括削除する方法を示しています。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/BulkDeleteMatchCriteria) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`BulkDeleteRequest` メッセージは、一括削除要求を作成する必要があるデータが含まれているシナリオで使用するためのものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
2. サンプルの取引先企業レコードを作成します。
3. 一括削除の操作が完了した後に、システム ユーザーの電子メールの送信先のクエリ。
3. `BulkDeleteRequest` では一括削除プロセスを作成し、要求プロパティを設定します。
4. `InspectBulkDeleteOperation`メソッドでは、作成された `BulkDeleteOperation` に関する情報を確認および表示します。
5. `RetrieveBulkDeleteOperation` メソッドは、`BulkDeleteOperation` を取得します。

### <a name="demonstrate"></a>使用方法

1. 標準の電子メール テンプレートが存在するかどうか確認します。
1. `PerformBulkDelete` メソッドでは、メインの一括削除操作が実行されます。

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) で作成されたサンプル データを削除するためのオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。

---
title: 'サンプル: 電子メールを一括送信して結果を監視する (Common Data Service) | Microsoft Docs'
description: このサンプルでは、電子メールを一括送信して結果を監視する方法を説明します
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
# <a name="sample-send-bulk-email-and-monitor-results"></a>サンプル: 電子メール広告を送信して結果を監視する

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/sample-send-bulk-email-monitor-results -->

このサンプルは、電子メールを <xref:Microsoft.Crm.Sdk.Messages.SendBulkMailRequest> を使用して一括送信し、`AsyncOperation` エンティティからレコードを取得することにより結果を監視する方法を示します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/BulkEmail) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`SendBulkMailRequest` メッセージは、電子メールを送信するシナリオで使用するためのものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします
1. `Contact` メソッドは、このサンプル用の 2 つの取引先担当者レコードを作成します。

### <a name="demonstrate"></a>使用方法

1. 送信者として使用するシステム ユーザーを取得します。
2. 一括電子メール要求に対して追跡 ID を設定します。
3. 一括操作のクエリ式を作成し、電子メールの一覧で取引先担当者を取得します。
4. 関連 ID を設定し、一括電子メール要求を実行します。
5. 一括電子メール非同期操作を取得し、ポーリングによって監視します。

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) で作成されたレコードを削除するオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。

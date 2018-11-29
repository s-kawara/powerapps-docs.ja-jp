---
title: 'サンプル: 通貨為替レートを取得する (Common Data Service for Apps) | Microsoft Docs'
description: このサンプルでは、新しい通貨を作成して通貨為替レートを取得および表示する方法を示します。
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
# <a name="sample-retrieve-currency-exchange-rate"></a>サンプル: 通貨為替レートを取得する

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/sample-retrieve-currency-exchange-rate -->

このサンプルは、新規の通貨の作成方法と、組織の基本通貨を基準とした通貨為替レートを取得および表示する方法を示します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/RetrieveCurrencyExchangeRate) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`RetrieveExchangeRateRequest` メッセージは、為替レートを取得するために必要なデータが含まれているシナリオで使用するためのものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。 
2. `TransactionCurrency` メソッドは、サンプル用の新しい通貨を作成します。

### <a name="demonstrate"></a>使用方法

1. `RetrieveExchangeRateRequest` メッセージは、組織の基本通貨に対する為替レートを取得します。

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup)で作成されたサンプル データを削除するオプションを表示します。
    サンプルで作成されたエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除しても同じ結果を得られます。

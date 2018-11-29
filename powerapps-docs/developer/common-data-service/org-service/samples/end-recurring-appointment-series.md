---
title: 'サンプル: 定期的な予定の終了 (Common Data Service for Apps) | Microsoft Docs'
description: サンプルでは、一連の定期的な予定を終了する方法を表示
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
# <a name="sample-end-a-recurring-appointment-series"></a>サンプル: 定期的な予定の系列を終了する

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/sample-end-recurring-appointment-series -->

[DeleteOpenInstancesRequest](https://docs.microsoft.com/en-us/dotnet/api/microsoft.crm.sdk.messages.deleteopeninstancesrequest?view=dynamics-general-ce-9) メッセージを使用して、サンプルでは定期的な一連の予定を終了する方法を説明します。 サンプルは、[こちら](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/EndRecurringAppointment) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`DeleteOpenInstanceRequest` メッセージは、`Open` 状態である定期的な予定マスターのインスタンスを削除する必要のあるデータを含むシナリオで使用するためのものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
2. 可能な定期的パターン値、可能な日付の値および定期的ルール パターンの終了型値を定義する匿名型を定義します。
3. サンプルに、必要な新しい定期的な予定を作成します。

### <a name="demonstrate"></a>使用方法

1. `RecurringAppointmentMaster` メッセージを使用して、[Setup](#setup) で作成された定期的な予定の系列を取得します。
2. `DeleteOpenInstanceRequest` メッセージを使用して、定期的な予定の系列を最後に発生したインスタンスの日付 w.r.t に終わらせます。 終了日の系列

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup)で作成されたサンプル データを削除するオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。

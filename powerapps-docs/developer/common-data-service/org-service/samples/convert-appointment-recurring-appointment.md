---
title: 'サンプル: 予定から定期的な予定へ変換する (アプリ用 Common Data Service) | Microsoft Docs'
description: このサンプルは 1 つの予定を一連の定期的な予定に変換する方法を説明します
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
# <a name="sample-convert-an-appointment-to-a-recurring-appointment"></a>サンプル: 予定から定期的な予定へ変換する

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/sample-convert-appointment-recurring-appointment -->

このサンプルは、[AddRecurrenceRequest](https://docs.microsoft.com/en-us/dotnet/api/microsoft.crm.sdk.messages.addrecurrencerequest?view=dynamics-general-ce-9) メッセージを使用して 1 つの予定を一連の定期的な予定に変換する方法を示しています。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/ConvertToRecurring) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`AddRecurrenceRequest` メッセージは、繰り返し情報を既存の予定に追加する必要があるデータが含まれているシナリオで使用するためのものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
1. 後に定期的な予定に変換されるサンプル予定を作成します。

### <a name="demonstrate"></a>使用方法

1. [セットアップ](#setup) クラスで作成される予定に追加される必要がある繰り返し情報を指定します。
2. 使用可能な定期パターン値と曜日の有効値も定義する、匿名型を定義します。
3. 定期ルール パターンおよび種類の有効値を定義する、匿名型を定義します。
4. `RecurringAppointmentMaster` は繰り返し情報を指定します。 
5. `AddRecurrence` メッセージは作成された予定を定期的な予定に変換します。

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup)で作成されたサンプル データを削除するオプションを表示します。 

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動で同じデータを削除しても同じ結果を得られます。

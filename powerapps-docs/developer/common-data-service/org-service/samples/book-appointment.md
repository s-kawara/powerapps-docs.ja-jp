---
title: 'サンプル: 予定の予約 (アプリ用 Common Data Service) | Microsoft Docs'
description: 'このサンプルは予定を予約またはスケジュールする方法を説明します。 '
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
# <a name="sample-book-an-appointment"></a>サンプル: 予定の予約

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/sample-book-appointment -->

このサンプルは [BookRequest](https://docs.microsoft.com/en-us/dotnet/api/microsoft.crm.sdk.messages.bookrequest?view=dynamics-general-ce-9) メッセージを使用して予定を予約またはスケジュールする方法を説明します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/BookAppointment) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`BookRequest` メッセージは、予定を予約またはスケジュールするシナリオで使用することを目的にしています。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
1. 現在のユーザー情報を取得し、ActivityParty インスタンスを作成します。

### <a name="demonstrate"></a>使用方法

1. [BookRequest](https://docs.microsoft.com/en-us/dotnet/api/microsoft.crm.sdk.messages.bookrequest?view=dynamics-general-ce-9) メッセージを使用して予定インスタンスを作成し、予定がスケジュールされたかどうかを検証します。

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) で作成されたレコードを削除するオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。

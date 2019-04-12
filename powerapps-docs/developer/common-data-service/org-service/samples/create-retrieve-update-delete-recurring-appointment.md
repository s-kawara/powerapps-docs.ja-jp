---
title: 'サンプル: CRUD の定期的な予定 (Common Data Service) | Microsoft Docs'
description: このサンプルは定期的な予定に関する CRUD 操作の実行方法を示します。
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
# <a name="sample-create-retrieve-update-and-delete-a-recurring-appointment"></a>サンプル: 定期的な予定を作成、取得、更新、および削除する

このサンプルでは、定期的な予定の系列を作成、取得、更新、および削除する方法を示します。 このサンプルでは、以下の共通メソッドを使用します。

- [IOrganizationService.Create](https://docs.microsoft.com/dotnet/api/microsoft.xrm.sdk.iorganizationservice.create?view=dynamics-general-ce-9)
- [IOrganizationService.Retrieve](https://docs.microsoft.com/dotnet/api/microsoft.xrm.sdk.iorganizationservice.retrieve?view=dynamics-general-ce-9)
- [IOrganizationService.Update](https://docs.microsoft.com/dotnet/api/microsoft.xrm.sdk.iorganizationservice.update?view=dynamics-general-ce-9)
- [IOrganizationService.Delete](https://docs.microsoft.com/dotnet/api/microsoft.xrm.sdk.iorganizationservice.delete?view=dynamics-general-ce-9)

サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/CRUDRecurringAppointment) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`IOrganizationService` メッセージは、組織のメタデータおよびデータにプログラムからアクセスする方法を提供するデータを含むシナリオで使用するものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。

### <a name="demonstrate"></a>使用方法

1. 可能な定期的パターン値、可能な曜日の値および定期的ルール パターンの終了型の値を定義する匿名型を定義します。 
1. `RecurringAppointmentMaster` メソッドでは、定期的な予定を作成します。
1. `QueryExpression` メソッドでは、新しく作成された定期的な予定を取得します。
1. `Update` メソッドでは、取得された定期的な予定に対する件名、 発生回数を 5 に、予定の間隔を 2 に更新します。


### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) で作成されたレコードを削除するオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。



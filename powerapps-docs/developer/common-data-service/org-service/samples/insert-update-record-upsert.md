---
title: 'サンプル: Upsert を使用したレコードの挿入または更新 (Common Data Service) | Microsoft Docs'
description: このサンプルは、Upsert メッセージを使用してレコードを挿入または更新する方法を示します。
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
# <a name="sample-insert-or-update-a-record-using-upsert"></a>サンプル: Upsert を使用してレコードを挿入または更新

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/sample-insert-update-record-upsert -->

このサンプル コードは、[UpsertRequest](https://docs.microsoft.com/dotnet/api/microsoft.xrm.sdk.messages.upsertrequest?view=dynamics-general-ce-9) メッセージを使用してレコードを挿入または更新する方法を示します。 サンプルは、[ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/InsertRecordUsingUpsert) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`UpsertRequest` メッセージは、レコードの更新または挿入を行う必要があるデータが含まれているシナリオで使用するためのものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
1. `sample_productcode` という名前の代替キーを持つ `sample_product` エンティティを作成するマネージド ソリューション (UpsertSample_1_0_0_0_managed.zip) をインポートします。 代替キーをサポートするインデックスが有効であることを確認します。

### <a name="demonstrate"></a>使用方法

1. `ProcessUpsert` メソッドは、`newsampleproduct.xml` 内のデータを処理して新しい製品を表し、新しく 13 レコードを作成します。
1. `ProcessUpsert` メソッドが二回目に呼び出されたとき、`updatedsampleproduct.xml` ファイル内のデータを処理して、以前に作成した製品の変更を表します。 
1. `UpsertRequest` メソッドは、6 つの更新されたレコードを作成します。 

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) で作成されたマネージド ソリューションを削除するためのオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。

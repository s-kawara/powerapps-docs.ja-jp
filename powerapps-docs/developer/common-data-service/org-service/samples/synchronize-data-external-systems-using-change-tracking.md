---
title: 'サンプル: 変更追跡システムを使用して外部システムとデータを同期する (Common Data Service for Apps) | Microsoft Docs'
description: このサンプルは、エンティティから変更を取得し、そのデータを外部システムと同期させる方法を示しています。
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
# <a name="sample-synchronize-data-with-external-systems-using-change-tracking"></a>サンプル: 変更の追跡を使用してデータを外部システムに同期

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/sample-synchronize-data-external-systems-using-change-tracking -->

このサンプル コードは、[RetrieveEntityChangesRequest](https://docs.microsoft.com/dotnet/api/microsoft.xrm.sdk.messages.retrieveentitychangesrequest) および [RetrieveEntityChangesResponse](https://docs.microsoft.com/dotnet/api/microsoft.xrm.sdk.messages.retrieveentitychangesresponse) クラスを使用して `RetrieveEntityChanges` メッセージを使用することで、エンティティから変更を取得し、データを外部システムと同期させる方法を示しています。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/Changetracking) からダウンロードできます。

このサンプルで説明されている機能の詳細については、「[変更の追跡を使用してデータを外部システムに同期](https://docs.microsoft.com/powerapps/developer/common-data-service/use-change-tracking-synchronize-data-external-systems)」を参照してください。
<!-- The link above won't work until the topic is published -->

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`RetrieveEntityChanges` メッセージは、外部システムからのデータが同期され、変更の追跡に使用する機能をデータの変更を検出して調整するために使用できるシナリオで使用するためのものです。

このシナリオを完全に複製するために必要な別個のシステムがないため、このサンプルでは、2 つの要求を実行してシナリオをシミュレートします。 次の要求までの間、2 番目の要求が時間の経過に伴って変更された内容に関するデータを返すように、一部のデータが変更されます。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. `sample_bookcode` という名前の代替キーを持つ `sample_book` エンティティを作成するマネージド ソリューション (ChangeTrackingSample_1_0_0_0_managed.zip) をインポートします。 代替キーをサポートするインデックスが有効であることを確認します
1. 最初の 10 個の sample_book エンティティ レコードは、エンティティに対する変更を追跡できるように作成されます。

### <a name="demonstrate"></a>使用方法

1. 初期要求を実行して、`DataToken` などの結果をキャッシュします。
1. [セットアップ](#setup)で作成されたレコードを更新する
1. 2 番目の要求を実行します。今回は、初期要求から取得された `DataToken` 値を使用して `DataVersion` を渡します。
1. 第 2 の要求により返されたエンティティの変更を表示する

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup)でインポートされる管理ソリューションを削除するオプションを表示します。これにより、`sample_book` エンティティとサンプルで作成されたすべてのデータが削除されます。

    サンプルで作成されたエンティティおよびデータを検証する場合、削除は任意です。 手動で `ChangeTrackingSample` を削除しても同じ結果を得られます。

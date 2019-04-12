---
title: 'サンプル: 作業するキュー アイテムの指定 (Common Data Service) | Microsoft Docs'
description: このサンプルはキュー アイテムを操作するユーザーの指定方法を示します
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
# <a name="sample-specify-a-queue-item-to-work-on"></a>サンプル: 作業するキュー アイテムの指定

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/sample-specify-queue-item-work-early-bound -->

このサンプルはキュー アイテムを操作するユーザーの指定するのに [PickFromQueueRequest](https://docs.microsoft.com/dotnet/api/microsoft.crm.sdk.messages.pickfromqueuerequest?view=dynamics-general-ce-9) を使用する方法を示します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/SpecifyQueueItem) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`PickFromQueueRequest` メッセージは、キュー アイテムをユーザーに割り当てて、オプションでキューからキュー アイテムを削除するために必要なデータが含まれているシナリオで使用するためのものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
2. `Queue` メソッドではプライベート キュー インスタンスが作成され、プロパティ値が設定されます。
3. `QueueItem` メソッドは、キュー アイテムの新しいインスタンスを作成し、プロパティを初期化します。

### <a name="demonstrate"></a>使用方法

1. `WhoAmIRequest` メソッドは、現在のユーザー情報を取得します。
1. `PickFromQueueRequest` メソッドは、操作するユーザーを指定するために既存のキュー アイテムのインスタンスを作成します。


### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) で作成されたサンプル データを削除するためのオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。

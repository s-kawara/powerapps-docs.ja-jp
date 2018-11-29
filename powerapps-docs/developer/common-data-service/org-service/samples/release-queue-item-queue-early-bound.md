---
title: 'サンプル: キューへのキュー アイテムの解放 (Common Data Service for Apps) | Microsoft Docs'
description: このサンプルは、ReleaseToQueueRequest メッセージの使用方法を示しています
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
# <a name="sample-release-a-queue-item-to-the-queue"></a>サンプル: キュー アイテムのキューへの解放

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/sample-release-queue-item-queue-early-bound
Couldn't each of the operations in this series of samples be added to just one sample?
 -->
 このサンプルは、[ReleaseToQueueRequest](https://docs.microsoft.com/en-us/dotnet/api/microsoft.crm.sdk.messages.releasetoqueuerequest?view=dynamics-general-ce-9) を使用して、ユーザーが作業しているキュー アイテムとそのユーザーの関連付けを解除し、キュー アイテムを解放してキューに戻す方法を示します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/ReleaseQueueItems) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`ReleaseToQueueRequest` メッセージは、キュー アイテムをキューの所有者に戻して他のユーザーが取得できるようにするために必要なデータが含まれているシナリオで使用するためのものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
2. `Queue` メッセージは、新しいキューを作成し、返された GUID を変数に保存します。
3. `QueueItem` メッセージは、キュー アイテムの新しいインスタンスを作成し、プロパティを初期化します。
4. `WhoAMIRequest` は、現在のユーザー情報を取得します。

### <a name="demonstrate"></a>使用方法

1. `ReleaseToQueueRequest` メッセージは、キュー アイテムからワーカーを削除し、ワーカーのキューからキューに入れられたオブジェクトを解放します。

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup)で作成されたサンプル データを削除するオプションを表示します。

    サンプルで作成されたエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除しても同じ結果を得られます。

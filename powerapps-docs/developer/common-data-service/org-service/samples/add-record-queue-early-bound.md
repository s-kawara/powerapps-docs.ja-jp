---
title: 'サンプル: レコードをキューに追加する (Common Data Service) | Microsoft Docs'
description: このサンプルはキューにレコードを追加する方法を示します。
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
# <a name="sample-add-a-record-to-a-queue"></a>サンプル: キューへのレコードの追加

このサンプルはキューにレコードを追加する方法を示します。 ソース キューと宛先キューを作成します。 レター活動をソース キューに追加してから、宛先キューに移動します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/RecordToQueue) からダウンロードできます。

このサンプルでは、システムに存在しない追加のユーザーが必要です。 **Office 365** でユーザーを手動で作成し、サンプルがエラーなしで実行されるようにします。 このサンプルでは、次に示す**現状有姿**でユーザー プロファイルを作成します。 

**名**: Kevin<br/>
**姓**: Cook<br/>
**セキュリティ ロール**: 営業課長<br/>
**ユーザー名**: kcook@yourorg.onmicrosoft.com<br/>

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`AddToQueueRequest` メッセージは、エンティティ レコードを元のキューから宛先キューに移動する必要があるデータが含まれているシナリオで使用するためのものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
2. `Queue` メソッドでは元のキューおよび宛先キューを作成し、変数で返された GUID を保存します。
3. レター エンティティを作成します。
4. `AddToQueueRequest` メソッドではエンティティ レコードをキューに追加し、このサンプルでは文字を最初のキューに関連付けます。
5. キュー アイテムをユーザー キューに割り当てるため、**Office 365** で手動で作成されたユーザーを取得します。

### <a name="demonstrate"></a>使用方法

1. `RetrieveUserQueueRequest` メッセージでは、ユーザーに対する既知のプライベート キューを取得します。
2. `AddToQueueRequest` メッセージでは、元のキューから宛先キューへレコードが追加されます。

### <a name="clean-up"></a>クリーンアップ

1. [セットアップ](#setup) で作成されたサンプル データを削除するためのオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。

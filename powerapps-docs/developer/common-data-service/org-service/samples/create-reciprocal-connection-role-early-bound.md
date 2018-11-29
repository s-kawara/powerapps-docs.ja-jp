---
title: 'サンプル: 相互つながりロールの作成 (アプリ用 Common Data Service) | Microsoft Docs'
description: このサンプルでは、相互つながりロールの作成方法を説明します
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
# <a name="sample-create-a-reciprocal-connection-role"></a>サンプル: 相互つながりロールの作成

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/sample-create-reciprocal-connection-role-early-bound -->

このサンプルは、相互関係ロールを作成する方法を示します。 取引先企業のつながりロールを 1 つと取引先担当者のつながりロールを 1 つ作成し、それらを互いに関連付けて相互ロールにします。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/ReciprocalConnection
) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`ConnectionRole` および `ConnectionRoleObjectTypeCode` メッセージは、新しいつながりロールとつながりロール オブジェクト タイプを作成する必要があるデータが含まれているシナリオで使用するためのものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
2. `ConnectionRole` メッセージは、サンプルに必要なつながりロールを作成します。
3. `ConnectionRoleObjectTypeCode` メッセージは、取引先企業に対するつながりロールのオブジェクトの種類のレコードを作成します。
4. `AssociateRequest` メッセージは、つながりロールを相互に関連付けます。

### <a name="demonstrate"></a>使用方法

1. 初期要求を実行して、`DataToken` などの結果をキャッシュします
1. [セットアップ](#setup) で作成されたレコードを更新する
1. 2 番目の要求を実行します。今回は、初期要求から取得された `DataToken` 値を使用して `DataVersion` を渡します。
1. 第 2 の要求により返されたエンティティの変更を表示する

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) で作成されたサンプル データを削除するためのオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。

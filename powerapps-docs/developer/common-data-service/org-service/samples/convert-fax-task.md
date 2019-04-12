---
title: 'サンプル: FAX をタスクに変換する (Common Data Service) | Microsoft Docs'
description: 'FAX のタスクへの変換方法を示したサンプル '
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
# <a name="sample-convert-a-fax-to-a-task"></a>サンプル: FAX をタスクに変換する

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/sample-convert-fax-task -->


このサンプルは  **FAX** を**タスク**に変換する方法を示します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/ConvertFaxToTask) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]


## <a name="what-this-sample-does"></a>このサンプルの概要

`CreateRequiredRecords` メソッドは、サンプルに必要なサンプル データを作成します。 `retrievedFax` メソッドは、FAX を取得します。 `DeleteRequiredRecords` メソッドは、サンプルが作成したすべてのデータを削除するためのオプションを提供します。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
1. `WhoAmIRequest` メソッドは、現在のユーザーの詳細を取得します。
1. `ActivityParty` メソッドは、FAX の送受信の活動関係者を作成します。
1. `Fax` メソッドは、サンプルに必要な FAX を作成します。


### <a name="demonstrate"></a>使用方法

1. [セットアップ](#setup) で作成されたすべての FAX ID を取得します。
2. タスクを作成し、そのタスクが作成済みであるかを検証します。 

### <a name="clean-up"></a>クリーン アップ

1. サンプルで作成されたすべてのデータを削除するためのオプションを表示します。
2. サンプルで作成されるデータを検証する場合、削除は任意です。 手動でデータを削除することで同じ結果を得られます。

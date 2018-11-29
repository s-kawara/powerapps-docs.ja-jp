---
title: 'サンプル: つながりロールの作成 (アプリ用 Common Data Service) | Microsoft Docs'
description: このサンプルでは、つながりロールの作成方法を説明します。
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
# <a name="sample-create-a-connection"></a>サンプル: つながりの作成

このサンプルは、一致するつながりロールを持った、取引先企業と取引先担当者エンティティ間のつながりを作成する方法を示しています。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/ConnectionEarlyBound) からダウンロードできます。 
  
## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

このサンプルは、一致するつながりロールを持った、取引先企業と取引先担当者間のつながりを作成する方法を示しています。  

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
2. 取引先企業および取引先担当者のつながりロールを作成します。
3. 取引先企業および取引先担当者エンティティに対する関連するつながりロールのオブジェクトの種類コードを作成します。
4. つながりロールを自身に関連付けます。

### <a name="demonstrate"></a>使用方法

1. 取引先企業および取引先担当者エンティティ間のつながりを作成します。 
2. つながりロールをレコードに割り当てます。

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) で作成されたレコードを削除するオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。

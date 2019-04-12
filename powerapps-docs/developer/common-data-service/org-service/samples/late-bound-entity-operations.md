---
title: 'サンプル: 遅延バインドの作成、取得、更新および削除 (Common Data Service) | Microsoft Docs'
description: このサンプルは、遅延バインド エンティティ クラスを使用して、アカウントの作成、取得、更新、および削除の各操作を実行する方法を説明します。
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
# <a name="sample-late-bound-entity-operations"></a>サンプル: 遅延バインド エンティティの操作

<!-- show deep insert equivalent 

sample-initialize-record-existing-record.md
sample-create-retrieve-update-delete-late-bound.md

https://docs.microsoft.com/dynamics365/customer-engagement/developer/org-service/sample-create-retrieve-update-delete-late-bound

-->
このサンプルは、遅延バインド エンティティ クラスを使用して、アカウントの作成、取得、更新、および削除の各操作を実行する方法を説明します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/LateBoundEntityOperations) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]


## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。


### <a name="demonstrate"></a>使用方法

1. 取引先企業オブジェクトをインスタンス化します。
1. 取引先企業レコードを作成します。
1. アカウントおよびその属性を取得します。
1. Postal1 コードの属性更新したうえで、Postal2 コードを null に設定します。
1. 取引先企業を更新します。 
1. 作成された取引先企業レコードを削除するよう求められます。


### <a name="clean-up"></a>クリーンアップ

1. 使用方法のセクションで作成されたすべてのサンプル レコードを削除したなら、クリーンアップは必要ではありません。

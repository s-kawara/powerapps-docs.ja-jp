---
title: 'サンプル: 交差テーブルからのレコードの取得 (Common Data Service for Apps) | Microsoft Docs'
description: このサンプルでは、交差テーブルからレコードを取得する方法を示しています。
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
# <a name="sample-retrieve-records-from-an-intersect-table"></a>サンプル: 交差テーブルからレコードを取得する

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/org-service/sample-retrieve-records-intersect-table --> このサンプルでは、交差テーブルからレコードを取得する方法を示しています。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/RetrieveRecordsFromIntersectTable) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`QueryExpression` メッセージは、式の階層にクエリを含むシナリオで使用するためのものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。 
1. `CreateRequireRecords` メソッドは、サンプルで使用するエンティティ レコードを作成します。
1. `QueryExpression` メッセージは、チームを作成する必要がある既定の部署を取得するために使用されします。
1. `WhoAmIRequest` は、現在のユーザーの GUID を取得します。
1. `Role` メッセージは、ロールのエンティティ レコードをインスタンス化し、プロパティ値を設定します。
1. `AssociateRequest` は、管理者ロールにユーザーを割り当てます。 

### <a name="demonstrate"></a>使用方法

1. `QueryExpression` は、交差テーブルからレコードを取得します。
1. `RetrieveMultipleRequest` は、フェッチ要求をビルドして、結果を取得します。
### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) で作成されたレコードを削除するオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。

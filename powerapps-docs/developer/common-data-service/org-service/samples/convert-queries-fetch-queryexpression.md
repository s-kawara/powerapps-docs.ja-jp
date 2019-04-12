---
title: 'サンプル: Fetch と QueryExpression の間でクエリを変換する (Common Data Service) | Microsoft Docs'
description: このサンプルは、FetchXML と QueryExpression の間でクエリを変換する方法を示します
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
# <a name="sample-convert-queries-between-fetchxml-and-queryexpression"></a>サンプル: FetchXML と QueryExpression の間でクエリを変換

このサンプルは、FetchXML と QueryExpression の間でクエリを変換する方法を示します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/Convertqueriesfetchqueryexpressions) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`QueryExpression` および `fetchExpression` メッセージは、式の階層と FetchXML にクエリを含むシナリオで使用するためのものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。 
1. `CreateRequireRecords` メソッドは、サンプルで使用する取引先企業と 2 つの取引先担当者レコードを作成します。
1. `QueryExpression` は FetchXML に変換するクエリ式を作成します。
1. `DoFetchXmlToQueryExpressionConversion` クラスは、クエリ式に変換する Fetch クエリを作成します。
1. `conversionRequest` メソッドは生成したクエリ式を FetchXML に変換したりその逆も行います。
1. 変換されたクエリを使用して、複数の要求を取得します。 

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) で作成されたレコードを削除するオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。

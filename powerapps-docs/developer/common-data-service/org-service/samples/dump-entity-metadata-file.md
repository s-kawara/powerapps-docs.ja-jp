---
title: 'サンプル: エンティティ メタデータをファイルへダンプ (アプリ用 Common Data Service) | Microsoft Docs'
description: このサンプルは、XML ファイルからすべてのエンティティ メタデータを書き出す方法を示しています。
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
# <a name="sample-dump-entity-metadata-to-a-file"></a>サンプル: エンティティ メタデータのファイルへのダンプ

このサンプルは、`XML` ファイルからすべてのエンティティ メタデータを書き出す方法を示しています。 [RetrieveAllEntitiesRequest](https://docs.microsoft.com/en-us/dotnet/api/microsoft.xrm.sdk.messages.retrieveallentitiesrequest?view=dynamics-general-ce-9) メッセージを使用します。

次のサンプルでは、`\Entities\bin\Debug\EntityInfo.xml` に新しいファイルを作成します。 Office Excel でこのファイルを開き、表形式のレポートを表示できます。 この情報は、レポート内で使用するユーザー定義エンティティのエンティティの種類コードを確認するために必要となる場合があります。 サンプルは、[こちら](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/DumpEntityMetadata) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`RetrieveAllEntitiesRequest` メッセージは、すべてのエンティティに関するメタデータ情報を検出する必要があるデータが含まれているシナリオで使用するためのものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。


### <a name="demonstrate"></a>使用方法

1. `RetrieveAllEntitiesRequest` メソッドは、メタデータを取得します。 
1. `StreamWriter` では、StreamWriter のインスタンスを作成し、テキストをファイルへ書き込みます。

### <a name="clean-up"></a>クリーン アップ

1. このサンプルでは、レコードは作成されません。 クリーンアップの必要はありません。



---
title: 'サンプル: 添付ファイルをアップロード、取得、およびダウンロードする (アプリ用 Common Data Service) | Microsoft Docs'
description: このサンプルでは添付ファイルをアップロード、取得、ダウンロードする方法を示します。
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
# <a name="sample-upload-retrieve-and-download-an-attachment"></a>サンプル: 添付ファイルのアップロード、取得、およびダウンロード

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/sample-upload-retrieve-download-attachment -->

このサンプルでは、 [IOrganizationService.Create](https://docs.microsoft.com/en-us/dotnet/api/microsoft.xrm.sdk.iorganizationservice.create?view=dynamics-general-ce-9) および [IOrganizationService.Retrieve](https://docs.microsoft.com/en-us/dotnet/api/microsoft.xrm.sdk.iorganizationservice.retrieve?view=dynamics-general-ce-9) メソッドを使用して、コメント用の添付ファイルをアップロード、取得、およびダウンロードする方法を示します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/URDAttachement) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]


## <a name="what-this-sample-does"></a>このサンプルの概要

`IOrganizationService` メソッドは、組織のメタデータおよびデータにプログラムからアクセスする方法を提供するシナリオで使用するものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルは何をするか](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います:

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。

### <a name="demonstrate"></a>実際にやってみます
1. `Annotation` メソッドは annotation オブジェクトのインスタンスを作成します。
1. `IOrganizationService` メソッドは annotation オブジェクトを作成し、アップロードします

### <a name="clean-up"></a>クリーンアップ

1. サンプルで作成されたすべてのデータを削除するためのオプションを表示します。

サンプルで作成されるデータを検証する場合、削除は任意です。 手動でデータを削除することで同じ結果を得られます。

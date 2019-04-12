---
title: 'サンプル: CRUD 電子メール添付ファイル <Topic Title> (Common Data Service) | Microsoft Docs'
description: このサンプルは電子メール添付ファイルに関する CRUD 操作の実行方法を示します。
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
# <a name="sample-create-retrieve-update-and-delete-an-email-attachment"></a>サンプル: 電子メールの添付ファイルの作成、取得、更新、および削除

このサンプルは、次のメソッドを使用して電子メールの添付ファイルを作成、取得、更新、および削除する方法を示します。

- [IOrganizationService.Create](https://docs.microsoft.com/dotnet/api/microsoft.xrm.sdk.iorganizationservice.create?view=dynamics-general-ce-9)
- [IOrganizationService.Retrieve](https://docs.microsoft.com/dotnet/api/microsoft.xrm.sdk.iorganizationservice.retrieve?view=dynamics-general-ce-9)
- [IOrganizationService.Update](https://docs.microsoft.com/dotnet/api/microsoft.xrm.sdk.iorganizationservice.update?view=dynamics-general-ce-9)
- [IOrganizationService.Delete](https://docs.microsoft.com/dotnet/api/microsoft.xrm.sdk.iorganizationservice.delete?view=dynamics-general-ce-9)

サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/CRUDEmailAttachements) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`IOrganizationService` メッセージは、組織のメタデータおよびデータにプログラムからアクセスする方法を提供するシナリオで使用するものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
1. `Email` メソッドは、サンプルに必要な電子メール活動を作成します。

### <a name="demonstrate"></a>使用方法

1. `ActivityMimeAttachment` メソッドでは 3 つの電子メール添付ファイルを作成します。 
1. `Retrieve` メソッドでは、添付ファイルの ID、件名、ファイル名、本文を含む添付ファイルを取得します。
1. `Update` メソッドでは、既存の添付ファイルのファイル名を更新します。


### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) で作成されたレコードを削除するオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。



---
title: 'サンプル: 電子メール テンプレートの電子メール添付ファイルを取得する (Common Data Service) | Microsoft Docs'
description: このサンプルは、.電子メール テンプレートに関連付けられた電子メール添付ファイルを取得する方法を示します
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
# <a name="sample-retrieve-email-attachments-for-an-email-template"></a>サンプル: 電子メール テンプレート用の電子メールの添付ファイルの取得

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/sample-retrieve-email-attachments-email-template -->

このサンプルは、[IOrganizationService.RetrieveMultiple](https://docs.microsoft.com/dotnet/api/microsoft.xrm.sdk.iorganizationservice.retrievemultiple?view=dynamics-general-ce-9) メソッドを使用して、電子メール テンプレートに関連付けられた電子メール添付ファイルを取得する方法を示します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/RetrieveEmailAttach) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`IOrganizationService.RetrieveMultiple` メソッドはレコードのコレクションを取得するシナリオで使用するためのものです。


## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
2. `Template` メソッドを使用してサンプル電子メール テンプレートを作成します。

### <a name="demonstrate"></a>使用方法

1. `QueryExpression` は、すべての添付ファイルを取得します。

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) で作成されたサンプル データを削除するためのオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。

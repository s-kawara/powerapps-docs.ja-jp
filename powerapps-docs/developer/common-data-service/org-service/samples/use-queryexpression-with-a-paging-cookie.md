---
title: 'サンプル: ページング Cookie と共に QueryExpresion を使用する (アプリ用 Common Data Service) | Microsoft Docs'
description: このサンプルは QueryExpresion でページング Cookie を使用する方法を示します
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
# <a name="sample-use-queryexpression-with-a-paging-cookie"></a>サンプル: ページング Cookie を使用した QueryExpression の使用

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/org-service/sample-use-queryexpression-with-a-paging-cookie -->

このサンプルでは QueryExpression クエリでページング Cookie を使用して、クエリ結果の連続ページを取得する方法を示しています。 [IOrganizationService.RetrieveMultiple](https://docs.microsoft.com/en-us/dotnet/api/microsoft.xrm.sdk.iorganizationservice.retrievemultiple?view=dynamics-general-ce-9) メソッドを使用します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/UseQueryExpressionwithPaging) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`IOrganizationService.RetreiveMultiple` メソッドはレコードのコレクションを取得するシナリオで使用するためのものです。
## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルは何をするか](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います:

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
1. `Account` メソッドは親取引先企業レコードと 10 の子取引先企業レコードを作成します。

### <a name="demonstrate"></a>使用方法

1. `ConditionExpress` はレコードを取得するための条件式を定義します。
1. `OrderExpression` メソッドはレコードを取得する順序式を定義します。

### <a name="clean-up"></a>クリーンアップ

1. サンプルで作成されたすべてのデータを削除するためのオプションを表示します。

サンプルで作成されるデータを検証する場合、削除は任意です。 手動でデータを削除することで同じ結果を得られます。

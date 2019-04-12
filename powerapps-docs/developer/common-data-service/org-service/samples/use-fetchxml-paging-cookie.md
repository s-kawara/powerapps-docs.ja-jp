---
title: 'サンプル: ページング Cookie と共に FetchXML を使用する (Common Data Service) | Microsoft Docs'
description: 'この例は FetchXML でのページング Cookie の使用方法を示します:'
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
# <a name="sample-use-fetchxml-with-a-paging-cookie"></a>サンプル: ページング Cookie を使用した FetchXML の使用

<!-- This could be greatly simplified IMHO 
https://docs.microsoft.com/dynamics365/customer-engagement/developer/org-service/sample-use-fetchxml-paging-cookie
-->
このサンプルでは FetchXML クエリでページング Cookie を使用して、クエリ結果の連続ページを取得する方法を示しています。 [IOrganizationService.RetrieveMultiple](https://docs.microsoft.com/dotnet/api/microsoft.xrm.sdk.iorganizationservice.retrievemultiple?view=dynamics-general-ce-9) メソッドを使用します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/UseFetchXMLWithPaging) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`IOrganizationService.Retrieve` メソッドはすべてのレコードを取得するデータを含んでいるシナリオで使用するためのものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルは何をするか](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います:

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
1. `Account` メソッドは親取引先企業レコードと 10 の子取引先企業レコードを作成します。

### <a name="demonstrate"></a>使用方法

1. `fetchXml` は親取引先企業にすべての子取引先企業を取得する FetchXML 文字列を作成します。 このFetch クエリは 1 つのプレースホルダーを使用して親取引先企業IDを指定し、必須の取引先企業を除外します。

### <a name="clean-up"></a>クリーンアップ

1. サンプルで作成されたすべてのデータを削除するためのオプションを表示します。

サンプルで作成されるデータを検証する場合、削除は任意です。 手動でデータを削除することで同じ結果を得られます。


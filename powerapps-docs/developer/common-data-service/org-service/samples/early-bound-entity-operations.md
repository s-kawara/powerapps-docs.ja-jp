---
title: 'サンプル: 関連するレコードの事前バインドを作成および更新 (Common Data Service for Apps) | Microsoft Docs'
description: 'このサンプルは、事前バインド クラスを使用して、アカウントの作成、取得、更新、および削除の各操作を実行する方法を示します。 '
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
# <a name="sample-early-bound-entity-operations"></a>サンプル: 事前バインド エンティティのオペレーション

<!-- sample-associate-records-early-bound.md 

sample-create-update-records-related-records-early-bound.md

show deep insert equivalent

sample-initialize-record-existing-record.md

https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/org-service/sample-create-retrieve-update-delete-records-early-bound

-->

このサンプルは、事前バインド クラスを使用して、アカウントの作成、取得、更新、および削除の各操作を実行する方法を示します。 このサンプルでは、以下の共通メソッドを使用します。

- <xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Create*>  
  
-   <xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Retrieve*>  
  
-   <xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Update*>  
  
-   <xref:Microsoft.Xrm.Sdk.IOrganizationService>.<xref:Microsoft.Xrm.Sdk.IOrganizationService.Delete*>  

サンプルは、[こちら](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/EarlyBoundEntityOperations) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`IOrganizationService` メッセージは、組織のメタデータおよびデータにプログラムからアクセスする方法を提供するシナリオで使用するものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
1. サンプルに必要なアカウント レコードを作成します。

### <a name="demonstrate"></a>使用方法

1. アカウント オブジェクトのインスタンスを作成します。
1. 属性を含むアカウントを取得します。
1. アカウントのバージョン番号を取得します。
1. Postal1 コードの属性でアカウントを更新します。 


### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) で作成されたレコードを削除するオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。


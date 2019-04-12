---
title: 'サンプル: フィールド共有レコードの取得 (Common Data Service) | Microsoft Docs'
description: このサンプルはエンティティのフィールド共有レコードを取得する方法を説明します。
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
# <a name="sample-retrieve-field-sharing-records"></a>サンプル: フィールド共有レコードの取得

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/sample-retrieve-field-sharing-records -->

このサンプルはエンティティの `PrincipalObjectAttributeAccess` (フィールド共有) レコードを取得する方法を説明します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/RetrieveFieldSharing) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`PrincipleObjectAttributeAccess` メッセージは、エンティティのフィールド共有レコードを取得するシナリオで使用するためのものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
2. `CreateAttributeRequest` メソッドは、サンプルに必要なカスタム レコードを作成します。

### <a name="demonstrate"></a>使用方法

1. `WhoAMIRequest` は、現在のユーザー情報を取得します。
2. `RetrieveUserPrivilegesRequest` メッセージは、現在のユーザーが `prvReadPOAA` を持っているかどうかを調べます。
3. `PrincipalObjectAttributeAccess` は、セットアップ (#setup) で作成されたカスタム フィールドの POAA エンティティを作成します。
4. `QueryExpression` を使用して、ユーザーの共有属性アクセス許可を取得します。

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) で作成されたサンプル データを削除するためのオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。

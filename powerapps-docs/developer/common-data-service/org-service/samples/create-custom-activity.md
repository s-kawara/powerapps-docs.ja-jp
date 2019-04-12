---
title: 'サンプル: カスタム活動の作成 (Common Data Service) | Microsoft Docs'
description: このサンプルでは、カスタム活動の作成方法を説明します。
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
# <a name="sample-create-a-custom-activity"></a>サンプル: カスタム活動の作成

このサンプルは、[CreateEntityRequest](https://docs.microsoft.com/dotnet/api/microsoft.xrm.sdk.messages.createentityrequest?view=dynamics-general-ce-9) および [CreateAttributeRequest](https://docs.microsoft.com/dotnet/api/microsoft.xrm.sdk.messages.createattributerequest?view=dynamics-general-ce-9) を使用して、カスタム活動を作成する方法を示しています。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/CustomActivity) からダウンロードできます。 

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`CreateEntityRequest` メッセージおよび `CreateAttributeRequest` メッセージは、カスタム活動を作成するシナリオで使用することを目的にしています。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 現在の組織の現在のバージョンをチェックします。

### <a name="demonstrate"></a>使用方法

1. `CreateEntityRequest` メッセージを使用して、カスタム活動エンティティを作成します。
2. 作成したカスタム活動エンティティを公開します。
3. `CreateAttributeRequest` メッセージを使用して、カスタム活動エンティティへのいくつかの属性を作成します。

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) でレコードを削除するためのオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。

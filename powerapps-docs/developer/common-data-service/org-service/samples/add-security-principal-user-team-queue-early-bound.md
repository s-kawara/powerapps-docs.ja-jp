---
title: 'サンプル: セキュリティ プリンシパル (ユーザーまたはチーム) をキューに追加する (Common Data Service) | Microsoft Docs'
description: 'サンプル: キューへのセキュリティ プリンシパルの追加'
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
# <a name="sample-add-a-security-principal-user-or-team-to-a-queue"></a>サンプル: キューへのセキュリティ プリンシパル (ユーザーまたはチーム) の追加 

このサンプルは、ユーザーまたはチームにキューへのアクセス権を与える方法を紹介します。 [AddPrincipalToQueueRequest](https://docs.microsoft.com/dotnet/api/microsoft.crm.sdk.messages.addprincipaltoqueuerequest?view=dynamics-general-ce-9) では、キュー メンバーの一覧に指定したプリンシパルが追加されます。 渡されたセキュリティ プリンシパルがチームの場合、キューにチームの各メンバーが追加されます。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/AddSecurityPrincipalToQueue) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`AddPrincipalToQueueRequest` メッセージは、キュー メンバーの一覧に指定したプリンシパルが追加する必要があるデータが含まれているシナリオで使用するためのものです。 プリンシパルがチームの場合、キューに各チーム メンバーを追加します。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
2. `Queue` メソッドではキュー インスタンスが作成され、プロパティ値が設定されます。 返された GUID は変数で保存されます。
3. `QueryExpression` は、チームおよびロールの作成に対する既定の部署を取得します。
4. サンプルに必要な、新しいチームおよびロールの例を作成します。
5. `prvReadQueue` および `prvAppendToQueue` 特権を取得します。
6. `AddPrivilegeRoleRequest` メソッドでは、ロールの例に `prvReadQueue` および `prvAppendToQueue` が追加されます。

### <a name="demonstrate"></a>使用方法

1. `AddPrincipalToQueueRequest` メソッドでは、キューにチームが追加されます。
### <a name="clean-up"></a>クリーンアップ

1. [セットアップ](#setup) でサンプル データを削除するためのオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。

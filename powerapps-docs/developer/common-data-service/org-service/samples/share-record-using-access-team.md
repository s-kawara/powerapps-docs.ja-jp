---
title: 'サンプル: アクセス チームを使用してレコードを共有する (Common Data Service) | Microsoft Docs'
description: このサンプルは、アクセス チームを使用してレコードにアクセスを許可する方法を示します。
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
# <a name="sample-share-a-record-using-an-access-team"></a>サンプル: アクセス チームを使用してレコードを共有

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/sample-share-record-using-access-team -->

このサンプルは、アクセス チームを使用してレコードにアクセスを許可する方法を示します。 チームのすべてのメンバーには、チームに付与されていると同じ、レコードへのアクセスが提供されます。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/ShareRecordUsingAccessTeam) からダウンロードできます。

このサンプルでは、システムに存在しない追加のユーザーが必要です。 **Office 365** で必要なユーザーを手動で作成し、サンプルがエラーなしで実行されるようにします。 このサンプルでは、次に示す**現状有姿**でユーザー プロファイルを作成します。 `yourorg` を組織名で置換します。

**名**: Nancy<br/>
**姓**: Anderson<br/>
**セキュリティ ロール**: SalesPerson<br/>
**ユーザー名**: nanderson@yourorg.onmicrosoft.com<br/>

**名**: David<br/>
**姓**: Bristol<br/>
**セキュリティ ロール**: SalesPerson<br/>
**ユーザー名**: dbristol@yourorg.onmicrosoft.com<br/>

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`AddMembersTeamRequest`、`GrantAccessRequest`、`RemoveMembersTeamRequest` メッセージは、メンバーを追加、付与、削除するために必要なデータが含まれているシナリオで使用するためのものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
2. サンプルのテスト取引先企業レコードを作成します。

### <a name="demonstrate"></a>使用方法

1. チームに追加される、**Office 365** で手動で作成される販売者を取得します。
1. `WhoAMIRequest` は、現在のユーザーと部署の ID を取得します。
1. サンプル アクセス チームを作成します。 `AddMembersTeamRequest` は、アクセス チームに 2 つの販売者を追加します。
1. `GrantAccessRequest` は、セットアップ (#setup) で作成された取引先企業への読み取り/書き込みアクセス権をチームに付与します。
1. `RetrieveAndDisplayEntityAccess` は、エンティティ アクセス情報を取得して表示します。
1. `RetrieveAndDisplayPrincipalAccess` は、プリンシパル アクセス情報を取得して表示します。

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) で作成されたサンプル データを削除するためのオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。

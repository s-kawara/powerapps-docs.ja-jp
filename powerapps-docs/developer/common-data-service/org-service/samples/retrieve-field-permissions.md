---
title: 'サンプル: フィールド権限の取得 (Common Data Service) | Microsoft Docs'
description: このサンプルは、ユーザーのセキュリティで保護されたフィールドを取得する方法を説明します
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
# <a name="sample-retrieve-field-permissions"></a>サンプル: フィールドのアクセス許可の取得

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/sample-retrieve-field-permissions -->

このサンプルは、[フィールド セキュリティ エンティティ](https://docs.microsoft.com/dynamics365/customer-engagement/developer/field-security-entities) で説明されている手順に従って、ユーザーがセキュリティで保護されたフィールドを取得する方法を示しています。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/RetrieveFieldPermission) からダウンロードできます。

このサンプルでは、システムに存在しない追加のユーザーが必要です。 **Office 365** で必要なユーザーを手動で作成し、サンプルがエラーなしで実行されるようにします。 このサンプルでは、次に示す**現状有姿**でユーザー プロファイルを作成します。 `yourorg` を組織名で置換します。

**名**: Samantha <br/>
**姓**: Smith<br/>
**セキュリティ ロール**: マーケティング マネージャー<br/>
**ユーザー名**: ssmith@yourorg.onmicrosoft.com<br/>

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

`FieldPermission` クラスは、使用できるフィールド アクセス許可の種類を定義するデータが含まれているシナリオで使用するためのものです。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
1. **Office 365** で、手動で作成されたユーザー情報を取得します。
1. ユーザーに割り当てる必要があるセキュリティ ロールを取得する `QueryExpression` メソッド。
1. `Team` メソッドは、チームのエンティティ レコードをインスタンス化し、プロパティ値を設定します。

### <a name="demonstrate"></a>使用方法

1. `FieldSecurityProfile` メソッドは、フィールド セキュリティ プロファイルを作成します。
1. `AssociateRequest` メソッドはプロファイルにチームおよびユーザーを追加します。
1. `CreateEntityRequest` メソッドは、サンプル用の新しいユーザー定義活動エンティティを作成します。
1. `RolePrivilege` メソッドは、新しいカスタム エンティティの特権を追加します。
1. `AddPrivilegeRoleRequest` メソッドは、メソッド `RolePrivilege` を作成して実行します。
1. `FieldPermission` メソッドは、ID のフィールド権限オブジェクトを作成します。

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) で作成されたレコードを削除するオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。

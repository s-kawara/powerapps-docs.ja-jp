---
title: 'サンプル: エンティティのフィールド セキュリティを有効化 (Common Data Service) | Microsoft Docs'
description: このサンプルでは、エンティティのフィールド セキュリティを有効にする方法を示します。
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
# <a name="sample-enable-field-security-for-an-entity"></a>サンプル: エンティティでのフィールド セキュリティの有効化

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/sample-enable-field-security-entity -->

このサンプルでは、エンティティのフィールド セキュリティを有効にする方法を示します。  サンプルは、[こちら](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/FieldSecurity) からダウンロードできます。 

このサンプルでは、システムに存在しない追加のユーザーが必要です。 **Office 365** で必要なユーザーを手動で作成し、サンプルがエラーなしで実行されるようにします。 このサンプルでは、次に示す**現状有姿**でユーザー プロファイルを作成します。 

**名**: Samantha<br/>
**姓**: Smith<br/>
**セキュリティ ロール**: マーケティング マネージャー<br/>
**ユーザー名**: ssmith@yourorg.onmicrosoft.com<br/>

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

上述のシナリオをシミュレートするために、サンプルは次のことを行います:

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
2. **Office 365** で、手動で作成されたユーザーを取得します。
3. ユーザーに割り当てる必要があるセキュリティ ロールを取得します。 
4. チームを作成する必要がある既定の部署を取得します。
5. チームのエンティティ レコードをインスタンス化し、プロパティ値を設定します。 

### <a name="demonstrate"></a>使用方法

1. フィールド セキュリティ プロファイルおよびオブジェクトの要求を作成し、teamprofiles_assocation 関連づけで Moniker を設定します。
2. `CreateEntityRequest` と `CreateAttributeRequest` メッセージを使用して、カスタム活動エンティティおよび属性を作成します。
3. ID 属性のフィールド アクセス許可を作成します。

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) でレコードを削除するためのオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。

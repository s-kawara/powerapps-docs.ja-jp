---
title: 'サンプル: ユーザー アクセスの監査 (Common Data Service) | Microsoft Docs'
description: このサンプルでは、ユーザー アクセスを監査する方法を説明します。
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
# <a name="sample-audit-user-access"></a>サンプル: ユーザー アクセスの監査

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/sample-audit-user-access -->

このサンプル コードは、ユーザー アクセスを監査する方法を示します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/AuditUserAccess) からダウンロードできます。

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>このサンプルの概要

このサンプルでは、最初に、ログオンしたユーザーの組織によるユーザー アクセスの監査を有効にします。 次に、アカウント エンティティを作成し、変更して、監査レコードが生成されるようにします。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
1. 新しい取引先企業エンティティを作成し、新しい取引先企業エンティティでの監査を有効化します。

### <a name="demonstrate"></a>使用方法

1. システム ユーザー レコードからの組織の ID を取得し、組織レコードを取得します。
2. ユーザーアクセスの監査を含む、組織の監査を有効にします。
3. 監査によって追跡される取引先企業エンティティへの更新要求を作成します。
4. 組織および取引先企業の監査フラグを古い値に設定し、実際に変更された場合はそれらを取得します。

### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) 中に作成されたレコードを削除するオプションを表示します。 

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。

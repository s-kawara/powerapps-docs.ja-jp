---
title: 'サンプル: 有効な状態遷移の取得 (Common Data Service) | Microsoft Docs'
description: このサンプルは、有効な状態遷移を取得する方法を説明します。
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
# <a name="sample-retrieve-valid-status-transitions"></a>サンプル: 有効な状態の遷移を取得する

 このサンプルは、エンティティのカスタム状態の遷移が定義されているかどうかに関係なく、有効な状態の遷移を取得する方法を示します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/RetrieveValidTransitions) からダウンロードできます。
 
 ## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]


## <a name="what-this-sample-does"></a>このサンプルの概要

`GetValidStatusOptions` メソッドは、状態遷移がエンティティで有効になっているかどうかにかかわらず、有効な状態オプション遷移を返すデータを含むシナリオで使用するためのものです。
## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
1. `MetadataFilterExpression` メソッドは、エンティティ メタデータをチェックします。

### <a name="demonstrate"></a>使用方法
1. `MetadataFilterExpression` メソッドは、`Incident` エンティティの状態オプションを取得します。
1. `RetrieveMetadataChangeRequest` メソッドは、メタデータを取得します。
1. `GetValidStatusOptions` メソッドは、各状態オプションの有効な状態遷移を取得します。

### <a name="clean-up"></a>クリーン アップ

1. このサンプルでは、レコードは作成されません。 クリーンアップの必要はありません。

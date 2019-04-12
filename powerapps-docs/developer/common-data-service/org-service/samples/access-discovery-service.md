---
title: 'サンプル: 探索サービスに関する作業 <Topic Title> (Common Data Service) | Microsoft Docs'
description: このサンプル コードは、探索サービスの使用方法について説明します
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
# <a name="sample-access-the-discovery-service"></a>サンプル: 探索サービスへのアクセス

# <a name="work-with-discovery-service"></a>探索サービスに関する作業 
このサンプル コードは、SDK アセンブリで探索サービスの使用方法について説明します。 サンプルは [ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/DiscoveryService) からダウンロードできます

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

このサンプルでは接続情報の入力を求めるダイアログが開きません。

App.config 接続文字列で `Username` および `Password` 値を設定すると、それらを使用できます’。 それ以外の場合は、`username` および `password` 変数を `SampleProgram.Main` メソッドで設定します。

## <a name="what-this-sample-does"></a>このサンプルの概要

このサンプルは SDK アセンブリ `DiscoveryServiceProxy` を使用して、ユーザーの資格情報で探索サービスをクエリし、接続できる環境を特定します。

1 つ以上の環境が返された場合、サンプルはユーザーに 1 つを選択させ、`WhoAmIRequest` を使用してその環境に対する `SystemUser.UserId` を返します。

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

このサンプルでは、ユーザー資格情報のユーザー名およびパスワードを使用する以外に、特別な設定は必要ありません。

環境が存在する地域データ センターを知っている場合、 SampleProgram.cs ファイルの 40 行目でこの値を設定すると、サンプルがより速く実行されます。

SampleMethods.cs では、既知の各データ センターに対する `DataCenter` 列挙があります。 各列挙メンバーは `Description` 表記で装飾されます。 これらのすべてのメンバーは、地域の探索サービスに対する URL がある `Unknown` 以外は、説明として設定されます。 


### <a name="demonstrate"></a>使用方法

1. ユーザーの資格情報および `dataCenter` 値を使用して、プログラムは `GetAllOrganizations` 静的メソッドを使用してユーザーに対するすべての既知の環境を取得します。
1. `GetAllOrganizations` メソッドは、`dataCenter` 値が `DataCenter.Unknown` に設定されているかどうかを検出します。 このメンバーに設定されている場合、このメソッドは `DataCenter` 列挙でほかのすべてのメンバーにループし、`GetOrganizationsForDataCenter` 静的メソッドを使用して検出された任意の環境を取得します。

    特定のデータ センターが設定されている場合、`GetAllOrganizations` は単にそれらの値で `GetOrganizationsForDataCenter` を呼び出します。

1. `GetOrganizationsForDataCenter` メソッドはメンバー `Description` 装飾からデータ センター探索サービス URL を解凍し、それをユーザー資格情報と共に使用して `RetrieveOrganizationsRequest` 探索サービス メッセージを実行します。

    ユーザーに特定のデータ センターでの環境がない場合は、`System.ServiceModel.Security.SecurityAccessDeniedException` が必要です。

1. 任意の環境が `GetAllOrganizations` メソッドで返されると、コンソールに表示され、番号を入力して 1 つを選択するように求められます。 選択が有効な場合、選択された環境データは `WhoAmIRequest` を実行するために使用され、その環境でのユーザーに対する `SystemUser.UserId` を返します。

### <a name="clean-up"></a>クリーンアップ

このサンプルでは、レコードは作成されません。 クリーンアップの必要はありません。

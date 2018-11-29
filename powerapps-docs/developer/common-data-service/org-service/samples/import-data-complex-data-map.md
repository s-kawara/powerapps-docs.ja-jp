---
title: 'サンプル: 複雑なデータ マップを使用したデータのインポート (アプリ用 Common Data Service) | Microsoft Docs'
description: このサンプルは、データ インポートによって、新しいレコードを作成する方法を示します。
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
# <a name="sample-import-data-using-complex-data-map"></a>サンプル: 複雑なデータ マップを使用してデータをインポートする

このサンプルは、データ インポートによって、新しいレコードを作成する方法を示します。 このサンプルは、複雑なデータ マップを使用します。 サンプルは、[ここ](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/ImportComplexDataMap) からダウンロードできます。

>[!NOTE]
> このサンプルのソース データは、次のファイルに含まれています。`ImportComplexDataMap\import accounts.csv`

## <a name="how-to-run-this-sample"></a>このサンプルを実行する方法

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="how-this-sample-works"></a>このサンプルがどのように動作するか

[このサンプルの概要](#what-this-sample-does) で説明されているシナリオをシミュレートするために、サンプルは次のことを行います。

### <a name="setup"></a>セットアップ

1. 組織の現在のバージョンをチェックします。
1. `ImportMap` メソッドは、インポート マップを作成します。
1. `ColumnMapping` メソッドは、`text` タイプのフィールドに列マッピングを作成します。
1. `EntityReference` メソッドは、列マッピングとデータ マップを関連付けます。
1. `LookUpMapping` メソッドは、取引先企業の親会社に検索のマッピングを作成します。
1. `ImportFile` メソッドは、インポート ファイルを作成します。
1. `GetHeaderColumnsImportFileRequest` メソッドは、インポート ファイルで使用されている見出し列を取得します。
1. `ParseImportRequest` メソッドは、インポート ファイルを解析します。 
1. `RetrievedParsedDataImportFileRequest` メソッドは、解析テーブルからデータを取得します。
1. `TransformImportRequest` メソッドは、インポートを変換します。


### <a name="clean-up"></a>クリーン アップ

1. [セットアップ](#setup) で作成されたレコードを削除するオプションを表示します。

    サンプルで作成されるエンティティおよびデータを検証する場合、削除は任意です。 手動でレコードを削除することで同じ結果を得られます。


### <a name="see-also"></a>関連項目

[データのインポート](../../import-data.md)<br />
[ソース ファイルのインポートを準備する](../../prepare-source-files-import.md)<br />
[インポート用データ マップの作成](../../create-data-maps-for-import.md)<br />
[インポート用の変換マッピングの追加](../../add-transformation-mappings-import.md)<br />
[データ インポートの構成](../../configure-data-import.md)<br />
[データ インポートの実行](../../run-data-import.md)<br />
[データ インポート エンティティ](../../data-import-entities.md)<br />
[サンプル: データ マップのエクスポートおよびインポート](export-import-data-map.md)<br />

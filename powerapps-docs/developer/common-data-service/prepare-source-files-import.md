---
title: ソース ファイルのインポートを準備する (アプリ用 Common Data Service) | Microsoft Docs
description: データ インポートでは、コンマ区切り値 (.csv)、XML スプレッドシート 2003 (.xml)、またはテキストのいずれかの形式のファイルとして書式設定したソース ファイルをサポートします。
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: mayadumesh
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="prepare-source-files-for-import"></a>ソース ファイルのインポートを準備する

データをアプリ用 Common Data Service (CDS) にインポートするには、まず、ソース データ ファイルを作成する必要があります。  
  
インポートで使用するデータのソース ファイルは、コンマ区切り値 (.csv)、XML スプレッドシート 2003 (.xml)、またはテキストのいずれかの形式のファイルとして書式設定する必要があります。 ソース ファイルを使用すると、異なる形式を使用するデータベース システムからアプリ用 CDS にデータを転送することができます。  
  
ソース ファイルには、取引先企業や取引先担当者など、1 種類以上のエンティティのデータを含めることができます。 複数のエンティティ データを含むソース ファイルの場合、`<EntitiesPerFile>` タグを含むマップを提供する必要があります。 このタグの値を "Multiple" に設定して、ソース ファイルに複数の種類のエンティティが存在することを指定します。 `Dedupe = “Eliminate”` 属性を `<EntityMap>` タグに追加します。 これにより、ソース ファイル内で、特定の種類のエンティティの行が重複していても、単一の行しか使用されないことで、ルックアップ関連のエラーが最小限に抑えられます。  
  
複数の種類のエンティティがあるデータ マップの例を、 [Microsoft ダウンロード: DataImportMaps.zip](http://download.microsoft.com/download/D/5/F/D5F73E15-439B-4EBC-BFFB-C6837B146C76/DataImportMaps.zip) からダウンロードできます。 `MapForSalesForceContactAccount.xml` ファイルを参照します。  
  
 ソース ファイルのフィールド値は、コンマ、タブ、または `ImportFile.FieldDelimiterCode` 属性で定義されているその他の文字で区切ることができます。  
  
> [!NOTE]
>  フィールドの値の区切り文字として、印字不能文字、**null** (\0)、改行 (\b) を使用しないでください。  
  
 ソース ファイルの 1 行目には、列見出しが含まれている必要があります。 見出しを含めない場合は、`ImportFile.IsFirstRowHeader` 属性を使用して、1 行目に実際のデータが表示されるように指定します。 この場合は、既定の列見出しが Col1、Col2 などの名前で作成されます。  

### <a name="see-also"></a>関連項目

[データのインポート](import-data.md)<br />
[インポート用データ マップの作成](create-data-maps-for-import.md)<br />
[インポート用の変換マッピングの追加](add-transformation-mappings-import.md)<br />
[データ インポートの構成](configure-data-import.md)<br />
[データ インポートの実行](run-data-import.md)<br />
[データ インポート エンティティ](data-import-entities.md)<br />
[サンプル: データ マップのエクスポートおよびインポート](org-service/samples/export-import-data-map.md)<br />
[サンプル: 複雑なデータ マップを使用してデータをインポートする](org-service/samples/import-data-complex-data-map.md)<br />